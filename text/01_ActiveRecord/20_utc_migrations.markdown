## 根據時間戳記的Migrations (Timestamped Migrations)
              
當你一個人使用Rails開發時，**migrations**似乎是所有問題的最好解決方案。不過當和團隊的其他成員共同開發一個專案時，你會發現(如果你還沒發現)處理**migrations**的同步是非常棘手的。Rails 2.1中根據時間戳記的**migrations**解決方案則是漂亮的解決了這個問題。

在根據時間戳記的**migrations**引入之前，建立每個migration都會在其名字之前產生一個數字，如果兩個**migrations**分別由兩個開發者產生，並且都沒有即時的提交到版本庫中，那麼最後就有可能存在相同的前綴數字，但是不同內容的**migrations**，這時你的schema_info表就會過期，同時在版本控制系統中出現衝突。

嘗試解決這個問題的方式有很多，人們建立了很多plugins以不同的方式解決這個問題。儘管有些plugins可用，不過有一點是非常清楚的，舊的方式已經無法滿足我們的要求了。

如果你使用Git，那麼你可能再給自己挖一個更大的陷阱，因為你的團隊可能同時有幾個working branches，過期的migrations則在每個branch中都存在。這樣當合併這些branches時就會有嚴重的衝突問題。

為了解決這個大問題，Rails核心團隊已經改變了**migrations**的運作方式。他們捨棄了原有以當前schema_info中version列的值作為migration前綴的依據方式，取而代之的是根據**UTC**時間按照YYYYMMDDHHMMSS格式的字串表達方式作為前綴。

同時建立了一個新的叫做**schema_migrations**的表，表中存著哪些**migrations**已經執行了，這樣如果發現有人建立了一個有較小值的**migration**，Rails會回滾(rollback)**migrations**到之前的版本，然後重新執行所有的**migration**直到當前的版本。

顯然這樣的做法解決了**migrations**所帶來的衝突問題。

有兩個新的和**migrations**相關的rake指令：

	rake db:migrate:up
	rake db:migrate:down

