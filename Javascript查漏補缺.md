# Javascript查漏補缺

---

## let與var的差別(ES6)

let只會作用於當前的區塊,適用於只在特定區塊內使用的變數,例如:

```javascript
let x = 1;

if(x === 1){
    let x = 2;
    console.log(x);
    //output: 2
}

console.log(x);
//output: 1
```

var則是全域的,若是在區塊之外更改他,他會跟著改變

---

## const的細節(ES6)

當const是一個array時,你可以用`array[x] = value`去改變他們,也可以用Array的methods去改變,但是不能一次改變一整個array

```javascript
const cars = ["Saab", "Volvo", "BMW"];

//更改一個元素
cars[0] = "Toyota";

// 使用methods
cars.push("Audi");

//這樣不行
cars = ["Toyota", "Volvo", "Audi"];
```

一個const object也是

```javascript
const car = {type:"Fiat", model:"500", color:"white"};

//更改一個屬性
car.color = "red";

//添加一個屬性
car.owner = "Johnson";

//不行
car = {type:"Volvo", model:"EX60", color:"red"};
```

---

## 次方運算子**(ES6)

ES6添加的次方運算子:

```javascript
let x = 2;

//y是2的2次方等於4
let y = x**2;
//z是2的4次方等於16
let z = x**4;
```

---

## 當function沒有()回傳

當函數沒有()時會回傳函數物件,而不是結果

```javascript
function mo(i){
    return 3;
}
//output: function mo(i){ return 3; }
console.log(mo)
```

---

## String Methods

| Method        | 說明                                                         | 例子                       |
| ------------- | ------------------------------------------------------------ | -------------------------- |
| length()      | 回傳字串長度                                                 | string.length              |
| slice()       | 回傳範圍內的字串,最後一個是切出位置,不會擷取                 | string.slice(2,7)          |
| slice(負值)   | 使用負值回從最後開始擷取                                     | string.slice(-7,-2)        |
| substring()   | 與slice相似,無法接受負值                                     | string.substring(2,7)      |
| substr()      | 類似slice,但是第2個參數是指要擷取的字串長度(也可輸入負值)    | string.substr(2,5)         |
| replace()     | 把目標字串替換掉,第一個參數是目標,第二個是結果,一般只會替換第一個遇到的[註1] [註2] | string.replace("yes","no") |
| toUpperCase() | 轉換大寫                                                     | string.toUpperCase()       |
| toLowerCase() | 轉換小寫                                                     | string.toLowerCase()       |
| trim()        | 去頭尾的空格                                                 | string.trim()              |
| padStart()    | 從頭部填充,第一個參數是數量,第二個是字串                     | string.padStart(2,"s")     |
| padEnd()      | 從尾部填充,參數設置同上                                      | string.padEnd(2,"e")       |
| charAt()      | 回傳索引值的字符(若為空回傳"")                               | string.charAt(3)           |
| charCodeAt()  | 回傳索引值的UTF-16 code                                      | string.charCodeAt(3)       |
| string[]      | 由索引值去訪問自符(只讀,若為空回傳undefined)                 | string[3]                  |
| split()       | 將字串轉為array,參數為忽略的字串                             | split(",")                 |

[^註1]: 正則表達式 : 在/STRING/i中,大小寫會被視為相同
[^註2]: 正則表達式 : 若要替換所有目標,可用/string/g

---

## String Search

| Search        | 說明                                        | 例子                         |
| ------------- | ------------------------------------------- | ---------------------------- |
| indexOf()     | 回傳目標出現的第一個字符索引值[註3] [註4]   | string.indexOf("target")     |
| lastIndexOf() | 回傳目標出現的最後一個字符索引值[註3] [註4] | string.lastIndexOf("target") |
| search()      | 回傳目標出現的第一個字符索引值[註5]         | string.seach("target")       |
| match()       | 回傳與參數相同的字串,若為多個,形成array     | string.match(/target/g)      |
|               |                                             |                              |

[^註3]: 若沒找到,回傳-1
[^註4]: 都能接受從哪裡開始搜索,由第二個參數填入
[^註5]: search()無法選擇從哪裡搜索,indexOf()不能用正則表達式

