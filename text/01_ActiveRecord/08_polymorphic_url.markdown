## Polymorphic url

一些多型URL的輔助方法也被引入到新的Rails中，用來提供一種更為簡潔優雅的routes操作方式。

這些方法在你想生成基於**RESTful**資源的URL，同時又不必顯示指定資源的類型的時候會顯得十分有用。

使用方面則是非常的簡單，來看看一些例子(注釋的部份是Rails 2.1之前的做法)：

	record = Article.find(:first) 
	polymorphic_url(record) #-> article_url(record)

	record = Comment.find(:first)
	polymorphic_url(record)  #->  comment_url(record)

	# it can also identify recently created elements
	record = Comment.new
	polymorphic_url(record)  #->  comments_url()
	                  
注意到**polymorphic_url**方法是如何確認傳入參數的類型並生成正確的routes，內嵌資源(**Nested resources**)和**namespaces**也同樣支援：

	polymorphic_url([:admin, @article, @comment])
	#-> this will return:
	admin_article_comment_url(@article, @comment)
	           
你同樣可使用**new**, **edit**, **formatted**等前綴，看看下面的例子：

	edit_polymorphic_path(@post)
	#=> /posts/1/edit

	formatted_polymorphic_path([@post, :pdf])
	#=> /posts/1.pdf
