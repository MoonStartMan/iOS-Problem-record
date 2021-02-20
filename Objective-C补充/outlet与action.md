# outlet 和 action

## outlet输出口

+ 为了能让代码引用nib中的对象，我们在代码中对应的变量前面加上IBOutlet来修饰标记，本身来说它只是个标记，没有什么实际意义，只是用来告诉编译器，这个变量有些特别，是个界面的Outlet，Outlet要和nib文件（也就是storyborad里面的界面）里面的一个对象关联起来（建立了一个connection），一旦建立了连接，我们就说当前这个标记了IBOutlet的变量是nib文件中某对象（object）的referencing outlet

+ 所以说 Outlet是一个变量，是一个带有outlet标记的变量，outlet connection是nib对象创建之后，通过nib里面的定义，在runtime的时候，把它们关联起来的一个机制，这个关联关系建立起来之后，这个outlet就是这个nib对象的referencing outlet

## action操作

+ 界面发生事件后，需要一段代码来调用一个方法，响应这个操作，IBAction就是用来标记代码中这个方法的。

+ 在代码中对应的方法前面加上IBAction标记，本身来说它只是个标记，没有什么实际意义，只是用来告诉编译器，这个方法有点特别，是一个界面中的对象的Action行为方法，Action要和nib文件里面（也就是界面）的一个界面对象关联起来（建立了一个Action Connection），一旦建立了连接，我们就说当前这个标记了IBAction的方法是nib文件（也就是界面）中某对象所需要响应的事件
