##table_exists?方法
           
**AbstractAdapter**類別有個新方法**table\_exists**，用法非常容易：

	>> ActiveRecord::Base.connection.table_exists?("users")
	=> true
