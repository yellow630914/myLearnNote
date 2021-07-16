

# vue學習

***

## 如何安裝

- 直接連接CDN : 直接使用`<script src:"https://unpkg.com/vue@next">`連接vue

- 使用npm安裝CLI : 使用npm安裝vue官方的CLI

---

## 使用Vue設定元素的text

使用vue去改變元素的text,此方式是響應式的方法,網頁會隨著資料實時改變

```html
<div id="app">
    <!--在p中放置一個msg-->
    <p>{{ msg }}</p>   
</div>
<!--這個msg因為不在#app內所以不會被作用-->
<p>{{ msg }}</p>       
<!--從本地載入vue-->
<script src="js/vue.global.js"></script> 
<script> 
    //HelloVue為一常量,其中data屬性回傳值為{msg: 'Hello Vue'}對應<p>的msg
    const HelloVue = {
        data() {
            return {
                msg : 'Hello Vue!' 
            }
        }
    }
    //創建vue的實體導入HelloVue並指向id為app的元素
    const app = Vue.createApp(HelloVue).mount('#app');
</script>
```

---

## 使用Vue生成<li>元素

使用vue可以依照資料生成list,以下三個例子都引用同樣的資料,別有不同的結果:

```html
<div id="app">
    <!--第一種方法直接引用-->
    <div>{{colleges}}</div>
    <!--結果為['list-01','list-02','list-03']-->
    <p>-----------------------------</p>
    <!--第二種方法分別將特定欄位的資料填入<li>-->
    <ul>
        <li>{{colleges[0]}}</li>
        <li>{{colleges[1]}}</li>
        <li>{{colleges[2]}}</li>
    </ul>
    <!--結果是正常的list-->
    <p>-----------------------------</p>
    <!--第三種方法是使用vue的指令-->
    <ul>
        <li v-for="list in colleges">{{list}}</li>  <!--將colleges導入{{list}}-->
    </ul>
    <!--結果與第二種一樣,但是使用vue指令之後更精簡,也更有拓展性-->
</div>
<script src="js/vue.global.js"></script>
<script>
const listApp = {
    data() {
        return {
            colleges : ['list-01','list-02','list-03']  //Array型別的資料
        }
    }
}
    
const app = Vue.createApp(listApp).mount('#app');
</script>
```



---

## Vue的事件

在vue中也可以觸發事件,以下用兩個例子示範:

```html
<body>
    <div id="app">
        <!--此元素用於顯示事件結果,與msg同步-->
        <h2>{{ msg }}</h2>
        <p>------------------------------</p>
        <!--使用v-on:click將按鈕指定為brand()的觸發器-->
        <button v-on:click="brand()">Hello</button>
        <!--v-on:click的另一種寫法可以讓code更簡潔-->
        <button @click="url()">URL</button>
    </div>
    <script src="js/vue.global.js"></script>
    <script>
        const app = Vue.createApp({
            data() {
                return {
                    //原本為空的msg,由brand()與url()等methods去改變
                    msg: ""
                }
            },
		   //methods是Vue.createApp中的屬性之一,可以寫入函式以供使用		
            methods : {       
                brand() {
                    //觸發時將msg改為指定字串
                    this.msg = 'Hello Vue!';
                },  //this指的是vue.create本身

                url() {
                    this.msg = 'https://v3.cn.vuejs.org/';
                }
            }
        }).mount('#app');
    </script>
</body>
```



---

## 簡單了解MVC,MVP與MVVM

### MVC架構

​		MVC架構是由Model,View,Controller組成,處理用戶需求的流程如圖:

​			1.先由用戶從view發出請求

​			2.controller接收到請求後開始處理邏輯,並依照邏輯透過model去改變資料

​			3.model的資料改變之後,透過view呈現給用戶

