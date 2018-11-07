<div align="center">
    <h1>
    	DesignPattern - HeadFirst
	</h1>
</div>

## About	
	
	《HeadFirst设计模式》这本书中所讲解的常见的设计模式以及本书中示例源码实现

## Catalogue

### 策略模式
```
封装和继承可以实现代码复用，但是Java接口不具备代码实现功能，无法达到代码的复用。
不同对象具有同一行为的不同实现，将此行为抽离出来定义为接口，行为的不同实现类都将实现此接口。
在基类中定义接口变量，不同的派生类对象赋予此接口变量不同的实现，利用多态执行此行为的具体实现。
可以在基类中定义接口的set方法，实现动态调用不同的实现方法。

设计原则：
	1.找出应用中可能变化的部分，将他们独立出来；
	2.针对接口编程，而不是针对实现编程（关键在于多态）；
	3.多用组合，少用继承；
总结：策略模式定义了算法族，分别封装起来，让他们之间可以相互替换，此模式让算法的变化独立于此算法的客户。
```

### 观察者模式
```
观察者模式定义的是一对多的依赖关系，一个被观察者可以拥有多个观察者，并通过接口对观察者与被观察者进行逻辑解耦，降低两者的直接耦合。

实现方式：
1.包含Subject与Observer接口的类设计 
	被观察者定义观察者集合，并定义添加、删除操作用于实现观察者的注册和除名；
	被观察者定义通知方法，用于将新状态通知给观察者用户；
	观察者需要有接收被观察者通知的方法，复写接口方法；
	观察者需要有被观察者对象用于实现注册与退出；
2.Java为观察者模式提供了内置的支持
	Observable类与Observer接口
	setChanged()指示状态改变，notifyObservers()传送数据对象，addObserver(Observer obj)注册
设计原则：交互对象之间松耦合

应用：许多GUI框架（如swing），ActionListener响应按钮上的动作

总结：观察者模式定义了对象之间的一对多依赖，当一个对象状态改变时，所有依赖者都会收到通知并自动更新
```

### 装饰者模式
```
继承会引发类数量爆炸和基类加入新功能并不适用于所有子类。
装饰者模式允许不直接修改代码的情况下对其进行拓展。
每个装饰者都有一个组件，即被装饰者变量，通常以构造函数赋值。
装饰者类型来于继承，行为来于组件。装饰者与被装饰者有相同的父类或接口；
可以用一个或多个装饰者包装一个对象；
装饰者可以在被委托的被装饰者的行为前后加上自己的行为，已达到特定的目的；

应用：java.io类

总结：装饰者模式动态地将责任附加到对象上。若要扩展功能，装饰者提供了比继承更有弹性的替代方案。
```

### 工厂模式
```
工厂模式用来封装对象的创建，创建一个框架，由子类决定要如何实现。客户在实例化对象的时候，只会依赖于接口，而不是具体类。
设计原则：要依赖抽象，不要依赖具体类。不能让高层组件依赖底层组件。
	依赖倒置原则：
	变量不可以持有具体类的引用；
	不要让类派生自具体类；
	不要覆盖基类中以实现的方法；

总结：工厂方法模式定义了一个创建对象的接口，但由子类决定要实例化的类是哪一个。工厂方法让类把实例化推迟到子类。抽象工厂模式提供一个接口，用于创建相关或依赖对象的家族。

区别：工厂方法用的是继承，通过子类来创建对象；抽象工厂用的是组合，提供一个抽象类型，，其子类定义了生产对象的方式，要使用工厂必须先实例化，然后将其传入一些针对抽象类型所写的代码中。
```
### 单例模式
```
对比：利用关键词synchronized实现方法同步，但是同步一个方法可能造成程序执行效率下降很多。
利用双重检查加锁，只有第一创建时会执行同步区块的代码。
用处：数据库连接，redis数据访问
注意：不同的类加载可能会加载同一个类，同一个类可能会被加载多次。解决方法是：自行指定类加载器，并指定同一个类加载器。
总结：单例模式确保一个类只有一个实例，并提供一个全局访问点。
```

