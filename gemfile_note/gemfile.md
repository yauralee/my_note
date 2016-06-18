#Gemfile
###RubyGems、Bundler、Gemfile
1. The RubyGems software allows you to easily download, install, and use ruby software packages on your system. The software package is called a “gem” and contains a package Ruby application or library.                  
2. Bundler 是管理Gem依赖的工具，执行bundle install时，会根据应用程序目录中Gemfile的设定，检查指定的Gem与想依赖套件是否已安装，如果已安装了Gem，就会显示Using，如果是新下载安装的Gem，就会显示Installing，可以使用`bundle show gemname`可以知道Gem的安装位置。     
3. Gemfile是一个用于描述gem间依赖的文件。gem是一堆ruby代码的集合，能够被我们所调用。Gemfile必须放在项目的根目录下， 这是Bundler的要求，对于任何形式的包管理文件来说这也是标准。当在Bundler上下文环境中被执行的时候能够使我们访问一些方法，我们用这些方法来解释gem之间的require关系。

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

###设置gem被required
在Rails项目的config/application.rb文件里面有这么一行代码： 
   
		Bundler.require(:default, Rails.env)
意思是require所有没有被放入group里面的gems和所有放入和当前rails环境（RAILS_ENV, development, test, production)同名的group里面的gems。          
默认方式下，如果你在Gemfile里面包含一个gem，当Bundler.require被调用的时候会被包含进来。               

