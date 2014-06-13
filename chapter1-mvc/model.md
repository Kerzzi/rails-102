#Model

## Model是什麼？

Model是繼承於ActiveRecord的Class，所以每個Model都可以取用ActiveRecord裡面的Method，例如我們有一個Model叫做Post，這個Model會長這樣：
```ruby
class Post < ActiveRecord::Base
end
```
而這個Model將會負責操作`Posts`的資料庫，由於Post Model繼承ActiveRecord，所以我們可以用ActiveRecord的method，例如：
```ruby
# first就是ActiveRecord的Method
Post.first
# => 回傳第一個Post
```

## 什麼東西應該放在Model

只要是跟操作資料庫有關的行為基本上都應該儘量放在Model裡面實作，大部份情況是要操做已經叫出來的實例變數（若對ruby的變數不太了解請先參考[ruby系列教學](chapter3-ruby/README.md)）。
