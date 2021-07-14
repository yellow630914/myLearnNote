

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
    <p>{{ msg }}</p>   <!--在p中放置一個msg-->
</div>
<p>{{ msg }}</p>       <!--這個msg因為不在#app內所以不會被作用-->
<script src="js/vue.global.js"></script>  <!--從本地載入vue-->
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

## Pr2

---

## PR3

---

## 簡單了解MVC,MVP與MVVM

### 	MVC架構

​		MVC架構是由Model,View,Controller組成,處理用戶需求的流程如圖:

​			1.先由用戶從view發出請求

​			2.controller接收到請求後開始處理邏輯,並依照邏輯透過model去改變資料

​			3.model的資料改變之後,透過view呈現給用戶

![img](https://i.imgur.com/fkA5OeM_d.webp?maxwidth=760&fidelity=grand)

​		這種架構的優點是分工明確,View負責呈現,Controller負責處理邏輯,Model負責調用更改資料,耦合度低,重複使用性高,更新方便,較適合大型的重邏輯的項目

	### 	MVP架構

​		MVP架構是由Model,Veiw,Presenter構成,流程如下:

​			1.先由用戶透過view發送請求

​			2.請求由presenter處理後找model調用資料

​			3.資料經過presenter後再呈現給用戶

​		![img](https://i.imgur.com/v5TD2A8_d.webp?maxwidth=760&fidelity=grand)

​		這種架構適合事件驅動架構,但是會造成presenter過於擁腫

	### 	MVVM架構

​		MVVM架構,是由Model,VeiewModel,View組成,其架構與MVP很相似,

​	不同的是viewmodel與view之間是緊密相連的,每當model改變時view跟viewmodel可以很快地實時響應,每一個view跟viewmodel之間是一對一綁定的,已達成他們之間的快速響應

![img](https://i.imgur.com/IDAECHN.png)

