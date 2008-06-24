## Dirty Objects
                  
在新的Rails當中，我們同樣可以跟蹤對**ActiveRecord**所做的更改。我們能夠知道是否一個物件被進行了修改，如果有更改就能跟蹤到最新的變更。來看看例子：

  article = Article.find(:first)
	article.changed?  #=> false

	article.title  #=> "Title"
	article.title = "New Title"
	article.title_changed? #=> true

	# shows title before change
	article.title_was  #=> "Title"

	# before and after the change
	article.title_change  #=> ["Title", "New Title"]

可以看到，使用上非常的簡單，同時也能透過下列兩種方法的任意一種列出對一個物件的所有更改：

	# returns a list with all of the attributes that were changed
	article.changed  #=> ['title']

	# returns a hash with attributes that were changed 
	# along with its values before and after
	article.changes  #=> { 'title’ => ["Title", "New Title"] }
             
注意到一個物件被儲存後，他的狀態也隨之改變：

	article.changed?  #=> true
	article.save  #=> true
	article.changed?  #=> false
   
如果不透過**attr=**來更改一個物件的狀態，那你需要透過呼叫**attr\_name\_will\_change!**方法(用物件的實際屬性名稱替換**attr**)來通知屬性已經被更改，來看最後一個例子：
    
	article = Article.find(:first)
	article.title_will_change!
	article.title.upcase!
	article.title_change  #=> ['Title', 'TITLE']