我们也能通过下面的设置让gem不被包含进来(这样就只能安装这个gem，在使用的时候必须在你的代码里手动的添加`require ‘my_gem’`来调用my_gem里面的方法了。因为并不是所有的地方都需要使用这个gem，比如在rake task里面使用了my_gem, 而其他地方没有使用，故你只需要在这个gem require到task里面，避免了所有的进程都把这个gem加载进去）

    gem "my_gem", require: false
也可以指定哪些文件夹被required的，如下： 

    gem "my_gem", require: ["my_gem/specific_module/my_class", "my_gem"]
这点在当gem有很多功能的，必须每次手动require的时候非常有用。
###gem分组
一个gem可以属于一个或多个group，当它不属于任何group的时候，就被放入了:default group。有两种方法可以对一个gem分组。       
1. 第一种是对group属性进行赋值，如下所示：

		gem "my_gem", group: :development
意思是，这个gem只在development环境下被require。这也意味着当在安装gems的时候，可以指定某个group下面的gems不被安装，这样在一定程度上能加快gem的安装。

		bundle install --without development test
上面的意思是安装除development和test group意外的所有gems。       
2. 第二种gem分组的方法就是你可以将gems放入一个block里面，如下所示：
		
		group :development do
		   gem "my_gem"
		   gem "my_other_gem"
		end
并且也可以设置多个group。
		
		group :development, :test do
		  gem "my_gem"
		  gem "my_other_gem"
		end
如果想让某个group变成可选的形式，也可以像下面这样，设置optional: true        

		group :development, optional: true do
		  gem "my_gem"
		  gem "my_other_gem"
		end		
当上面被设置时，为了安装development group下面的gems，需要运行

		bundle install —with development

###设置gem的平台

如果某个gem只能在某个平台上使用，也可以在gemfile里面设置。平台的原理和group很类似，不同的是不需要去通过`—without`这样的option去指定，它会自动根据平台判断执行。

	gem "my_gem", platform: :jrubygem "my_other_gem", platform: [:ruby, :mri_18]

下面是一个不同平台的list:      

	  * ruby – C Ruby (MRI) or Rubinius, but not Windows
	  * ruby_18 to ruby_22 – ruby & (version 1.8 .. version 2.2)
	  * mri – Same as ruby, but not Rubinius
	  * mri_18 to mri_22 – mri & (version 1.8 .. version 2.2)
	  * rbx – Same as ruby, but only Rubinius (not MRI)
	  * jruby – JRuby
	  * mswin – Windows
	  * mingw – Windows 32 bit mingw32 platform (aka RubyInstaller)
	  * mingw_18 to mingw_22 – mingw & (version 1.8 .. version 2.2)
	  * x64_mingw – Windows 64 bit mingw32 platform
	  * x64_mingw_20 to x64_mingw_22 – x64_mingw & (version 2.0 .. version 2.2)
	
使用block语法来使用platform设定:

		platforms :jruby do
		  gem "my_gem"
		  gem "my_other_gem"
		end
		
###设置gem的源
设置gem的源，如下所示:       

	gem "my_gem", source: "https://my_awesome_gemsite.com"

如果这个my_gem 在source里面找不到的话，Bundler也不会去default的源里面找，所以找不到的情况下这个gem就不会被安装。           
###从git安装gem
可以设置gem的安装源为一个git repo，比如GitHub, 只需要source属性替换为git。可以设置这个repo的链接为HTTP(S), SSH, GIT等协议，但最好使用HTTP(S)和SSH，因为其他的可能受到man-in-the-middle的攻击。如果把gem放入到repo里面，则必须要在repo根目录文件夹下面有一个`.gemspec` 文件。这里面需要包含一个合法gem的声明。如果没有提供这个文件，Bundler会尝试创建一个，但是它不会被依赖。如果去include一个没有提供`.gemspec`文件的git repo里面的gem，则必须指定一个版本号。         
可以为gem设置branch，tag，ref，默认是使用master branch。也可以强制Bundler扩展submodule，通过以下方式来设置：

	gem "my_gem", git: "ssh@githib.com/tosbourn/my_gem", branch: test_branch, submodules: true
	
如果有多个gem来自同一个git repo，也可以通过下面block形式组织起来。          

	git "git@github.com:tosbourn/my_gems.git" do
	  gem "my_gem"
	  gem "my_other_gem"
	end

###设置Git作为source
可以设置一个URL来作为一个更广义的源，通过调用`#git_source`方法并将name作为参数传进去，以及一个接收一个参数的block，并返回一个string作为repo的URL。如下所示：

	git_source(:custom_git){ |repo| "https://my_secret_git_repos.com/#{repo}.git" }
	gem "my_gem", custom_git: "tosbourn/test_repo"
	
###BitBucket和Github的helper method
因为BitBucket和Github都是比较流行的git repo host，所以有两者的helper method。在两者里面，Bundler都默认repo是public的。

	gem "my_gem", github: "tosbourn/my_gem"
	gem "my_gem", bitbucket: "tosbourn/my_gem"
也可以设置两者的branch。当用户名和repo名字一致的时候，可以省略一个。       

	gem "rails", github: "rails"
	gem "rails", bitbucket: "rails"

_注意：在Bundler 2出来之前，不能使用`:github`这个参数，目前它是使用git://协议的，就是前面讲过的可能会受到man-in-the-middle攻击的。还有一个`helper :gist`, 如果Github上是以gist的形式存放的话就能够使用它。可以只使用gist ID作为path，也可以像`:github, :bitbucket`那样传入:branch参数。_

	gem "my_gem", :gist => "5935162112", branch: "my_custom_branch"
	
###用path包含本地Gem
可以通过传入:path参数来依赖本地的gems。

	gem "my_gem", :path => "../my_path/my_gem"

如果传入一个相对路径，这个路径是相对于Gemfile路径的。如果想把某个文件夹下所有的gems都包含进去的话，可以使用如下的block。

	path "../my_path/gems" do
	  gem "my_gem"
	  gem "my_other_gem"
	end

###选择性的安装gems
有时候想在某个前提条件被满足的情况下安装这个gem，比如系统里面是否有某个程序。下面这个方法能够接收一个proc或lambda，下面的例子将在系统是mac的时候安装这个gem:
	
	install_if -> { RUBY_PLATFORM =~ /darwin/ } do
	  gem "my_osx_gem"
	end
	
###Gemfile和Gemfile.lock间的关系
1. Gemfile是指定需要使用的哪些gem及其版本的地方；     
2. Gemfile.lock文件是Bundler记录已经安装了的版本的地方。通过这样的方式，当相同库/项目在另外一台机器上部署的时候，运行bundle install将会查看Gemfile.lock，然后安装同样的版本，而不是使用Gemfile以及安装最新的版本。（在不同的机器上运行不同版本会导致测试的失败……）你不需要直接地更改Gemfile.lock.
