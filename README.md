# Backend_Script_Session_Cookie

Web Server 處理用戶端的 Request 時，伺服器端會找出相應的函數，將結果轉成 html ，傳送並且呈現予用戶端並且中斷這請求和回應的連線。

倘若要紀錄這連線，需要使用 cookie 和 session，用戶端擁有自己的 session，伺服器端會紀錄這些來自客戶們的 session（有利於記憶登入，免於再次登入，紀錄會員的登入次數，和訪問網站的次數）。

Session 其實就是 Cookie，但是不同於客戶端的 cookie，session 是紀錄在伺服器端的，預設的生命週期始於 Browser 開始執行，死亡於 Browser 終止執行，也可由開發者自行定義特定秒數後，需要重新登入的方式。通常伺服器不必自行紀錄 session，然而有些客戶端會禁止伺服器端在用戶端寫入 cookie 亦或是瀏覽器不支援，所以伺服器端要承受負擔，自行紀錄 session，如果想減輕負擔，建議使用客戶端的 cookie 即可。
