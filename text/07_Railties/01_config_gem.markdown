## config.gem

新特性**config.gem**使專案在執行時載入所有必須的gems成為可能。在*environment.rb*中可以指定專案所依賴的gems，如下：

	config.gem "bj" 

	config.gem "hpricot", :version => '0.6',
	                      :source => "http://code.whytheluckystiff.net" 

	config.gem "aws-s3", :lib => "aws/s3"

要一次安裝所有的gem依賴，我們只需要執行下面那個Rake任務：

	# Installs all specified gems
	rake gems:install

你也可以在專案執行時列出正被使用的gems：

	# Listing all gem dependencies
	rake gems

如果有個gem含有**rails/init.rb**這個檔案並且想將它放到專案中，可以用：

	# Copy the specified gem to vendor/gems/nome_do_gem-x.x.x
	rake gems:unpack GEM=gem_name

這會把這個gem複製到**vendor/gems/gem\_name-x.x.x**。若不指定gem的名稱，Rails將複製所有gems到**vendor/gem**裡面。

## 在外掛內設定gem (config.gem in plugins)

新特性**config.gem**也同樣適合在外掛中使用。

一直到Rails 2.0外掛內的**init.rb**都是如以下方式使用：

	# init.rb of plugin open_id_authentication
	require 'yadis' 
	require 'openid' 
	ActionController::Base.send :include, OpenIdAuthentication 

而在Rails 2.1中則是這樣：

	config.gem "ruby-openid", :lib => "openid", :version => "1.1.4"
	config.gem "ruby-yadis",  :lib => "yadis",  :version => "0.3.4" 

	config.after_initialize do
	  ActionController::Base.send :include, OpenIdAuthentication
	end

那麼，當你執行該任務來安裝所需的gems時，這些gems都將被包含在內。