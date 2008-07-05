## 使用method\_missing時請小心

由於Ruby是動態語言，這樣就使得**respond\_to?**非常重要，你是否經常檢查某個物件是否擁有某個方法？你是否經常使用**is\_a?**來檢查某個物件是否是我們所需要的？


然而，人們常常忘記這樣做，先來看個**method\_missing**的例子吧：

    class Dog
        def method_missing(method, *args, &block)
            if method.to_s =~ /^bark/
                puts "woofwoof!"
            else
                super
            end
        end
    end

    rex = Dog.new
    rex.bark #=> woofwof!
    rex.bark! #=> woofwoof!
    rex.bark_and_run #=> woofwoof!

我想你肯定知道**method\_missing**！在上面的例子中我建立了一個**Dog**類別的實體，然後呼叫三個並不存在的方法：**bark**, **bark!**與**bark\_and\_run**，它就會去呼叫**method\_missing**按照我用正規表達式規定的只要是bark開頭就輸出"woofwoof!"。

看起來沒任何問題吧？那麼請繼續看看我用**respond\_to?**來檢查：

    rex.respond_to? :bark #=> false
    rex.bark #=> woofwoof!

看到了嗎？它返回false，也就是說它認為該實體並沒有bark方法，怎辦？是時候來按照我們的規則來完善**respond\_to?**了！

    class Dog
    METHOD_BARK = /^bark/
        def respond_to?(method)
            return true if method.to_s =~ METHOD_BARK
        super
        end
        def method_missing(method, *args, &block)
            if method.to_s =~ METHOD_BARK
                puts "woofwoof!"
            else
                super
            end
        end
    end
    rex = Dog.new
    rex.respond_to?(:bark) #=> true
    rex.bark #=> woofwoof!

 

OK！搞定了！這樣的問題在Rails中普遍存在，你可以試試看用**respond\_to?**來檢查**find\_by\_xxx**就很明白了。

Ruby的擴展性能讓人稱奇，但是如果一不注意就有機會把自己搞得一頭霧水。

當然你應該已經猜到我要說什麼了，在Rails 2.1中這個問題已經修復了，不信的話你一樣可以試試看用**respond\_to?**來檢查**find\_by\_xxx**