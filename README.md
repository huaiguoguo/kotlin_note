# kotlin_note
kotlin 学习笔记


import com.sun.corba.se.impl.orbutil.graph.Graph
import com.sun.xml.internal.fastinfoset.util.StringArray
import org.omg.CORBA.Context

import javax.swing.text.AbstractDocument
import javax.swing.text.View
import kotlin.reflect.KProperty

/**
 * Created by huochai on 2017/5/29.
 */


//数据类型
/**
 * 浮点型 Double 64位
 * 浮点型 Float  32位
 * 整型   Long 64位
 * 整型   Int  32位
 * 整型   Short 16位
 * 字节   Byte   8位
 */





//String?
//String!!
//String

//data?.let{
//    当data不为空的时候，会执行下面
//}
//
//data?:let{
//    当data为空的时候，会执行下面
//}


//kotlin里面所有名称是分大小写的

//定义包
/*
1.包的声明处于源文件的顶部部分
2.包的路径与目录的路径没有关系
3. 以下包会默认导入每个kotlin文件中
    kotlin.*
    kotlin.annotation.*
    kotlin.collections.*
    kotlin.comparisons.* （自 1.1 起）
    kotlin.io.*
    kotlin.ranges.*
    kotlin.sequences.*
    kotlin.text.*
    如果是JVM平台的话还会导入以下额外的包：
    JVM:
        java.lang.*
        kotlin.jvm.*
3.可以导入一个作用域  包含下面的所有类 函数 变量
    例如： import foo.Bar.*
4. 可以用as来解决名字冲突的问题
   import foo.Bar
   import food.Bar as fBar
5. import不仅可以导入类  1) 还可以导入顶层函数和属性  2) 枚举常量 3)在对像声明中的声明的函数和属性
 */

//基本类型
/** Kotlin中 字符不是数字
 *  kotlin里面的所有东西都是对像  我们可以在任何变量上调用其成员函数和属性
 *  1. 数字有以下数字类型  (数字没有隐式转换)
 *      Double 64
 *      Float  32
 *      Long   64
 *      Int    32
 *      Short  16
 *      Byte    8
 *
 *  2.字面常量 数值常量字面值有以下几种(暂不支持八进制)
 *    十进制(
 *           Long类型用大写的L加在数值后面 123L
 *          123.4 默认为double类型  要在后面加上f/F表示浮点数
 *          )
 *    十六进制
 *    二进制
 *  3.数字字面值中的下划线 可以使用下划线 使得 字面值更易读
 *     val oneMillion = 1_000_00
 *     val oneMillion = 1_000_000
 *     val creditCardNumber = 1234_5678_9012_3456L
 *     val socialSecurityNumber = 999_99_9999L
 *     val hexBytes = 0xFF_EC_DE_5E
 *  4.表示方式
 *  5.显式转换
 *     较小类型不能隐式转换为大类型  也就是说  较小类型不能赋值给较大类型的变量
 *     val b:Byte = 1
 *     val i:Int = b  这样是错误的
 *     可以显示的转换
 *     var i:Int = b.toInt();
 *     每个数值类型的变量都可以：toByte(),toInt(),toLong(),toShort(),toFloat(),toDouble(),toChar()
 *
 *   6.运算 位运算
 *   7.字符  用Char来表示  不能直接当作数字  比如 var c:Char = 3  这是错误的，字符类型的值必须用 单引号 包含起来
 *      特殊字符可以用\来转义  例如：\t \b \n \r \' \" \\ \$
 *     显示把字符类型的数值转换为数值  比如： '123'.toInt();
 *   8.布尔  用Boolean表示  有两个值: true false
 *      可空引用会被装箱
 *      内置的布尔运算有：||(短路逻辑或) &&(短路逻辑与)  !(逻辑非)
 *   9.数组 Array表示 它里面有：get()、set()、size属性等等
 *      可以用arryOf()来创建数组并且给数组元素传递值
 *      var test = arrayOf(1,2,3,4,5) 属于装箱操作
 *      var test:Array<String> = arrayof("a", "b", "c")
 *      var asc = Array(5,{i->i*i}) 用闭包方式进行初始化
 *      var empty = emptyArray<Int>();
 *      var tt = Array<String>(5, {"a";"b";"c"})
 *
 *      //无装箱操作的原生类型数组  i
 *      val x: IntArray = intArrayOf(1, 2, 3)
 *      val x: FloatArray = floatArrayOf(1, 2, 3)
 *      val x: LongArray = LongArrayOf(1, 2, 3)
 *      val x: ShortArray = ShortArrayOf(1, 2, 3)
 *
 *
 *
 *   10.字符串
 *      字符串的值是不可变的
 *      字符串可以用str[num] 来访问
 *      原生字符串是用  """ hello world """ 用这个符号来括起来  里面没有转义符  可以包含任何字符
 *      var text = """  for (c in text){ println(c) }""".trimMargin() 去除前导空格
 *      默认|用作边界前缀     用trimMargin(">")可以选对其它字符作为参数传入
 *   11.字符串模板 用$符号  或者 $加大括号 {}
 *      var i = 10;
 *      var s = "i=$i"
 *      var s = "abc"
 *      var str = "$s.length is ${s.length}"
 *      如果在字符串中需要一个无意议的$符号的话可以使用 '$'
 *      $符不支持转义
 *      像如：var price = """ ${'$'}9.99"""
 *
 */

