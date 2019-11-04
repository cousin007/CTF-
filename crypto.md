## Cypto PicoCTF2019

### Day 5

1. The Numbers

26個英文字母的對應數值 A -> 1。

2. 13

ROT13 (Rotate by 13)，弱化版的subsitution cipher，恆定推遲13位字母 A -> N。

3. Easy1

Vigenère cipher，Polyalphabetic cipher的一種，根據key把plaintext推遲。(0-25)若key短於plaintext時，把key重覆使用直至把所有字加密。

4. ceaser

經典的凱撒密碼，key通常為一整數，把所有文字推遲的值。

5. Flags

Signal flag，海事用信號旗。

### Day 6

6. Mr-Worldwide

不知道這題是有點誤導還是我太嫩，題目說"musician left us message"，查了很久以為是db還是Hz之類的東西。一怒之下找write-up發現這是經緯度...

7. Tapping

Morse Code。

---
```
經緯度(longitude & latitude): 東經 +/- 西經、北緯 +/- 南緯
```
