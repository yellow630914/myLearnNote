

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

