## Web Exploration PicoCTF2019

### Day 1

1. Insp3ct0r

Web Exploit 的基礎知識，front-end 有三樣東西需要記住 html, css, js。

2. dont-use-client-side

這題我想得太複雜，心想答案沒可能就掛著給你看，結果那邊真的是答案。/唉 (這是入門啊!)
把js的flag重組就可以了。

3. logon

既然有input field，不打點東西試試太可惜了。發現是不需要password的，雖然有flag的框框，但就是不給你看，再檢查一下html 跟 js吧，沒發現可疑的地方，flag似乎是在server side。由於沒有input field，那就先檢查一下cookie，就發現cookie有一項叫"admin"的field，用cookie editor把Fasle改成True，F5就拿到flag了。

### Day 2

4. where are the robots

現在的網站上通常會有一個txt檔叫robots.txt，主要是給爬蟲看，說某某網址不想被crawler訪問。

5. Client-side-again

遇到了比較複雜的題目，與第2題相似，不過js script被obfuscate了，掉上beautify js的網站，還是很難看。其實是自己對js的寫法不熟悉所以敏感度不足，不然應該是挺容易的。看到function就直接run一下，發現array的字串是調亂過的，寫一個loop把他們都print出來吧。把新的字串順序套進verify()裡就能得到flag了。

### Day 3

6. Open-to-admins

提示很清楚要求我們修改cookies了，隨便在browser安裝一個能修改cookies的add-on，把admin跟time加進去就可以了。

7. picobrowser

首先我們把flag按一按，出現的錯誤資訊是自身browser的信息。這裡我走了一下歪路，以為是js的問題，把appVersion修改了幾次還是不行。找狂之下意外看到了header那邊有一個field叫User-Agent儲存同樣的資訊，明白了問題原來是出在request header，同樣裝一下修改header的add-on，改成picobroswer就過關了。

這邊證明了對web機制不熟悉的缺點，在看到flag是redirect的時候應該要想到問題是出在header身上，解完之後看了一下其他大大的write-up，如果是linux系統的話，直接打
```
curl -A 'picobrowser' https://....
```
簡單直接。

8. Irish-Name-Repo 1

Sql injection 的熱身題，用經典 'or 1=1 解決

9. Irish-Name-Repo 2

上一題的進階版，把' or 1=1 打進去回覆是sqli detected，證明輸入是篩選過的，接下來就測試一下那個字元是不准過的。經過一輪測試，只有or是會被偵測，換言之，這次sqli就不能夠用or來完成。最直接的替換是and，用and來造句的話，那麼2個input都要是True才會回報正確，變相必需知道正確的username才可以bypass密碼，那就來試試最常見的admin，組成下面這句:
```
admin' and 1 != 0 --
```
過關!

### 16/11/19

10. Empire1

這條有相當難度，筆者是解不到的/逃。這條明顯是insert statement，思路就是如何把insert中插入select query。嘗試把不合法的sqli打進去只會顯示500，是沒有任何error message的blind sql injection。那我們只能靠自己了。筆者是走上歪路以為他會過濾'(sigle quote)，但其實是沒有的，而且應該要發現把2個''打進去，是可以成功insert。答案是用上concatanate的技巧，這邊只可以用|| (用+會出現奇怪的東西)。
先用'脫離String，好讓我們執行sql，但我們還是在insert裡面，所以我們需要構建valid的sql statement，所以用||接上我們等下injection的result，後面也要接一下對稱的，因為需要把原本結尾的'處理掉，最後變成了這個樣子。
```
'|| 123 ||'
```
123那邊就是執行sql的地方，我們需要用括號包著要執行的語句，不過原因不明。
```
'|| (select secret from user) ||'
```
因為是blind sql injection，column跟table name都需要靠自己猜出來，不過這樣顯示的東西還不是我們需要的。這邊可能只是返回了一個result，我們可以用group_concat()把整個column串成string。
```
'|| (select group_concat(secret) from user) ||'
```
真是複雜...

---
###### 小知識
```
ascii code為1byte大小，然而最後1bit為checksum，故此只有7bits的大小
65(0x41) -> A 
97(0x61) -> a
```
```
javascript 的dot跟square bracket存在很奇妙的關係，在一句中同時有兩種notation的話，[]會被優先處理。
eg. document["getElementById"]("pass")["value"]，其實是等同於
    document.getElementById("pass").value
```
