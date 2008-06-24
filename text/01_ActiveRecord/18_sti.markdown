## 使用單表繼承(STI)的時候儲存類別的全名

當我們的**models**有**namespace**，並且是單表繼承(STI)時，**ActiveRecord**僅僅將類別名稱而不是包括**namespace**(**demodulized**)在內的全名存起來。這種情況僅僅當單表繼承的所有類別在一個**namespace**的時候有效，看例子：

	class CollectionItem < ActiveRecord::Base; end
	class ComicCollection::Item < CollectionItem; end

	item = ComicCollection::Item.new
	item.type # => 'Item’

	item2 = CollectionItem.find(item.id)
	# returns an error, because it can't find
	# the class Item
      
新的Rails添加了一個屬性，從而使**ActiveRecord**能儲存類別的全名。
可以在**environment.rb**當中添加如下程式碼來啟動/關閉這個功能：

	ActiveRecord::Base.store_full_sti_class = true
                             
預設值是true。