//控制流
/**
 * 1.if表达式
 *      kotlin里面  if是一个表达式  即它会有一个返回值，所以三元运算符在kotlin里面就不需要了
 *      //这是传统的写法
 *      var max:Int
 *      var a=3, b=4
 *      if(a>b) max = a
 *      //kotlin里面直接   如果使用这种的话  必须有一个else分支块
 *      var max  = if(a>b) a else b
 *      var max = if(a>b){
 *              println("a")
 *              a
 *          }else{
 *              println(b)
 *              b
 *          }
 *
 *
 * 2.when表达式
 *      when取代了 以前编程语言里面的switch case
 *      when(max){
 *          1->println("max == 1")
 *          2->println("max == 2")
 *          else->{
 *              println("max is neither 1 nor 2")
 *          }
 *      }
 *      如果有多种情况是一样的除理方法则可以：
 *      when(max){
 *          1,2->println("max == 2")
 *          else->{
 *              println("max is neither 1 nor 2")
 *          }
 *      }
 *      用in作为条件
 *      when (max) {
 *           in 1..10 -> print("max is in the range")
 *           in validNumbers -> print("max is valid")
 *           !in 10..20 -> print("max is outside the range")
 *           else -> print("none of the above")
 *       }
 *
 *      也可以用is来作为判断条件 判断值是不是某种类型
 *      fun hasPrefix(max:Any){
 *          is String->x.startsWith("prefix")
 *          else->false
 *      }
 *      //也可以不用is来判断条件是否为真  有时候可以用内置的函数来判断，如果此值为真则执行该分支
 *      when {
 *           x.isOdd() -> print("x is odd")
 *          x.isEven() -> print("x is even")
 *          else -> print("x is funny")
 *      }
 *
 *      注意：如果 when 作为一个表达式使用，则必须有 else 分支
 * 3.For循环
 *      for循环可以对任何有迭代器(iterator)的对像进行遍历
 *      for(item in collection) { println(item) }
 *      for(item:Int int ints){
 *
 *      }
 *      即：迭代器iterator()返回类型里面有一个next()函数 和 hasNext()(hasNext() 返回一个Boolean的值)
 *      这三个函数都需要标记为 operator。
 *
 *      for循环对数组循环 会被编译为：不创建迭代器的  基于索引的循环
 *      换句话说： for循环数组的时候 不是用迭代器循环的，而是用索引循环的
 *      如果想用索引的方式循环数组或者list的话，就用下面的这种方式
 *      for(i in testArr.indices){
 *          println(testArr[i])
 *      }
 *      以上的编历方式：会编译成优化的实现  而不会  创建额外对象
 *
 *      也可以用库函数: withIndex
 *      for((index, value) in arrTest.withIndex()){
 *          println("the element at $index is $value")
 *      }
 * 4. while循环  和其它语言的while循环语法一样
 */

//返回和跳转
/**
 * Kotlin 有三种结构化跳转表达式
 *   return。默认从最直接包围它的函数或者匿名函数返回。
 *   break。终止最直接包围它的循环。
 *   continue。继续下一次最直接包围它的循环。
 *
 *   Break和Continue 标签
 *   任何的表达式都可以标记，标记的格式为：标识符@
 *   例如：abc@   fooBar@都是有效的标签
 *   为一个表达式加标记：
 *   abc@ for(index in 1..100){
 *          for(j in 1..100){
 *              if(....) break@abc  直接跳转到最外层的循环  有点像其它语言的go to(php)
 *          }
 *      }
 *
 *   这个地方还要再看一下文档，有点看不懂。。。。
 *
 */

//函数
/*
*      1.函数的声明用fun关键字声明  fun Test(x:Int):Int{ return x*3}
*      2.函数的用法 var test = Test(3)
*      3.类的成员函数调用方法：Sample().foo();
*      4.函数还可以用中缀表示法调用  但条件是：
*           他们是成员函数或扩展函数
*           他们只有一个参数
*           他们用 infix 关键字标注
*      5.函数的参与用Pascal表示法定义  即 name:type 参与之间用逗号隔开 每个参数必须是显式声明类型
*      6.函数参数默认值  fun read(b: Array<Byte>, off: Int = 0, len: Int = b.size()) {}
*      7.在类中 某个父类中的函数的参数有默认值  子类如果重载了父类中的方法时 此参数不能有默认值
*        换句话说：父类中的函数有默认值  子类再重载的时候  此参数不能有默认值  而且类型必须相同
*        open class A {
*            open fun foo(i: Int = 10) { …… }
*        }
*
*        class B : A() {
*            override fun foo(i: Int) { …… }  // 不能有默认值
*        }
*      8.命名参数  所谓命名参数就是在调用的时候 传参时 写上原来函数的参数名称
*      9. 无返回值的函数  :Unit 可以省略：  fun test(x:Int):Unit{}
*      10.单表达式函数 fun test(x:Int):Int = 2  此此的返回值类型:Int 是可选的
*      11.具有代码块的函数 必须显示指定返回类型 :Unit除外
*      12.可变数量的参数
            fun <T> asList(vararg ts: T): List<T> {
                val result = ArrayList<T>()
                for (t in ts) // ts is an Array
                    result.add(t)
                return result
            }
            val a = arrayOf(1, 2, 3)
            val list = asList(-1, 0, *a, 4)  在参数前加一个*号  表示使用伸展操作符
       13.局部函数  也就是在一个函数在另一个函数内部  局部函数可以访问外部函数(闭包函数)中的局部变量
            fun test(){
                fun test_copy(){
                
                }
            }
       14.成员函数：在类内部的函数叫成员函数  调用方法 类名().成员函数名称()
       15.泛型函数  fun <T> singletonList(item: T): List<T> {}
       16.内联函数
       17.扩展函数
       18.高阶函数和Lambda表达式
       19.尾递归函数  tailrec  当一个函数被tailrec 修饰时 并且本身又是一个递归的时候  就称为 尾递归函数
            注意有2种情况不能使用尾递归
            1.在递归调用后面有更多的代码的时候 不能使用尾递归
            2.在try/catch/finally块中


*/

