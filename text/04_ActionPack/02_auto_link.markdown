## Auto Link

為那些不知道這個方法的人，**auto\_link**方法接收所有文字參數，如果這個文字包含一個e-mail或者一個網址，將返回相同的文字，但是包含了超連結。

例如：

	auto_link("Go to this website now: http://www.rubyonrails.com")
	# => Go to this website now: http://www.rubyonrails.com

一些網站，像是Amazon，使用"="在URL中，該方法不認可這個符號，看這個方法怎樣處理這種情況：

	auto_link("http://www.amazon.com/Testing/ref=pd_bbs_sr_1")
	# => http://www.amazon.com/Testing/ref

注意該方法會截斷"="後面的東西，因為它不支援這個符號。我的意思是，它通常是不被支援的，但在Rails 2.1中根本沒有這個問題。

同樣的方法將在稍後更新，允許在網址中使用括號。

這就是括號的範例：

	http://en.wikipedia.org/wiki/Sprite_(computer_graphics)
