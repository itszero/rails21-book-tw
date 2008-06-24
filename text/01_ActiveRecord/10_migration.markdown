## add\_timestamps和remove\_timestamps方法     
  
現在我們有兩個新的方法**add\_timestamps**與**remove\_timestamps**，他們分別添加、刪除**timestamp**列。看個例子：

	def self.up
	  add_timestamps :feeds
	  add_timestamps :urls
	end

	def self.down
	  remove_timestamps :urls
	  remove_timestamps :feeds
	end
