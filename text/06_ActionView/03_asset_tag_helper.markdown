## ActionView::Helpers::AssetTagHelper

### register\_javascript\_expansion

這個方法可用來定義一個符號作為稍後在 **javascript\_include\_tag** 方法中可識別的參數，使用這個方法註冊一個或是多個 JavaScript 文件可以隨著該符號被引入。這個方法是在 **init.rb** 中呼叫的，將位於 **public/javascript** 下面的 JavaScript 文件註冊進來。讓我們看看它是怎麼運作的：

	# In the init.rb file
	ActionView::Helpers::AssetTagHelper.register_javascript_expansion 
		:monkey => ["head", "body", "tail"] 

	# In our view:
	javascript_include_tag :monkey

	# We are going to have:
	<script type="text/javascript" src="/javascripts/head.js"></script>
	<script type="text/javascript" src="/javascripts/body.js"></script>
	<script type="text/javascript" src="/javascripts/tail.js"></script>


### register\_stylesheet\_expansion

這個方法跟剛剛提到的 **ActionView::Helpers::AssetTagHelper#register\_javascript\_expansion** 很類似，不同點只在於它針對的是 CSS 文件而不是 JavaScript 文件。如下面的例子：

	# In the init.rb file
	ActionView::Helpers::AssetTagHelper.register_stylesheet_expansion 
		:monkey => ["head", "body", "tail"] 

	# In our view:
	stylesheet_link_tag :monkey

	# We are going to have:
	<link href="/stylesheets/head.css"  media="screen" rel="stylesheet" 
		type="text/css" />
	<link href="/stylesheets/body.css"  media="screen" rel="stylesheet" 
		type="text/css" />
	<link href="/stylesheets/tail.css"  media="screen" rel="stylesheet" 
		type="text/css" />