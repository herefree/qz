JAVASE

https://www.nowcoder.com/discuss/447742?channel=2002&source_id=discuss_center_discuss_history

[https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E5%9F%BA%E7%A1%80.md#%E7%BC%93%E5%AD%98%E6%B1%A0]    
  (https://github.com/CyC2018/CS-Notes/blob/master/notes/Java 基础.md#缓存池)

1.java8流处理

2.基本数据类型占用的字节数

![](http://www.herefreelucky.com/kedaoyun/index.php?user/publicLink&fid=207e45fOYU7mhwcnPIAtrFrb6USZ-FJMWZD2M3HWcwwu9eJLYgKkBBju_KG6AqsHhRg5FY6fhLZW-VpdYxxyAGgYBrtKvEEmHqNeZ1OUnVLSuc4sLmZyazeCTtohMUaaMaO8BhrNmX2iZdOMqyiMHaBPh2gXc_UfdZKqfBEQ18qgglkrBg&file_name=/jibenshujileiixng.png)

   1.简单的Object对象要占用8个字节的内存空间，因为每个实例都至少必须包含一些最基本操作,比如:wait()/notify(),equals(),  hashCode()等  
   2.使用Integer对象占用了16个字节,而int占用4个字节,说了封装了之后内存消耗大了4倍  
    3.那么Long看起来比Integer对象应该使用更多空间,结果Long所占的空间也是16个字节.  
 那么就正好说明了JVM的对于基本类型封装对象的内存分配的规则是如下:  
 Object所占内存(8个字节)+最大基本类型(long)所占内存(8个字节)  =  16字节.  
 JVM强制使用8个字节作为边界.  
 所以所有基本类型封装对象所占内存的大小都是16字节.但是还是有区别,比如:Integer对象虽然占用了16个字节的内存,但是只是利用了Object所占内存(8个字节)+int所占内存(4个字节)  =  12字节.还有4个字节根本没有被使用

3.syn与lock哪个更快

