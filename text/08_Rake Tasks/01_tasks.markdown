## Tasks

### rails:update

從Rails 2.1開始，每次執行**rake rails:freeze:edge**指令時都會自動執行**rails:update**來更新設定檔(config)與*JavaScripts*檔案。

### Database in 127.0.0.1

databases.rake以前只用於local資料庫，現在增加對IP為127.0.0.1的資料庫。其主要是用於建立(**create**)和刪除(**drop**)任務。databases.rake採取refactored避免程式碼重複。

### 凍結指定的Rails版本 (Freezing a specific Rails release)

在Rails 2.1之前，你無法在專案內指定一個Rails版本來凍結，只能用當前版本作為參數；而在Rails 2.1後則可以用下面的指令直接指定要凍結的Rails版本：

	rake rails:freeze:edge RELEASE=1.2.0

## 時區 (TimeZone)

#### rake time:zones:all

根據時區位移(offset)分組列出所有Rails所支援的時區；你也可以透過OFFSET參數來過濾回傳的時區，例如：OFFSET=-6

#### rake time:zones:us

顯示美國的所有時區，OFFSET參數依然有效。

#### rake time:zones:local

回傳本地端系統上Rails所支援且相同的時區。

範例：

	C:\project_1> rake time:zones:local
	(in C:/project_1)
	* UTC +08:00 *
    Beijing
    Chongqing
    Hong Kong
    Irkutsk
    Kuala Lumpur
    Perth
    Singapore
    Taipei
    Ulaan Bataar
    Urumqi