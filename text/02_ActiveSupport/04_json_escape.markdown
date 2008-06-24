## JSON escape

**json\_escape** 方法就像是 **html\_escape** 所做的事情一樣。當我們想在 **HTML** 頁面中顯示 **JSON** 字串的時候非常有用。例如：
  
    json_escape("is a > 0 & a < 10?")
    # => "is a \u003E 0 \u0026 a \003C 10?"

在 ERB 樣板中，我們可以使用簡寫 **j** (就像是 **h** 一樣)：

    <%= j @person.to_json %>
    
如果您希望所有 **JSON** 碼都自動被跳脫（esacped），您可以在 *environment.rb* 中加入下面的程式碼：
  
    ActiveSupport.escape_html_entities_in_json = true
