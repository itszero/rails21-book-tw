## Increment 和 decrement

**ActiveRecord**的方法**increment**,**increment!**,**decrement**和**decrement!**現在支援一個新的可選參數。之前版本的Rails中你可以透過這些方法指定的屬性值加一或減一。在Rails 2.1中，你可以指定要增加或者減少的值，像這樣：

	player1.increment!(:points, 5)
	player2.decrement!(:points, 2)
                                      
上面的例子中，我向player加了5分，從player2減了2分。由於這是一個可選填的參數，所以之前的程式碼不會受到影響。