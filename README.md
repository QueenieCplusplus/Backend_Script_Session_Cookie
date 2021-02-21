# Backend_Script_Session_Cookie

Web Server 處理用戶端的 Request 時，伺服器端會找出相應的函數，將結果轉成 html ，傳送並且呈現予用戶端並且中斷這請求和回應的連線。

倘若要紀錄這連線，需要使用 cookie 和 session，用戶端擁有自己的 session，伺服器端會紀錄這些來自客戶們的 session（有利於記憶登入，免於再次登入，紀錄會員的登入次數，和訪問網站的次數）。

Session 其實就是 Cookie，但是不同於客戶端的 cookie，session 是紀錄在伺服器端的（或是從用戶端的瀏覽器記憶體取得），預設的生命週期始於 Browser 開始執行，死亡於 Browser 終止執行，也可由開發者自行定義特定秒數後，需要重新登入的方式。通常伺服器不必自行紀錄 session，然而有些客戶端會禁止伺服器端在用戶端寫入 cookie 亦或是瀏覽器不支援，所以伺服器端要承受負擔，自行紀錄 session，如果想減輕負擔，建議使用客戶端的 cookie 即可，細節原理就是伺服器在用戶端寫入小檔案，是伺服器放在用戶端的記憶體或磁碟中的一識別紀錄（類似叫號的號碼牌），所以如果使用者重複登入網站，伺服器端利用取出客戶端小檔案的識別號碼認得用戶是誰，進而得知用戶端訪問網站的次數。

資安問題的話，用戶端為了避免個資外洩，通常會選擇拒絕寫入伺服器檔案至自己瀏覽器的記憶體和磁碟。至於開發者的設定方式如下：

     setcookie("name", "value", expire: int, path: string, domain: string, secure: bool)
     
     // 如同食物有包鮮期限，cookie 也會因為開發者設定的秒數而自動消失。
     // 關於網域，伺服器可能同時擁有很多網域，為避免一網域存取另一網域 cookie，需要分開設定。
     // 路徑為根目錄，識別檔案存放在用戶端的存放路徑。



Session 如同 cookie 作為全領變數能存放陣列型態的資料，陣列通常是 DB 的取出物件，是個二維陣列型態的資料。使用方式，可詳見同一母標題的後端腳本類別中的購物車範例：


    session_start();
    
    
    if(!empty($_GET["action"])) {
    
      switch($_GET["action"])){
      
         case "A": // switch 用於『多途決策』， if 用於查核驗證。
            if(!empty($_POST["數量"])){
               if(in_array(某碼, array_key($_SESSION["購物車品項"]))){
                  foreach($_SESSION["購物車品項"] as $key=>$value){
                      if(某碼==$key){
                      
                         // if 多做一道驗證，例如數量為 0 則如下行數字為 0
                         $_SESSION["購物車品項"][$key]["數量"] += $_POST["數量"]
                      
                      }
                  }
               }
            }
         break;
         case "B":
            if(!empty($_SESSION["購物車品項"])){
                foreach($_SESSION["something"] as $key=>$value) // 此處的 => 即 java 中的 dot 
            
            }
         break;
         case "c":
            unset($_SESSION["購物車品項"]);
         break;
      }
    
    }
  
     ....
  
   // 倘若使用者按下了淨空資料，則 ... 金額與數量歸零。
   
    <a id="btnEmpty" href="index.php?action=empty">Clean the Cart Record!</a>
    <?php
    if(isset($_SESSION["購物車品項"])){
        $total_quantity = 0;
        $total_price = 0;
    ?>
    else {
    ?>
    <div class="no-records">Your Cart is Empty</div>
    <?php 
    }
    ?>
    
   // 倘若需要計算總數量與總金額，仍要與 Session 合作。
   // 第一則函數為小計
   // 第二則函數為總計
   
       <?php		
        foreach ($_SESSION["購物車品項"] as $item){
        
            $item_price = $item["數量"]*$item["價格"];
            
            }
        ?>
				
		<?php
			$total_quantity += $item["數量"];
			 $total_price += ($item["數量"]*$item["價格"]);
		
		?>
   
   // 單純地秀出商品的編號、品名、照片、金額，邏輯與紀錄 session 無關。
   

#SID 

同一台電腦，倘若分成 safari、chrome、IE 三種瀏覽器登入同一網站，cookie 是不同的！但是同一瀏覽器，不同分頁，則是同一 cookie。

https://bbs.csdn.net/topics/300114707 
