## change\_table
        
在Rails 2.0中建立的**migrations**要比之前的版本更為性感，不過要想用**migrations**修改一個表可就不那麼性感了。

在Rails 2.1中修改表也由於新方法**change\_table**而變得同樣性感了。來看看性感的例子：

	change_table :videos do |t|
	  t.timestamps # this adds columns created_at and updated_at
	  t.belongs_to :goat # this adds column goat_id (integer)
	  t.string :name, :email, :limit => 20 # this adds columns name and email
	  t.remove :name, :email # this removes columns name and email
	end
              
新方法**change\_table**的使用就如同他的表兄**create\_table**，不過不是建立新的表，而是透過添加或者刪除列或索引來更改現有的表。

	change_table :table do |t|
	  t.column # adds an ordinary column. Ex: t.column(:name, :string)
	  t.index # adds a new index.
	  t.timestamps
	  t.change # changes the column definition. Ex: t.change(:name, :string, :limit => 80)
	  t.change_default # changes the column default value.
	  t.rename # changes the name of the column.
	  t.references
	  t.belongs_to
	  t.string
	  t.text
	  t.integer
	  t.float
	  t.decimal
	  t.datetime
	  t.timestamp
	  t.time
	  t.date
	  t.binary
	  t.boolean
	  t.remove
	  t.remove_references
	  t.remove_belongs_to
	  t.remove_index
	  t.remove_timestamps
	end