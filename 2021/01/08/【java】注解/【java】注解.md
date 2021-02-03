# 【java】About 注解

## 什么是注解？

   我们学习注解的第一步，首先就是先从最基本的开始，看看注解到底是什么？

   > 注解和反射是Java中非常让人容易忽略的东西，但却很重要，在主流的Spring中更是充满了注解，注解和注释很像，两者其实本质就差不多，注释是给我们程序员看的，而注解呢其实就是给程序看的(关于反射，下一篇咱就开讲)

   上面所说希望你着重注意以下两点：

   1、注解和注释很像
   2、注释是给我们程序员看的，而注解呢其实就是给程序看的

   我们初步理解注解就从上面两点开始，我们先看注释，比如这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2U5YWQ1MDJkZTVmNjZmYjhlYmRkNzgxN2E4M2NmZWQ4LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_e9ad502de5f66fb8ebdd7817a83cfed8.jpg)

   这就是一个注释，那么注释有什么用呢？简单来说就是对相关的类或者方法加以说明，比如这里的Test类，上面的注释大致告诉我们这类是谁编写的，做什么的以及何时编写的这些信息，当然，信息其实还可以有更多。

   所以，你要明白，注释是干嘛的，是给我们这些程序员看的，看到注释我们就明白了，哦，这个类原来是这样的……

   注释是给程序员看的，那么注解呢？相差一个字，注解是给程序看的，先记住即可。

   ### 进一步理解注解

   上面我们说了，注解和注释是很像的，注释是给我们人看的，注解就是给程序看的，前面的好理解，这个注解是给程序看的，你或许还有一点懵，我进一步解释下。

   首先，直观感觉下什么是注解，比如我们在代码中写的这个：

   ```java
   /**
    * @Description 用户类
    * @Author ithuangqing
    * @Date 2020-07-31 15:33
    **/
   @Repository
   public class UserBean {
       private String name;
       private int age;
   }
   12345678910
   ```

   这里的@Repository就是一个注解，看这段代码，上面还有注释，我们看到注释，发现都看得明白，但是看到@Repository之后，就不那么明白，这是啥，有啥用？

   于是我们查，大概知道，哦，这是个注解，有了这个注解，UserBean就会被装载进Spring容器中，我们可以知道这些信息，但是，它实际上做了哪些事情，是如何起作用，也就是如何把UserBean交给Spring去处理的，这个内部实现，我们不清楚。

   但是，我们虽然不清楚，有个东西它清楚，什么呢？就是一个特定的程序，也就是说，有一个专门的程序，当它看到这个UserBean上面有一个@Repository之后，这个程序就知道了，原来要把这个UserBean装载进Spring容器中，于是这个程序员就开始执行一系列的操作区把这个UserBean装载进Spring容器中。

   所以，你到此应该明白：

   > 注释是给人看到的，注解是给程序看的。

   我们再进一步总结下什么是注解：

   > 在程序中，可以把注解看成一种特殊的标记，一般是用来标记类，方法或者接口等，这些标记有一些特点，比如可以在编译的时候，（javac命令把java源文件编译成字节码文件class），类加载和运行的时候（使用java命令执行字节码文件的时候，类的生命周期开始，从加载到卸载）被读取到（一般是有专门的程序去读区这些注解，利用反射技术去解析注解，然后根据得到的信息做相应的处理）

   是的，关于注解，你要知道这么一个知识点了：

   > 对于注解，是有专门的程序去读取它，解析它，然后根据得到的消息去执行相应的操作。

   关于这个程序，要看具体的场景，也就是说这个程序是不同的，那么关于这个程序怎么知道读到哪个注解该干嘛，这个还是依靠注解本身的定义，比如@Repository注解被定义成是把被注解的装载进Spring容器中，那么特有的程序获取到这个注解就知道该干什么事了。

   到此，你应该知道什么是注解了，当然，是概念上的一些东西，另外，对注解是怎么起作用的，你也应该有点内味了……

   ### 注解的简单分类

   这个知识点很是轻松愉快，不需要你失去多少脑细胞。

   注解是有分类的，一般有三种类型的注解：

   1. 自定义注解（实际很少）
   2. JDK内置注解（@Override检验方法重写）
   3. 框架中的注解

   不知道这个能不能理解，就是说，对于注解而言，是有几种不同分类的，首先，我们可以自己写一个注解出来（下面会讲），另外对于JDK本身而言有自己的的注解，我们看个代码，你就知道了：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzA0NjhlZjM4MTY4NjFlMjUzZTliOGI5MzE3ZTMxMjU0LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_0468ef3816861e253e9b8b9317e31254.jpg)

   比如这个，是重写toString方法，上面就有个JDK的内置注解@Override，这个注解就起到一个检验的作用，因为它是Object的方法，你现在要重写它，那么名字啊，参数啊要和之前的一样，不一样，就给你报错，不信你试试：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2E4YWYwOTM0NzdjNmE0MjU0MGU3MDZlZTJkMWViZGM1LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_a8af093477c6a42540e706ee2d1ebdc5.jpg)

   这个是关于JDK的内置注解，那么最后一个关于框架的注解，我想你只要学过Spring都知道，比如@Controller，熟悉吧，这就是框架中的注解。

   ## 注解的本质

   经过上面的讲解，我们应该大致了解了什么是注解，以及注解的一些分类，现在，我们对于概念上的注解算是清楚了，但是这个注解本质是个什么呢？

   告诉你吧，注解的本质是个接口，为啥，先来看下，如何定义一个注解（下面会详细讲解）

   ```java
   public @interface Main {
   }
   12
   ```

   就这些，就定义了一个注解，不知道你发现了没，这个和接口很像啊，有啥区别，就是多了一个@，不然就是接口啊，接下来我们使用XJad把这个注解反编译一下看看：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzFiODdmNDM3OTQxMjhlMTQ4YWQzMzc2ZDg2YjFlZGY2LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_1b87f43794128e148ad3376d86b1edf6.jpg)

   看到没，这里的Main直接就是interface定义，然后还继承了Annotation，这个足以说明，注解其实就是接口啊。

   这个暂且聊到这，记住即可！

   ## 如何定义注解

   接下来我们就来聊聊如何去自定义一个注解，我们在上面说过，注解的本质其实就是接口，上面也简单演示了一个注解的定义，如下：

   ```java
   public @interface Main {
   }
   12
   ```

   想一下，我们平常怎么定义一个接口，是不是使用关键字interface，那么类呢？是不是使用class关键字，也就是说啊，定义这些一般都是需要一个关键字来加以声明的，显而易见，定义注解的关键字就是@interface，它和接口的定义就是多了一个@，但是注解的定义却不仅仅是如此！

   ### 元注解

   这里要引入一个元注解的概念，我们先来想一下，注解我们上面说了，一般可以用来标记类，接口或者方法等，那么这里就有一个问题了，比如我定义了这么一个Main注解：

   ```java
   public @interface Main {
   }
   12
   ```

   那么，我这个注解是不是可以用在类上，也可以用在接口或者方法上？一般类呀，接口啊，方法啊等等它们还是有点差别的，所以对于这些最好有区分，也就是说，有些注解只能标记类，有些注解只能标记方法等，这样一来就需要对注解的作用域去进行限制。

   那么这个该怎么搞，答案就是元注解，那什么是元注解呢？

   > 元注解就是标记注解的注解

   啥意思，来看下，比如我们定义的这个Main注解，我们规定它只能用来标记方法，那么可以这样做：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzkyZTY3N2JhNjYwMDUzMDdhYzUzYzlkZGUyZmI4MWVjLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_92e677ba66005307ac53c9dde2fb81ec.jpg)

   我们在上面加了一个注解@Target，后面还有参数（下面会讲），这个参数
   ElementType.METHOD就代表我们这个注解是用于注解方法的，来，试一下：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzMyNzIyYWFlYzExODY0ODk3NGQxNDA4NWNmY2ZmZmE3LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_32722aaec118648974d14085cfcfffa7.jpg)

   你看，可以用在我们的main方法上，那么是不是不能用于类呢？我们试下：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2M2ZjBhZjg3NmNlMTc4NmRlOWU2ZDJiZTk1N2Y3MWE2LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_c6f0af876ce1786de9e6d2be957f71a6.jpg)

   报错了，看来是不行，所以这个@Target就是一个元注解，可以用来注解注解，也就是标记注解的注解。

   关于元注解，一般有以下主要的几个：

   1. @Documented 用于制作文档
   2. @Target 指定注解的使用位置，不指定的话任何位置都可以使用
   3. @Retention（注解的保留策略）

   这里单独提一下最后一个也就是声明注解的保留策略@Retention，这个是什么意思呢？

   这个保留策略啊，简单来讲就是说你这个注解可以在哪个时间段起作用，这个就得说说我们的代码从写出来，然后编译到执行的主要三个阶段了，画个图就是这样的：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzJkZTU4OWNmMGVlZmM5MDQyMmQwYmUyN2MxOTkzZTdlLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_2de589cf0eefc90422d0be27c1993e7e.jpg)

   这个我已经画的很清楚了吧，一般来说，我们的注解都是要保留到运行期间的，所以一般就是这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzY2OGYxNzNlYjRiMmM0Y2RhNDQ3ZGY0MzI0MzU1ZjExLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_668f173eb4b2c4cda447df4324355f11.jpg)

   当然，具体情况具体对待。

   到这里你可能发现，这个注解里面可以有参数？当然是可以的，我这里简单演示下，下面讲到注解的语法的时候你就知道了：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzU1ZTdlZGE4OTU0NWJmMDU0NTFlMzQ3ZjkyZjdiZWMxLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_55e7eda89545bf05451e347f92f7bec1.jpg)

   然后再看下使用：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzE0NDEwMzE3ZGU0Mzk1ZjE4MWRkMmQxYWY2ZTY3OGNjLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_14410317de4395f181dd2d1af6e678cc.jpg)

   其实还是蛮简单的！

   ## 注解的基本使用语法

   接下来我们就来看看注解的语法吧，就是注解具体是如何使用的。

   对于注解，我们知道了如何去定义它，比如简单定义一个注解：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzAwN2Y3M2U0ZDNkNzU5M2U5MDRkMGM1MjY3YTRkMWYzLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_007f73e4d3d7593e904d0c5267a4d1f3.jpg)

   这很简单，我们继续去看，对于注解还可以定义属性：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzU2NjM1OTRkMThjYzBjZmNmNTU2Mjc0N2U2NmNjMGQ2LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_5663594d18cc0cfcf5562747e66cc0d6.jpg)

   虽然这个属性看起来很像方法，但是人家就是属性，注解还是比较特殊的，那么现在我们来使用下这个注解：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzI1Y2Y4ZWQ3OGU4OTNiNzIxNGQzZTI2ZjM1MTQyZTY0LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_25cf8ed78e893b7214d3e26f35142e64.jpg)

   这个时候它会报错，告诉我们需要一个value值，其实也好理解，你的注解定义中定义的有一个value属性，那么你在使用的时候就需要把这个属性值给用上，那你说我可不可以不用，可以的，那定义注解属性的时候就需要给属性添加默认值，就是这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2M0YjQxMjcyYWYxMWY0YTk4NWJmOTFkY2VkNDNlNTAxLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_c4b41272af11f4a985bf91dced43e501.jpg)

   可以设置成一个空字符串也可以设置成具体的值。除此之外我们还可以设置多个属性值，像这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzZjNmEzNDVkOThkNzk5ZTYzYTA0MmQ4ZjhiMDk3YWMxLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_6c6a345d98d799e63a042d8f8b097ac1.jpg)

   这里就有知识点了，如果你在使用的时候只是给一个属性值赋值，那么在使用的时候可以这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2U4YWQwMzg2YjQxNzllNTFjNDJjYzNkOGNjNWU3MzRiLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_e8ad0386b4179e51c42cc3d8cc5e734b.jpg)

   那有人可能疑问，我这个hello对应的是value还是name啊，默认对应的都是value，所以这个要牢记。

   但是给多个属性值赋值的时候就必须指明具体的属性名称了，就是这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzBjYTQ0ZjU1MWM2NGFjMjQxMDRjYzI4MmRmYWFjMWY2LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_0ca44f551c64ac24104cc282dfaac1f6.jpg)

   > PS：通过上面的介绍我们会发现注解一个比较奇怪的地方，就是对于注解而言，我们可以定义属性，但是注解的属性长得真的像方法，但是在注解里面，它就是属性，就可以直接赋值，这里需要注意下！

   ### 属性的类型

   上面简单介绍了注解的属性，那么这些属性都是可以取哪些类型值呢？大致有如下这么多：

   1. 基本数据类型
   2. String
   3. 枚举
   4. Class
   5. 注解类型
   6. 数组（以上类型的一维数组）

   关于数组的看个例子，比如这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzYyMWZlYmU4MTNjZjYwNDdkZWMwZmRmOThlYTdkY2ZjLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_621febe813cf6047dec0fdf98ea7dcfc.jpg)

   使用的时候也是同样的道理：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzI5ZmFlOWFmODA2NWU2MWRlMWNkNTM4YmY4NTAxMDIyLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_29fae9af8065e61de1cd538bf8501022.jpg)

   ## 如何真正的理解注解

   我们平常对于注解之所以忽视的原因在于，很多地方只需要我们去使用，比如这样：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2FiZDQ5OWRhY2NiMmVmMjMzMmQ3NDEyZTNkYTEwMDU1LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_abd499daccb2ef2332d7412e3da10055.jpg)

   至于注解是怎么定义的以及注解是怎么起作用的都不太了解，好像需要我们自定义注解的也都很少，所以不去系统化的学习注解的话，会忽略掉注解的很多东西，只会使用，也就是@XXX

   那么，从今天开始，我希望你能够记住，对于注解而言，它一定有如下三个流程：

   1. 定义注解
   2. 使用注解
   3. 读取并执行相应流程

   下面我们就以@Repository这个注解来看看这三个流程，首先是定义注解，这个我们可以在IDEA中按住Ctrl点进去@Repository来看，是这样的：

   ![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzQxODVlOTg2NGMxYzdmYzQxZmIxMTczZDY1MjZhOWRmLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_4185e9864c1c7fc41fb1173d6526a9df.jpg)

   这个就是@Repository注解的定义，接着我们看看@Repository的使用：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzQ4YTQ4YmY2YmNjOWY0NTgyMDYwMmIxNjcyNjllM2M5LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_48a48bf6bcc9f45820602b167269e3c9.jpg)

   然后就是对注解的读取了，怎么读取呢？很多人对这块是比较模糊的，这也是对注解理解最大的障碍所在。

   我们一般就是使用注解，对于注解的定义和读取这块一般都是框架什么的给我们搞定了，我们不看源码一般不知道是怎么回事的，也就不清楚注解到底是怎么运行起来的，简单的理解就是注解需要靠反射去读取，然后做相应的处理。

   但是我想你一定和我一样好奇，为啥加了个@Repository注解之后，这个UserBean就被装载进Sring容器中生成了一个bean呢？

   还记得我在最开始就一直在说的吗？注解是需要有专门的程序取读取的，然后根绝读取到的注解获取的信息去执行相应的操作。

   所以这里，在Spring源码中，一定有某个或者某些程序在做这个事情。

   ## 注解的读取（注解如何起作用）

   上面说了注解的定义何使用，在这里单独把注解的读取拿出来说下，因为这点事理解注解的重点，很多人觉得对注解不理解的一个原因就在于不清楚加了个注解之后到底干了啥？

   也就是注解到底是如何起作用的？搞明白这个，将对你理解注解有极大的帮助。

   ### 注解主要被反射读取

   对于注解的读取，一般就是通过反射技术来实现，这里就有知识点了，对于反射而言，它只能读取内存中的字节码信息，然后还记得之前我们说的注解的作用域@Target吗？

   它里面有几个主要的作用域，也就是这张图片，再来回顾下：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2FjYmZlY2EyNTBiNDc1ZjExZmMwMGE4ODIyZGQ2M2FiLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_acbfeca250b475f11fc00a8822dd63ab.jpg)

   对于RetentionPolicy.CLASS而言，这个就是指的字节码这一阶段，这个时候这个字节码文件是由Java源文件通过javac编译生成，这个时候class字节码文件其实还是在磁盘内，并没有进入内存中。

   而反射只能取读取内存中的字节码信息，所以注解的保留策略也就是这个@Target只能是RUNTIME，也即运行的时候仍然可以读取。

   ### 我的理解（精华）

   很多人对注解不理解，或者觉得很模糊的一个原因就是你让我定义一个注解，我也能按照基本的注解语法去定义一个注解，你说怎么使用注解我也知道在类，方法等上面使用 @+注解名称的方式，但是也就到此为主了，更进一步的理解就有点模糊了，比如：

   1. 为什么要这样用？
   2. 原理是什么，怎么起作用的？

   你想啊，我们就这样在类或者方法上面写了这么一个@+注解名称就行了？后续是怎么起作用的呢？这里你得首先清楚，注解有三大步骤：

   1. 定义注解
   2. 使用注解
   3. 读取注解（这块是大部分人缺少的，也是大部分人对注解不理解的关键所在）

   再理解下什么是注解，与注释一字之差，肯定有相似之处，两者都是提供额外信息的，好比备注，注释是给我们程序员看到，看到注释我们知道某个类是干啥的，有啥用，看到方法的注释，我们知道这个方法有什么作用需要什么参数以及参数的含义等等，那么注解嘞，注解其实是给程序看到，当程序读到注解，会从注解这里得到一些信息，知道该如何处理被该注解标记的类或方法等。

   好好理解上面的，我们下面再以Spring的一个例子来加以说明。

   对于Spring简单的大家都知道IOC吧，直白点就是不用你new对象，需要什么直接从Spring容器中获取，那么首先就需要把我们的bean注册到Spring容器中吧，这个一般有xml配置方式和注解方式，当然我们这里要说的是注解方式，也就是使用@+注解名称的形式，举个简单的例子，如下：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kX2Y3NTUxMDU5ZDA0MGM2NTI2YzEzNDY0YzE3NmYzYzY4LmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_f7551059d040c6526c13464c176f3c68.jpg)

   这个注解熟悉吧，它就是可以把我们的Person类注册到Spring容器中去，当然，这里就是在对这个注解的使用，我们点进去看看这个注解是怎么定义的：

   [![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5pdGh1YW5ncWluZy52aXAvd3AtY29udGVudC91cGxvYWRzLzIwMjAvMDcvd3BfZWRpdG9yX21kXzU3Y2Q0MmZmYjZkZjJmMTQzYmIzZTgxMjBhZGRhYTJkLmpwZw?x-oss-process=image/format,png)](http://www.ithuangqing.vip/wp-content/uploads/2020/07/wp_editor_md_57cd42ffb6df2f143bb3e8120addaa2d.jpg)

   这个定义我们应该已经熟悉了，对于@Component也是一个注解，它其实是最基础的把类注册到Spring容器中的注解，后来的像我们现在说的@Repositoy以及@Service和@Controller这些都是在@Component的基础上发而来。

   这里就需要注意了，其实这几个注解不管是哪个，都要清楚明白的一点就是，要它们啥用，之所以需要这些注解，就是希望在哪个类上使用这些注解，就自动把这个类注册到Spring容器中，这个要比我们写xml配置简单的多，我们就在一个类上写个@Repositoy，它就被注册到Spring容器中了？

   是不是很神奇，然后看下注解的定义，也很简单，没啥东西啊，怎么就自动注册到Spring容器中了呢？

   还记得之前说的注解三大步骤嘛？首先你需要定义一个注解，然后就是使用注解，那么注解是怎么起作用的就需要有程序去读注解，这个注解就好比一个标志，一个标签一样，比如这里的@Repositoy，当一个类被这个注解标志，那么当特有的程序去读到这个注解的时候，这个程序就知道，哦，原来是要把这类注册到Spring容器中啊，那么程序怎么知道要把这个类注册到Spring容器中呢？这就是 @Repositoy 告诉它的。另外我们知道注解一般可以设置一个value属性值，可以通过反射技术拿到之类的，那么在具体的将这个类注册到Spring容器的过程中可能就会用到这个value属性值，比如设置成bean的名字。

   我们一般使用了注解，在Spring配置文件中就需要配置注解的包扫描：

   ```java
   <context:component-scan base-package="com.ithuangqing.*"/>
   1
   ```

   这个其实就是在扫描，看看哪个类上使用到了@Repositoy这些注解，扫描到的就需要特殊处理将其注册到Spring容器。想一下，这里Spring其实就会对这个标签进行解析，核心代码：

   ```java
   registerBeanDefinitionParser("component-scan", new ComponentScanBeanDefinitionParser());
   1
   ```

   然后具体的处理流程就是在ComponentScanBeanDefinitionParser处理，代码如下：

   ```java
   @Override
   	public BeanDefinition parse(Element element, ParserContext parserContext) {
   		String basePackage = element.getAttribute(BASE_PACKAGE_ATTRIBUTE);
   		basePackage = parserContext.getReaderContext().getEnvironment().resolvePlaceholders(basePackage);
   		String[] basePackages = StringUtils.tokenizeToStringArray(basePackage,
   				ConfigurableApplicationContext.CONFIG_LOCATION_DELIMITERS);
   
   		// Actually scan for bean definitions and register them.
   		ClassPathBeanDefinitionScanner scanner = configureScanner(parserContext, element);    //得到扫描器
   		Set<BeanDefinitionHolder> beanDefinitions = scanner.doScan(basePackages);             //扫描文件，并转化为spring bean，并注册
   		registerComponents(parserContext.getReaderContext(), beanDefinitions, element);       //注册其他相关组件
   
   		return null;
   	}
   1234567891011121314
   ```

   上述代码的主要作用就是扫描base-package 下的文件，然后把它转换为Spring中的bean结构，接着将其注册到容器中……

   怎么样，是不是越来越看不懂代码？很正常，这里只需要大家记住，注解是会被特有的程序去读取，然后去做相关的处理的，而这个处理逻辑，一般就比较复杂了，尤其框架中。

   ### 获取注解的属性

   上面讲解的关于注解是如何起作用的是很重要的，一定要理解，下面我们聊聊注解使用的最后一步：特有的程序去读取注解。

   注解使用最终是需要依靠程序去读取注解，得到注解的一些信息，然后才判断接下来应该去做什么事情，那么接下来我们就要知道注解的属性值该如何获取。

   其实注解的属性，用到的技术就是反射，反射是一个很重要的知识点，以后会单独写文通俗易懂的去聊一聊的。

   接下来我们来看如何使用反射来获取注解的属性。，主要就是一下三个基本的方法：

   ```java
   /**是否存在对应 Annotation 对象*/
   public boolean isAnnotationPresent(Class<? extends Annotation> annotationClass) 
   {
       return GenericDeclaration.super.isAnnotationPresent(annotationClass);
   }
   
   /**获取 Annotation 对象*/
   public <A extends Annotation> A getAnnotation(Class<A> annotationClass) 
   {
       return (A) annotationData().annotations.get(annotationClass);
   }
   
   /**获取所有 Annotation 对象数组*/   
   public Annotation[] getAnnotations() 
   {
       return AnnotationParser.toArray(annotationData().annotations);
   }
   1234567891011121314151617
   ```

   然后接下来看一段简单的代码：演示利用注解获取注解属性

   ```java
   public class Test {
       public static void main(String[] args) throws Exception {
           Class<Test> testClass = Test.class;
           Method toGetString = testClass.getMethod("toGetString");
           //获取注解对象
           Main main = toGetString.getAnnotation(Main.class);
           System.out.println(main.value());
   
       }
   
       @Main("这是自定义注解的value值")
       public static String toGetString() {
           return "";
       }
   }
   123456789101112131415
   ```

   其实很简单，记住以上三个获取注解的方法，关于反射我们后面会详细聊聊。

   到现在基本知道了注解需要先定义出来，然后使用，那么怎么起作用，大概就是需要一个程序去专门利用反射技术去读取注解，得到注解里面的信息然后做相应的事情。

   ## 总结

   到这里，关于注解的讲解其实就差不多了，也许你看了也就忘了，也许你根本就没有看完，但是我希望记住一下内容：

   1. 定义注解
   2. 使用注解
   3. 读取注解