//类属性和字段
/**
 * 1.属性声明的标准语法是: var/val <propertyName>[: <PropertyType>] [= <property_initializer>]
 *                              [<getter>]
 *                              [<setter>]
 * 2.属性分为可变属性和不可变属性   可变属性用var关键字  不可变属性用val关键字
 * 3.初始化器和get set都可以省略 属性类型如果可以从初始化器中推断出来，也可以省略
 *      var allByDefault:Int?  //错误：需要显式初始化器，隐含默认 getter 和 setter
 *      var initialized = 1     // 类型 Int、默认 getter 和 setter
 *    以上这种声明变量的方法 不常用，可以做为了解  在我们声明变量的时候 kotlin已经帮我们隐式 使用了getter setter
 *    这种方法后面再做深入研究
 * 4.只读属性(以val声明的变量)不允许setter
 * 5. 从kotlin1.1开始 如果可以从getter推断出属性类型的话，则可以省略 变量名称后面的那个类型
 *      var isEmpty get() = this.size == 0;
 * 6. 如果想改变一个访问器(getter/setter)的可见性或者给其增加注解, 可以定义访问器而不定义实现
 *      var setterVisibility:String = "abc"
 *          private set   // 此 setter 是私有的并且有默认实现
 *      var setterWithAnnotation:Any?=null
 *          @Inject set  // 用 Inject 注解此 setter
 * 7.幕后字段 field  只能用在属性的访问器(setter / gettter)当中
 *     如果一个属性 至少有一个访问器使用默认实现 或者 通过访问器 用field 引用幕后字段 就会给该属性生成一个幕后字段
 *      var counter = 0
 *          set(value){
 *              if(value>=0){
 *                  field = value   直接通过field 引用了幕后字段 所以该属性就会生成一个幕后字段
 *              }
 *          }
 *
 *      var isEmpty:Boolean
 *          get() = this.size == 0  这个属生没有使用默认的访问器  也没有直接用field 引用幕后字段 所以此属性没有 幕后字段
 *
 * 7.幕后属性 这个看不明白
 * 8.编译期常量：【已知值的属性可以使用 const 修饰符标记为 编译期常量】    并且需要满足以下三个条件
 *      1) 位于顶层或者是object的一个成员
 *      2) 用String或者原生类型 值初始化
 *      3) 没有自定义的getter
 * 9.延迟初始化属性   一般地，属性声明为非空类型必须在构造函数中初始化 然而，这经常不方便。例如：属性可以通过依赖注入来初始化， 或者在单元测试的 setup 方法中初始化。
 *                  这种情况下，你不能在构造函数内提供一个非空初始器。 但你仍然想在类体中引用该属性时避免空检查
 *                  为了这种情况  我们可以在属性前面加一个 lateinit 来修饰符来标记该属性
 *      注意:1) lateinit修饰符只能用在 类体中的 var属性（不是在主构造函数中）
 *          2) 该属性没有自定义的访问器：getter/setter
 *          3) 该属性必须是非空类型
 *          4) 该属性不能是原生类型
 * 10.覆盖属性
 * 11.委托属性
 */

//类
/**
 * 1.类的声明
 *      class invoice{
 *
 *      }
 *   声明类的标准备格式：
 *   类关键字 类名 类头(指定其类型参数, 主构造函数) 和 类体(大括号) 组成, 类头和类体都是可选的
 *   如果一个体没有类体的话  可以省略后面的花括号
 *   class Empty
 *
 * 2.构造函数
 *      可以有一个主构造函数和一个或多个次构造函数  主构造函数是类头的一部分 跟在类名后面
 *      class Test constructor(firstName:String){}
 *      1) 注意：如果一个主构造函数没有任何注解或者可见修饰符  则可以省略些construct关键字
 *      2)主构造函数的参数可以是可变的(var)，也可以是不可变的(val)
 *      3)主构造函数的参数可以放在初始化代码块(init{})内使用
 *      4)主构造函数的参数可以用在类体内的属性上面
 *
 *      5)如果主构造函数有注解或可见性修饰符 这个constructor必须存在
 *          //class Customer public @Inject constructor(name: String) { …… }
 *          class Test(firstname:String){
 *              init{
 *                  这里是初始化代码块 初始化的代码可以放到这里
 *                  主构造函数的参数可以放在这里使用
 *                  logger.info("Customer initialized with value ${name}")
 *              }
 *              主构造函数的参数也可以用在 类体内的属性上
 *          }
 *      4) 如果主构造函数的所有的参数都有默认值，编译器会生成 一个额外的无参构造函数，它将使用默认值。
 *
 * 3.次构造函数
 *      1)类可以声明前缀带有constructor的次构造函数
 *          class Test private constructor(var firstName:String, val lastName:String){
 *              constructorABC(name:String, parent:Test):this(name){}
 *          }
 *      2)如果有主构造函数 则：类中的每个次构造函数需要委托给主构造函数
 *          可以直接委托或者通过别的次构造函数间接委托。
 *          委托到同一个类的另一个构造函数 用 this 关键字即可：
 *          class Person(val name: String) {
 *               constructor(name: String, parent: Person) : this(name) {
 *                  parent.children.add(this)
 *               }
 *           }
 *       3)如果有主构造函数  则：类中不能再声明一个和主构造函数参数类型相同的次构造函数
 *
 *       如果一个非抽像类当中没有声明任何的主次构造函数  它会生成一个不带参数的主构造函数 可见性为public
 *       如果你不希望 此类的这个无参构造参数 为公共的（也就是public的） 那就显示的声明一个无参的主构造函数 并且限制它的可见性
 *       class DontCreateMe private constructor(){}
 *       此时DontCreateMe 就变成了不可调用 不可实例化的 类了
 *
 * 4. 创建类的实例    var test = Test();   var test = Test("huochai")
 *
 *
 *
 *
 */

