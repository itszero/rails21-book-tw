## ActiveRecord::Base.create接受blocks

我們已經習慣**ActiveRecord::Base.new**接受block作為參數了，現在**create**也同樣支援block了：

	# Creating an object and passing it a block describing its attributes
	User.create(:first_name => 'Jamie') do |u|
	  u.is_admin = false
	end

我們也能用同樣的方法一次建立多個物件：

	# Creating an array of new objects using a block.
	# The block is executed once for each of object that is created.
	User.create([{:first_name => 'Jamie'}, {:first_name => 'Jeremy'}]) do |u|
	  u.is_admin = false
	end

同樣在關聯中也可以使用：

	author.posts.create!(:title => "New on Edge") {|p| p.body = "More cool stuff!"}

	# or

	author.posts.create!(:title => "New on Edge") do |p|
	  p.body = "More cool stuff!"
	end
