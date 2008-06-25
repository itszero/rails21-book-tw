## flash.now現在可以在test中運作

誰沒有因為這個而頭痛過？這個問題在我們測試期間無法確定訊息已經儲存到了Flash中，因為它在到你的測試代碼之前就被Rails清掉了。

在Rails 2.1中已經沒有這個問題。現在你可以包含下面的程式碼運行在你的測試中：

	assert_equal '>value_now<', flash['test_now']
