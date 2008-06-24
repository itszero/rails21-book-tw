## Time.current

**Time** 類別中的新方法。 **current** 的回傳值將視 **config.time\_zone** 而定。如果之前有指定時區，則傳為 **Time.zone.now**，否則回傳 **Time.now** 。

	# return value depends on config.time_zone
	Time.current

**since** 和 **ago** 方法同樣的也受到影響, 如果 **config.time\_zone** 已經指定了，它就會回傳一個 *TimeWithZone**。
 
這個修正使得 **Time.current** 方法作為取得目前時區的預設方法，替換了原有的 **Time.now** （這個方法依然可以使用，只是他不會考慮時區差異）。

**datetime\_select**方法， **select\_datetime** 和 **select\_time** 也已經改用  **Time.current** 了。