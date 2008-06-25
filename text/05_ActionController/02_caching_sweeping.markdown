## ActionController::Caching::Sweeping

在之前的 Rails 版本裡，當我們正在宣告 **sweeper** 的時候，我們必須使用 symbols：

	class ListsController < ApplicationController
	  caches_action :index, :show, :public, :feed
	  cache_sweeper :list_sweeper,
	                :only => [ :edit, :destroy, :share ]
	end

現在我們可以使用一個類別型態來宣告，而不需要使用 symbol。這個改變讓藏在 model 中的 **sweeper** 也可以被使用了。雖然平時您依然可以使用 symbol 宣告，但是在 Rails 2.1 中，您可以這麼做：

	class ListsController < ApplicationController
	  caches_action :index, :show, :public, :feed
	  cache_sweeper OpenBar::Sweeper,
	                :only => [ :edit, :destroy, :share ]
	end