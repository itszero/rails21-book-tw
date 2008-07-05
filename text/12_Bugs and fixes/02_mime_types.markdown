##Mime Types

不允許定義被指派過的屬性以symbol型態給**request.format**的問題已經解決了，現在你可以以以下的方式來撰寫程式碼：

	request.format = :iphone
	assert_equal :iphone, request.format
