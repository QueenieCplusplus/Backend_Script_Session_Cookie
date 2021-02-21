# Backend_Script_Session_Cookie

Web Server 處理用戶端的 Request 時，伺服器端會找出相應的函數，將結果轉成 html ，傳送並且呈現予用戶端並且中斷這請求和回應的連線。

倘若要紀錄這連線，需要使用 cookie 和 session，用戶端擁有自己的 session，伺服器端會紀錄這些來自客戶們的 session（有利於記憶登入，免於再次登入，紀錄會員的登入次數，和訪問網站的次數）。

Session 預設的生命週期始於 Browser 開始執行，死亡於 Browser 終止執行。
