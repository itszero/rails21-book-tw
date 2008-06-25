## 定義你的routes文件位置

在Rails 2.1中你可以定義你的routes放在哪個文件中，把底下那段程式碼寫到*environment.rb*中：

	config.routes_configuration_file

這在你擁有兩種分開的前端共享同models、libraries與plugins時非常有用。

例如，getsatisfaction.com和api.getsatisfaction.com共用相同的models，但使用不同的controllers、helpers和views。getsatisfaction擁有自己針對SEO優化的routes文件，但API routes不需要任何關於SEO的優化。