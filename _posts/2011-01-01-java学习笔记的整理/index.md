---
title: "Java学习笔记的整理"
date: 2011-01-01
categories: 
  - "software_programming"
tags: 
  - "java"
---

《Java学习笔记》，良葛格，清华大学出版社。

原名：林信良 网站：[http://caterpillar.onlyfun.net/Gossip/](http://caterpillar.onlyfun.net/Gossip/) （繁体）

Java Gossip是作者Java的学习笔记。

**以下是本人在原作的基础上根据个人实际情况整理的结果，版权归原作者所有。**

1\. Java版本发表是以JDK名称发表。

2\. Java不再是表示程序语言，而是一种开发软件的平台，也是一种开发软件的标准和框架的总称。

3\. 需要掌握的Java API有：字符串处理、异常处理、容器、输入/输出、线程。

4\. Java技术论坛：http://www.javaworld.com/

5\. 一个文件中可以编写数个类，但是只能有一个公开的类（public），而且主文件名必须与这个公开的类名一致。

6\. main()方法一定是public成员，这样它才能够在执行环境中被调用；main()方法不需要产生对象（object）就能被执行，所以它必须是个static成员。Main()方法不需要返回任何值，所以一律定义为void.

7\. System.out.println(); //使用Java.lang包下的System下的out对象所提供的println方法。

8\. 取得使用者输入:

import java.util.Scanner;

public class HelloUser {

public static void main(String\[\] args) {

Scanner scanner = new Scanner(System.in);

System.out.print("Please input your name: ");

System.out.printf("Hello! %s!", scanner.next());

}

}

"new"表示新增一個 Scanner物件，在新增一個 Scanner物件時需要一個System.in物件，因為實際上還是System.in在取得使用者的輸入，您可以將Scanner看作是 System.in物件的支援者，System.in取得使用者輸入之後，交給Scanner作一些處理。也就是使用它的next()方法來取得使用者的輸入字串。

9\. 使用Scanner來取得使用者的輸入很方便，但是它以空白來區隔每一個輸入字串，在某些時候並不適用，因為使用者可能輸入一個字串，中間會包括空白字元，而您希望取得完整的字串。比较简单的方法是使用java.io.BufferedReader类取得输入。

import java.io.\*;

public class Echo {

public static void main(String\[\] args) throws IOException {

BufferedReader buf = new BufferedReader(

new InputStreamReader(System.in));

System.out.print("請輸入一列文字: ");

String text = buf.readLine();

System.out.println("您輸入的文字: " + text);

}

}

BufferedReader在构造時接受一個Reader对象，在 讀取標準輸入串流時，會使用InputStreamReader， 它繼承了Reader類。

10\. autoboxing的作用就是把基本数据类型变成object来处理，unboxing的作用相反。

Autoboxing：

Integer integer = 10;

Unboxing：

Integer fooInteger = 10;

int fooPrimitive = fooInteger;

11\. '=='可用來比較兩個基本型態的變數值是否相等，事實上'=='也用於判斷兩個object变量名稱是否指向同一個object.

12\. 数组的定义与初始化：（简易方式）

int\[\] score = {90, 85, 55, 94, 77};

数组在Java中得看成对象，Java中的对象是以new来分配内存空间。完整的数组定义方式：

int\[\] arr = new int\[10\];

在使用new新增数组时一并指定初始值，不必指定数组长度：

int\[\] arr = new int\[\]{45,85,66,23,77};

动态配置数组长度：

import java.util.Scanner;

public class CustomArrayLength {

public static void main(String\[\] args) {

Scanner scanner = new Scanner(System.in);

System.out.print("請輸入Array大小: ");

int length = scanner.nextInt();

int\[\] arr = new int\[length\]; // 動態配置長度

System.out.println("Array長度: " + arr.length);

System.out.print("內容: ");

for(int i = 0; i < arr.length; i++)

System.out.print(arr\[i\] + " ");

System.out.println();

}

}

13\. 二维数组初始化

int\[\]\[\] arr = {{1, 2, 3},{4, 5, 6}};

在使用二維陣列物件時，注意length所代表的長度，陣列名稱直接加上length，所指的是有幾列（Row），而使用索引加上length，指的是該列所擁有的元素，也就是行（Column）數目。

二维数组定义：

int\[\]\[\] arr = new int\[2\]\[3\];

二维数组初始化（以对象形式）：

int\[\]\[\] arr = new int\[\]\[\]{{1,2,3},{4,5,6}};

14\. 数组元素值的复制

在Java中数组是一個object，而使用 = 指定時是將object指定給数组名稱來參考，而不是数组複製，如果您想將整個数组的值複製給另一個数组，您可以使用循环，將整個数组的元素值走訪一遍，並指定給另一個数组相對應的索引位置。

public class AdvancedArray {

public static void main(String\[\] args) {

int\[\] arr1 = {1, 2, 3, 4, 5};

int\[\] arr2 = new int\[5\];

for(int i = 0; i < arr1.length; i++)

arr2\[i\] = arr1\[i\];

for(int i = 0; i < arr2.length; i++)

System.out.print(arr2\[i\] + " ");

System.out.println();

}

}

另一個更簡便的方法是使用System類別所提供的靜態方法arraycopy()，其語法如下：

System.arraycopy(來源, 起始索引, 目的, 起始索引, 複製長度);

public class AdvancedArray {

public static void main(String\[\] args) {

int\[\] arr1 = {1, 2, 3, 4, 5};

int\[\] arr2 = new int\[5\];

System.arraycopy(arr1, 0, arr2, 0, arr1.length);

for(int i = 0; i < arr2.length; i++)

System.out.print(arr2\[i\] + " ");

System.out.println();

}

}

在JDK 6中，Arrays 類別 新增了copyOf()方法，可以直接傳回一個新的陣列物件，而當中包括複製的內容，例如：

import java.util.Arrays;

public class ArrayDemo {

public static void main(String\[\] args) {

int\[\] arr1 = {1, 2, 3, 4, 5};

int\[\] arr2 = Arrays.copyOf(arr1, arr1.length);

for(int i = 0; i < arr2.length; i++)

System.out.print(arr2\[i\] + " ");

System.out.println();

}

}

15\. foreach与数组

例如傳統上循序存取一個陣列的方式如下：

int\[\] arr = {1, 2, 3, 4, 5};

for(int i = 0; i < arr.length; i++)

System.out.println(arr\[i\]);

在J2SE 5.0中可以這麼寫：

int\[\] arr = {1, 2, 3, 4, 5};

for(int element : arr)

System.out.println(element);

每次从arr中取出的元素，会自动设定给element，你不用自己判断是否超出了数组的长度，注意element的类型必须与数组元素的类型相同。

16.

一個字符串对象一旦被配置，它的內容就是固定不可變的（immutable），例如下面這個宣告：

String str = "caterpillar";

這個宣告會配置一個長度為11的字串物件，您無法改變它的內容。

String str = "just";

str = "justin";

它們兩個是不同的字符串对象，您並不是在 "just"字串後加上"in"字串，而是讓str名稱參考至新的字符串对象。

17.

String str1 = "flyweight";

String str2 = "flyweight";

System.out.println(str1 == str2);

程式的執行結果會顯示true，在Java中，會維護一個String Pool，對於一些可以共享的字串物件，會先在String Pool中查找是否存在相同的String內容（字元相同），如果有就直接傳回，而不是直接創造一個新的String物件，以減少内存的耗用。

18.

在 J2SE 5.0 提供StringBuilder類別，使用這個類別所產生的物件預設會有16個字元的長度，您也可以自行指定初始長度，如果附加至物件的字元超出可容納的長度，則StringBuilder物件會自動增加長度。

在StringBuilder中，length()可傳回目前物件中的字元長度，而capacity()可傳回該物件目前可容納的字元容量，下面這個程式是個簡單的示範：

public class UseStringBuilder {

public static void main(String\[\] args) {

StringBuilder strBuilder =

new StringBuilder("Knowledge is power!");

System.out.println("內容: " + strBuilder);

System.out.println("長度: " + strBuilder.length());

System.out.println("容量: " + strBuilder.capacity());

}

}

19\. Main（）方法的参数为String\[\] args，它就是用來接受一個字符串数组，您只要使用索引取出args中的元素值，就可以取出程式運行時的參數。

20\. 使用类定义出对象的规范，再根据类来构建出一个个的对象，然后通过对象所提供的操作接口来与程序互动。屬性是对象的静态表现，而方法則是对象與外界互動的動態操作。

21\. 在定义类时，您可以使用「构造方法」（Constructor）來進行对象的初始化。

22\. 在构造方法中，您可以定義無參數的构造方法，或具有參數的构造方法，程式在運行時，會根據配置对象時所指定的参数型態等來決定，該使用哪一個构造方法。

23\. 參數名稱與域成員名稱相同時，為了識別是參數或是域成員，我們必須明確的使用this參考來指定，但如果參數名稱與域成員名稱不相同則不用特别指定。

public Ball(double radius, String name) {

this.radius = radius;

this.name = name;

}

public Ball(double r, String n) {

radius = r; // 實際等於this.radius = r;

name = n; // 實際等於this.name = n;

}

24.

this除了上面的用法之外，還有一種可以帶參數的用法，主要是用於類中调用构造方法，而避免直接以构造方法的名稱來调用，例如：

public class Ball {

private String name;

public Ball() {

this("No name");

....

}

public Ball(String name) {

this.name = name;

....

}

}

25\. 對於每一個基於相同類所產生的对象而言，其擁有各自的域成員，然而在某些時候，您會想要這些对象擁有相同的域成員，其域成员是共享的。这时候我们需要用static来标记，比如public static double PI = 3.14159; // 宣告static域成员

静态成员或者静态方法是用类名.来调用。由於static成員屬於類所擁有，所以在不使用对象名稱的情況下，您可以使用類名稱加上 . 運算子來存取static域成員。

26\. 当类的成员声明为受保护的成员之后，继承的类就可以直接使用这些成员，不需要经过public方法。但这些成员依然受到保护，仅可以使用于对象内部或者子对象，不可以被外部对象直接使用。

27.

"final" 關鍵字可以使用在變數宣告時，表示該變數一旦設定之後，就不可以再改變該變數的值，例如在下面的程式碼中，PI這個變數一旦設定，就不可以再有指定值給 PI的動作：

final double PI = 3.14159;

如果在方法成員宣告時使用"final"，表示該方法成員在無法被子類別重新定義（Override）

28\. Java在实现多态时可以让程序依赖于抽象类或接口。

29\. 當您定義類別時，可以僅宣告方法名稱而不實作當中的邏輯，這樣的方法稱之為「抽象方法」（Abstract method），如果一個類別中包括了抽象方法，則該類別稱之為「抽象類別」（Abstract class），抽象類別是個未定義完全的類別，所以它不能被用來生成对象，它只能被擴充，並於擴充後完成未完成的抽象方法定義。在Java中要宣告抽象方法與抽象類別，您使用"abstract"關鍵字.

30\. 當您實作多個接口時，記得您必須實作每一個接口中所定義的方法，由於您實作了多個接口，所以要操作物件時，必要時您必須作「接口轉換」，如此程式才能知道如何正確的操作物件，例如假設someObject實作了ISomeInterface1與ISomeInterface2兩個接口，則我們可以如下對物件進行接口轉換與操作：

ISomeInterface1 obj1 = (ISomeInterface1) someObject;

obj1.doSomeMethodOfISomeInterface1();

ISomeInterface2 obj2 = (ISomeInterface2) someObject;

obj2.doSomeMethodOfISomeInterface2();

31\. 使用內部類別的好處在於可以直接存取外部類別的私用（private）成員，另一個好處是，當某個Slave類別完全只服務於一個Master類別時，我們可以將之設定為內部類別，如此使用Master類別的人就不用知道 Slave的存在。

32\. 匿名内部类可以不声明类名称，而是用new直接产生一个对象，它可以继承某个类或者某个接口。声明方式如下：

new \[类或接口()\] {

// 实现

}

public class UseInnerClass {

public static void main(String\[\] args) {

Object obj = new Object() {

public String toString() {

return "匿名類別物件";

}

};

System.out.println(obj.toString());

}

}

如果要在內部匿名類別中使用某個方法中的變數，此变量必须声明为final类型。究其原因，在於區域變量 x 並不是真正被拿來於內部匿名類中使用，而是在內部匿名類中複製一份，作為field成員來使用，由於是複本，即便您在內部匿名類別中對 x 作了修改，也不會影響真正的區域變數 x，事實上您也通不過編譯器的檢查，因為編譯器要求您加上"final"關鍵字，這樣您就知道您不能在內部匿名類別中改變 x 的值。

33\. 當您使用"enum"定義枚举类型時，實質上您定義出來的类型繼承自 java.lang.Enum 類別，而每個列舉的成員其實就是您定義的枚举类型的一個實例（Instance），它們都被預設為 final，所以您無法改變它們，它們也是 static 成員，所以您可以透過型態名稱直接使用它們，當然最重要的，它們都 是公開的（public）。每个枚举类型的成员都是一个对象实例。

34\. toString()方法被重新定義了，可以讓您直接取得列舉值的字串描述，而列舉物件定義的values ()方法可以讓您取得所有的列舉實例，並以陣列方式傳回，您使用這兩個方法來簡單的將OpConstants的內容顯示出來：

public class ShowEnum {

public static void main(String\[\] args) {

for(OpConstants constant: OpConstants.values()) {

System.out.println(constant.toString());

}

}

}

35\. Collection 類包括了 List 類與 Set 類，List 以放置物件至容器中的順序來排列物件，Set 類不接受重覆的物件，並有自己的一套排序規則。

36\. ArrayList实现了List接口，Arraylist使用数组结构实现List数据结构。使用add()方法可以將一個对象加入ArrayList中，使用size()方法可以傳回目前的ArrayList的長度，使用get()可以傳回指定索引處的对象，使用toArray()可以將ArrayList中的对象轉換為对象数组。

37\. iterator()方法會傳回一個Iterator对象，這個对象提供的遍訪的方法，hasNext()方法測試Iterator中是否還有对象，如果有的話，可以使用next()取出。

Iterator iterator = list.iterator();

while(iterator.hasNext()) {

System.out.print(iterator.next() + " ");

}

使用增強的for循环可以直接遍訪List的所有元素，例如：

for(String s : list) {

System.out.print(s + " ");

}

38\. 如果您會經常從容器中作移除或插入物件的動作，則使用LinkedList會獲得較好的效能。

39\. 簡單的說，您將Map容器物件當作一個有很多間房間的房子，每個房間的門有一把鑰匙，您將物件儲存至房間中時，要順便擁有一把鑰匙，下次要取回物件時，就是根據這把鑰匙取得。

40\. 容器：它不僅持有对象，還負責对象的生命周期與相關服務的連結。

41\. Thread类也实现了Runnable接口，您也可以繼承Thread类並重新定義它的run()方法，好處是可以使用Thread上的一些繼承下來的方法，例如yield()，然而繼承了Thread就表示您不能讓您的类再繼承其它的类。

42\. 在Java中要實現线程功能，可以实现Runnable接口，Runnable接口中只定義一個run()方法，然後實例化一個 Thread对象時，傳入一個实现Runnable接口的对象作為引數，Thread对象會調用Runnable对象的run()方法，進而執行當中所定義的流程。

43\. 一個Daemon執行緒是一個在背景執行服務的執行緒，例如網路伺服器傾聽連接埠的服務、隱藏的系統執行緒如垃圾收集執行緒或其它JVM 建立的執行緒，如果所有的非Daemon的執行緒都結束了，則Daemon執行緒自動就會終止。

44\. 從Main函式開始的是一個非Daemon執行緒，如果您希望某個執行緒在非Daemon執行緒都結束後也跟著終止，那麼您要將它設定為Daemon執行緒。
