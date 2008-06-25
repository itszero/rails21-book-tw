## TimeZone

### 定義一個預設的時區

一個新的選項被加入到**time\_zone\_select**方法，在你的用戶沒有選擇任何**TimeZone**或者資料庫欄位為空時，你可以顯示一個預設值。它已經建立一個**:default**選項，你可以按照下面的方式使用這個方法：

	time_zone_select("user", "time_zone", nil, :include_blank => true)
	
	time_zone_select("user", "time_zone", nil, 
		:default => "Pacific Time (US & Canada)" )
	
	time_zone_select( "user", 'time_zone', TimeZone.us_zones, 
		:default => "Pacific Time (US & Canada)")

如果我們使用**:default**選項，它就會顯示**TimeZone**已被選擇的選項。

### formatted_offset 方法

**formatted\_offset**方法被包含在**Time**和**DateTime**類別中，回傳**+HH:MM**格式的UTC時差。例如，在我們的時區(台北時間)，這個方法回傳的時差是一個字串**"+08:00"**。

讓我們看看一些範例：

從一個DateTime得到時差：

	datetime = DateTime.civil(2000, 1, 1, 0, 0, 0, Rational(-6, 24))
	datetime.formatted_offset         # => "-06:00″
	datetime.formatted_offset(false)  # => "-0600″

從Time：

	Time.local(2000).formatted_offset         # => "-06:00″
	Time.local(2000).formatted_offset(false)  # => "-0600″

注意這個方法回傳字串，可以格式化或者不依賴於一個被給予的參數。

### with\_env\_tz 方法

**with\_env\_tz**方法允許我們以非常簡單的方式測試不同的時區：

	def test_local_offset
	  with_env_tz 'US/Eastern' do
	    assert_equal Rational(-5, 24), DateTime.local_offset
	  end
	  with_env_tz 'US/Central' do
	    assert_equal Rational(-6, 24), DateTime.local_offset
	  end
	end

這個Helper可以呼叫**with\_timezone**，但是為了避免使用**ENV['TZ']**和**Time.zone**時混亂，他被重新命名為**with\_env\_tz**。

### Time.zone_reset!

該方法已經跟我們說再見了。

### Time#in\_current\_time\_zone

該方法修改為當**Time.zone**為空時傳回**self**

### Time#change\_time\_zone\_to\_current

該方法修改為當**Time.zone**為空時傳回**self**

### TimeZone#now

該方法修改為傳回**ActiveSupport::TimeWithZone**顯示當前在**TimeZone#now**中已經設定的時區。例如：

	Time.zone = 'Hawaii'  # => "Hawaii"
	Time.zone.now         # => Wed, 23 Jan 2008 20:24:27 HST -10:00

### Compare\_with\_coercion
	
在**Time**和**DateTime**類別中新增了一個方法：**compare\_with\_coercion**(和一個alias <=>)，它使在**Time**、**DateTime**類別和**ActiveSupport::TimeWithZone**實體之間可以按照年代順序排列的比較。為了容易理解，請看下面的例子(行尾是顯示的結果)：

	Time.utc(2000) <=> Time.utc(1999, 12, 31, 23, 59, 59, 999) # 1
	Time.utc(2000) <=> Time.utc(2000, 1, 1, 0, 0, 0) # 0
	Time.utc(2000) <=> Time.utc(2000, 1, 1, 0, 0, 0, 001)) # -1

	Time.utc(2000) <=> DateTime.civil(1999, 12, 31, 23, 59, 59) # 1
	Time.utc(2000) <=> DateTime.civil(2000, 1, 1, 0, 0, 0) # 0
	Time.utc(2000) <=> DateTime.civil(2000, 1, 1, 0, 0, 1)) # -1

	Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(1999, 12, 31, 23, 59, 59) )
	Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(2000, 1, 1, 0, 0, 0) )
	Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(2000, 1, 1, 0, 0, 1) ))

### TimeWithZone#between?

在**TimeWithZone**類別中包含**between?**方法檢驗一個實體被建立在兩個日期之間。

	@twz.between?(Time.utc(1999,12,31,23,59,59),
	              Time.utc(2000,1,1,0,0,1))
	
### TimeZone#parse
	
這個方法從字串建立一個**ActiveSupport::TimeWithZone**實體。例如：

	Time.zone = "Hawaii"
	# => "Hawaii"
	Time.zone.parse('1999-12-31 14:00:00')
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00


	Time.zone.now
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00
	Time.zone.parse('22:30:00')
	# => Fri, 31 Dec 1999 22:30:00 HST -10:00

### TimeZone#at

這個方法可以從一個Unix epoch數字建立一個**ActiveSupport::TimeWithZone**實體，例如：

	Time.zone = "Hawaii" # => "Hawaii"
	Time.utc(2000).to_f  # => 946684800.0

	Time.zone.at(946684800.0)
	# => Fri, 31 Dec 1999 14:00:00 HST -10:00

### 其他方法

**to\_a**, **to\_f**, **to\_i**, **httpdate**, **rfc2822**, **to\_yaml**, **to\_datetime** 和 **eql?**被加入TimeWithZone類別中。更多關於這些方法的訊息請查閱同版本的Rails文件。

### TimeWithZone為了Ruby 1.9而準備

在Ruby 1.9中我們有了一些新的方法在 **Time**類別中，如：

	Time.now
	# => Thu Nov 03 18:58:25 CET 2005

	Time.now.sunday?
	# => false

一週的每天都有對應的方法。

另一個新的是**Time**的**to\_s**方法將會有一個不同的傳回值。現在當我們執行**Time.new.to\_s**，將得到：

	Time.new.to_s
	# => "Thu Oct 12 10:39:27 +0200 2006″

在Ruby 1.9中我們將得到：

	Time.new.to_s
	# => "2006-10-12 10:39:24 +0200″

Rails 2.1擁有哪些相關的東西？答案是所有東西，從Rails開始準備這些修改。**TimeWithZone**類別，例如，剛收到一個第一個範例的方法實現。