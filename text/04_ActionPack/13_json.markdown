## JSON

Rails現在支援POST一個JSON內容的請求，例如你可以像這樣丟出一個POST：

	POST /posts
	{"post": {"title": "Breaking News"}}

所有參數都將到**params**中。例如：

	def create
	  @post = Post.create params[:post]
	  # …
	end

為了那些不知道JSON是一個XML競爭者的人，它在JavaScript資料交換中相當廣泛，因為它呈現為這種語言。它的名字是來自於：**JavaScript Object Notation**。