//继承
/**
 * 1.在kotlin当中  所有的类都有一个共同的父类:Any 所有的类都默认隐式继承 父类在有些文档当中称为：超类
 * 2. 继承方式是：把父类(超类) 放在类头的冒号后面  注意：如果父类有一个主构造函数的话  子类必须用 子类的主构造函数参数 就地 初始化
 *          class open class Base(p: Int)
class Derived(p: Int) : Base(p) 就地初始化:Base(p)
 * 3.如果子类没有主构造函数 那么子类的每个次构造函数 必须用supper函数初始化父类
open class Base(p:Int){

}
class Derived:Base{  //在此子类没有主构造函数 所在在此不能就地初始化
constructor(p:Int):super(p){  //在每个次构造函数当中用 :supper(p) 的方式 初始化父类 注意：子类中不同的次构造函数可以调用基类型的不同的构造函数

}
}
 *
 * 4.所有的类默认都是final类型的  如果某类要想被继承必须加上显式的用open加以修饰
 *
 * 5.覆盖(重写)方法
 *      kotlin力求清晰明显 与java不同 kotlin需要显式标注可以覆盖的成员(称为开放)和覆盖后的成员
 *      1)父类中的成员方法如果希望被覆盖(重写) 必须加上open关键字进行修饰  同时此类也是open修饰过的, 换言之 父类名前面也必须加上open关键字
 *      2)子类中的覆盖父类的成员方法 要加上override
 *      3)如果子类的的成员方法不想再被无限制的覆盖(重写) 那就再次给此成员函数加上final关键字
 *          open class AnotherDerived:Base(){
 *              final override fun v(){}  //此成员函数重新加上final后，就不会再被覆盖了
 *          }
 * 6.覆盖属性
 *      属性覆盖与方法覆盖类似
 *      可以用一个 var 属性覆盖一个 val 属性，但反之则不行。
 *      这是允许的，因为一个 val 属性本质上声明了一个 getter 方法，而将其覆盖为 var 只是在子类中额外声明一个 setter 方法
 *      注意，你可以在主构造函数中使用 override 关键字作为属性声明的一部分。

interface Foo {
val count: Int
}

class Bar1(override val count: Int) : Foo  //可以在此类的主构造函数中 用override关键字 作为参数声明的一部分

class Bar2 : Foo {
override var count: Int = 0
}

 * 7.覆盖规则
 *  实现继承由下述规则规定：如果一个类从它的直接超类继承相同成员的多个实现， 它必须覆盖这个成员并提供其自己的实现（也许用继承来的其中之一）。
 *  为了表示采用从哪个超类型继承的实现，我们使用由尖括号中超类型名限定的 super，如 super<Base>：
open class A {
open fun f() { print("A") }
fun a() { print("a") }
}

interface B {
fun f() { print("B") } // 接口成员默认就是“open”的
fun b() { print("b") }
}

class C() : A(), B {
// 编译器要求覆盖 f()：
override fun f() {
super<A>.f() // 调用 A.f()
super<B>.f() // 调用 B.f()
}
}
同时继承 A 和 B 没问题，并且 a() 和 b() 也没问题因为 C 只继承了每个函数的一个实现。
但是 f() 由 C 继承了两个实现，所以我们必须在 C 中覆盖 f() 并且提供我们自己的实现来消除歧义。
 *
 * 8.抽像类  类和类里面的成员可以用abstruct来修饰 就变成了抽像类/抽像成员属性/抽像成员函数  抽像类不需要open关键字修饰
 *   我们可以用一个抽像类/抽像成员来覆盖非抽像的开放式(加了open的)成员
open class Base {
open fun f() {}
}
abstract class Derived : Base() {
override abstract fun f()
}
 *   我们也可以用一个非抽像类来覆盖抽像成员
 *   class BC:Derived(){
 *      override fun f(){}
 *   }
 *
 */

//接口 既可以包含抽象方法的声明，也可以包含实现。与抽象类不同的是，接口无法保存状态。它可以有 属性但必须声明为抽象或提供访问器实现
/**
 * 1.kotlin中接口的定义用关键字interface来定义
 *      interface MyInterface{
 *          fun bar()
 *          fun foo(){}
 *      }
 * 2.实现接口 一个类或者对象可以实现多个接口
 *      一个类或者对象可以实现一个或多个接口
 *      class Child:MyInterface{
 *          override fun bar(){
 *              //方法体
 *          }
 *      }
 * 3.接口中的属性
 *      你可以在接口中定义属性，但是属性必须是：抽像属性  或 实现了访问器的实现 getter
 *      接口属性不能有幕后字段 因此接口中声明的访问器不能 引用幕后字段
 *      interface MyInterface{
 *          val prop:Int //抽象属性   接口属必须是抽象的或者 实了访问器的
 *          val propertyWithImplementation:String  //此属性实现了 访问器
 *              get() = "foo" //在此不能使用幕后字段
 *
 *         fun foo(){
 *              print(prop)
 *         }
 *      }
 *
 *      class Child:MyInterface{
 *          override val prop:Int = 29
 *      }
 * 4.解决覆盖冲突  如果一个类实现了多个接口，接口与接口之间有重复的方法  此时就要在实现方法中用声明语句 明确表示 实现的是哪个接口的哪个方法
 *   具体格式为：supper<B>.bar  例子如下：
 *   注意：在接口中没有方法体的  成员方法 默认为：抽像方法  因为不需要再加abstruct关键字进行修饰  切记切记
 *   interface A{
 *      fun foo(){ print("A foo") }
 *      fun bar()  //此成员方法没有方法体，所以默认就是抽象方法  这一点要记住
 *   }
 *
 *   interface B{
 *      fun foo(){ print("B foo") }
 *      fun bar(){ print("B bar") }
 *   }
 *
 *   class C:A{
 *      override fun bar(){ print("bar") }
 *   }
 *
 *   class D:A,B{
 *      override fun foo(){
 *          supper<A>.foo()
 *          supper<B>.foo()
 *      }
 *
 *      override fun bar(){
 *          supper<B>.bar()
 *      }
 *   }
 *
 */

