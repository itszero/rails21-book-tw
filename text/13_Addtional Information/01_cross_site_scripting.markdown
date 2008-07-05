## Cross-Site Scripting的防禦

在Rails 2.0的*application.rb*中應該曾留意過以下程式碼吧？

    class ApplicationController < ActionController::Base
       helper :all
       protect_from_forgery
    end

請注意上面這段程式碼中對**protect\_from\_forgery**的呼叫。

你聽說過跨站(XSS)嗎？最近一段時間XSS攻擊日益風行，就目前而言在大多數的網站中或多或少都存在著XSS的漏洞；而XSS漏洞會被一些懷有惡意的人利用，可以用來修改網站內容、釣魚，甚至通過JavaScript來控制其他用戶的瀏覽器等等。儘管攻擊方式不同，但是其主要的目的都是使用戶在不知情的狀態下做出一些邪惡到讓我都想不出來的事情。最新的攻擊手段就叫做"Cross-Site Request Forgery"。

Cross-Site Request Forgery與前面所說的XSS原理差不多，但是更有危害性，隨著Ajax的流行，此類漏洞的利用空間與手法更加靈活！(補充：此文章簡體中文版翻譯者在之前曾寫了一篇介紹CSRF的文章，建議一讀：CSRF: 不要低估了我的危害和攻?能力)

protect_from_forgery用來確保系統接收到的表單訊息都來自於系統本身，而不會是從第三方傳送過來的；實做的原理是在表單中與Ajax請求中添加一個基於Session的標示(token)，Controller收到表單的資訊時會檢查這個Token是否匹配以決定如何回應這個Post請求。

不過這個方法並不保護以Get為主的請求，但是也沒關係，Get主要就是為了要求資料，而不會修改到資料庫中。

如果你想更多的了解CSRF (Cross-Site Request Forgery)，請參考底下幾個網址：

    * http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750
    * http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750
    * (再多一個：前面所介紹的《CSRF: 不要低估了我的危害和攻?能力》。)

請謹記，此方法並不能夠萬無一失，就像平常我們都喜歡說的那樣：他並不是銀彈！(It's not a silver bullet)