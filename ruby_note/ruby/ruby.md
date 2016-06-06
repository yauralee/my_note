# Ruby Programming
## 第1部分
* rib命令：以交互式命令在控制台执行，不需要指定程序文件
* print()方法中输出字符串，若用双引号则转义输出所有特殊字符，若用单引号则除了斜杠 \ 和单引号转义之外，其他特殊字符原样输出。puts方法和print方法的区别是puts方法输出结尾自动换行；p方法将字符串带引号输出，数值结果和字符串结果区分形式输出，特殊字符不转义。 
* print方法可以使用
`print “表面积”，area, “\n”`的方式输出，也可以使用`print “表面积 = #{area}\n” ` 两种方法结果相同，第二种使用`#{…}`的写法，可以把area的值嵌入字符串中。
* ruby中的方法调用可以省略（）
* 魔法注释（magic comment）:在首行添加代码“#encoding:编码方式”。windows平台使用GBK，OS X和Unix使用UTF-8。从ruby2.0开始ruby默认采用UTF-8编码。
* 控制语句分为：顺序控制，条件控制，循环控制，异常控制

## 对象
* 像数组、散列这样保存对象的对象称为容器。
* 数组是保存多个对象的对象,可以保存任何对象。size方法返回大小。指定数组中不存在的索引会扩展数组。

        a = [1, 2]
        a[3] = 4
        a  #=> [1, 2, nil, 4]
