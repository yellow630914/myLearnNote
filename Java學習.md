# Java語法

---

每個java檔案都由一個或多個`class`構成，在每個`class`中有一個主`class`為`public`，此`class`必須與檔名相同。

```java
public class MainClass {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```

在上述代碼中`MainClass`是公開的主類，所以它的檔名必須是MainClass.java。

## main方法

`main()`方法是必須出現在java程式中的，它是java程式的入口。

```java
public static void main(String[] args)
```

`main()`方法會出現在java檔中的主`class`中，也就是與java檔案同名的`class`。

---

# Java變數

---

java中主要的變數類型有：

| 類型    | 說明                          |
| :------ | ----------------------------- |
| String  | 存儲文本，例如"蘋果"。        |
| int     | 存儲整數，例如123。           |
| float   | 存儲浮點數，例如1.23。        |
| char    | 存儲單個字符，例如'a'。       |
| boolean | 存儲真假值，例如true或false。 |

以下以創建一個字串型別變數作為一個例子：

```java
String example = "I am example.";
```

---

# Java型別轉換

---

## 原始數據型別

java的型別中，有分為原始型別的數據與非原始型別的數據，原始型別的數據有`byte`，`short`，`int`，`long`， `float`，`double`，`boolean`和`char`，這幾種型別的大小與儲存數據說明如下：

| 型別    | 大小   | 說明                                                         |
| ------- | ------ | ------------------------------------------------------------ |
| byte    | 1 byte | 儲存-128到127的整數。                                        |
| short   | 2 byte | 儲存-32,768到32,767的整數。                                  |
| int     | 4      | 儲存-2,147,483,648到2,147483,647的整數。                     |
| long    | 8      | 儲存-9,223,372,036,854,775,808到9,223,372,036,854,775,807的整數。 |
| float   | 4      | 儲存小數點後6到7位的浮點數。                                 |
| double  | 8      | 儲存小數點後15位的浮點數。                                   |
| boolean | 1      | 儲存真假值。                                                 |
| char    | 2      | 儲存單一個字符或ASCII值。                                    |



---

## 非原始數據類型

也稱引用型別(**reference types**)，他們的主要特點有：

- 他們大部分是由程序員創造(除了String)。
- 可調用方法(methods)執行操作。
- 可以是**null**值。
- 以大寫開頭。
- 非原始類型的大小都相同。

---

## 兩種型別轉換

Java的型別轉換主要分為2種，一是由小至大的**Widiening Casting**與由大至小的**Narrowing Casting**：

- **Widiening Casting**(自動轉換)：可以無痛的將較小的型別轉換成較大的型別。


    `byte`-> `short`-> `char`-> `int`-> `long`-> `float`->`double`

- **Narrowing Casting**(手動) ：可能會丟失細節，由大到小的轉換，必須手動。

  `double`-> `float`-> `long`-> `int`-> `char`-> `short`->`byte`

  ---

  ### Widiening Casting

  