### 命令模式（封装方法调用）
```
命令模式可以将“动作的请求者”从“动作的执行者”中解耦出来，两者之间通过命令对象进行沟通，命令对象所属类实现了命令接口，封装了命令的具体操作。调用者通过调用命令对象的execute()方法发出请求，接收者会执行特定的方法。宏命令是一种延伸允许调用多个命令。
命令对象的作用：一个命令对象通过在特定接收者上绑定一组动作来封装一个请求。要达到这一点，命令对象将动作和接收者上绑定包进对象中。这个对象只暴露出一个execute()方法，当此方法被调用的时候，接收者就会进行这些动作。从外面来看，其他对象不知道究竟哪个接收者进行了什么动作，只知道调用execute()方法，目的就能达到。
用处：队列请求，工作队列类与进行运算的对象之间是完全解耦的；日志请求，通过记录日志，将上次检查点之后的所有操作记录下来，系统出现问题则从检查点应用这些操作。
总结：命令模式将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可以撤销的操作。
```

### 适配器模式
```
适配器模式的目的是包装某些对象，转换接口。这样做可以将类的接口转换成想要的接口以便实现不同的接口。创建适配器进行接口转换，让不兼容的接口变成兼容，同时让用户从实现的接口解耦。
过程：客户是依据目标接口实现的，适配器(TurkeyAdapter)实现了目标接口(Duck)，并持有被适配者(Turkey)的实例。①客户通过目标接口调用适配器的方法对适配器发出请求。②适配器使用被适配器接口把请求转换成被适配者的一个或多个调用接口。③客户接收到调用的结果，但并未察觉这一切是适配器在起转换作用。
探讨：①实现适配器所需要做的工作和目标接口的大小成正比，如果不要适配器，就必须改写客户端接口来调用这个新的接口。②适配器模式的工作是将一个接口转换成另一个，通常一个适配器只包装一个被适配者。③新旧接口同时并存，创建一个双向适配器，必须实现所涉及的两个接口。
对象适配器与类适配器：对象适配器使用组合来适配被适配者，类适配器使用继承被适配者与目标类的方法来实现的。
装饰模式与适配器模式：前者增强功能，后者转换接口，主要是意图不同。
总结：适配器模式将一个类的接口，转换成客户期望的另一个接口。适配器让原本接口不兼容的类可以合作无间。Java在集合类采用了迭代器适配了以前的联合类。
```

### 外观模式
```
外观模式是改变接口的新模式，与适配器模式不同的是，适配器意图在于转换接口，而外观模式主要是为了简化接口。使用方式为：创建了一个接口简化而统一的类，用来包装子系统中一个或多个复杂的类。值得注意的是，外观模式提供简化的接口的同时，依然将系统完整的功能暴露出来，以供需要的人使用。
外观模式不只是简化了接口，也将客户从组件的子系统中解耦。外观模式可以附加功能，让子系统使用起来更加方便。一个子系统也可以创建多个外观。
设计原则：“最少知识”原则：只和你的密友谈话，即减少对象之间的交互。当我们设计一个系统时，不管是任何对象，你都要注意它所交互的类有哪些，并注意它和这些类是如何交互的。所以在对象方法内，只应该调用以下范围内的方法：①该对象本身的方法②被当做方法的参数而传递进来的对象③此方法创建或者实例化的任何对象④对象的任何组件；
最小知识原则减少了对象之间的依赖，减少软件维护的成本；但是也会导致制造了更多的包装类，这样会导致复杂度和开发时间的增加，并降低运行时性能。
总结：外观模式提供了一个统一的接口，用来访问子系统中的一群接口。外观模式定义了一个高层接口，让子系统更容易使用。
```
### 模板方法模式
```
模板方式模式使用抽象类作为算法的模板，具体处理方法由子类完成，需要子类提供的方法，必须在超类中声明为抽象。模板方式模式用于封装算法块，创建框架。
抽象类的定义：作为基类，其子类必须实现其所有抽象操作；模板方法里面可以有“默不做事的方法”（hook），子类可以视情况选择是否覆盖他们，从而进行拓展影响抽象类中的算法流程；模板类中抽象方法的数量根据实际情况而定，步骤太少没有弹性，步骤太细，子类实现起来会很麻烦。
设计原则：高层组件对待低层组件的方式是“别调用我们，我们会调用你”。
总结：模板方法模式在一个方法中定义了一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中的某些步骤。
```

	
## References

<https://github.com/iluwatar/java-design-patterns>