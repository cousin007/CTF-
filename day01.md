## Day 1 - PicoCTF2019

### Web Exploration

1. Insp3ct0r

Web Exploit 的基礎知識，front-end 有三樣東西需要記住 html, css, js。

2. dont-use-client-side

這題我想得太複雜，心想答案沒可能就掛著給你看，結果那邊真的是答案。/唉 (這是入門啊!)
把js的flag重組就可以了。

3. logon

既然有input field，不打點東西試試太可惜了。發現是不需要password的，雖然有flag的框框，但就是不給你看，再檢查一下html 跟 js吧，沒發現可疑的地方，flag似乎是在server side。由於沒有input field，那就先檢查一下cookie，就發現cookie有一項叫"admin"的field，用cookie editor把Fasle改成True，F5就拿到flag了。

---
###小知識
ascii code為1byte大小，然而最後1bit為checksum，故此只有7bits的大小
65(0x41) -> A 
97(0x61) -> a