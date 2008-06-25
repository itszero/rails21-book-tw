## 在 caches\_page method 方法中的條件式

**caches\_page**方法現在支援**:if**選項，例如：

	# The Rails 2.0 way
	caches_page :index

	# In Rails 2.1 you can use :if option
	caches_page :index, :if => Proc.new { |c| !c.request.format.json? }
