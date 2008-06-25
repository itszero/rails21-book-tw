## ActionView::Helpers::TextHelper

### excerpt

**excerpt** 方法是一個 helper 方法，能夠在一段文字中搜尋一個單字，同時傳回包含這個單字之前、之後各依照指定數量的字母縮寫。像是這樣：

	excerpt('This is an example', 'an', 5)
	# => "…s is an examp…"

但是這個方法卻是有 bug 的，如果你算算看，你會發現他會回傳6個字母而不是五個。這個bug已經在這個版本中解決了，下面是正確的輸出結果：

	excerpt('This is an example', 'an', 5)
	# => "…s is an exam…"
	
###simple\_format

**simple\_format** 方法接受任何文字參數並用簡單的方式格式化為 **HTML**。它會將文字參數中的換行符號（\n) 換成 **HTML** 標記的 "<br />"，而當我們有連續換了兩行像是 (\n\n)，它就會用<p> 標籤標成一個段落。

	simple_format("Hello Mom!", :class => 'description')
	# => "<p class=’description’>Hello Mom!</p>"

**HTML** 屬性將會被加到每個 "<p>" 標記的段落上。