//可见性修饰符  类、对像、接口、构造函数、方法、属性和它们的setter都有可见性修饰符，getter总是与属性有着相同的可见性;
//在kotlin中有4个可见性修饰符：private、protected、internal和public  如果没有显示指定修饰符的话，默认的可见性是：public
/**
 * 根据声明作用域的不同来解释
 * 1.包名 函数 属性和类 对象和接口 可以在顶层声明，即可以直接在包内
 *      package foo
 *
 *      fun baz(){}
 *      class Bar{}
 *      --如果显示的指定任何的修饰关键字 默认为：public, 这意味着你的声明 随处可见
 *      --如果用可见性修饰符：private 则被修饰"对象"的可见性范围：在声明文件内
 *      --如果用：internal 它会在相同模块内随处可见
 *      --如果用：protected 不适用于顶层声明 【适用于类和接口 属生 函数 方法等】
 * 2.类和接口
 *    对于类内部的成员：
 *    --private 只在类内部(包含其所有成员)可见;
 *    --protected 和 private 一样， 不同的是 protected可以在子类中可见
 *    --internal 能见到类声明的 本模块内的任何客户端都可见其internal成员
 *    --public 能见到类声明的 任何客户端都可见其public成员
 *    注意 对于Java用户：Kotlin 中外部类不能访问内部类的 private 成员。
 *    例子：
 *    open class Outer{
 *          private val a = 1
 *          protected  open val b = 2
 *          internal val c = 3
 *          val d = 4
 *
 *          protected class Nested{
 *              public val e:Int = 5
 *          }
 *    }
 *
 *    class Subclass:Outer(){
 *          //a 不可见
 *          //b、c、d 可见
 *          //Nested和e 可见
 *          override val b = 5 // "b" 为protected
 *    }
 *
 *    class Unrelated(o:Outer){
 *          //o.a、o.b不可见
 *          //o.c、o.d可见(相同模块)
 *          //Outer.Nested不可见，Nested::e 也不可见
 *    }
 *
 * 3.构造函数 要指定一个类的主构造函数的可见性 使用以下语法(注意你需要添加一个 显式 constructor关键字)
 *      class C private constructor(a:Int){.......}
 *      这里的构造函数是私有的。默认情况下，所有的构造函数都是public ,实际上 等于类可见的地方它就可见(即一个internal类的构造函数只能 在相同模块内可见)
 *
 * 4.局部声明     局部变量、函数和类不能有可见性的修饰符
 *
 * 5.模块         可见性修饰符 internal 意味着该成员只在相同模块内可见。更具体地说，一个模块是编译在一起的一套kotlin文件
 *      --一个Intellij IDEA 模块;
 *      --一个Maven 或者 Gradle项目
 *      --一次<kotlin>Ant任务执行所编译的一套文件
 *
 */

//泛型
/**
 * 1.与java类似，Kotlin中的类也可以有类型参数
 *  class Book<T>(t:T){
 *      var value = t
 *  }
 *  一般来说，要创建这样类的实例，我们需要提供类型参数
 *  val box:Box<Int> = Box<Int>(1)
 *  但是如果类型参数可以推断出来，例如从构造函数的参数或者从其它途径，允许省略类型参数
 *  val box  =  box(1) //1具有类型Int ，所以编译器知道我们说的是Box<Int>
 * 2.型变  java类型系统中最棘手的部分之一是通配符类型。
 * 而kotlin中没有。相反，kotlin中有两个其它东西：
 * 1)声明处型变  out相当于java当中的 上边界符 <? extends xxx>  in相当于java当中的 下边界符<? super xxx>
 *     为什么叫声明处型变呢，因为在声明形参的时候就为其加上：out 或  in 关键字  所以叫：声明处型变
 * 2)类型投影   【这个有点难，真的难】  主要是在传入函数时加上out 或in 关键字 以仿函数里面对参数的 生产或消费
 * 3)星投影    【这个我也有看的太明白】  星投影非常像java的原始类型 非常安全
 * 4)泛型函数  不仅类可以有类型参数。函数也可以有。类型参数要放在函数名称之前：
 *      fun <T> singletonList(item:T):List<T>{
 *
 *      }
 *
 *      fun <T> T.basicToString():String(){  // 扩展函数
 *
 *      }
 *      调用泛型函数的方法：在调用处，函数名之后加上类型
 *      var l = singletonList<Int>(1)
 *
 * 5)泛型约束  能够替换  给定类型参数的 所有可能类型的 集合  可以由泛型约束限制。
 *
 * 上界 最常见的约束类型是与 Java 的 extends 关键字对应的 上界:
 *      fun<T:Comparable<T>> sort(list:List<T>){
 *
 *      }
 * 冒号之后指定的类型是上界：只有 Comparable<T> 的子类型可以替代 T。 例如
 * sort(listOf(1, 2, 3)) // OK。Int 是 Comparable<Int> 的子类型
 * sort(listOf(HashMap<Int, String>())) //错误：HashMap<Int, String> 不是 Comparable<HashMap<Int, String>> 的子类型
 *
 * 注意：1)如果没有显式声明上界：默认是Any?。
 *      2)在尖括号中只能指定一个上界。如果同一类型参数需要多个上界，我们需要一个单独的where子句 【真TM蛋疼，条条框框真多】
 *      fun <T> cloneWhenGreater(list: List<T>, threshold: T): List<T>
 *           where T : Comparable,
 *                T : Cloneable {
 *          return list.filter { it > threshold }.map { it.clone() }
 *      }
 *
 *
 */

