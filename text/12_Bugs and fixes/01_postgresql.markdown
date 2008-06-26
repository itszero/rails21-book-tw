## �bPostgreSQL���s�W���

�b�ϥ�**PostgreSQL**����bug�A�z�Lmigration�s�W�@�Ӥw�g�s�b�������ɷ|�X���A�Ӭݬݽd�ҡG

�ɮסG *db/migrate/002\_add\_cost.rb*

	class AddCost < ActiveRecord::Migration
	  def self.up
	    add_column :items, :cost, :decimal, :precision => 6, 
	   :scale => 2
	  end

	  def self.down
	    remove_column :items, :cost
	  end
	end

�ݤ@�U�A�ڭ̫إߤ@�����åB**:precision => 6**�B**:scale => 2**�A�{�b����**rake db:migration**�M��ݬݧڭ̪������G�G

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

�ݬݧڭ̭�إߪ�"cost"���C���O�@�ӱ`�����ƭȡA���O��ӹ��O�W�������p"price"�A���T���ӬO**numeric(6, 2)**�C�bRails 2.1���o�Ӱ��D�N�w�g�ѨM�o�C