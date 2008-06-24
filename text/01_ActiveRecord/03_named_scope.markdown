## Named_scope

*has\_finder* gem已經添加到Rails當中了，有一個新名字**:named_scope**。

為了全面了解一下這為Rails帶來了什麼，我們看看下面的例子：

	class Article < ActiveRecord::Base
	  named_scope :published, :conditions => {:published => true}
	  named_scope :containing_the_letter_a, :conditions => "body LIKE '%a%’"
	end 

	Article.published.paginate(:page => 1)
	Article.published.containing_the_letter_a.count
	Article.containing_the_letter_a.find(:first)
	Article.containing_the_letter_a.find(:all, :conditions => {…})
 
通常我會建立一個新的叫做**published**的方法來取得所有已經發布的文章，不過在這裡我是用了**named\_scope**來做相同的事情，而且還能得到其他的效果。來看看另一個例子：

	named_scope :written_before, lambda { |time|
	  { :conditions => ['written_on < ?', time] }
	}

	named_scope :anonymous_extension do
	  def one
	    1
	  end
	end

	named_scope :named_extension, :extend => NamedExtension 

	named_scope :multiple_extensions, 
		:extend => [MultipleExtensionTwo, MultipleExtensionOne]

## 用proxy\_options來測試named\_scope
                                                                                 
**Named scopes**是Rails 2.1中很有趣的新功能，不過使用一段時間以後你就會發現想建立一些複雜的情況的測是會有點麻煩，看看例子：

		class Shirt < ActiveRecord::Base
		  named_scope :colored, lambda { |color|
		    { :conditions => { :color => color } }
		  }
		end

該如何建立一個可以測試scope的結果的測試呢？

為了解決這個問題，**proxy\_options**被開發出來。它允許我們來檢測**named_scope**使用的選項。為了測試上面的程式碼，我們可以這樣寫測試：

		class ShirtTest < Test::Unit
		  def test_colored_scope
		    red_scope = { :conditions => { :colored => 'red' } }
		    blue_scope = { :conditions => { :colored => 'blue' } }
		    assert_equal red_scope, Shirt.colored('red').scope_options
		    assert_equal blue_scope, Shirt.colored('blue').scope_options
		  end
		end
