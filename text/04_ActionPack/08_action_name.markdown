## action\_name

現在，要知道在運行時哪個View被呼叫，我們只需使用**action\_name**方法：

	<%= action_name %>

回傳值將使用**params[:action]**一樣，但更優雅。