![img](https://i.imgur.com/fkA5OeM_d.webp?maxwidth=760&fidelity=grand)

​		這種架構的優點是分工明確,View負責呈現,Controller負責處理邏輯,Model負責調用更改資料,耦合度低,重複使用性高,更新方便,較適合大型的重邏輯的項目

### MVP架構

​		MVP架構是由Model,Veiw,Presenter構成,流程如下:

​			1.先由用戶透過view發送請求

​			2.請求由presenter處理後找model調用資料

​			3.資料經過presenter後再呈現給用戶

​		![img](https://i.imgur.com/v5TD2A8_d.webp?maxwidth=760&fidelity=grand)

​		這種架構適合事件驅動架構,但是會造成presenter過於擁腫

### MVVM架構

​		MVVM架構,是由Model,VeiewModel,View組成,其架構與MVP很相似,

​	不同的是viewmodel與view之間是緊密相連的,每當model改變時view跟viewmodel可以很快地實時響應,每一個view跟viewmodel之間是一對一綁定的,已達成他們之間的快速響應

![img](https://i.imgur.com/IDAECHN.png)

---

## Vue中的MVVM

下圖為vue在MVVM中的扮演的角色,接著將三個部分分開解釋:

![img](https://i.imgur.com/2meYFZy_d.webp?maxwidth=1520&fidelity=grand)

1. View : 視圖層,主要為用戶提供各種頁面訊息,在前端中指DOM
2. Model : 資料層,提供各種資料
3. ViewModel : 視圖模型層,view之間model的溝通橋樑,主要實現資料綁定(Data Binding)與DOM監聽(DOM Listeners)

![img](https://i.imgur.com/RrqvW3h_d.webp?maxwidth=760&fidelity=grand)

上圖為MVVM的一個實例,view負責呈現,viewmodel負責寫入動作,model負責裝載資料

---

## 安裝Vue.js Devtools

Vue.js Devtools是在瀏覽器上的開發工具,能夠幫助開發者在瀏覽器上調整vue代碼,此工具可以直接在chrome與firefox插件商店找到

- [google chrome](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-TW)

---

## Mustache語法

example : `{{ msg }}`就是vue中的Mustache語法,主要放置一些變數或簡單的表達式,以下示範4個例子:

```html
<body>
	<div id='app'>
		<!--在{{ msg }}後也可增加一段text-->
		<h2>{{ msg }}  https://v3.cn.vuejs.org/</h2>
		<!--{{}}中可以有簡單的表達式,如下-->
		<h2>{{ msg + '  ' + site }}</h2>
		<!--在通一個元素裡可同時存在兩個{{}}-->
		<h2>{{ msg }}  {{ site }}</h2>
		<!--在{{}}中也可進行簡單的計算-->
		<h2>計算: {{ count * 10 }}</h2>
	</div>
	<script src='js/vue.global.js'></script>
	<script>
		const app = Vue.createApp({
			data() {
				return {
					msg: 'Hello Vue!',
					site: 'https://v3.cn.vuejs.org/',
					count: '2'
				}
			}
		}).mount('#app');
	</script>
</body>
```

值得注意的是`{{}}`只能適用於元素之內,無法在元素的屬性欄位使用

---

## Vue的插值語法

vue的插值語法主要負責填入mustache中的相關變數,常用的有`v-text,v-html,v-pre,v-once,v-cloak`接著依序看這5個語法的實例與用途

### v-once的用途與實例

```html
<div id='app'>
  <!--這個msg會隨著model中的msg改變-->
  <h2>會變的: {{ msg }}</h2>
  <!--這個msg會保持原樣,之後即使model中的msg改變也不會隨著改變-->
  <h2 v-once>不變的: {{ msg }}</h2>
</div>

```

被`v-once`語法標記的元素中,所有`{{}}`中的變數只能保持原樣,不會跟著model的資料而改變

### v-text的用途與實例

```html
<div id='app'>
  <!--這個msg與下面的是一樣的-->
  <h2>{{ msg }}</h2>
  <!--這個元素中的text是由vue的語法填充,若是其中已經有其他內他會覆蓋之-->
  <h2 v-text="msg">Vue is bad</h2>
</div>
```

`v-text="msg"`的功能與`{{ msg }}`相差無幾,但是`{{ msg }}`能夠更有彈性,例如:`<h2>{{ msg }}!!!!<h2>`等等,`v-text`還有一個特點,就是它會覆蓋原本的text,如上面的例子中`Vue is bad`就不會被顯示

### v-html的用途與實例

```html
<div id='app'>
  <!--直接將site放入會當作文本呈現-->
  {{site}}
  <!--使用了v-html之後,就能夠正常顯示連結了-->
  <div v-html="site"></div>
</div>
```

`v-html`可以插入html的標籤語法,如果直接將html語法放入`{{}}`中的話,他們會被當成文本處裡,使用了v-html後就能正常呈現了

### v-pre的用途與實例

```html
<div id='app'>
  <!--這個msg會正常顯示-->
  <h2>編譯: {{ msg }}</h2>
  <!--這個msg因為v-pre而不去編譯,所以顯示{{ msg }}-->
  <h2 v-pre>不編譯: {{ msg }}</h2>
</div>
```

v-pre會讓元素內的{{}}不被vue編譯

### v-cloak的用途與實例

v-cloak是一個在編譯完成後會被消除的語法,而它的使用情況通常都在防止編譯前,網站把原碼呈現到用戶頁面上,因此我們的以下例子先以`setTimeout()`延遲了編譯完成的時間,去模擬網路不順的情況,然後我們賦予`v-cloak`一個樣式,讓元素在有`v-cloak`時被隱藏,例如:

```html
<style>
  /*指定v-cloak的樣式*/
  [v-cloak]{
    display:none;
  }
</style>
```
以下有兩個`{{ msg }}`沒有`v-cloak`的會在延遲的五秒內保持{{ msg }},而有`v-claok`則是會被隱藏

```html
<body>
  <div id='app'>
    <!--普通的{{ msg }}-->
    <h2>沒有v-cloak: {{ msg }}</h2>
    <!--v-claok會在Vue編譯完成之後消失-->
    <h2 v-cloak>有v-claok: {{ msg }}</h2>
  </div>
  <script src='js/vue.global.js'></script>
  <script>
    //這裡用setTimeout延遲5秒,模擬網路不順的情況
    setTimeout(()=>{
      const app = Vue.createApp({
      data() {
        return {
          msg: 'Hello Vue!'
        }
      }
    }).mount('#app');
    }
    ,5000)
  </script>
</body>
```

---

## v-bind

### v-bind的基礎

v-bind主要負責綁定元素的屬性,將元素中屬性與model綁定,讓他們可以隨著動態改變,簡單的範例如下:

```html
<body>
  <div id='app'>
    <h2>{{ msg }}</h2>
    <!--沒有加入v-bind的元素,其在屬性中的值會直接視為字串-->
    <img src="imgUrl" alt="">
    <!--加入v-bind之後就可以調用model裡的值了-->
    <img v-bind:src="imgUrl" v-bind:alt="alt">
    <!--v-bind的簡寫使用':'-->
    <a :href="site">vue</a>
  </div>
  <script src='js/vue.global.js'></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          //model層
          msg: 'Hello Vue!',
          imgUrl:'https://i.imgur.com/EpGLUi4.gif',
          alt:'報社',
          site:'https://v3.cn.vuejs.org/'
        }
      }
    }).mount('#app');
  </script>
</body>
```

範例中只要更改`model`中的的資料即可實時更改`view`中的圖片,網址等等...

### v-bind綁定class

`v-bind`也可以綁定css中的class,先從style中設定class

```html
<style>
  .red{
    color: red;
  }
  .f60{
    font-size: 60px;
  }
</style>
```
接著將vue中的data綁定到css中的class,使用了`v-bind`之後,class屬性會依照vue中的data找

```html
<body>
  <div id='app'>
    <!--直接從使用class-->
    <h2 class='red'>{{ msg }}</h2>
    <!--當加入:後編譯器會從model去找class-->
    <h2 :class='red'>{{ msg }}</h2>
    <!--此h2成功在model找到了class-->
    <h2 :class='css1'>{{ msg }}</h2>
    <p>---------------------------------------------------</p>
    <!--當需要使用到多個class時可以使用以下方法,值得注意的是{}中的class名不會從vue中找,而是從css直接找class,vue只負責處理布林值-->
    <h2 :class="{ red: isCss1, f60: isCss2 }">{{ msg }}</h2>
    <!--設置一個按鈕事件change()-->
    <button @click="change">switch</button>
    <p>---------------------------------------------------</p>
    <!--另一個調用多class的方法,無法用布林值控制-->
    <h2 :class="[css1 ,css2]">{{ msg }}</h2>
    <!--直接使用封裝好的array-->
    <h2 :class="mixClass()">{{ msg }}</h2>
  </div>
  <script src='js/vue.global.js'></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          msg: 'Hello Vue!',
          //這是綁定到css中class的參數
          css1: 'red',
          css2: 'f60',
          //這是用於開關v-bind{}中的布林值
          isCss1: true,
          isCss2: true
        }
      },
      methods: {
        //與按鈕事件相綁定,當按下按鈕時兩布林值逆轉
        change(){
          this.isCss1 = !this.isCss1;
          this.isCss2 = !this.isCss2;
        },
        //將兩個class封裝成一個array
        mixClass(){
          return [this.css1 ,this.css2];
        }    
      }
    }).mount('#app');
  </script>
</body>
```

若是需要使用多個class,可以用`{}`,`{}`的格式是`{className1: boolean, className2: boolean}`,值得注意的是,`className`指的是css中的class,而不是vue中的data

除了{}之外也可使用[]來實現多個class,[]無法使用布林值控制,當class使用過多,過於冗長時可以直接用methods將之封裝起來,{}也可使用此方法

### v-bind綁定style

`v-bind`可以綁定style屬性,並讓style動態變化,透過vue設定style時需要使用{},{}中的格式是`{界值: '字串'}`,界值因不能有-符號,所以`font-size`必須變為`fontSize`,而60px必須套上' '

```html
<body>
  <div id='app'>
    <!--直接設定style-->
    <h2 style="font-size: 60px;">{{ msg }}</h2>
    <!--透過vue設定style-->
    <h2 :style="{fontSize: '60px'}">{{ msg }}</h2>
    <!--設定多項style-->
    <h2 :style="{fontSize: f60, backgroundColor: bColor}">{{ msg }}</h2>
    <!--直接使用封裝好的style-->
    <h2 :style="mixStyle()">{{ msg }}</h2>
  </div>
  <script src='js/vue.global.js'></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          msg: 'Hello Vue!',
          f60: '60px',
          bColor: 'red'
        }
      },
      methods: {
        //封裝可讓v-bind使用的style
        mixStyle(){
          return {fontSize: this.f60, backgroundColor: this.bColor}
        }
      },
    }).mount('#app');
  </script>
</body>
```

---

## v-on

### v-on的基礎

v-on是在元素上附加事件的vue語法,他可以將view的元素與viewmodel端的函式相綁定,以達到當觸發事件時,執行methods中的函式,以下示範click事件:

```html
<body>
  <div id='app'>
    <h2>{{ count }}</h2>
    <!--當按下按鈕時觸發add事件-->
    <button v-on:click="add">+</button>
    <!--當按下按鈕時觸發sub事件-->
    <button @click="sub">-</button>
  </div>
  <script src='js/vue.global.js'></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          //count是一個數值物件
          count: 0
        }
      },
      methods: {
        add(){
          //當add被執行時count+1
          this.count++;
        },
        sub(){
          //當sub被執行時count-1
          this.count--;
        }
      },
    }).mount('#app');
  </script>
</body>
```

### v-on參數傳遞

v-on中,當函數有參數需要輸入時,會有各種情況,以下列出4種情況:

```html
<body>
  <div id='app'>
    <!--指定函式帶有(),代表輸入空值-->
    <button @click="btn1()">btn1</button>
    <!--指定函式時沒有(),則選擇自動填入事件本身-->
    <button @click="btn2">btn2</button>
    <!--填入的參數可以是數字,字串,布林值,同時也可以是data內的物件,他會去vue中找msg-->
    <button @click="btn3(123, 'fff', true ,msg)">btn3</button>
    <!--當你需要填入參數與事件本身時可以使用$,通常需要填入事件時會放在最後-->
    <button @click="btn4(123, 'fff', true ,msg ,$event)">btn4</button>
  </div>
  <script src='js/vue.global.js'></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          msg: "哭阿"
        }
      },
      methods: {
        btn1(logText){
          //有(),而沒有填入參數時會log undefined
          console.log(logText);
        },
        btn2(logText){
          //沒有()時直接log事件本身
          console.log(logText);
        },
        btn3(log1,log2,log3,log4){
          //一一顯示個參數
          console.log(log1,log2,log3,log4);
          //直接抓取參數array
          console.log(arguments);
        },
        btn4(log1,log2,log3,log4,event){
          //顯示事件本身
          console.log(log1,log2,log3,log4,event);
        }
      },
    }).mount('#app');
  </script>
</body>
```

### v-on常用修飾符



