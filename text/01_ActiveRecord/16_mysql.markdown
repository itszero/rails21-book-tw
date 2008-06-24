## MySQL中使用Smallint, int還是bigint？
                       
現在建立或者更改整行列的時候，**ActiveRecord**的**MySQL**介面(Adapter)會用更聰明的方式去處理，它可根據**:limit**屬性確定一個欄位的類型應該是**smallint**、**int**還是**bigint**。我們來看個實現上述功能的例子：

	case limit
	when 0..3
	  "smallint(#{limit})"
	when 4..8
	  "int(#{limit})"
	when 9..20
	  "bigint(#{limit})"
	else
	  'int(11)'
	end

現在我們在**migration**中使用它，看看每個欄位應該匹配什麼類型：

	create_table :table_name, :force => true do |t|

	  # 0 - 3: smallint
	  t.integer :column_one, :limit => 2 # smallint(2)

	  # 4 - 8: int
	  t.integer :column_two, :limit => 6 # int(6)

	  # 9 - 20: bigint
	  t.integer :column_three, :limit => 15 # bigint(15)

	  # if :limit is not informed: int(11)
	  t.integer :column_four # int(11)
	end

**PostgreSQL**介面(Adapter)已經有這個功能了，現在**MySQL**也不甘落後了。

譯者注：
前些日子在Rails的Git中注意到一個新的fix，是MySQL Adapter的更新，剛好就是這個部份。
修改的部份原始碼是：
        case limit
        when 1; 'tinyint'
        when 2; 'smallint'
        when 3; 'mediumint'
        when 4, nil; 'int(11)'
        else; 'bigint'
        end
注意到了嗎？現在只要limit是4以上就屬於bigint，所以跟原文有點出入，請注意。
未來會怎樣變更不一定，不過我想可能會就此固定也說不定
更改的Commit網址是：http://github.com/rails/rails/commit/290e1e2fc53d80165cc876491ec0cbe18be376cf
今天日期：2008-06-24