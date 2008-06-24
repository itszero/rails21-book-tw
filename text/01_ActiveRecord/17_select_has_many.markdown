## has\_one和belongs\_to中的:select選項

已經為人熟知的**has\_one**和**belongs\_to**方法現在接收一個新屬性：**:select**。

他的預設值是"*"(正如同"SELECT * FROM table")，不過你可以更改預設值來獲得任何你希望取得的欄位。

也別忘了把主鍵(Primary key)與外鍵(Foreign key)一併包入，不然會錯誤。

**belongs_to**方法不再支援**:order**了，不過不要擔心，因為基本上也沒什麼用處。