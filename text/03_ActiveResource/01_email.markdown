## 使用Email當作使用者名稱

某些服務使用Email作為使用者名稱，這會要求使用如下形式的URL：

	http://ernesto.jimenez@negonation.com:pass@tractis.com

這個URL中有兩個"@"，這會帶來些問題：直譯器無法正確解析這個URL。因此對**ActiveResource**的使用方式做了擴展，以方便使用Email進行身分驗證。可以這樣使用：

	class Person < ActiveResource::Base
	  self.site = "http://tractis.com"
	  self.user = "ernesto.jimenez@negonation.com"
	  self.password = "pass"
	end
