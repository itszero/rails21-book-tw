## 在字串中應用格式化標題

以前當你在一個包含了 's 的字串中使用**String#titleize**方法時有個bug，這個bug返回大寫的'S，看看：

	>> "brando’s blog".titleize
	=> "Brando’S Blog"
	
相同的範例，但是此Bug已經修復了：

	>> "brando’s blog".titleize
	=> "Brando’s Blog"
