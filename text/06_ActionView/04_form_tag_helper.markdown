## ActionView::Helpers::FormTagHelper

### submit\_tag

**#submit\_tag** 方法中新增了 **:confirm:: 選項，同樣的選項也可以在 **link\_to** 方法中使用，像是下面這個用法：

	submit_tag('Save changes', :confirm => "Are you sure?")