//扩展   kotlin能够扩展一个类的新功能而无需继承该类或使用像装饰者这样的任何类型的设计模式。 这通过叫做_扩展_的特殊声明完成。Kotlin 支持_扩展函数_ 和 扩展属性。
/**
 * 1.扩展函数  会讲到泛型函数
 *    声明一个扩展函数需 有一个接收类类型 也就是被扩展的类型来作为他的前缀  有点像golang里面的方法的声明
 *    fun MutableList<Int>.swap(index1:Int, index2:Int){
 *          val tmp = this[index1] 此处的this代表 接收者对象：MutableList
 *          this[index1] = this[index2]
 *          this[index2] = tmp
 *    }
 *
 *    然后我们可以对MutableList的对象 任意调用swap函数了
 *    val l= mutableListOf(1,2,3)
 *    l.swap(0,2)
 *
 *    我还可以泛型化 swap函数
 *    fun <T> MutableList<T>.swap(index1:Int, index2:Int){
 *          val tmp = this[index1]
 *          this[index1] = this[index2]
 *          this[index2] = tmp
 *    }
 *
 *    为了在接收者类型表达式中使用泛型，我们需要在函数名前声明泛型参数，就是在接收者前面 声明泛型参数
 *
 * 2.扩展是静态解析的
 *     扩展不能真正的修改被扩展的类。通过定义一个扩展，你并没有在一个类中插入新成员，仅仅是可以通过该类型的变量 用点 的表达式去调用这个新函数
 *     注意：扩展函数是静态分发的，即他们不是根据接收者类型的虚方法。这意味着 调用的扩展函数是由函数调用所在的表达式的类型决定的，
 *     而不是由表达式运行时求值结果决定的。
 *     例如：
 *     open class C
 *     class D:C()
 *     fun C.foo() = "c"
 *     fun D.foo() = "d"
 *     fun printFoo(c:C){
 *          println(c.foo())
 *     }
 *     printFoo(D())
 *     注意：如果一个类定义一个成员函数和一个扩展函数，而这两个函数又有相同的接收者类型，相同的名字 并且都适用给定的参数，
 *     这种情况：总是提取成员函数。例如：
 *     class C{
 *          fun foo(){ println("member") }
 *     }
 *
 *     fun C.foo(){ println("extension") }
 *     如果我们调用 C类型的c的c.foo() ,它将输出“member” 而不是 “extension”
 *     当然，扩展函数重载同样名字但不同参数的成员函数也完全可以：
 *     class C{
 *          fun foo(){ println("member") }
 *     }
 *
 *     fun C.foo(i:Int){ println("extension") }
 *
 *     这次再调用的时候  C().foo() 还是输入member
 *     而如果：C().foo(1) 则输出“extension”
 *
 * 3.可空接收者
 *      可以为可空的接收都类型定义扩展。这样的扩展可以在对象变量上调用，即使其值为null，并且可以在函数体内检测 this==null,
 *      这能让你 在没有检测null的时候 调用kotlin中的toString()：检测发生在扩展函数的内部
 *
 *      fun Any?.toString():String{
 *          if(this == null) return "null"
 *          return toString()
 *      }
 *
 * 4.扩展属性
 *     和扩展函数类似，kotlin也支持扩展属性：
 *     val <T> List<T>.lastIndex:Int
 *          get() = size-1
 *   注意：由于扩展并没有实际的把成员插入类中，因此对扩展属性来说 幕后字段 是无效的。这就是为什么 【扩展属性不能有初始化器】
 *   必须用显式的 访问器getter/setter进行初始化  var Foo.bar = 1 这样是错误的
 *   var Foo.bar
 *      get() = 1  //这样是正确的
 *
 * 5.伴生对像的扩展
 *  ++++先讲一下伴生对象的声明
 *  1)在一个类内部声明一个对象 用companion关键字 就成为伴生对象
 *  2)并且一个类当中只能一个伴生对象
 *      class Myclass{
 *              companion object Factory{ 此处的伴生对象名称(Factory)可以省略
 *
 *              }
 *      }
 *      //伴生对象名称没有省略的情况下可以用 val instance = Myclass.create()   或者 val instance = Myclass.Factory.create()
 *      //在伴生对象名称 省略的情况下用 val instance = Myclass.Companion
 *  3) 伴生对象的成员 运行时仍然是真实的对象的实例成员，而且，例如还可以实现接口：
 *      interface Factory<T>{
 *          fun create():T
 *      }
 *
 *      class Myclass{
 *          companion object:Factory<Myclass>{
 *              override fun create():Myclass = Myclass()
 *          }
 *      }
 *  ++++伴生对像的扩展
 *          class Myclass{
 *              companion object{}
 *          }
 *          fun Myclass.Companion.foo(){ 给Myclass的伴生对象扩展了一个函数
 *
 *          }
 *
 *          调用的时候：Myclass.foo()
 *
 * 6.扩展的作用域
 *      大多数时候我们在顶层定义扩展，即直接在包里：
 *       package foo.bar
 *       fun Bar.goo(){.....}
 *      要使用所定义包之外的一个扩展，我们需要在调用方导入它：
 *      package com.example.usage
 *      import foo.bar.goo  //导入所有名为：“goo”的扩展
 *      import foo.bar.*   //从foo.bar导入一切
 *      fun usage(baz:Baz){
 *          baz.goo()
 *      }
 *
 * 7.扩展声明为成员
 *      在一个类的内部为另一个类声明扩展，在扩展内部，有多个 隐式接收者--其中的对像成员可以无需通过限定符访问。
 *      扩展声明所在的类的实例称为 分发接收者， 扩展方法调用的接收者类型的实例为 扩展接收者
 *
 *      class D{
 *          fun bar(){.....}
 *      }
 *
 *      class C{  【c的实例就是分发接收者】
 *          fun baz(){.....}
 *          fun D.foo(){
 *              bar() //调用D.bar
 *              baz() //凋用C.baz
 *          }
 *
 *          fun caller(d:D){ 【此处的d 为 扩展接收者】
 *              d.foo() //调用扩展函数
 *          }
 *      }
 *
 *      注意：对于分发接收者和扩展接收者的成员名字冲突的情况，扩展接收者优先。 要引用分发接收者的成员你可以使用 限定的this语法
 *      class C{
 *          fun D.foo(){
 *              toString()        //调用D.toString()
 *              this@C.toString() //调用C.toString()
 *          }
 *      }
 *
 *      声明为成员的扩展可以声明为 open 并在子类中覆盖。
 *      这意味着这些函数的分发 对于分发接收者类型是虚拟的，但对于扩展接收者类型是静态的。
 *      【这块有点绕】
 *
 * 8.动机
 */

