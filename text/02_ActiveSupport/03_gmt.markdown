## UTC or GMT?

這是一個很有趣的修正。:P 到目前為止，Rails 通常使用 UTC 這個縮寫。但是在 **TimeZone.to_s** 裡頭，它卻回傳 GMT，而不是熟系的 UTC。這是因為使用 GMT 對您的產品使用者來說是最為熟悉的縮寫。
  
如果您注意觀察 Windows 的時間設定視窗，時區它也使用 GMT 作為縮寫。同樣的，Google 和 Yahoo 也在他們旗下的產品中使用 GMT。

	TimeZone['Moscow'].to_s #=> "(GMT+03:00) Moscow"
