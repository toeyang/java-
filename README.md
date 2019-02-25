# java-java总结
java总结
=====
五片内存：寄存器，本地方法区，方法去，堆，栈<br>
堆：数组，对象，也就是封装好的实体
栈：局部变量。
堆得变量都有默认初始化
构造代码块：所有的对象进行初始化，所有的对象都会调用一个代码块
构造函数：给相对应的对象进行初始化，具有针对性
this：代表对象，就是锁在函数所属对象的引用（在构造函数中必须是第一行）
静态方法：只能访问静态成员。不能使用this，super
静态变量存在方法区。成员变量在堆内存
静态代码块：有静态关键字标识的代码块，只执行一次
静态代码块>构造代码块>构造函数
单例模式：保证一个类在内存中的对象唯一性
代码体现：私有化构造函数
创建私有并静态的本类对象
定义公有并静态的方法，返回该对象
//饿汉式
class Single{
private Single(){}//私有化构造函数
private static Single s=new Single();//创建私有并静态的本类对象
public static Single getInstance(){//定义公有并静态的方法，返回该对象
return s;
}
}
//懒汉式:延迟加载
class Single2{
private Single2(){}
private static Single2 s=null;
public static Single2 getInstance(){
if(s==null)
s=new Single2();
return s;
}
}
java不支持多继承，但是支持多重继承
子类实例化过程：首先调用父类的构造函数，子类所有的构造函数都会默认访问父类的空构造函
数，
每一个子类构造函数第一行隐藏super（）；如果父类没有空构造，子类构造
函数
必 须通过super指定访问父类构造函数；如果子类构造函数中用this来指定子类
自己
的构造函数，被调用的构造函数一样会访问父类的构造函数
super()和this()不可出现在相同的构造函数中
方法的覆盖：子类权限大于等于父类方法权限。要么都静态，要么都不静态
final：修饰类，方法，变量
被final修饰的类不可被继承
被final修饰的方法不可被继承
被final修饰的变量是常量，只能赋值一次
抽象类：abstract
抽象方法只能定义在抽象类中，抽象类和抽象方法必须由abstract关键字修饰（不可描述
变量
抽象方法只能定义方法声明，不可以出现函数体
抽象对象不可以被实例化
只有通过子类继承抽象类并覆盖了抽象类所有的抽象方法后，该子类才可以实例化，否
则还是抽象类
抽象类有构造函数，用来给子类对象进行初始化
抽象类中可以定义非抽象方法，但是抽象方法一定在抽象类中
abstract不可以和final，private，static共存
接口：关键字interface
接口成员：全局变量，抽象方法。
变量（public static final) 方法(public abstract)
类和类之间是继承关系，类和接口是实现的关系
继承extends，实现implements
接口可以被多实现，接口的出现避免了单继承的局限性
java中存在多继承吗？（存在，接口和接口之间存在着继承关系，接口可以多继承接口）
接口设计的特点（1.对外提供的规则，2.功能的拓展.3降低了耦合性）
抽象类和接口的区别：1.抽象类只能被单继承，接口需要被实现，可以多实现
2.抽象类可以定义非抽象方法，子类可以直接继承使用，接口的抽
象方法，需要子类去实现
3.抽象类使用的是is a关系，接口是like a的关系
4.抽象类的成员修饰符可以自定义，接口成员修饰符固定public
多态：体现：父类引用或者接口的引用只想了自己的子类对象//Animal a=new Cat（）；
优点：提高了程序的扩展性
弊端：只能访问子类中父类具备的方法，不可以访问子类的特有方法
前提：必须要有继承或者实现，通常会有覆盖操作
instanceof：判断对象是否实现了指定的接口或继承了指定的类
对象 instanceof 类型（true，false）
Object：所有类的直接或间接父类。
具体方法：equals（比较地址，等同于==）（通常被复写）
toString（转换成String类型）（通常被复写）
Class getClass（获取运行的字节码文件）
int hashCode（返回对象的哈希码值）（通常被复写）
内部类：A类需要直接访问B类成员。而B又需要建立A的对象，可以直接将A定义在B的内部
内部类可以直接访问外部类成员，外部类必须建立内部类对象才能访问内部类
class Out{
int num=4;
class inner{
void show(){
System.out.println(num);
}
}
public void method(){
inner in=new inner();
in.show();//调用内部类方法
}
}
内部类定义在外部类成员位置上，可以使用修饰符
1.默认修饰符：out.inner in=new out.new inner();
（很少用）
2.私有修饰符：被私有化，封装好，不允许其他程序直接访问
3.静态修饰符：如果内部类被静态修饰，相当于外部类，只能访问外部类的静态成员
（如果内部类中定义了静态成员，则内部类必须是静态的）
内部类编译后的文件名：“外部类名$内部类名.java”
为什么内部类可以直接访问外部类成员（内部类有一个外部类的引用 外部类名.this）
当内部类被定义在局部位置上，只能访问局部中被final修饰的局部变量。
匿名内部类：没有名字的内部类，就是一个匿名子类对象。前提：内部类必须继承一个
类或许实现接口，格式：new 父类名&接口名(){定义子类成员或者覆盖父类方法}.方法
new Object(){
void show(){
System.out.println("1321");
}
}.show();
异常：编译异常和运行异常
try对应多个catch时，如果有父类的catch语句，一定放在下面
throw用于跑出异常对象，用在函数中，后面跟异常对象
throws用于跑出异常类，后面跟异常类名，可以跟多个，用逗号隔开，用在函数上
两种异常的区别：编译被检查的异常在函数中杯跑出，函数必须声明，否则编译失败
需要调用者对该异常进行处理
运行时异常如果在函数内被抛出，在函数上不需要声明
不需要调用者处理，异常发生时，程序无法继续运行
功能内部如果出现异常，内部可以处理，就try；
如果处理不了，就声明出来，让调用者处理
finally：主要用于关闭用户资源，无论是否发生异常，资源必须关闭
System.exit(0);//退出jvm，只有这样finally不执行
常见异常：角标越界异常（IndexOutOfBoundsExceptions）
空指针异常（NullPointerException）
类型转换异常（ClassCastException）
范围 public protected default private
同一类 √ √ √ √
同一包√ √ √
子类 √ √
不同包√
常见包名：java.lang核心包，自动导入
java.awt java图形界面开发
javax.swing 提供所有的windows桌面应用程序的控件
java.net 用于java网络编程
java.io 读写操作
java.util 工具包，时间对象，集合框架
java.applet application+let客户端java小程序
多线程：
进程：一个程序就是一个进程，就是一个应用程序运行时的内存分配空间
线程：进程的一个程序控制单元，一条执行的路径。进程负责应用程序的空间标识，线
程负责程序的执行顺序
一个进程至少有一个线程运行，当一个进程中出现多个线程，称之为多线程应用程序，
每个线程在栈区中都有自己的执行空间，方法区，变量
在jvm启动时，主线程调用main函数，当产生垃圾时，会运行垃圾回收器代码
随机性：cpu快速切换，哪个线程获取到了cpu的执行权，哪个线程就执行
返回当前现成的名称：Thread.currentThread().getName()
线程要运行的代码都统一放在了run方法中
线程运行必须通过类的start方法（1.启动线程 2.jvm调用run方法）
创建线程的第一种方式：继承Thread，子类复写run方法
1.定义类继承Thread类
2.复写run，将运行的代码写在run方法中
3.创建Thread类的子类对象，创建线程对象
4.调用线程的start方法，开启线程，执行run方法
线程的状态：就绪，运行，阻塞，销毁
第二种方式：实现Runnable接口
1.定义类实现Runnable接口
2.覆盖接口的run方法
3.通过Thread类常见线程对象
4.将实现了Runnable接口的子类对象作为实际参数传递给Thread类的构造函数
5.调用Thread对象的start方法，开启线程
cat a=new a();
Thread t1=new Thread(a);//创建线程
t1.start;
第二种方式的优点：通过继承Thread可以完成多线程，但是一个类已经有了父类，
就不可以继承其他类了。所以Runnable接口避免了单继承的局限性
多线程安全问题：将操作共享数据的语句在某一时段让一个线程执行完，其他线程无法
进来执行就可以保证线程安全。
解决多线程安全的方法：同步代码块
格式：synchronize（对象）{
//同步代码块
}
好处：解决了线程安全
弊端：降低性能，判断锁需要消耗资源，产生了死锁
同步的前提：有两个或两个以上的线程
多个线程用同一个锁
同步函数：将同步关键字定义在函数上。
线程暂停，后期开新的模块详细叙述，较为复杂。
String：字符串被初始化就不可改变，存放在方法区的常量池中。
equals方法比较的是内容，==比较的是地址
将字符数组转换成字符串 new String(char[])
length()字符串长度,char charAt(int index)指定位置字符
int indexOf(int ch)返回第一次找到的字符角标
int indexOf(int ch,int fromIndex)返回从指定位置开始第一次找到的角标
int indexOf(String str)返回第一次找到的字符串角标
String substring(int start)截取字符串，从start开始，到length-1为止
String substring(int start，int end)，截取字符串，从start开始，到end为止，不包含
end
substring（0，str.length());获取整串
boolean contains(String str)判断是否包含指定字符串
boolean startsWith（String str)是否指定字符串开头
boolean endsWith（String str)
boolean equals（string）判断内容相等（忽略大小写equalsIgnoreCase)
String.copyValueOf(char[])
String.valueOf(char[])通过静态方法将字符数组转换成字符串
其他类型同理
转换大小写：toLowerCase();toUpperCase()
转换数组：char[]toCharArray();字符数组
byte[] getBytes();转换字节数组
切割字符串：String[] split(分割规则)
内容置换（变成新的字符串）：String replace(oldChar,newChar)
String replace(oldstring,newstring)
String concat(string)追加字符串
String trim()去除两端空格
StringBuffer：特点：可以对字符串内容进行修改，是一个容器，可变长度，缓冲区可以存任意类
型
最终需要变成字符串
方法：添加（append(data)追加到尾部，insert(index,data)指定位置插入数据）
删除（delete(start,end)删除从start到end-1范围的元素，
deleteCharAt(index)
删除指定位置元素）
修改（replace(start,end,string)）
反转（reverse()）
StringBuilder：线程不安全，而StringBuffer安全。
单线程时，StringBuilder效率高，多线程时，使用StringBuffer安全
基本数据类型包装类：将基本数据类型封装成对象
好处：可以通过属性和行为操作数据，可以实现与字符串的转换
Byte，Short静态方法parseShort(numstring)，Integer静态方法
parseInt(numstring)，Long,Float,Double,Character,Boolean,都有***parse***方法，只有
Character没有
（了解）十进制转成其他进制：二进制toBinaryString,八进制toOctalString,十六进
制,toHexString,
toString(int num,int radix);
在jdk1.5后，可以这么写：Integer i =4;
//数值相同时装箱操作，地址不变
例：Integer a=100;Integer b=100;a==b为真
集合框架（！！）特点：集合用于存储对象，长度可变
集合与数组的区别：固定长和可变长，数组可以存基本数据和引用数据，集合只能存引
用
数组所有元素数据类型相同，集合可以存不同的数据类型
集合体系：向上抽取，参阅顶层内容，简历底层对象
Collection：list：有序，元素存入顺序和取出顺序一致，每个元素都有索引，可重复
Set:无序，不可以存储重复元素，元素唯一性
方法：add(obj),addAll(Collection)添加一个集合所有元素,clear();
remove(obj);removeAll(collection)删除部分元素
判断contains(obj),containsAll(Collection);isEmpty();
size();获取集合所有元素：Iterator iterator()(迭代器)
集合变数组：toArray();
Iterator:迭代器，是一个接口，作用是取集合中的元素
用法：Iterator it=coll.iterator()
List：Collection子接口
ArrayList：底层数据结构是数组，线程不同步，查询速度非常快
LinkedList：底层数据结构是链表，线程不同步，增删快
Vector：底层数据结构是数组，线程同步，无论查询还是增删都贼鸡儿慢
添加add(index,element),addAll(index,collection)
删除remove(index),获取get(index)，indexOf(index)第一次出现的索引位
List subList(start,end)获取子列表
修改set(index,element);
获取所有元素：listlterator();List特有的迭代器
List支持增删改查
LinkedList特有方法：addFirst();addLast();
Set：与Collection方法一致，取出方式只有迭代器这一种
HashSet：底层数据结构是哈希表，线程不同步，高效
保证元素的唯一性，通过元素的hashCode方法，和equals完成
当元素的hashCode值相同时，才继续判断元素的equals是否为true
如果为true，则元素相同，不存。若hashCode值不同，则不判断equals
LinkedHashSet:有序，是hashset的子类
TreeSet：对Set集合中的元素的进行指定顺序的排序，不同步，底层数据结构
是
二叉树
用于对Set集合进行元素的指定顺序拍序，元素本身具备比较性
需要元素实现Comparable接口，强制让元素具备比较性，复写
compare to 方法，根据返回值确定位置。
保证元素唯一性：比较方法结果是否为0。0为重复
哈希表的原理：
对对象元素的关键字进行哈希算法的运算，得到一个具体的算法值，成为
哈希
值，哈希值就是这个元素的位置，如果哈希值出现冲突爱判断对应的对象
是否
相同，相同不存，不同将哈希值+1顺延。
对于ArrayList集合，判断元素是否存在，依据是equals方法
对于HashSet集合，判断元素是否存在，依据是hashCode和equals方法
Map集合：HashTable：底层是哈希表，线程同步，不可以存储null建，null值
HashMap：底层是哈希表，线程不同步，可以存null键值
TreeMap：底层二叉树，对map集合中的键进行指定顺序的排序
Map和Collection区别：collection一次存一个元素，map存一对
collection单列集合，map双列集合
map存储一个是键，一个是值，键值有对应关系
保证map集合键唯一性
方法：添加put(key,value),当存的键相同时，新值会替换旧的，返回旧值
否则返回null
删除clear()；清空，remove(key)
判断isEmpty();containsKey(key);containsValue(value)
取出size(),get(key)通过指定键获取对应得值，返回null，判断
键值不存在，特殊情况hashmap中可以允许空键值对
Collection values();获取map集合所有的值
map转set：Set keySet();Set entrySet();
取出map元素步骤：
Set keyset=map.keySet();
Iterator it=keyset.iterator();
while(it.hasNext()){
Object key=it.next();
Object value =map.get(key);
}
方法二
Set entry=map.entrySet();
Iterator it=entry.iterator();
while(it.hasNext()){
Map.Entry me =(Map.Entry)it.next();
System.out.println(me.getKey()+me.getValue());
}
技巧：看到Array就是数组结构，有角标，查询快
link就是链表，增删快
hash就是哈希表，唯一性，要覆盖hashcode,equals方法
tree就是二叉树，排序，比较
比较的两种方式：Comparable：覆盖compare To方法
Comparator：覆盖compare方法
LinkedHashSet，LinkedHashMap可以保证哈希表存入和取出顺序一直，保证
有序
存储一个元素就用Collection，对象之间存在映射关系用Map集合
保证唯一就Set，不唯一就用List
collections的静态方法：Collections.sort(list),Collections.max(list)
Collections.reverseOrder()逆向反转排序
Collections.shuffle(list)随即对list中元素置换
非同步集合转同步集合的方法：List synchronizedList(list)
Map synchronizedList(map)
原理，定义一个类，将集合所有的方法加同一把锁返回
Collection与Collections区别：
后者为java.util下的类，是针对集合类的一个工具类
前者为java.util下的接口，是各种集合结构的父接口
Arrays：用于操作数组对象的工具类，都是静态方法
asList(array)将数组转换成list集合，优点是可以使用list集合的方法操作元素
局限性：数组是固定长度，不可以使用集合对象增删
如果数组存的引用数据类型，直接作为集合的元素可以直接用集合方法操作
如果数组存的是基本数据类型，asList将数组实体作为集合元素
集合变数组：toArray()；如果传递的数据长度小于集合的size，那么会自动创建新数组
如果长度大于集合size，那么剩余存储元素默认为null
增强for循环：foreach语句 for(元素类型 变量名:Collection集合&数组){
}
枚举：关键字enum，是一个特殊的java类，可以定义属性，方法，构造函数，实现接口继承
类
自动拆装箱：Integer x=1;x=x+1;经历了装箱，拆箱，装箱
泛型技术：应用在编译期间，运行期间泛型就不存在了
当类中的操作的引用数据类型不确定时候，可以用泛型来表示
避免强制转换的麻烦
将泛型定义在类上：
class Tool<T>{
private Q obj;
}
泛型定义在方法上：
public <W>void method(W w){
}
静态方法泛型：
public static <Q>void fun(Q q){
}
泛型接口
interface inter<T>{
void show(T t);
}
泛型的通配符：当操作类型时，不需要使用类型的具体功能，可以用？通配符
泛型限定：上限：？extends E：可以接收E类型或者E的子类型对象
下限：？ super E：可以接收E类型或者E的父类型对象
上限用法：在集合中添加元素，既可以添加E类型对象，又可以加
E的子类对象
下限同理
细节：泛型代表的类型取决调用者传入的类型，没传默认Object
创建对象等式两边指定泛型必须一致
等式两边可以在任意一边使用泛型，另一边不使用（考虑向后兼容）
ArrayList<String>al=new ArrayList<Object>()；错误
保证一致肯定不会出错
ArrayList<? extends Object>al=new ArrayList<String>();
java.lang.System属性和行为都是静态的
long currentTimeMills()会当前时间毫秒值
exit()退出虚拟机
java.util.Math用于数学运算的工具类，属性和行为都是静态，final不允许继承
static double ceil(doble a)返回大于指定数值的最小整数
static double floor(double a)返回小于指定数值的最大整数
static long round(double a)四舍五入成整数
static double pow(double a,double b)a的b次幂
static double random();返回0~1的伪随机数
IO流：流可以理解数据的流动，处理设备上的数据
分为输入流和输出流
分为字节流和字符流
字节流：处理字节数据的流对象，设备上的数据文件，都以二进制存储
二进制的最终都是以一个8位为数据单元进行体现，意味着字节流
可以处理所有数据。包括字符数据
字符流：考虑到了国家不同的字符编码，考虑到操作字符数据，优先字符流
流的操作：读和写，共有四个基类，且都是抽象类
字节流：InputStream OutputStream
字符流：Reader Writer
他们的特点就是子类名后缀是父类名，前缀名是这个子类的功能名称
建立流的步骤：
1.创建字符流输出对象，操作文件，必须在建立对象时明确数据位置，是文件
2.产生对象，堆内存存在实体，调用系统底层资源，在指定位置创建一个存储
数据文件
3.指定位置文件同名会被覆盖
FileWriter fw = new FileWriter("demo.txt");
fw.write("abcde");
此时并未写入文件，只是写到了流中
fw.flush();刷新缓冲区，将数据刷到目的地文件
fw.close();关闭流，在关闭前会刷新该流
二者区别就是flush刷到目的地后，流还可以使用，close直接关闭
写入追加数据：fw = new FileWriter("demo.txt",true);
注意，io流的finally必须写
FileReader:使用Reader体系，读取文本数据，返回-1，标记到结尾
FileReader fr=new FileReader("demo.text");
int ch=0;
while((ch=fr.read())!=-1){
System.out.println((char)ch);
}
fr.close();
读取数据的第二种方式：自定义缓冲区
char[]buf=new char[1024];
int len=0;
while((len=fr.read(buf))!=-1){
}
fr.close();
io中用到了一个设计模式：装饰设计模式（对一组类进行功能的增强）
字符流：Reader读取字符流的抽象类，子类必须实现read(char[],int,int)
和close();
BufferedReader:从字符输入流中读取文本
LineNumberReader：跟踪行号的缓冲字符输入流
InputStreamReader：字节流通往字符流的桥梁
流的规律：读取InputStream,Reader
写入OutputStream,Writer
纯文本数据：Reader，Writer
其余两个不是
编码转换：InputStreamReader isr = new InputStreamReader(new
FileInputStream("a.txt"),"gbk");
File类：创建：CreateNewFile();创建文件，已存在不创建
mkdir()创建抽象路径名指定的目录
mkdirs()创建多级目录
删除：delete();删除路劲的目录或文件
deleteOnExit()；在虚拟机退出时删除
获取：length()获取文件大小
getName()返回文件
getPath()返回路径字符串
getAbsolutePath()返回绝对路径名字字符串
getParent()返回父目录路径名，没有则null
lastModified()返回最后一次被修改的时间
判断:exists()判断文件或文件夹是否存在
isDirectory()测试此路径名表示的文件是否为目录
isFile()测试路径标识文件是否为标准文件
isHidden()测试路径文件是否为隐藏文件
isAbsolute()测试路径是否为绝对路径
String[]list()列出指定目录下的当前文件和文件夹的名称
Properties:一个可以将键值进行持久化存储的对象，是Hashtable的子类
键值都是字符串，一般用在配置文件
对象的序列化：将一个具体的对象进行持久化，写到硬盘
静态数据不可以被序列化
Serializable:用于启动对象的序列化功能，
网络编程：Socket，套接字，通信的端点。
就是为网络服务提供的一种机制，通信两端都有Socket，数据
在两个Socket间通过IO传输
UDP传输：只要是网络传输，必须有socket。
数据一定要封装到数据包中，包括目的地址，端口，数据等信息
不可以直接操作udp
Datagramocket：封装了udp传输协议的socket对象
udp发送端：1.建立udp的socket服务，未明确端口则自动分配
2.明确发送的数据
3.将数据封装成数据包
4.用socket服务的send方法将数据包发送出去
5.关闭资源。
DatagramSocket ds = new DatagramSocket(8888);
String text="1111";
byte[]buf=text.getBytes();
DatagramPacket dp = new DatagramPacket(buf,
buf.length,InetAddress.getByName("10.1.31.127"),10000);
ds.send(dp);
ds.close();
udp接收端：1.创建udp的socket服务，必须明确一个接口
2.定义数据包，用于存储接受数据
3.通过socket服务接受数据到数据包
4.通过数据包方法获取具体内容
5.关闭
DatagramSocket ds = new DatagramSocket(10000);
byte[] buf = new byte[1024]; DatagramPacket dp =
new
DatagramPacket(buf,buf.length);
ds.receive(dp);
String ip = dp.getAddress().getHostAddress();
int port = dp.getPort();
String text = new String(dp.getData(),0,dp.getLength());
ds.close();
TCP传输：两个端点建立连接后会有一个传输数据的流通道，称为socket流,有读有
写
客户端：Socket
服务端：ServerSocket
客户端：1.建立tcp的socket服务，明确地址和端口，在创建时就可以
对指定的ip和端口进行连接（三次握手）。
2.连接成功，通道建立，socket流产生，通过
getInputStream
和getOutputStream就可以获取两个流对象
3.关闭资源
Socket s=new Socket("120.1.1.1",8080);
OutputStream out=s.getOutputStream();
out.write("tcp".getBytes());
s.close();
服务端：1.创建服务端socket服务，并监听一个端口
2.通过accept方法获取连接过来的客户端对象
3.可以通过获取到的socket对象中的socket流和具体的客户
端
通信
4.通讯结束，先关客户端，再关服务器
ServerSocket ss = new ServerSocket(8080);
Socket s = ss.accept();//获取客户端对象
String ip = s.getInetAddress().getHostAddress();
InputStream in = s.getInputStream();
byte[] buf = new byte[1024];
int len = in.read(buf);
String text = new String(buf,0,len);
s.close();
ss.close();
BIO AIO NIO的区别
BIO：建立网络连接，先在服务器启动一个ServerSocket，然后在客户端启动Socket来
对
服务端进行通信，默认情况下服务端需要对每个请求建立一堆线程等待请求，
而客
户端发送请求后，先咨询服务端是否有线程相应，如果没有则会一直等待或者
遭到
拒绝请求，如果有的话，客户端会线程会等待请求结束后才继续执行。
NIO：解决BIO的大并发问题，在使用同步I/O的网络应用中，如果要同时处理多个客户
端请
求，或是在客户端要同时和多个服务器进行通讯，就必须使用多线程来处理。
如果客户端的请求过多，服务端程序可能会因为不堪重负而拒绝客户端的请
求，甚
至服务器可能会因此而瘫痪。
NIO基于Reactor，当socket有流可读或可写入socket时，操作系统会相应的通
知引
用程序进行处理，应用再将流读取到缓冲区或写入操作系统。 也就是说，这个
时
候，已经不是一个连接就要对应一个处理线程了，而是有效的请求，对应一个
线
程，当连接没有数据时，是没有工作线程来处理的。
BIO与NIO一个比较重要的不同，是我们使用BIO的时候往往会引入多线程，每
个连
接一个单独的线程；而NIO则是使用单线程或者只使用少量的多线程，每个连
接共
用一个线程。
在NIO的处理方式中，当一个请求来的话，开启线程进行处理，可能会等待后
端应
用的资源(JDBC连接等)，其实这个线程就被阻塞了，当并发上来的话，还是会
有
BIO一样的问题。
AIO：与NIO不同，当进行读写操作时，只须直接调用API的read或write方法即可。这两
种方
法均为异步的，对于读操作而言，当有流可读取时，操作系统会将可读的流传
入
read方法的缓冲区，并通知应用程序；对于写操作而言，当操作系统将write方
法传
递的流写入完毕时，操作系统主动通知应用程序。 即可以理解为，read/write
方法
都是异步的，完成后会主动调用回调函数。
BIO：同步并阻塞，一个连接一个线程。适合连接数较小且固定的架构
NIO：同步非阻塞，一个请求一个线程，多路复用器得到连接有IO请求时才启动线程
适合连接数目多比较短（轻操作）的架构，比如聊天服务器。
AIO：异步非阻塞，一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务
器
应用去启动线程进行处理，用于连接数目多且连接比较长（重操作）的架构。
反射：对一个类进行解刨，大大的增强了程序的扩展性。
1.获得Class对象，获取到指定名称的字节码文件对象
2.实例化对象，获得类的属性，方法，构造函数
3.访问属性，调用方法，调用构造函数创建对象
反射的三种方式：1.调用实例对象的getClass方法，前提是必须要创建该类对象
2.每一个数据类型都有一个静态属性class，前提是必须要明确该类
3.使用Class.forName(class)方法，扩展性最强，最常用
Class clazz=Class.forName(classname);
Class clazz1=obj.getClass();
Class clazz2=ClassName.class获得某个类的Class对象，主要来传参
反射和正则表达式会详细整理
