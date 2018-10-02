| **SRP** | [The Single Responsibility Principle](http://www.objectmentor.com/resources/articles/srp.pdf) | 单一责任原则 |
| ------- | ------------------------------------------------------------ | ------------ |
| **OCP** | [The Open Closed Principle](http://www.objectmentor.com/resources/articles/ocp.pdf) | 开放封闭原则 |
| **LSP** | [The Liskov Substitution Principle](http://www.objectmentor.com/resources/articles/lsp.pdf) | 里氏替换原则 |
| **ISP** | [The Interface Segregation Principle](http://www.objectmentor.com/resources/articles/isp.pdf) | 接口分离原则 |
| **DIP** | [The Dependency Inversion Principle](http://www.objectmentor.com/resources/articles/dip.pdf) | 依赖倒置原则 |

1. 单一责任原则（SRP）

   当需要修改某个类的时候原因有且只有一个。

   换句话说就是让一个类只做一种类型责任，当这个类需要承当其他类型的责任的时候，就需要分解这个类。

   类被修改的几率很大，因此应该专注于单一的功能。

   如果你把多个功能放在同一个类中，功能之间就形成了关联，改变其中一个功能，有可能中止另一个功能，这时就需要新一轮的测试来避免可能出现的问题，非常耗时耗力。

2. 开放封闭原则（OCP）

   对年扩展是开放的，对修改是封闭的。

   1) 通过增加代码来扩展功能，而不是修改已经存在的代码

   2) 若客户模块和服务模块遵循同一个接口来设计，则客户模块可以不关心服务模块的类型，服务模块可以方便扩展服务（代码）

   3) OCP支持替换的服务，而不用修改客户模块

   ```java
   public boolean sendByEmail(String addr, String title, String content) {
   
   }
   
   public boolean sendBySMS(String addr, String content) {
   
   }
   
   // 在其它地方调用上述方法发送信息
   sendByEmail(addr, title, content);
   
   sendBySMS(addr, content);
   
   /*
    *如果现在又多了一种发送信息的方式，比如可以通过QQ发送信息，那么不仅需要增加一个方法sendByQQ()，还需要
    *在调用它的地方进行修改，违反了OCP原则，
    *更好的方式是抽象出一个Send接口，里面有个send()方法，然后让SendByEmail和SendBySMS去实现它既可。
    *这样即使多了一个通过QQ发送的请求，那么只要再添加一个SendByQQ实现类实现Send接口既可。
    *这样就不需要修改已有的接口定义和已实现类，很好的遵循了OCP原则。
    */
   ```
