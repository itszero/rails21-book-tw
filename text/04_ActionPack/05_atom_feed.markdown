## Atom Feed 中新的 namespaces

你知道**atom\_feed**方法嗎？這是Rails 2.0的一個新特性，使得建立Atom feeds變得更容易。來看看怎樣操作：

在一個*index.atom.builder*檔案中：

	atom_feed do |feed|
	  feed.title("Nome do Jogo")
	  feed.updated((@posts.first.created_at))

	  for post in @posts
	    feed.entry(post) do |entry|
	      entry.title(post.title)
	      entry.content(post.body, :type => 'html')

	      entry.author do |author|
	        author.name("Carlos Brando")
	      end
	    end
	  end
	end

Atom feed是什麼？Atom的名字是根據XML的樣式與meta資料。在網路中它是一個發佈經常更新內容的協議，如：Blog、新聞。Feeds經常以XML或Atom的格式發佈標示為applicaton/atom+xml類型。

在Rails 2.0的第一個版本中，該方法允許**:language**、**:root_url**和**:url**參數，你可以從Rails文件中獲得更多關於這些方法的訊息。但是這次的更新我們更可以包含新的namespace在一個Feed的root元素中，例如：

	atom_feed('xmlns:app' => 'http://www.w3.org/2007/app') do |feed|

將返回：

	<feed xml:lang="en-US" xmlns="http://www.w3.org/2005/Atom" 
		xmlns:app="http://www.w3.org/2007/app">

修改這個之前的範例，我們可以這樣寫：

	atom_feed({'xmlns:app' => 'http://www.w3.org/2007/app',
		'xmlns:openSearch' => 'http://a9.com/-/spec/opensearch/1.1/'}) do |feed| 

	  feed.title("Nome do Jogo")
	  feed.updated((@posts.first.created_at))
	  feed.tag!(openSearch:totalResults, 10) 

	  for post in @posts
	    feed.entry(post) do |entry|
	      entry.title(post.title)
	      entry.content(post.body, :type => 'html')
	      entry.tag!('app:edited', Time.now) 

	      entry.author do |author|
	        author.name("Carlos Brando")
	      end
	    end
	  end
	end
