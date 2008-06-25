## Labels

當使用**scaffold**產生一個新表單時，將會建立下面的程式碼：

	<% form_for(@post) do |f| %>
	  <p>
	    <%= f.label :title %><br />
	    <%= f.text_field :title %>
	  </p>
	  <p>
	    <%= f.label :body %><br />
	    <%= f.text_area :body %>
	  </p>
	  <p>
	    <%= f.submit "Update" %>
	  </p>
	<% end %>

這種方法更有意義，它包含了**label**方法。該做法在HTML標籤中回傳一個標題列。

	>> f.label :title
	=> <label for="post_title">Title</label>

	>> f.label :title, "A short title"
	=> <label for="post_title">A short title</label>

	>> label :title, "A short title", :class => "title_label"
	=> <label for="post_title" class="title_label">A short title</label>

有在標籤中注意到**for**參數嗎？"post\_title"是包含了我們的post title的文字框。這個<label>標籤實際上是一個關連到**post\_title**物件。當有人點了這個label(非連結)時，被關聯的元件就會接收到焦點。

Robby Russell在他的Blog中寫了一個關於這個主題的有趣文章。你可以從這裡閱讀：
[http://www.robbyonrails.com/articles/2007/12/02/that-checkbox-needs-a-label](http://www.robbyonrails.com/articles/2007/12/02/that-checkbox-needs-a-label)

在**FormTagHelper**中同樣也擁有**label\_tag**方法。該方法的工作方式與label一樣，但更簡單：

	>> label_tag 'name'
	=> <label for="name">Name</label> 

	>> label_tag 'name', 'Your name'
	=> <label for="name">Your name</label> 

	>> label_tag 'name', nil, :class => 'small_label'
	=> <label for="name" class="small_label">Name</label>

該方法同樣接收**:for**選項，看一個範例：

	label(:post, :title, nil, :for => "my_for")

這將回傳這樣的結果：

	<label for="my_for">Title</label>