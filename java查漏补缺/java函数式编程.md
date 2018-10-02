（资料)[https://github.com/RichardWarburton/java-8-lambdas-exercises]

Lambda 的参数中引用的是值而非变量。final

java中的函数接口

|     接口     |   参数   |   返回值类型   |    示例      |
| :---------:  | :-----: | :----------: | :---------- |
| Predicate<T> |    T    |    boolean   |   这个行不    |
|   Consumer            |          T         |              void           |       输出一个值      |
|   Function<T,R>      |          T        |               R               | 获得Artist的名字   |
|   Supplier<T>         |       None      |              T                |         工厂方法      |
| UnaryOperator<T> |          T         |              T                |          逻辑非        |
| BinaryOperator<T> |       (T,T)      |              T                |  求两个数的乘积  |

聚合（早求值）	返回 非stream

非聚合（懒性求值） 	返回	stream

## Stream -> List (流转换成列表)

* collect(toList());

## map( 类型转换 function)

## flatMap (对 Stream 数组进行处理)

```java
List<Integer> together=Stream.of(asList(1,2),asList(3,4))
                .flatMap(Collection::stream)
                .collect(toList());
        assertEquals(asList(1,2,3,4),together);
```

## filter (过滤 predicate)

## max/min (Comparator co) return Optional<T>  

* Comparator.comparing(int/long) 可直接生成一个比较器

## reduce（init,accumulator)

* 从一组值中生成一个值（min/max/count)

## 减小包装类的性能开销 

* mapToInt
* mapToLong
* mapToDouble

```java
public static void main(String[] args) {
        Integer[] a={1,2,3,4,5,6,7,8,9};
        IntStream intStream = Arrays.stream(a).mapToInt(e -> e);
        IntSummaryStatistics intSummaryStatistics = intStream.summaryStatistics();
        System.out.println(intSummaryStatistics.getAverage());
        System.out.println(intSummaryStatistics.getCount());
        System.out.println(intSummaryStatistics.getMax());
        System.out.println(intSummaryStatistics.getMin());
    }
```

## @FunctionInterface

## 接口

* java8的接口可以有默认方法，用【default】修饰

## 方法引用（凡是用到lambda的地方都能用方法引用）

方法引用可以有多个参数

静态方法：Calssname::methodName

对象方法：Instance::methodName

## 收集器

```java
stream.collect(Collectors.toList());
stream.collect(Collectors.toSet());
stream.collect(Collectors.toCollection(ArrayList::new));
```

## 数据分成两部分

```java
List<Integer> integers=Arrays.asList(1,2,3,4,5,6,7,8,9);
Stream<Integer> stream = integers.stream();
Map<Boolean, List<Integer>> collect = stream.collect(partitioningBy(e -> e % 3 == 0));
List<Integer> integers1 = collect.get(true);
List<Integer> integers2 = collect.get(false);
System.out.println(integers1.size());
System.out.println(integers2.size());
```

## 数据分组

```java
List<Integer> integers=Arrays.asList(1,2,3,4,5,6,7,8,9);
Stream<Integer> stream = integers.stream();
Map<Integer, List<Integer>> collect = stream.collect(groupingBy(e -> e % 3));
collect.keySet().forEach(key->{
    System.out.println(key+":"+collect.get(key).size());
});
```

## 字符串组合

```java
List<String> list=Arrays.asList("first","second","three");
String collect = list.stream().collect(joining(", ","[","]"));
System.out.println(collect);
```

