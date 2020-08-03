#### JVM

[https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E8%99%9A%E6%8B%9F%E6%9C%BA.md#%E4%B8%80%E8%BF%90%E8%A1%8C%E6%97%B6%E6%95%B0%E6%8D%AE%E5%8C%BA%E5%9F%9F](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java 虚拟机.md#一运行时数据区域)

1.new 一个对象的过程

当一个类被创建（A a=new A();），并且这个类是首次被加载时，方法区会开辟出一块内存存放类的class文件并且将全部成员放入。之后会在堆中开辟一块内存，存储这个类并且将这个类的非静态的成员变量拷贝过来（静态成员不拷贝，所有实例共享），并持有对应的方法区的方法的句柄，这块内存有一个唯一内存地址，栈中的a对象指向的就是这个内存地址。
之后你为类的成员变量赋值时，堆中的变量的值会从默认值更改为设定值（方法区中变量无值）。
如果此时在实例化一个新的类(A a2=new A()),此时方法区中已经有一个A类的class，所以不会在创建一个A.class，但是此时会在堆中开辟一块新的空间并且将这个类的非静态成员拷贝并持有对应的方法区类的方法的句柄，这块内存空间标注一个新的内存地址。

初始化完成后在加入引用！！！！！！！

栈中a指向的是堆中第一个类的内存地址，a2指向的是堆中的第二个类的内存地址，而堆中这两块内存地址指向的是同一个方法区的class文件。

2.GC算法

3.GC回收器

4.可达性分析如何解决循环引用

5.jvm里如何判断类死亡。面试官解答：三个角度，看类实例是否被回收，类加载器是否被回收，Class对象是否被回收