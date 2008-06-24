## Has\_one
   
### 支援 through 選項

**has\_one**方法現在支援**through**選項。他的用法與**has_many :through**相同，不過代表的是和單一一個**ActiveRecord**物件的關連。

	class Magazine < ActiveRecord::Base
	  has_many :subscriptions
	end

	class Subscription < ActiveRecord::Base
	  belongs_to :magazine
	  belongs_to :user
	end

	class User < ActiveRecord::Base
	  has_many :subscriptions
	  has_one :magazine, :through => : subscriptions, 
		        :conditions => ['subscriptions.active = ?', true]
	end
	
### Has\_one :source\_type 選項

上面提到的**has\_one :through**方法還能接收一個**:source\_type**選項，我會試著透過一些例子來解釋。我們先來看看這個類別：

	class Client < ActiveRecord::Base
	  has_many :contact_cards 

	  has_many :contacts, :through => :contact_cards
	end 

上面的程式碼是一個**Client**類別，**has_many**種聯絡人(contacts)，由於**ContactCard**類別具有多型的關連。

下一步將建立兩個類別來表示**ContractCard**：

	class Person < ActiveRecord::Base
	  has_many :contact_cards, :as => :contact
	end

	class Business < ActiveRecord::Base
	  has_many :contact_cards, :as => :contact
	end

**Person**和**Business**透過**ContactCard**表與**Client**類別做關聯，換句話說，我有兩個聯絡人，私人的(personal)與工作上的(business)。然而，這樣做卻行不通，看看當我試著獲取一個contact時發生了什麼事情：

	>> Client.find(:first).contacts
	# ArgumentError: /…/active_support/core_ext/hash/keys.rb:48:
	# in `assert_valid_keys’: Unknown key(s): polymorphic 

為了讓上述程式碼成功，我們需要使用**:source_type**。我們修改一下**Client**類別：

	class Client < ActiveRecord::Base
	  has_many :people_contacts,
	           :through => :contact_cards,
	           :source => :contacts,
	           :source_type => :person 

	  has_many :business_contacts,
	           :through => :contact_cards,
	           :source => :contacts,
	           :source_type => :business
	end
	                       
注意到現在我們有兩種取得聯絡人的方式，我們可以選擇我們期待哪種**:source_type**。

	Client.find(:first).people_contacts
	Client.find(:first).business_contacts
