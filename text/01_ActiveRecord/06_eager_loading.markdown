##Eager Loading

為了解釋這個新的功能，我們看看下面的代碼：

	Author.find(:all, :include => [:posts, :comments])
	
我在查詢**authors**這個表的記錄，同時通過**author_id**包含進**posts**和**comments**表。這個查詢原本會產生這樣的SQL查詢語句：

	SELECT
	  authors."id"          AS t0_r0,
	  authors."created_at"  AS t0_r1,
	  authors."updated_at"  AS t0_r2,
	  posts."id"            AS t1_r0,
	  posts."author_id"     AS t1_r1,
	  posts."created_at"    AS t1_r2,
	  posts."updated_at"    AS t1_r3,
	  comments."id"         AS t2_r0,
	  comments."author_id"  AS t2_r1,
	  comments."created_at" AS t2_r2,
	  comments."updated_at" AS t2_r3
	FROM
	  authors
	  LEFT OUTER JOIN posts ON posts.author_id = authors.id
	  LEFT OUTER JOIN comments ON comments.author_id = authors.id


這個SQL可真夠長的了，在**authors**，**posts**和**comments**三個表之間用了joins。我們叫這個為笛卡爾乘積(**cartesian product**)。


這種查詢往往效率上不高，所以Rails 2.1做了些改進。同樣對於**Author**表的查詢，現在使用了一種不同的方式從三個表中取得資料。原來用了一條SQL語句獲得三個表的記錄，現在Rails用三條不同的查詢語句，每個表一條，這比之前生成的查詢要更短。新的結果可以在執行上述程式碼後的log中看到：

	SELECT * FROM "authors"
	SELECT posts.* FROM "posts" WHERE (posts.author_id IN (1))
	SELECT comments.* FROM "comments" WHERE (comments.author_id IN (1))

絕大多數的情況下，三個簡單的查詢要比一個複雜的場查詢語句執行得更快。