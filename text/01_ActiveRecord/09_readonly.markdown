## 唯讀關聯 (Readonly relationships)

一個新的功能被添加到了models之間的關聯當中。為了避免更改關聯模型的狀態，現在你可以使用**:readonly**來描述一個關連。我們來看例子：

	has_many :reports, :readonly => true

	has_one :boss, :readonly => :true

	belongs_to :project, :readonly => true

	has_and_belongs_to_many :categories, :readonly => true
	      
這樣，關聯的models就能避免在model中被更改，如果試圖更改就會得到一個**ActiveRecord::ReadOnlyRecord**異常