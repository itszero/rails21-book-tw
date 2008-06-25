## 在Views之外存取Helpers

有多少次你建立了一個**helper**希望它在一個**controller**中使用？要做到這樣，你必須包含這個**helper** module到這個**controller**之中，但這使你的程式碼看起來很髒。

Rails 2.1已經開發了一個方法在Views以外的地方使用Helpers。已很簡單的方式運作：

 	# To access simple_format method, for example
	ApplicationController.helpers.simple_format(text)

簡單而乾淨！