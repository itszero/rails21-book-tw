## Cache

現在所有的**fragment\_cache\_key**方法預設回傳'view/'前綴。

所有快取儲存已經從**ActionController::Caching::Fragments::**刪除，並替換為**ActiveSupport::Cache::**。在這種情況下，如果你指定一個儲存位置，像**ActionController::Caching::Fragments::MemoryStore**，你需要這樣寫：**ActiveSupport::Cache::MemoryStore**。

**ActionController::Base.fragment\_cache\_store**已經不再使用，**ActionController::Base.cache\_store**取代了它的位置。

由於這個新的**ActiveSupport::Cache::**函式庫使得**ActiveRecord::Base**中的**cache\_key**方法容易快取一個Active Records，它是這樣運作的：

	>> Product.new.cache_key
	=> "products/new"

	>> Product.find(5).cache_key
	=> "products/5"

	>> Person.find(5).cache_key
	=> "people/5-20071224150000"

它包含了**ActiveSupport::Gzip.decompress/compress**使得用**Zlib**壓縮更加容易。

現在你可以在environment選項中使用**config.cache\_store**，指定一個預設的暫存位置。有價值提起的是，如果**tmp/cache**目錄存在，預設的暫存位置是**FileStore**，否則使用**MemoryStore**。你可以用下面的方式設定它：

	config.cache_store = :memory_store
	config.cache_store = :file_store, "/path/to/cache/directory"
	config.cache_store = :drb_store, "druby://localhost:9192"
	config.cache_store = :mem_cache_store, "localhost"
	config.cache_store = MyOwnStore.new("parameter")

為了把事情變得更容易，在*environments/production.rb*檔案中包含了以下註解，提醒你記得這個選項：

	# Use a different cache store in production
	# config.cache_store = :mem_cache_store
