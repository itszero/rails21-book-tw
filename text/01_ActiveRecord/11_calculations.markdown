## Calculations 
                         
**ActiveRecord::Calculations**做了些更改已支援資料庫表名。這個功能在幾個不同表之間存在關聯且相關列名相同時會非常有用。我們有兩個選項可用：

	authors.categories.maximum(:id)
	authors.categories.maximum("categories.id")
