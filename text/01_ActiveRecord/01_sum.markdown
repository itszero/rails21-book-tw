## **sum**方法

### **sum**方法中的表達式

現在我們可以在**ActiveRecord**方法當中使用表達式來處理諸如**sum**等各種計算，如:

	Person.sum("2 * age")

### **sum**方法預設返回值的改變

在之前的版本中，當我們使用**ActiveRecord**的**sum**方法來計算表中所有記錄的和的時候，如果沒有跟所需條件匹配的記錄時，則預設的返回值是**nil**‧在Rails 2.1中，預設返回值(當沒有匹配的記錄的時候)是0，如：

	Account.sum(:balance, :conditions => '1 = 2') #=> 0
