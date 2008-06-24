##Removing whitespaces with squish method

**String**物件中增加了兩個方法， **squish** 和 **squish!**。

這兩個方法和 **strip** 一樣，它刪除了文字前後的空格，也刪除了文字中間無用的空格。像是下面這個例子：

	“    A    text    full    of     spaces    “.strip
	#=> “A    text    full    of     spaces”

	“    A    text    full    of     spaces    “.squish
	#=> “A text full of spaces”