* Hash以键值对形式存在，一般以字符串或符号作为键。
* **符号(symbol)：** 与字符串相似，符号也是对象，一般作为名称标签使用，用来表示方法等的对象的名称。符号和字符串之间可以通过to_s和to_sym方法转换。具体参考 [Symbol](http://daringfireball.net/projects/markdown/syntax).
*  **散列：** 创建散列的方法：    
      
         address = {:name => "zs", :postal => "123"}
         address = {name: "zs", postal: "123"}



## 对象、变量、常量
* ruby中表现数据的基本单位是对象
* **常用的对象包括：** 数值对象（Numeric）、字符串对象(String)、数组(Array)和散列对象(Hash)、正则表达式对象(Range)、时间对象()、文件对象(File)、符号对象(Symbol)、范围对象（Range）、异常对象（Exception）。类的对象即类实例（instance）。
* **四种类型变量：**   
  **局部变量**（local variable）：以英文字母或_开头   
  **全局变量**（global variable）:以$开头，在程序的任何地方都可以修改，不建议使用。    
  **实例变量**（instance variable）:以@开头   
  **类变量**(class variable):以@@开头   
  _伪变量：ruby中预先定义好的代表某特定值的特殊变量，如nil、true、false、self等。_
* **多重赋值：**只用一个表达式给多个变量赋值。如

        a, b, c = 1, 2, 3
        
        a, b, c ,d = 1, 2
        puts [a, b, c]  #=> [1, 2, nil]
        
        a, b, c, d = 1, 2, 3, 4
        puts [a, b, c]  #=> [1, 2, 3]
        
        a, b, *c = 1, 2, 3, 4, 5
        puts [a, b, c]  #=> [1, 2, [3, 4, 5]]
        
 使用多重赋值，可以直接置换变量值。
 
        a, b = 0, 1
        a, b = b, a
        puts [a, b]  #=> [1, 0]
* **命名：**对于多个单词组合命名用_连接或用驼峰命名法。一般变量名和方法名使用前者，类名和模块名使用后者。
        
## 条件判断
* 约定返回真假值的方法以？结尾。
* **if语句：**
  
        if 条件 
           处理
        elseif  条件 
           处理
        else  条件
           处理
        end
* **unless语句：**
       
        unless 条件
           处理1
        else
           处理2
        end
* **case语句：**
  
         case 比较对象
         when 值1 
            处理1
         when 值2
            处理2
         else
            处理3
         end
  when的值可以一次指定多个。可以是对象、类、正则，分别判断比较对象是不是和when值相等，或者属于when值的类，或者和when值正则匹配。
   
 判断比较对象和when值实际使用===运算符，当比较具体的对象是否相等时；===相当于==，当比较是否属于类或者正则匹配时，===相当于=~。
 
* **===**可以表达广义的相等
 
         puts (/zz/ === "xyzzy")   #=> true
         puts (String === "abc")   #=>true
         puts ((1..3) === 2)       #=>true
* **if修饰符 vs unless修饰符：**    
  if和unless可以写在希望执行的代码之后
  
         puts "a=b" if c>d
* **对象的同一性：**
使用object_id（或__id__）和equal?方法判断是否是同一个对象，使用==和eql?方法判断对象值相等。==和eql?在判断数值相等时，结果会不同。
   
          p 1.0 == 1   #=> true
          p 1.0.eql?(1)  #=>false
注意：Hash内部键的比较用eql?方法，所以有：
       
          hash = {0 => 0.0}
          p.hash[0]   #=>0.0
          p.hash[0.0]   =>nil
## 循环
ruby中使用循环语句或方法实现循环。    
循环方法： times   each    loop      
循环语句： for    while    until
* **for语句：**

          for 变量 in 开始值..结束值 do 
              处理
          end
          for 变量 in 对象 do
              处理
          end
  例如：
  
          for i in 2..5
              i += 1
          end
          for item in ["item1","item2","item3"]
              puts item
          end
* **while语句：**
         
          while 条件 do
              处理
          end
* **until语句：** 
  until语句与while语句结构相同，只是条件判断相反，当条件为假时执行循环处理。
* **times方法：**
当执行确定次数的处理时，使用times。

           循环次数.times do
                处理
           end
           循环次数.times {
                处理
           }
           循环次数.times do |i|
                处理
           end
 i是当前循环的次数，从0开始。
* **each方法：**
 each方法遍历集合中的对象。ruby中的for语句是用each方法实现的，可以使用each的对象同样可以使用for。
          
           对象.each do |变量|
                处理
           end
           对象.each {|变量|
                处理
           }
 例如：
               
            (2..5).each do |i|
              i += 1
            end
            ["item1","item2","item3"].each do |item|
              puts item
            end
* **loop方法：**
  loop没有终止条件，一直循环，可以使用break跳出。
  
            loop do
               p 123
            end
* **循环控制：**

 命令  | 用途
-----  | -------------
break | 终止程序，跳出循环
next  | 跳到下次循环
redo |在相同条件下重复刚才的处理
例如：
   
        puts "break例子:"
        i = 0
        ["ruby", "java", "perl"].each do |lang|
            i += 1
            if i == 2
               break
            end
            p [i,lang]
        end

        puts "next例子:"
        i = 0
        ["ruby", "java", "perl"].each do |lang|
             i += 1
             if i == 2
                next
             end
             p [i,lang]
        end

        puts "redo例子:"
        i = 0
        ["ruby", "java", "perl"].each do |lang|
            i += 1
            if i == 2
               redo
            end
            p [i,lang]
        end
 会输出：
 
	       break例子:
	       [1, "ruby"]
	       next例子:
	       [1, "ruby"]
	       [3, "perl"]
	       redo例子:
	       [1, "ruby"]
	       [3, "java"]
	       [4, "perl"]
redo与next不同在于，next直接进入下次循环，而redo会再执行一次相同循环。
* **do~end vs {~}**
块的两种写法。约定程序跨行写时用前者，写在一行时用后者。
## 方法
* ruby中的运算符、负号、指定数组散列元素下标的[]等实际都是方法。
* **方法的分类：**    
根据接收者不同，ruby方法分为3类：    
 **（1）实例方法**   
 以对象或实例为接收者。
 
		  p 1000.to_s
		  p [1,2,3].size
**（2）类方法**   
 以类为接收者,调用类方法时可以用：：代替.
 
         Array.new
         Time.now
 **（3）函数式方法**   
 省略接收者。    
  
         print "hello"
         sleep(10)   
* **方法的定义：**

         def hello(name)
            puts "hello, #{name}"
         end
  指定默认值给参数：
  
         def hello(name=“ruby”)
            puts "hello, #{name}"
         end
  方法有多个参数时，默认值从右边开始指定。
* **方法返回值：**
  使用return返回。省略return时默认返回方法的最后一个表达式的值。终止程序可以使用return。
* **定义带块的方法：**
使用yield定义带块方法，调用方法时通过块传进来的处理在yield地方执行。当yield带参数时，程序将其作为块变量传入块里。

         def myloop
		    while true
		      yield("ruby")
		    end
		  end
		
		  myloop do |i|
			  puts "hello,#{i}"
		  end
* **参数个数不确定的方法：**    
使用“*变量名”的形式定义参数不确定的方法，使ruby将参数封装为数组。

			def meth(arg, *args)
			   [arg, args]
			 end
			
			 p meth(1)
			 p meth(1,2,3)
			 #=>
			 [1, []]
             [1, [2, 3]]
 只确定第一个和最后一个参数时：
 
			 def meth(a, *b, c)
			   [a, b, c]
			 end
			
			 p meth(1, 2, 3, 4)
			 p meth(1, 2)
			 #=>
			 [1, [2, 3], 4]
			 [1, [], 2]
* **关键字参数：**     
使用关键字参数可以将参数名和参数值成对传递。每个参数使用“参数名：值”的形式。调用方法时也要以这种形式传参，所以可以改变传参顺序。将未定义的参数名传入时报错。
			
			 def area(x: 0, y: 0, z:0)
			   (x*y + y*z)
			 end
			
			 p area(z: 4, x: 2, y: 3)
			 p area(z: 4, x: 2)
			 p area(m: 5)  #=> ArgumentError
为避免传入未定义的参数而报错，可以使用“**变量名”的形式传入,未定义的参数以散列形式保存：

			def area(x: 0, y: 0, **args)
			   [x, y, args]
			 end
			
			 p area(z: 4, m: 5, x: 2, y: 3)
			 #=>
			 [2, 3, {:z=>4, :m=>5}]
普通参数和关键字参数搭配：

			 def area(x, y: 0)
			   [x, y]
			 end
			
			 p area(1, y: 3)
使用散列传参，会将与方法名相同的键对应的值传入：

			 def area(x: 0, y: 0)
			   [x, y]
			 end
			
			 arg = {:x => 2, :y => 3}
			 p area(arg)   #=> [2, 3]
			 arg2 = {:x => 2}
			 p area(arg2)  #=> [2, 0]
			 arg3 = {:x => 2, :y => 3, :z => 4}
			 p area(arg3)  #=>ArgumentError
* **把数组分解为参数：**    
以“*数组”的方式传参，数组中的各元素按顺序传给方法。数组的元素个数必须和方法参数个数一样。

			 def area(a, b, c)
			   a + b + c
			 end
			
			 arg = [1, 2, 3]
			 p area(*arg)
			 arg2 = [2, 3]
			 p area(1, *arg2)
* **把散列作为参数传入：**
用{~}形式表示散列字面量，将散列字面量传入方法时可以省略{}。

			 def area(arg)
			   arg
			 end
			
			 p area({"a"=>1, "b"=>2})
			 p area("a"=>1, "b"=>2)
			 p area(a: 1, b: 2)
			 p area(:a=>1, :b=>2)
			 
			 #=>
			 {"a"=>1, "b"=>2}
             {"a"=>1, "b"=>2}
             {:a=>1, :b=>2}
             {:a=>1, :b=>2}
有多个参数时，只将散列作为最后一个参数传入。

			 def area(arg1, arg2)
			   [arg1, arg2]
			 end
			
			 p area(100, {"a"=>1, "b"=>2})
			 p area(100, "a"=>1, "b"=>2)
			 p area(100, a: 1, b: 2)
			 p area({a: 1, b: 2}, 100)
             p area({a: 1}, 100）
             
			 #=>						 
			[100, {"a"=>1, "b"=>2}]
			[100, {"a"=>1, "b"=>2}]
			[100, {:a=>1, :b=>2}]
			[{:a=>1, :b=>2}, 100]
            [{:a=>1}, 100]
传入  ` p area(a: 1, 100)`时提示错误。
## 类和模块
* **类和实例：**   
Ruby中的对象都一定属于某个类。使用类的new方法生成对象。   
对象.class  #=>  对象属于的类     
对象.instance_of(类)?   #=>对象是否属于类
* **继承：**
通过扩展已定义的类来创建新类。通过继承可以实现：
（1）在不影响原有功能的前提下追加新功能     
（2）重定义原有功能，使名称相同的方法产生不同效果
（3）在已有功能的基础上追加处理，扩展已有功能。
* **类名首字母大写**
* **initialize方法：**    
  使用new方法生成新的对象时，会调用initialize方法，同时new的参数传给initialize，初始化对象时需要处理的一般写在initialize中。
* **实例变量与实例方法：**
  
        def initialize(myname = "ruby")
            @name = myname
        end
  通过@name = myname这行程序，作为参数传进来的对象会被赋值给变量@name。@name是实例变量。程序中引用未初始化的实例变量时返回nil。      
  不同实例的实例变量值可以不同，只要实例存在，实例变量就不会消失，可以被任意使用。而局部变量则是在调用方法是被创建，只能在方法内使用。可以在实例方法中引用实例变量。
  
	    class HelloWorld
	        def initialize(myname = "ruby")
	            @name = myname
	        end
	        def hello
	            puts "hello, #{@name}"
	        end
	    end
  
* **存取器：**    
ruby中，从对象外部不能直接访问实例变量，需要借助方法访问。

			class HelloWorld
			  def initialize(myname)
			   @name = myname
			  end
			  def name
			   @name
			  end
			  def name=(value)
			   @name = value
			  end
			end
			
			test = HelloWorld.new("Bob")
			puts test.name
			puts test.name=("Jack")
			
			#=>
			Bob
            Jack   
            
 其中”name“方法只是简单返回实例变量@name的值；而`test.name=("Jack")`是在调用“name=”方法，这种方法可以实现从外部访问实例变量。              
 如果有多个实例变量，分别定义存取器不方便，可以使用`attr_reader`,`attr_writer`,`attr_accessor`方法，只需要指定实例变量名的符号，Ruby会自动定义相应的存取器。   
 
 定义  | 意义
-----  | -------------
attr_reader :name | 只读（定义name方法）
attr_writer :name  | 只写（定义name=方法）
attr_accessor :name |读写（定义name和name=方法）
Ruby中把设定实例变量的方法称为writer,读取实例变量的方法称为reader,两者合称为accessor。
* **特殊变量self:**
在实例方法中，可以用self来引用方法的接收者。

			class HelloWorld
			  attr_accessor :name
			  def great
			   puts "hi,#{self.name}"
			  end
			end
great方法中，引用了self作为name方法的接收者。如果省略self，Ruby会默认self接收。             
**注意:在方法内部调用`name=`方法时，必须加上self,否则视为为局部变量赋值。**		

			def test_name
			  name = "Ruby"     #为局部变量赋值
			  self.name = "Ruby"  #调用name=方法
			end
_备注：self本身与局部变量形式相同，但是是引用对象本身时的保留字，所以即便对其赋值也不会影响。类似这种被系统使用且不能被我们自定义的变量名还有nil, true, false等_
* **类方法：**                
方法的接收者是类本身的方法称为类方法。                  
定义类方法有四种方法：              
（1）在class << 类名 ~ end 这种特殊的类定义中，以实例方法的形式：

			class << HelloWorld
			   def hello(name)
			     puts "#{name} said hello."
			   end
			end
			HelloWorld.hello("John")
（2）在class上下文中使用self时，引用的对象是类本身，因此可以在class上下文中使用class << self ~ end这种形式定义：

			class HelloWorld
			   calss << self
			      def hello(name)
			         puts "#{name}."
			      end
			   end
			end
(3)以def 类名.方法名 ~ end的形式：
 
			 def HelloWorld.hello(name)
			    puts "#{name}"	
			 end
			 HelloWorld.hello("John")	
(4)以def 类名.self ~ end的形式：

			class HelloWorld
			   def self.hello(name)
			      puts "#{name}"
			   end
			end	
* **常量：**					 	
在class上下中定义：

			class HelloWorld
			   Version = "1.0"
			end
在类中定义的常量，可以使用`::`，通过类名来实现内部访问。

			p HelloWorld::Version  		
* **类变量：**				
以@@开头的变量是类变量。为该类的所有实例共享，可以多次修改值。    
与实例变量一样，从类的外部访问时需要存取器，但是不能使用`attr_accessor`这种存取器，需要直接定义。

		class HelloCount
		   @@count = 0      #定义类变量
		   
		   def HelloCount.count   #读取类变量的类方法
		      @@count       
		   end
		   
		   def initialize(myname = "ruby")
		      @name = myname        #实例变量
		   end
		   
		   def hello                #实例方法
		      @@count += 1
		   end
		end
		
		bob = HelloCount.new("bob")
		alice = HelloCount.new("alice")
		ruby = HelloCount.new
		
		p HelloCount.count   #=>0   #通过调用类方法访问类变量
		bob.hello
		alice.hello
		ruby.hello
		p HelloCount.count   #=>3
* **限制方法的调用：**		
Ruby提供了3中方法的访问级别：           
（1）public 以实例方法的形式向外部公开该方法
（2）private 在指定接收者的情况下不能调用该方法（只能使用缺省接收者的方式调用，因此无法从实例的外部访问）
（3）protected 在同一个类中时可以将该方法作为实例方法调用

			class AccTest
			  def pub
			    puts "pub is a public method"
			  end
			  public :pub    #把pub设为public
			
			  def priv
			    puts "priv is a private method"
			  end
			  private :priv  #把priv设为private
			
			  def invokePriv
			    priv         #以缺省的形式调用private
			  end
			end
			
			acc = AccTest.new
			acc.pub           #pub is a public method
			acc.priv          #NoMethodError
			acc.invokePriv    #priv is a private method
			
希望统一定义多个方法的访问级别时，可以：

			class AccTest
			  
			  public  #不指定参数时,以下方法都定义为public
			  def pub
			    puts "public method"
			  end
			  
			  private
			  def priv
			    puts "private method"
			  end
			  
			end
没有指定访问级别的默认为public,但initialize方法例外，通常是  private的。    
定义protected方法，在同一个类或其子类中可以作为实例方法使用，除此之外无法使用。            
下面例子中实例变量`x=`和`y=`方法被定义成protected的，所以不能在外部修改x,y的值，但是可以从类的内部更改。

			class Point
			  attr_accessor :x, :y   #存取器
			  protected :x=, :y=     # x= y=方法设为protected
			
			  def initialize(x=0, y=0)
			    @x, @y = x, y
			  end
			
			  def swap(other)
			    tmpx, tmpy = @x, @y
			    @x, @y = other.x, other.y
			    #在同一个类中可以调用x= y=
			    other.x, other.y = tmpx, tmpy 	    
			    return self
			  end
			end
			
			p0 = Point.new
			p1 = Point.new(1, 2)
			p [p0.x, p0.y]
			p [p1.x, p1.y]
			
			p0.swap(p1)
			p [p0.x, p0.y]
			p [p1.x, p1.y]
			
			P0.X = 10   
			
			#=>
			[0, 0]
		    [1, 2]
		    [1, 2]
		    [0, 0]
		    NoMethodError
* **继承：**         
利用继承可以在不对已有类进行修改的前提下，通过增加新功能或重定义已有功能来创建新的类。      

		class 类名 < 父类名
		  类定义
		end
下面程序通过super关键字调用父类中同名的方法：
		
		class RingArray < Array
		  def [](i)    #重定义运算符[]
		    idx = i % size
		    super(idx)
		  end
		end
		
		wday = RingArray["日","月","火","水","木","金","土"]
		p wday[6]   #=>"土"
		p wday[11]  #=>"木"
* **Object和BasicObject**          
定义类时若没有指定父类，则默认父类为Object类。Object类提供了许多便于编程的方法，但是某些情况希望使用更轻量级的类，就是BasicObject类。BasicObject类只提供了组成Ruby对象所需的最低限度的方法。类对象调用instance_method方法后，会以符号的形式返回该类的实例方法列表。定义BasicObject的子类时需要明确指定父类。
* **alias:**		          
使用alias方法给已经存在的方法设置别名。alias方法的参数为方法名挥着符号名。

		alias  别名  原名  #直接使用方法名
		alias  ：别名  ：原名  #使用符号名
在重定义已经存在的方法时，可以重新定义原来的方法，而使用alias给原方法设置别名。

			class C1
			  def hello
			    "hello"
			  end
			end
			
			class C2 < C1
			  alias old_hello hello  #给原方法设定别名
			  def hello
			    "#{old_hello}, again"
			  end
			end
			
			
			obj = C2.new
			p obj.old_hello
			p obj.hello
			
			#=>
			"hello"
			"hello, again"
* **undef:**        
undef用于删除已有方法。参数可以指定方法名或符号名。

			undef  方法名    #直接使用方法名
			undef  ：方法名   #使用符号名
例如在子类中想要删除父类中的方法，就可以使用undef。
* **单例类：**         
Ruby中所有的都是Class类的实例，对Class类添加实例方法时，就等于给所有的类都添加了该类方法。所以只希望给某个实例添加方法时，需要使用单例方法。

			str1 = "Ruby"
			str2 = "Ruby"
			
			class << str1
			  def hello
			    "Hello, #{self}"
			  end
			end
			
			p str1.hello
			p str2.hello
			
			#=>
			"Hello, Ruby"
			NoMethodError
* **模块：**						
模块是Ruby的特色之一。如果说类表现事物的实体（数据）及其行为（处理），那么模块表现的只是事物的行为部分。           
模块与类有两点不同：     
（1）模块不能拥有实例           
（2）模块不能被继承
* **模块的使用方法：**       
**（1）提供命名空间**        
 命名空间是对方法、常量、类等名称进行区分及管理的单位。模块拥有各自独立的命名空间。使用“模块名.方法名”的形式调用模块中定义的方法，这样的方法称为**“模块函数”**。           
 如果没有定义与模块内的方法、常量等同名的名称，那么引用时就可以省略模块名。通过include可以把模块内的方法名、常量名合并到当前的命名空间。
 
			include Math
			p PI
			p sqrt(2)
* **利用Mix-in扩展功能：**			
Mix-in就是将模块混合到类中。在定义类时使用include，模块里的方法、常量就能被类所用。Mix-in可以灵活解决下面问题：    
（1）虽然两个类拥有相似功能，但不希望把他们作为相同的种类      
（2）Ruby不支持父类的多重继承，因此无法对已经继承的类添加共通的功能          

			module MyMethod
			  #共通的方法等
			end
			
			calss MyClass1
			  include  MyMethod
			  #独有方法等
			end
			
			class MyMethod2
			  incluede MyMethod
			  #独有方法等
			end
* **创建模块：**			
			module 模块名
			  模块定义
			end
例如：
			
			module HelloModule
			  Version = "1.0"
			  def hello(name)
			    puts "Hello,#{name}"
			  end
			
			  module_function :hello   #指定为模块函数
			end
			
			p HelloModule::Version
			HelloModule.hello("alice")
			
			#=>
			"1.0"
			Hello,alice
* **模块中的常量：**         
模块中的常量可以通过模块名访问。

			p HelloModule::Version
* **模块中方法的定义：**          
如果仅仅定义了方法，虽然在模块内部和包含模块的上下文中可以直接调用，但是不能以“模块名.方法名”的形式调用。需要使用module_function方法将方法作为模块函数公开给外部使用。 module_function的参数是表示方法名的符号。

			def hello(name)
			   puts "hello, #{name}"
			end
			
			module_function :hello
以“模块名.方法名”的形式调用时，如果在方法中调用self，会获得该模块本身。
			module FooModule
			  def foo
			    p self 
			  end
			  module_function :foo
			end
			
			FooModule.foo 		
			
			#=>
			FooModule
如果类Mix-in了模块，就相当于为该类添加了实例方法。这时self代表的就是类的对象。
* **Mix-in:**	  

			 module M
				 def meth
				   "meth"
				 end
			 end
			 
			 class C
			   include M
			 end
            
通过include?方法可以知道类是否包含了某个模块。

			类名.include?(模块名) 
用ancestors方法和superclass方法可以调查类的继承关系。

		p C.ancestors   
		#=> [C, M, Object, Kernel, BasicObject]
		p C.superclass  
		#=> Object
_Kernel是Ruby内部的一个核心模块，Ruby程序运行所需的共通函数都在在此模块中。例如p方法。_			
通过使用Mix-in,可以既保持单一继承关系，又同时让多个类共享其他功能。
* **查找方法的规则：**            
（1）同继承关系一样，原类中已经定义了同名的方法时，优先使用该方法。     

（2）同一个类中包含多个模块时，优先使用最后一个包含的模块。
		
		module M1
		end
		
		module M2		
		end
		
		class C
		  include M1
		  include M2
		end
		
		p C.ancestors
		#=>
		[C, M2, M1, Object, Kernel, BasicObject]
(3)嵌套include时，查找顺序也是线性的。

		module M1
		end
		
		module M2
		end
		
		module M3
		  include M2
		end
		
		class C
		  include M1
		  include M3
		end
		
		p C.ancestors
		#=>
		[C, M3, M2, M1, Object, Kernel, BasicObject]
(4)相同的模块被包含两次以上时，第2次之后的会被省略。
* **extend方法：**		
使用Object#extend方法，可以说实现批量定义单例方法。

		module Edition
		  def edition(n)
		    "#{self}#{n}版"
		  end
		end
		
		str = "Ruby基础"
		str.extend(Edition)  #将模块Mix-in进对象
		p str.edition(4)
		#=>
		"Ruby基础4版"
**include可以突破继承的限制，通过模块扩展类的功能；     
  extend可以跨过类，直接通过模块扩展对象的功能。**
* **类与Mix-in:**  		
所有类都是Class类的对象，可以将类方法理解为：            
（1）Class类的实例方法        
（2）类对象的单例方法   
**使用extend可以为类追加类方法；        
使用include可以为类追加实例方法。**

			module ClassMethods
			  def cmethod
			    "class method"
			  end
			end
			
			module InstanceMethods
			  def imethod
			    "instance method"
			  end
			end
			
			class MyClass
			  extend ClassMethods
			  include InstanceMethods
			end
			
			p MyClass.cmethod
			p MyClass.new.imethod
			#=>
			"class method"
			"instance method"
## 错误处理与异常
程序执行中出现错误会发生异常。异常发生后，程序会暂停运行，并寻找是否有对应的异常处理程序，如果有则执行，如果没有则会显示异常信息并终止运行。       
异常处理的优点：          
程序不需要逐个确认处理结果，也能自动检查出程序错误。          
会同时报告发生错误的位置，便于排查错误。          
正常处理与错误处理的程序可以分开写，使程序便于阅读。

* **异常处理的写法：**     

			begin
			  可能会发生异常的处理
			rescue
			  发生异常时的处理
			end
在Ruby中，异常及其相关信息都是被当作对象来处理的。在rescue后指定变量名，可以获得异常对象。

          begin
			  可能会发生异常的处理
			rescue => 引用异常对象的变量
			  发生异常时的处理
			end
即使不指定变量，Ruby也会把异常对象赋值给变量：

			变量 |  意义
			----|----     
			$! | 最后发生的异常（异常对象）
			$@ |最后发生的异常的位置信息
异常对象的方法

			class| 异常的种类
			-------|-------
			message | 异常信息
			backtrace |异常发生的位置信息	
如果发生异常的方法中没有rescue处理，程序会逆向查找调用者中是否定义了异常处理。    
不捕捉异常时，如果有异常发生，程序会马上终止。
* **后处理：**						
不管是否发生异常都希望执行的处理，用ensure关键字来定义。     
			begin
			  可能发生异常的处理
			rescue => 变量
			  发生异常后的处理
			endure
			   不管是否异常都要处理
			end
* **重试：**			   
在rescue中使用retry后，begin以下的处理会再重做一遍。

			file = ARGV[0]
			begin
			  io = File.open(file)
			rescue
			  sleep 10
			  retry
			end
这段程序每隔10秒执行一次File.open，直到可以打开文件。
* **rescue修饰符：**		
	
		表达式1  rescue  表达式2
如果表达式1发生异常，表达式2的值会成为整体表达式的值。
* **异常处理语法补充：**		   
如果异常处理范围是整个方法体，则可以省略begin和end,直接写rescue和ensure的部分。

			def foo
			   方法体
			rescue => ex
			   异常处理
			ensure
			   后处理
			end
在类定义中也有rescue和ensure，如果在类定义中发生异常，则发生部分之后的方法的定义就不再执行，因此一般不在类定义中使用。
* **指定需要捕捉的异常：**      
当存在多个种类的异常，且需要对其进行分类处理时，用多个rescue来分开处理。

			begin 
			    可能发生异常的部分
			rescue Exception1, Exception2 => 变量
			   处理
			rescue Exception3 => 变量
			   处理
			rescue
			   对异常异常之外的异常处理
			end   
* **异常类：**		      	
所有的异常都是Exception类的子类。在rescue中指定的异常的种类实际是异常类的类名，如果rescue中不指定异常类，则程序默认捕捉StandardError类及其子类的异常。
* **主动抛出异常：**     
使用raise方法，可以使程序主动抛出异常。在基于自己判定的条件抛出异常，或者把刚捕捉的异常再次抛出并通知异常调用者等情况，会使用raise方法。       
raise方法有4种调用方式：        
 （1）raise message          
 抛出RuntimeError异常，并把字符串作为message设置给新生成的异常对象。               
 （2）raise 异常类       
 抛出指定的异常类。       
 （3）raise 异常类， message       
 抛出指定的异常，并把字符串作为message设置给异常对象。
 （4）raise      
 在rescue外抛出RuntimeError。在rescue中调用时，会再次抛出最后一次繁盛的异常（$!）.
 
## 块
 块是调用方法时，能与参数一起传递的多个处理的集合。接收块的方法会执行一定次数的块，执行次数由方法本身决定。把这样的方法调用称为“调用带块的方法”或“调用块”。
 
			 对象.方法名（参数列表）do |块变量|
			    处理
			 end
			 
			 对象.方法名（参数列表）{ |块变量|
			    处理
			 }
块的开头是块变量，块变量是在执行块的时候，从方法传进来的参数。不同的方法的块变量的个数不同。

* **块的使用方法：**			              
**（1）循环**        
使用块来实现循环。在接收块的方法中，实现了循环处理的方法称为迭代器。each方法就是一个迭代器。   
散列也能将元素逐个取出，但不同在于散列会取出[key,value]的组合作为数组来提取元素。         
**（2）隐藏常规处理**             
块还有别的用法，比如确保处理后被执行。

			File.open("sample.txt") do |file|
			   file.each_line do |line|
			      print line
			   end
			end
File对象读取数据部分与不使用块时一样，只是少了最后的close方法。但是即使遇到无法打开文件等错误也会正常关闭文件，因为块内部进行了处理：

			file = File.open("sample.txt")
			begin
			  file.each_line do |line|
			     print line
			  end
			ensure
			  file.close
			end		
* **定义带块的方法：**
传递块参数，获取块的值

			def block_args_test
			  yield()
			  yield(1)
			  yield(1,2,3)
			end
			
			block_args_test do |a|
			   p [a]
			end
			
			block_args_test do |a,b,c|
			   p [a,b,c]
			end
			
			block_args_test do |*a|
			   p [*a]
			end
         
          #=>
          [nil] [1] [1]
          [nil,nil,nil] [1,nil,nil] [1,2,3]
          [[]] [[1]] [1,2,3]
* **控制块的执行：**           
在块中使用break,next时，可以跳出块的执行。跳出时可以使用`break0`，`next 0`的方式返回某个值。           
使用break直接退出块的执行，使用next则程序中断当前处理，并执行下面的处理。
* **局部变量与块变量：**          
块内部的命名空间与块外部是共享的。在块外部定义的局部变量，在块中也可以继续使用，而被作为块变量使用的变量，即使与块外部的变量同名，ruby也会认为他们是不同的变量。


			x = 1
			y = 1
			ary = [1, 2, 3]
			ary.each do |x|
			  y = x
			end
			
			p [x, y]
			
			#=>
			[1,3]
在ary.each方法的块中，x的值被赋值给了局部变量y,因此y保留了最后一次调用块时块变量x的值3.但是变量x的值在调用ary.each前后并没有发生改变。          
在块内部定义的变量不能被外部访问，去掉第2行的代码，程序会报错。
			


			


      
 

	



		


 
    
			            
          

