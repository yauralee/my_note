#Gemfile
Gemfile是一个用于描述gem间依赖的文件。gem是一堆ruby代码的集合，能够被我们所调用。Gemfile必须放在项目的根目录下， 这是Bundler的要求，对于任何形式的包管理文件来说这也是标准。当在Bundler上下文环境中被执行的时候能够使我们访问一些方法，我们用这些方法来解释gem之间的require关系。

### 创建Gemfile:
首先要告诉Gemfile去哪里找到gems,即gem的源。             
 **使用source找到gem源：**                   
`source “http://rubygems.org"`            
 并不推荐一个项目有多个源，绝大多数项目的源都会设置为`“http://rubygems.org”`。对于一个源，唯一要求是它必须是一个合法的Rubygems的repo. 
              
###源的优先级：         
我们在Gemfile顶部为主定义一个源的同时，也可以针对每个gem定义一个源。也可以为一个本地的gem定义一个路径或者为gem定义一个git路径。
当Bundler尝试定位一个gem时，会先查看这个gem有没有显式的设置源，如果有就使用这个源。如果在设置gem的时候使用了source, path, git依赖，那么Bundler会先在这些地方找，然后再去其他地方找。如果没有显式的设置，Bundler会依照Gemfile里定义的源的顺序去找。如果一个gem可以在多个源里被找到，将会得到一个warning来提示。          
 **使用#source作为一个block来调用：**

		source "https://my_awesome_source.com" do
		   gem "my_gem"
		   gem “my_other_gem”
		
		end

###带验证的源：     
有些源需要使用验证才能被设定。Bundler有一个设置选项使我们可以为每个源设置用户名和密码：

		bundle config my_gem_source.com my_username:my_password

 这是通过Bundler安装gem时必须要的，因为这些信息不会被放入版本管理中。也可以直接在Gemfile中设置验证信息，但是验证信息会被commit到版本管理中：
 
		 source "https://username:password@my_gem_source.com"
 我们在源里面的设置都会被以bundle config的方式设置的东西所覆盖。     
 
###设置Ruby信息：   
如果你的应用程序需要使用一个特别的Ruby版本或是引擎，我们都能够在Gemfile里面进行设置。

		ruby "1.9.3", :patchlevel => "247", :engine => "jruby", :engine_version => "1.6.7"
     
 当设定这个的时候，需要的唯一点信息就是ruby的版本          
 1.  :pathlevel 声明了Ruby的patch level            
 2. :engine 声明了使用的Ruby引擎           
 3. :engine_version 声明了引擎的版本 (如果这个被设置了，engine也需要被设置）              
###设置Gems：    
设置gems最基本的语法如下：        

		gem "my_gem"
这里my_gem是 gem的名字，gem的名字是唯一要求的参数，此外还有几个可以选择的参数可以使用。

###设置Gem的版本：
如果不设置版本就代表任意的版本都可以。

		gem "my_gem", ">= 0.0"
这里有7个操作符供你用来设置gem:

		  * = Equal To "=1.0"
		  * != Not Equal To "!=1.0"
		  * > Greater Than ">1.0"
		  * < Less Than "<1.0"
		  * >= Greater Than or Equal To ">=1.0"
		  * <= Less Than or Equal To "<=1.0"
		  * ~> Pessimistically Greater Than or Equal To "~>1.0"
**Pessimistically Greater Than or Equal To:**          
 ~> 操作表示使用这个gem未来的某个安全的版本。
 
		gem "my_gem", "~> 2.0"
这样能够允许安装任意的2.x版本的gem，但是3.x版本是不被允许的。也可以声明一个更具体的版本，如下:

		gem "my_gem", "~> 2.5.0"
这样能够使用2.5.0到2.6.0之间的版本。

		  * gem "my_gem", "~> 1.0" –> gem "my_gem", ">= 1.0", "< 2.0"
		  * gem "my_gem", "~> 1.5.0" –> gem "my_gem", ">= 1.5.0", "< 1.6.0"
		  * gem "my_gem", "~> 1.5.5" –> gem "my_gem", ">= 1.5.5", "< 1.6.0"
		



