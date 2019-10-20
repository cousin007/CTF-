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
