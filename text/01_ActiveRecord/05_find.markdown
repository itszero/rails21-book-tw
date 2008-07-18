## Find

### Conditions
            
從現在開始，你可以向**ActiveRecord**的**find**方法中傳一個物件作為參數。看以下的例子：

	class Account < ActiveRecord::Base
	  composed_of :balance, :class_name => "Money", :mapping => %w(balance amount)
	end
       
這個例子中你可以向**Account**類別的**find**方法中傳入一個**Money**實體做為參數，像這樣：

	amount = 500
	currency = "USD"
	Account.find(:all, :conditions => { :balance => Money.new(amount, currency) })
	
### Last

到現在為止我們只能在**ActiveRecord**的**find**方法中使用三個運算子來搜尋資料，他們是**:first**,**:all**和物件自己的id(這種情況下，我們除了id以外，不再傳入其他的參數)。

在Rails 2.1中，有了第四個運算子**:last**，幾個例子：

	Person.find(:last)
	Person.find(:last, :conditions => [ "user_name = ?", user_name])
	Person.find(:last, :order => "created_on DESC", :offset => 5)
	                                                             
為了能明白這個新的運算子如何操作，來看看底下的測試：

	def test_find_last
	  last  = Developer.find :last
	  assert_equal last, Developer.find(:first, :order => 'id desc')
	end
	
### All

類別方法**all**是另外一個類別方法**find(:all)**的別名，如：
	
    Topic.all 等同於 Topic.find(:all)

### First
              
類別方法**first**是另外一個類別方法**find(:first)**的別名，如：

    Topic.first 等同於 Topic.find(:first)

### Last

類別方法**last**是另外一個類別方法**find(:last)**的別名，如：

    Topic.last 等同於 Topic.find(:last)
             
## 在**named\_scope**中使用**first**和**last**方法

所有上述的方法同樣適用於**named\_scope**。比如我們建立一個叫**recent**的**named\_scope**，下列程式碼是有效的：

		post.comments.recent.last