//数据类:我们经常创建一些只保存数据的类。在这些类中，一些标准函数往往从 数据机械推导而来的。在kotlin中，这叫做 数据类 用关键字：data
/**
 * 1.数据类的声明
 * data class User(val name:String, val age:Int)
 * 编译器会自从主构造函数当中 推导出：
 *  1).equals()/hasCode()对
 *  2).toString()格式是“User(name=join, age=24)”
 *  3).componetN()函数 按声明顺序对应于所有属性
 *  4).copy() 函数(见下文)
 *
 * 如果以上这几个函数中的任何一个在类中显式定义或继承自其基类型，则不会生成该函数
 * 为了确宝生成的代码的一致性和有意义的行为，数据类必须满足以下要求：
 *   1) 主构造函数需要至少一个参数
 *   2) 主构造函数的参数需要标记为 val 或 var
 *   3) 数据类不能是抽象、开放、密封或内部的
 *   4)(在1.1之前)数据类只能实现接口 (1.1之后)数据类可以扩展其它类
 *   在 JVM 中，如果生成的类需要含有一个无参的构造函数，则所有的属性必须指定默认值
 *      data class User(val name: String = "", val age: Int = 0)
 * 2.复制 在很多情况下 我们需要复制一个对象改变它的一些属性，但其余部分保持不变。copy()函数就是为此而生。
 *      对于上面的User类 其 实现 会类似下在这样：
 *          fun copy(name:String=this.name, age:Int=this.age)=User(name,age)
 *      这让我们可以写：
 *          val jack = User(name="jack", age=1)
 *          val olderjack = jack.copy(age=2)
 * 3.数据类和解构声明
 *      为数据类生成Component 函数   使它们可以在【解构声明】中使用：
 *      val jane = User("Jane", 35)
 *      val (name, age) = jane
 *      println("$name, $age years of age")   // 输出 "Jane, 35 years of age"
 * 4.标准数据类  标准库提供了 Pair和Triple.
 *   尽管在很多情况下命名数据类是更好的设计选择，因为它们通过为属性提供有意义的名称使代码更具有可读性
 *
 */

//解构声明
/**
 *
 */

//密封类 密封类用来表示受限的类继承结构：当一个值为有限集中的  类型，而不能有其它类型时。
// 有点像枚举类型，某种意义上说 密封类型是 枚举类型的扩展，不同的是：每个枚举常量只存在一个实例，而密封类可以有 可包含状态的多个实例
/**
 * 1.密封类的声明 要在类关键字 class 前面用sealed关键字声明
 * 2.密封类可以有子类，但是子类必须在与密封类本身相同的文件中声明(1.1之后，在1.1之前更严格：子类必须嵌套在密封类声明的内部)，这个有点像C++的头文件
 * 3.扩展密封类子类 的类 的声明可以放在任何位置，而无需在同一个文件中。
 *
 *  sealed class Expr
 *  data class Const(val number: Double) : Expr() //密封类的子类的声明 必须 和 父类在同一个文件当中声明
 *  data class Sum(val e1: Expr, val e2: Expr) : Expr()  //密封类的子类的声明 必须 和 父类在同一个文件当中声明
 *  object NotANumber : Expr()  //密封类的子类的声明 必须 和 父类在同一个文件当中声明
 *
 *  fun eval(expr: Expr): Double = when (expr) {
 *      is Const -> expr.number
 *      is Sum -> eval(expr.e1) + eval(expr.e2)
 *      NotANumber -> Double.NaN  //此处不需要加else了
 *  }
 *
 *
 *
 *
 * 4.使用密封类的关键好处是： 使用 when 表达式 的时候，如果能够 验证语句覆盖了所有情况，就不需要为该语句再添加一个 else 子句了。
 *  fun eval(expr: Expr): Double = when(expr) {
 *       is Expr.Const -> expr.number
 *      is Expr.Sum -> eval(expr.e1) + eval(expr.e2)
 *      Expr.NotANumber -> Double.NaN
 *      // 不再需要 `else` 子句，因为我们已经覆盖了所有的情况
 *  }
 *
 *
 */


//嵌套类 内部类 匿名类
/**
 * 1.类可以嵌套在其它类中
 *      class Outer{
 *          private val bar:Int=1
 *          class Nested{
 *              fun foo()=2
 *          }
 *      }
 *
 *      val demo = Outer.Nested().foo()
 * 2.内部类  内部类标记为 inner 以便能够访问外部类的成员。内部类会带有一个对外部类的对对象的引用
 *      class Outer{
 *          private val bar:Int = 1
 *          inner class Inner{
 *              fun foo() = bar
 *          }
 *      }
 *
 *      val  demo = Outer().Inner().foo() //==1
 *      参见限定的 this 表达式以了解内部类中的 this 的消歧义用法。
 *      https://www.kotlincn.net/docs/reference/this-expressions.html
 * 3.匿名内部类  使用对象表达式创建匿名内部类实例
 *      window.addMouseListener(object:MouseAdapter(){
 *          override fun mouseClicked(e:MouseEvent){
 *
 *          }
 *
 *          override fun mouseEntered(e:MouseEvent){
 *
 *          }
 *      })
 * 如果对象是函数式 Java 接口（即具有单个抽象方法的 Java 接口）的实例， 你可以使用带接口类型前缀的lambda表达式创建它：
 * val listener = ActionListener { println("clicked") }
 *
 *
 */


//枚举类
/**
 * 1.枚举类的最基本的用法是实现类型安全的枚举
 *      enum class Direction{
 *          NOTRH,SOUTH,WEST,EAST
 *      }
 *      每个枚举常量都是一个对像。 枚举常量用逗号分开
 * 2.初始化
 *      每个枚举都是枚举的实例，所以他们可以是初始化过的
 *      enum class Color(val rgb:Int){
 *          RED(0XFF0000),
 *          GREEN(0X00FF00),
 *          BLUE(0X0000FF)
 *      }
 * 3.匿名类  枚举常量也可以声明自己的匿名类以及相应的方法、以及覆盖基类的方法。注意：如果枚举类定义任何成员，要使用分号将成员定义中的枚举
 * 常量定义分隔开，就像在java中一样
 *      emum class ProtocolState{
 *          WAITING{
 *              overridde fun signal() = TALKING
 *          },
 *          TALKING{
 *              override fun signal()=WAITING
 *          };
 *          abstract fun signal():ProtocolState
 *      }
 * 4.使用枚举常量
 *  就像在 Java 中一样，Kotlin 中的枚举类也有合成方法允许列出定义的枚举常量以及通过名称获取枚举常量。
 *  这些方法的签名如下（假设枚举类的名称是 EnumClass）：
 *   EnumClass.valueOf(value: String): EnumClass
 *   EnumClass.values(): Array<EnumClass>
 * 5.可以使用enumValues<T>() 和 enumValueOf<T>() 函数 以泛型方式访问枚举类中的常量(kotlin1.1之后的特性)
 *      enum class RGB {RED, GREEN, BLUE }
 *       inline fun <reified T:Enum<T>> printAllValues(){
 *          println( enumValues<T>().joinToString { it.name }  )
 *      }
 * 6.每个枚举常量都具有在枚举类声明中获取其名称和位置的属性：
 *   val name: String
 *   val ordinal: Int
 *
 *   枚举常量还实现了 Comparable 接口， 其中自然顺序是它们在枚举类中定义的顺序。
 *
 */


