## 逾時

由於ActiveResource使用**HTTP**來存取RESTful API，當伺服器回應緩慢或者伺服器罷工時會出問題。在某些情況下呼叫ActiveResource會逾時失敗。現在可以用timeout屬性來設定逾時時間了。

	class Person < ActiveResource::Base
	  self.site = "http://api.people.com:3000/"
	  self.timeout = 5 # waits 5 seconds before expire
	end

本例子將逾時設定為5秒。推荐的做法是將該值設得小一點使系統能快速偵測到失敗，以避免相關錯誤引發伺服器錯誤。

ActiveResource內部使用Net::HTTP來發起HTTP請求。當timeout屬性設定時，該值同時被設定到Net::HTTP物件實體的**read\_timeout**屬性上。

該屬性的預設值是60秒。