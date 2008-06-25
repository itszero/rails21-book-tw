## ActionView::Helpers::DateHelper

現在，所有與時間處理有關的樣板方法 (**date\_select**, **time\_select**, **select\_datetime**......) 都接受 **HTML** 選項了。請看下面這個例子：

	<%= date_select 'item','happening', :order => [:day], :class => 'foobar'%>
	
### date\_helper

由於使用了 **Date.current**，用來定義預設職的 **date\_helper** 方法也隨之更新。
