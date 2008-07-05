## 在PostgreSQL中新增欄位

在使用**PostgreSQL**有個bug，透過migration新增一個已經存在的表的欄位時會出錯，來看看範例：

檔案： *db/migrate/002\_add\_cost.rb*

	class AddCost < ActiveRecord::Migration
	  def self.up
	    add_column :items, :cost, :decimal, :precision => 6, 
	   :scale => 2
	  end

	  def self.down
	    remove_column :items, :cost
	  end
	end

看一下，我們建立一個欄位並且**:precision => 6**、**:scale => 2**，現在執行**rake db:migration**然後看看我們的表的結果：

<table border="1" cellspacing="0" cellpadding="5">
	<tr>
		<td><strong>Column</strong></td>
		<td><strong>Type</strong></td>
		<td><strong>Modifiers</strong></td>
	</tr>
	<tr>
		<td>id</td>
		<td>integer</td>
		<td>not null</td>
	</tr>
	<tr>
		<td>desc</td>
		<td>character varying(255)</td>
		<td></td>
	</tr>
	<tr>
		<td>price</td>
		<td>numeric(5,2)</td>
		<td></td>
	</tr>
	<tr>
		<td>cost</td>
		<td>numeric</td>
		<td></td>
	</tr>
</table>

看看我們剛建立的"cost"欄位。它是一個常見的數值，但是更該像是上面的欄位如"price"，正確應該是**numeric(6, 2)**。在Rails 2.1中這個問題就已經解決囉。