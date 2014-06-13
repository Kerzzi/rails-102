# counter_cache

counter_cache是在做關聯性資料庫時計算資料量的一個方法


照樣舉`Board`has_many`Topics`的例子來看
正常我們會寫類似下方的code來算出這個Board內有多少個Topics

```ruby
@board.topics.count
```

這代表每次我們要算數量的時候都得下一個sql指令去算有多少topics，一樣是會造成效能問題。

所以rails內建了counter_cache的方法，我們只要在topic model內加上`counter_cache: true`

```ruby
class Topic < ActiveRecord::Base
	belongs_to :board, counter_cache: true
end
```

然後在board的資料庫內新增一個叫做`topics_count`的欄位

這樣以後當這個Board內的topic有增減的時候，rails就會幫我們增減`topics_count`的欄位，如此一來下次再下`@board.topics.count`的指令時rails就會預設去找`topics_count`的欄位，不用重新下sql指令計算。

```ruby
class Topic < ActiveRecord::Base
# 我們也可以覆蓋rails的預設規定，自己定義要增減的欄位名稱，此例為count_of_topics
	belongs_to :board, counter_cache: :count_of_topics
end
```

