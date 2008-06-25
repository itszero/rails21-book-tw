## ActionView::Helpers::FormHelper

### fields\_for form\_for 和 index 選項

原本的 **#fields\_for** 和 **form\_for** 方法接受 **:index** 選項。在 form 物件中，如果想要取消就必须使用 **:index => nil**。

以前的作法可能是：

	<% fields_for "project[task_attributes][]", task do |f| %>
	  <%= f.text_field :name, :index => nil %>
	  <%= f.hidden_field :id, :index => nil %>
	  <%= f.hidden_field :should_destroy, :index => nil %>
	<% end %>

現在的作法則是：

	<% fields_for "project[task_attributes][]", task,
	              :index => nil do |f| %>
	  <%= f.text_field :name %>
	  <%= f.hidden_field :id %>
	  <%= f.hidden_field :should_destroy %>
	<% end %>