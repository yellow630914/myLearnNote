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
| includes()    | 當字串包含參數,回傳true                     | string.includes("target")    |
| startsWith()  | 當字串的開頭與參數相同,回傳true             | string.startsWith("target")  |
| endsWith()    | 當字串以參數結尾,回傳true                   | string.endsWith("target")    |

[^註3]: 若沒找到,回傳-1
[^註4]: 都能接受從哪裡開始搜索,由第二個參數填入
[^註5]: search()無法選擇從哪裡搜索,indexOf()不能用正則表達式

---

## String Templates

### Back-Tics語法

Back-Tics是指用\`把內容包起來的語法,例如:

```javascript
`this is Back-Tics`
```

在Back-Tics內可以放入多行內容,插值,和簡單的表達式,例如:

```javascript
//多行內容
let text = 
`this
is
Back-Tics
`;
//插值
let x = "xxx";
let y = "yyy";
let text = `import ${x}, ${y}`;
//表達式
let price = 5;
let VAT = 3;
let total = `Total: ${price*VAT}`
```

---

## Number Methods

| Methods         | 說明                                              | 例子                  |
| --------------- | ------------------------------------------------- | --------------------- |
| toString()      | 轉成字串                                          | Nums.toString()       |
| toExponential() | 四捨五入並以指數表示法書寫,參數指定到小數點第幾位 | Nums.toExponential(3) |
| toFixed()       | 顯示到小數點第幾位                                | Nums.toFixed(3)       |
| toPrecision()   | 指定顯示的數字長度(自動四捨五入)                  | Nums.toPrecision(3)   |
| valueOf()       | 轉成數字(對Nums來說沒用)                          | Nums.valueOf()        |
| Number()        | 轉成數字,這是一個全局methods[註6]                 | String.Number()       |
| parseInt()      | 轉成整數,這是一個全局methods                      | String.parseInt()     |
| parseFloat()    | 轉成浮點數,這是一個全局methods                    | String.parseFloat()   |

[^註6]: 若是輸入Date,回傳值是1970年1月1日往後算的毫秒數

---

## Array Methods

| Methods    | 說明                                                         | 例子                |
| ---------- | ------------------------------------------------------------ | ------------------- |
| toString() | 將array合為String,元素間自動以","隔開                        | Ary.toString()      |
| join()     | 將array合為String,元素間以參數隔開                           | Ary.join("x")       |
| pop()      | 刪除最後一個元素                                             | Ary.pop()           |
| push()     | 在最後增加一個元素                                           | Ary.push("x")       |
| shift()    | 將array的第一個移出,可以指定移出地點                         | Ary.shift()         |
| unshift()  | 在第一個加入元素                                             | Ary.unshift("x")    |
| splice()   | 插入或刪除元素,第一個參數是元素位置,第二個參數是要刪除的元素數,其餘是要插入的元素值 | Ary.splice(2,0,"x") |
| concat()   | 合併兩個Array                                                | Ary1.concat(Ary2)   |
| slice()    | 切片Array,第一個參數是起始位置,第二個是結束位置,如果沒有結束位置則會切到底 | Ary.slice(1,5)      |

---

## Array Sort

| Sort      | 說明            | 例子          |
| --------- | --------------- | ------------- |
| sort()    | 依字母排列[註7] | Ary.sort()    |
| reverse() | 反轉Array順序   | Ary.reverse() |
|           |                 |               |

[^註7]: sort會把元素全部轉成string處理,導致在處理數字時會有誤差,所以我們必須用一個function去制定他的排序規則,例如:`Ary.sort( function(a,b){return a - b} )`當sort在比較前後值時傳回`a - b`如果傳回正值則是`true`,不會交換兩者位置,反之則是`false`,會交換兩者位置

