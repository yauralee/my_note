# Ruby中的Symbol
在 Ruby 中 Symbol 表示“名字”，比如字符串的名字，标识符的名字。
### 创建Symbol
     :foo
     :"foo"
     :+*=@
     :"hello ruby"
###  Symbol和String
![symbol1](https://github.com/yauralee/git-note/raw/master/ruby_note/ruby/symbol/picture/symbol1.png)
可以看出相同内容的字符串是不同对象，但一个名字唯一确定一个Symbol对象。创建Symbol对象时不能包含 ' \0 ' 字符。

* **Symbol 转化为 String：**     
 使用 to_s 或 id2name 方法将 Symbol 转化为一个 String 对象。每个 String 对象都是唯一的，因此对一个 Symbol 调用多次转换将产生多个 String 对象。
* **String 转化为 Symbol：**    
使用 to_sym 或 intern 方法将 String 转化为 Symbol ，如果该 Symbol 已经存在，则直接返回。
* **使用 Symbol：**    
Ruby 内部一直在使用 Symbol ，比如 Ruby 程序中的各种名字，Symbol本质上是 Ruby 符号表中的东西。使用 Symbol 处理名字可以降低 Ruby 内存消耗，提高执行速度。
使用 String 对内存开销大，因为每一个String 都是一个对象。    
通常来讲：    
如果使用字符串的内容，这个内容可能会变化，使用 String；   
如果使用固定的名字或者说是标识符，使用 Symbol；
### Ruby自动创建Symbol
除了可以采用一般的字符串，还可用变量，常量，方法甚至类的名字来创建Symbol 对象。实际上，在 Ruby 内部操作符、变量等名字本身就是作为Symbol 处理的，例如当你定义一个实例变量时， Ruby 会自动创建一个 Symbol 对象，如 @test 对应为 :@test 。
例如：

      class Test
         puts :Test.object_id
         Test = 10
         puts :Test.object_id

         def Test
            puts :Test.object_id
         end
         end

       Test.new.Test
运行结果：

       1109868
       1109868
       1109868
如果运行
       
       class Test
          puts :Test.object_id
          @@test = 10
          puts :@@test.object_id
          def test
            puts :test.object_id
            @test = 10
            puts :@test.object_id
          end
        end

        t =Test.new
        t.test 
则输出：

        1109868
        1110048
        196968
        1110108
可以看出第一个例子里，类名、常量名和方法名都是 Test ，因此相应的 Symbol 对象都是 :Test 。Ruby 可以很好区分它在不同上下文中到底表示什么。Symbol 表示一个名字，仅此而已。Symbol 对象一旦定义将一直存在，直到程序执行退出。