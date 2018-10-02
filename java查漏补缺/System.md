# 数组拷贝
System

```java
public static native void arraycopy(Object src,  int  srcPos,Object dest, int destPos, int length);
```

Arrays

```java
public static byte[] copyOfRange(byte[] original, int from, int to) {
        int newLength = to - from;
        if (newLength < 0)
            throw new IllegalArgumentException(from + " > " + to);
        byte[] copy = new byte[newLength];
        System.arraycopy(original, from, copy, 0,
                         Math.min(original.length - from, newLength));
        return copy;
}
```


# 类型转换

	向上转型是自动完成的

## 初始化块

```java
/*
 *在变量定义后，构造方法前执行，与变量定义时赋值代码的优先级相同，顺次执行
 *代码块中不能定义变量
 */
int a=9;
{
    a=8;
}
a:8
```


```java
{
    a=8;
}
int a=9;
a:9
```

## 包装类

	