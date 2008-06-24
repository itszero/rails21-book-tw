## clone 方法

現在我們可以複製已經有的resource：

	ryan = Person.find(1)
	not_ryan = ryan.clone
	not_ryan.new?  # => true

要注意複製出來的物件並不複製任何類別屬性，僅複製resource屬性。

	ryan = Person.find(1)
	ryan.address = StreetAddress.find(1, :person_id => ryan.id)
	ryan.hash = {:not => "an ARes instance"} 

	not_ryan = ryan.clone
	not_ryan.new?            # => true
	not_ryan.address         # => NoMethodError
	not_ryan.hash            # => {:not => "an ARes instance"}