/*对像【对像表达式、对像声明、伴生对象、对象表达式和对象声明之间的语义差异】
 *有时候，我们需要创建一个对某个类做了轻微改动的类的对象，而不用为之显式声明新的子类。Java 用匿名内部类 处理这种情况。
 * Kotlin 用对象表达式和对象声明对这个概念稍微概括了下。
 */
/**
 * 1.对象表达式
 */




//委托
/**
 * 1.类委托  此模多具说是实现继承的一个很好的替代方式，而kotlin可以零样板代码地原生支持它。
 *      类Derived可以继承一个接口Base,并将其所有共有的方法委托给一个指定的对象
 *      例：
 *      interface Base{
 *          fun print()
 *      }
 *
 *      class BaseImpl(val x:Int):Base{
 *          override fun print(){ println(x) }
 *      }
 *
 *      class Derived(b:Base):Base by b
 *
 *      fun main(args:Array<String>){
 *          val b = BaseImpl(10)
 *          Derived(b).print()
 *      }
 *
 *      Derived中的 by子句表示 b将会在Derived中内部存储。并且编译器将生成转发给b的所有Base方法
 *      注意：覆盖会以你所期望的方式工作：编译器会使用你的override 实现取代委托对象中的实现。
 *      如果在Derived中添加 override fun print(){ println("abc") }  这样就不会输入10，而是输入abc了
 */

//委托属性
/**
 * 1.有一些常见的属性类型，虽然我们可以在每次需要的时候手动实现它们，但是如果能够为大家把他们只实现一次并放入一个库会更好，所以由此
 * kotlin支持了 委托属性：
 * class Example{
 *      var p:String by Delegate()
 * }
 * 基本语法是：val/var <属性名>:<类型> by <表达式>。
 * by后面的表达式是 委托， 该属性的对应的访问器getter/setter会被委托给它的 getValue()和setValue()方法。委托不需要实现任何接口
 * 但是必须要实现一个getValue函数(如果此是var属性的话还需要一个setValue() )
 *
 * class Delegate{
 *      operator fun getValue(thisRef:Any?, property:KProperty<*>:String){
 *          return ""
 *      }
 *
 *      operator fun setValue(thisRef:Any?, property:KProperty<*>:String, value:String){
 *
 *      }
 * }
 *
 *
 *
 */







//this表达式相关解释
/**
 *
 */


interface Factory<T> {
    fun create(): T
}

class Myclass {

    companion object : Factory<Myclass> {
        override fun create(): Myclass = Myclass()
    }


}

var instance = Myclass.create()




fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1]
    this[index1] = index2
    this[index2] = tmp
}

class Foo {

}

var Foo.bar
    get() = 1
    set(value) {
        this.bar = value
    }


interface MyInterface {

    val prop: Int   //抽象的属性
    val propertyWithImplementation: String  //实现了访问器的属性
        get() = "foo"

}


interface AA {
    fun foo() {
        print("A")
    }

    fun bar()
}

interface BB {
    fun foo() {
        print("B")
    }

    fun bar() {
        print("bar")
    }
}

class CC : AA {
    override fun bar() {
        print("bar")
    }
}

class D : AA, BB {
    override fun foo() {
        super<AA>.foo()
        super<BB>.foo()
    }

    override fun bar() {
        super<BB>.bar()
    }
}


open class Base {
    open fun f() {}
}

abstract class Derived : Base() {
    override abstract fun f()
}

class CB : Derived() {
    override fun f() {

    }
}


fun dfs(graph: Graph): Unit {

}


infix fun Int.test(x: Int): Int {
    return x * 3;
}

//可变数量的参数的函数
fun <T> asList(vararg ts: T): List<T> {
    val result = ArrayList<T>()
    for (t in ts) // ts is an Array
        result.add(t)
    return result
}


class Test private constructor() {

}

class Customer(name: String) {
    constructor(name: String, age: Int) : this(name) {
    }
}

fun copy(from: Array<out Any>, to: Array<Any>) {
    assert(from.size == to.size)
    for (i in from.indices)
        to[i] = from[i]
}





class Example{
    var p:String by Haha()
}

class Haha{
    operator fun getValue(thisRef:Any?, property:KProperty<*>):String{
        return "$thisRef, thank you for delegating '${property.name}' to me!"
    }

    operator fun setValue(thisRef: Any?,property: KProperty<*>, value:String){
        println("$value has been assigned to '${property.name} in $thisRef.'")
    }
}

fun nihao(){
    println("hahah")
}

//延迟属性Lazy
val lazyValue:String by lazy {
    nihao()
    "hello"
}



fun main(args: Array<String>) {


    println(lazyValue)
    println(lazyValue)
    println(lazyValue)

    val e = Example()
    e.p="hahahha"
    println(e.p)
//    printAllValues<RGB>()
    return

    val ints: Array<Int> = arrayOf(1, 2, 3)
    val any = Array<Any>(5) { index -> index * 2 }


    copy(ints, any) // 错误：期望 (Array<Any>, Array<Any>)
    println(any)
    for (x in any) {
        println(x)
    }
    return


    println(0 test 2)

}


//var wo:Char = '3';
//var arr:Array<String> = arrayOf("a", "b");
//var asc = Array(5,{i->i*i})
//var tt = Array<String>(5, {"a";"b";"c"})

var str = """
    for (c in test){
        println(c);
    }
""";


fun test(): Unit {

}

fun test1(x: Any): Unit {

}

fun test2(x: Any, y: Any): Unit {

}
