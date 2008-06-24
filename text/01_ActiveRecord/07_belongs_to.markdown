## Belongs_to

為了能在關連中使用**:dependent => :destroy**與**:delete**, **belongs\_to**方法做了些變更，比如：

	belongs_to :author_address
	belongs_to :author_address, :dependent => :destroy
	belongs_to :author_address_extra, :dependent => :delete, 
		:class_name => "AuthorAddress"
