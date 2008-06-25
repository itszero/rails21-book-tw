## caches\_action 支援條件式

**caches\_action**方法現在支援**:if**選項，允許使用條件式指定一個**cache**可以被暫存。例如：

	caches_action :index, :if => Proc.new { |c| !c.request.format.json? }

在上面的例子中，只有當請求不是JSON的時候，**action index**將被暫存。