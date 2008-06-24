## 一種使用partials的新方法

在Rails開發過程中使用**partials**避免重複程式碼是很正常的方式，例如：

	<% form_for :user, :url => users_path do %>
		<%= render :partial => 'form' %>
		<%= submit_tag 'Create' %>
	<% end %>

**Partial**是一個程式碼片段(模版)。使用**partial**是避免不必要的程式碼重複。使用**partial**非常簡單，你可以這樣開始：**:render :partial => "name"**，之後，你必須建立一個與你的**partial**同樣名稱的文件，但是得先用一個底線作為開頭。

上面的程式碼是我們通常使用的方式，但在新的Rails版本中，我們使用不同的方式做相同的事情，如：

	<% form_for(@user) do |f| %>
		<%= render :partial => f %>
		<%= submit_tag 'Create' %>
	<% end %>

在這個範例中我們使用了partial "users/\_form"，將收到一個名為"form"被**FormBuilder**建立的變數。
不過以前的用法也是不被影響。