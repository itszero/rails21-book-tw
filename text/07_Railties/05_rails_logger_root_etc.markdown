## Rails 的日記記錄、根目錄、環境變數與快取(Rails.logger, Rails.root, Rails.env and Rails.cache)

在Rails 2.1內有新方式可以取代常數：**RAILS\_DEFAULT\_LOGGER**, **RAILS\_ROOT**, **RAILS\_ENV** 和 **RAILS\_CACHE**。取而代之的是：

	# RAILS_DEFAULT_LOGGER
	Rails.logger

	# RAILS_ROOT
	Rails.root

	# RAILS_ENV
	Rails.env

	# RAILS_CACHE
	Rails.cache
