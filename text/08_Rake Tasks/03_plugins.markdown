## 外掛 (Plugins)

### Gems可外掛化 (Gems can now be plugins)

現在，任何包含**rails/init.rb**文件的gem都可以以外掛的方式安裝在**vendor**目錄底下。

### 使用插件中的生成器 (Using generators in plugins)

可以設定**Rails**使其在除了**vendor/plugins**以外的地方加入外掛，設定方法則是在*environment.rb*中加入以下程式碼：

    config.plugin_paths = ['lib/plugins', 'vendor/plugins']
    
不過Rails 2.0在這個地方有個Bug，該Bug是只在**vendor/plugins**中尋找含有生成器(Generator)的外掛，所以上面設定的路徑下的外掛的生成器並不會生效。在Rails 2.1中已經修復此問題。