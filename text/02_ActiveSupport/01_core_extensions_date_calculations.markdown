## ActiveSupport::CoreExtensions::Date::Calculations

### Time#end\_of\_day

回傳當天的結束時間（11:59:59 PM)

### Time#end\_of\_week

回傳當週的週末結束時間 (Sunday 11:59:59 PM)

### Time#end\_of\_quarter

回傳一個 Date 物件，表示本季的最後一天。換句話說，他是根據目前日期回傳三月、六月、九月或者十二月的最後一天。

### Time#end\_of\_year

回傳本年度的結束時間，也就是 12/31 11:59:59 PM

### Time#in\_time\_zone

這個方法跟 **Time#localtime** 很類似，除了他使用 Time.zone 作為時區基準，而不是目前作業系統設定的時區。您可以傳入 **TimeZone** 或是 **String** 作為參數。如下面的例子：

    Time.zone = 'Hawaii'
    Time.utc(2000).in_time_zone
    # => Fri, 31 Dec 1999 14:00:00 HST -10:00
    
    Time.utc(2000).in_time_zone('Alaska')
	# => Fri, 31 Dec 1999 15:00:00 AKST -09:00

### Time#days\_in\_month

這個方法本來有個bug，當沒有指定年份的時候，對於二月他沒有辦法正確處理潤年。不過在 Rails 2.1 中這個問題已經被修正了。

這個修正的作法是，如果您沒有指定年份，則使用呼叫時的當年度作為預設值。如果您處於潤年的話，參考下面的例子：

	Loading development environment (Rails 2.0.2)
	>> Time.days_in_month(2)
	=> 28

	Loading development environment (Rails 2.1.0)
	>> Time.days_in_month(2)
	=> 29

### DateTime#to_f

DateTime 類別新增了一個方法 **to_f**，它的作用是將日期以浮點數的形態回傳。這個浮點數遞逮表從 Unix 紀元 (1970, 1月1日午夜。也就是平常熟知的 UNIX Timestamp) 開始計算經過的秒數。

### Date.current

Date 類別則新增了一個新方法稱為 **current** 來取代原有的 **Date.today** 。這個方法將會考慮到您在 **config.time\_zone** 中設定的時區。如果您有設定，這個方法將回傳 **Time.zone.today** 。如果沒有的話，則直接回傳 **Date.today** 。
