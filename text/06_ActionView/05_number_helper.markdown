## ActionView::Helpers::NumberHelper

### number\_to\_currency

**number\_to\_currency** 方法使用 **:format** 選項作為參數，讓我們可以格式化回傳值。之前的版本中，當我們需要對本地貨幣格式化時，我們需要在 **:unit** 選項前面多一個空格才能使輸出正確。像是下面的例子：

	# R$ is the symbol for Brazilian currency
	number_to_currency(9.99, :separator => ",", :delimiter => ".", :unit => "R$")
	# => "R$9,99″

	number_to_currency(9.99, :format => "%u %n", :separator => ",", 
		:delimiter => ".", :unit => "R$")
	# => "R$ 9,99″
	
之後，我們又更改成另外一個樣式：

	number_to_currency(9.99, :format => "%n in Brazilian reais", :separator => ",", 
		:delimiter => ".", :unit => "R$")
	# => "9,99 em reais"

當需要建立你自己的字串格式，您只需要使用下面的參數：

	%u For the currency
	%n For the number