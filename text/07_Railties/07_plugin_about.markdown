## 取得一個外掛的相關訊息 (Getting information about a plugin)

Rails 2.0 的新特性之一，或許你從未用過。我是說"大概、或許"，可能在一些比較特殊情況下會有用，來個例子，比如說取得一個外掛的版本號。

不如來玩玩看，我們要在plugin目錄裡面建立一個*about.yml*檔案，寫入下面的內容：

	author: Carlos Brando
	version: 1.2.0
	description: A description about the plugin
	url: http://www.nomedojogo.com

然後我們可以使用下面的方式來獲得相關訊息：

	plugin = Rails::Plugin.new(plugin_directory)
	plugin.about["author"] # => “Carlos Brando”
	plugin.about["url"] # => “http://www.nomedojogo.com”

如果你能在這個新特性中找到一些好的用處並願意分享，也許將改變我對它的一些看法.. 若真的有需要的話！