## 簡單的Testing Helpers

在早期最最最令人討厭的事情就是在Rails中測試**helpers**。我已經遭受到很多次100%的覆蓋，建立一些給**helpers**用的測試。

透過**ActionView::TestCase**類別，在Rails 2.1中這變得簡單多了。看個範例：

	module PeopleHelper
	  def title(text)
	    content_tag(:h1, text)
	  end

	  def homepage_path
	    people_path
	  end
	end

現在看我們在Rails 2.1中怎樣做同樣的事情：

	class PeopleHelperTest < ActionView::TestCase
	  def setup
	    ActionController::Routing::Routes.draw do |map|
	      map.people 'people', :controller => 'people', :action => 'index'
	      map.connect ':controller/:action/:id'
	    end
	  end

	  def test_title
	    assert_equal "<h1>Ruby on Rails</h1>", title("Ruby on Rails")
	  end

	  def test_homepage_path
	    assert_equal "/people", homepage_path
	  end
	end
