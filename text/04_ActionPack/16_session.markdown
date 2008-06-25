## session(:on)

或許你還不知道這個，Rails可以關閉sessions：

	class ApplicationController < ActionController::Base
	  session :off
	end

注意在我的範例中，我關閉了所有controllers中的session(**ApplicationController**)，但我也能單獨關閉某一個controller的Session。

但如果我只想打開一個controller的session，在Rails 2.1中，該方法允許**:on**選項，這樣做：

	class UsersController < ApplicationController
	  session :on
	end
