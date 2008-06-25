## ActionController::Routing

### Map.root

現在你可以透過別名，更加 **DRY** 的使用 **map.root**。

在之前的 Rails 版本裡，您可能是像下面的方法使用：

	map.new_session :controller => 'sessions', :action => 'new'
	map.root :controller => 'sessions', :action => 'new'
	
在 Rails 2.1 中，你則可以直接這樣使用：

	map.new_session :controller => 'sessions', :action => 'new'
	map.root :new_session
	
### 路由識別 （Routes recognition）

之前的路由識別實作方法是一個接著一個的檢查是否符合規則，這樣做事實上是非常耗時間的。新的路由識別功能則變的聰明了，他會依照路徑自動生成一棵路由樹。這樣只需要尋找路徑上的路由規則即可，這方式將時間的耗損減少了將近 2.7 倍。

如果您有興趣了解這些實作方式，您可以參考 **recognition\_optimisation.rb** 中的新方法。其中的註解很詳細的描述了工作細節，可以提供你更多實作的相關資訊。

**recognition\_optimisation.rb** 文件中新的方法和他们的工作细节都在注释中写得很详尽。通过直接阅读源代码的方份可以获得这些实现的更多信息。

### Assert_routing

現在可以透過一個 HTTP 方法來測試路由，如下面的例子：

	assert_routing({ :method => 'put',
	                 :path => '/product/321' },
	               { :controller => "product",
	                 :action => "update",
	                 :id => "321" })
	
### Map.resources

假設您的網站並不是使用英文寫的，而你想在路徑當中也使用相同的語言。像是：
	
	http://www.mysite.com.br/produtos/1234/comentarios

而不是：

	http://www.mysite.com.br/products/1234/reviews

目前雖然是可以做到的，但是並沒有一個簡單而不需要破壞 Rails 約定(conventions)的方法。

現在我們可以使用 **map.resources** 裡的 **:as** 來自定我們的路由路徑。像是剛剛那個葡萄牙語的例子：

	map.resources :products, :as => 'produtos' do |product|
	  # product_reviews_path(product) ==
	  # '/produtos/1234/comentarios’
	  product.resources :product_reviews, :as => 'comentarios'
	end