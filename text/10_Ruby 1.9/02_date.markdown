## DateTime類別的新方法 (New methods for DateTime class)

為了保證對**Time**類別的兼容性(duck-typing)，對**DateTime**加入了三個新方法：**#utc**, **#utc?**, **#utc_offset**：

	>> date = DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24))
	#=> Mon, 21 Feb 2005 10:11:12 -0600

	>> date.utc
	#=> Mon, 21 Feb 2005 16:11:12 +0000

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24)).utc?
	#=> false

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, 0).utc?
	#=> true

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24)).utc_offset
	#=> -21600
