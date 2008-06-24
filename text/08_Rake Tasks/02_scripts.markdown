## Scripts

### plugin

現在這個命令(script/plugin install)可以使用 –e/--export 參數來導出SVN。另外增加了對Git的支援。

### dbconsole

這個腳本和script/console一樣，但是是針對你的資料庫操作，換句話說，它採用命令列型態來連接到你的資料庫。

不過就目前為止，僅僅支援mysql, postgresql與sqlite(含第3版)，如果你在database.yml中設定其他類型的資料庫介面時，會顯示"Unknown command-line client for 你的資料庫名稱. Submit a Rails patch to add support!"(不明的命令列模式用戶端。給我們一個Patch讓Rails支援!)
