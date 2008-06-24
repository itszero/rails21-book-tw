## Mem\_cache\_store now accepts options

  自從 **Memcache-Client** 被包入 **ActiveSupport::Cache** 後就使得事情變得比以前更容易了。但是他也相對的剝奪了靈活性。它只允許您設定 **memcahced** 伺服器的 IP 位置而已。
  
  **Jonathan Weiss** 送給 Rails 團隊一個修正，使其能夠接受額外的選項，像是：

	ActiveSupport::Cache.lookup_store :mem_cache_store, "localhost"

	ActiveSupport::Cache.lookup_store :mem_cache_store, "localhost", '192.168.1.1', 
		:namespace => 'foo'

   或者

	config.action_controller.fragment_cache_store = :mem_cache_store, 'localhost', {:compression => true, :debug => true, :namespace =>'foo'}
