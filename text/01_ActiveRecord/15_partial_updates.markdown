## Partial Updates

**Dirty Objects**的實現讓另一個非常有趣的功能變為可能。

由於我們現在可以跟蹤一個物件的狀態是否發生改變，那麼為什麼不用它來避免那些不必要的對資料庫的更新呢？

在之前版本中的Rails，當我們對一個已經存在的**ActiveRecord**物件呼叫**save**方法時，所有資料庫中的欄位都會被更新，即使那些沒有做到任何更改的欄位。

這種方式在有了Dirty Objects以後會有很大的改進，而實際情況也的確如此。看看保存一個有一點更改的物件時，Rails 2.1產生的SQL查詢語句：

	article = Article.find(:first)
	article.title  #=> "Title"
	article.subject  #=> "Edge Rails"

	# Let's change the title
	article.title = "New Title"

	# it creates the following SQL
	article.save
	#=>  "UPDATE articles SET title = 'New Title' WHERE id = 1"
	
注意到，只有那些在應用中被更改的屬性才會被更新，如果沒有屬性被更改那**ActiveRecord**就不執行任何更新語句。

為了開啟/關閉這個新功能，你得更改model的**partial\_updates**屬性。

	# To enable it
	MyClass.partial_updates = true
         
如果希望對所有的models開啟/關閉這個功能，那你得編輯*config/initializers/new\_rails\_defaults.rb*：

	# Enable it to all models
	ActiveRecord::Base.partial_updates = true
      
別忘了如果你不透過attr=更改欄位，同樣得通過*config/initializers/new\_rails\_defaults.rb*來通知Rails，像這樣：

	# If you use **attr=**, 
	# then it's ok not informing
	person.name = 'bobby'
	person.name_change    # => ['bob', 'bobby']
	
	
	# But you must inform that the field will be changed
	# if you plan not to use **attr=** 
	person.name_will_change!
	person.name << 'by'
	person.name_change    # => ['bob', 'bobby']
         
如果你不通知Rails，那麼上述的程式碼同樣會更改物件的屬性，但是卻不能被跟蹤到，也就無法正確的更新資料庫中的對應欄位。