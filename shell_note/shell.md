##shell命令
###1. set:
set命令作用主要是显示系统中已经存在的shell变量，以及设置shell变量的新变量值。使用set更改shell特性时，符号"+"和"-"的作用分别是打开和关闭指定的模式。set命令不能够定义新的shell变量。如果要定义新的变量，可以使用declare命令以变量名=值的格式进行定义即可。  
        
* **语法：**          
`set (选项)（参数）           `
* **选项：**         
-a：标示已修改的变量，以供输出至环境变量。        
-b：使被中止的后台程序立刻回报执行状态。        
-C：转向所产生的文件无法覆盖已存在的文件。          
-d：Shell预设会用杂凑表记忆使用过的指令，以加速指令的执行。使用-d参数可取消。          
-e：若指令传回值不等于0，则立即退出shell。          
-f：取消使用通配符。            
-h：自动记录函数的所在位置。            
-H Shell：可利用"!"加<指令编号>的方式来执行history中记录的指令。                
-k：指令所给的参数都会被视为此指令的环境变量。            
-l：记录for循环的变量名称。                  
-m：使用监视模式。          
-n：只读取指令，而不实际执行。        
-p：启动优先顺序模式。           
-P：启动-P参数后，执行指令时，会以实际的文件或目录来取代符号连接。         
-t：执行完随后的指令，即退出shell。            
-u：当执行时使用到未定义过的变量，则显示错误信息。          
-v：显示shell所读取的输入值。           
-x：执行指令后，会先显示该指令及所下的参数。 

* **关联：**           
使用`declare`命令定义一个新的环境变量"mylove"，并且将其值设置为"Visual C++"，输入如下命令：          
`declare mylove='Visual C++'` #定义新环境变量        
再使用set命令将新定义的变量输出为环境变量，输入如下命令：       
`set -a mylove` #设置为环境变量        
执行该命令后，将会新添加对应的环境变量。用户可以使用`env`命令和`grep`命令分别显示和搜索环境变量"mylove"，输入命令如下：       
`env | grep mylove `#显示环境变量值        
此时，该命令执行后，将输出查询到的环境变量值。        

###2. echo:
在显示器上显示一段文字，一般起到一个提示的作用。 
        
* **语法：**        
echo 字符串           
* **参数：**       
-n 不要在最后自动换行           
-e 若字符串中出现以下字符，则特别加以处理，而不会将它当成一般文字输出：             
   \a 发出警告声；        
   \b 删除前一个字符；          
   \c 最后不加上换行符号；          
   \f 换行但光标仍旧停留在原来的位置；        
   \n 换行且光标移至行首；           
   \r 光标移至行首，但不换行；          
   \t 插入tab；         
   \v 与\f相同；         
   \\ 插入\字符；           
   \nnn 插入nnn（八进制）所代表的ASCII字符；          
–help 显示帮助       
–version 显示版本信息         

###3. pip:
pip类似RedHat里面的yum，安装软件非常方便.           
   
* **pip安装软件**
 `# pip install SomePackage`
* **pip检查哪些软件需要更新**
` # pip list --outdated`         
* **pip升级软件**
` # pip install --upgrade SomePackage`
* **pip卸载软件**
`$ pip uninstall SomePackage`

### 4. Linux文件查找命令find,xargs
####find:

* **语法：**           
`find [起始目录] 寻找条件 操作`           
`find pathname -options [-print -exec -ok ...]`
* **参数:**      
pathname: find命令所查找的目录路径。例如用.来表示当前目录，用/来表示系统根目录。           
-print： find命令将匹配的文件输出到标准输出。           
-exec： find命令对匹配的文件执行该参数所给出的shell命令。相应命令的形式为'command' {  } \;，注意{   }和\；之间的空格。            
-ok： 和-exec的作用相同，只不过以一种更为安全的模式来执行该参数所给出的shell命令，在执行每一个命令之前，都会给出提示，让用户来确定是否执行。             
* **选项:**           
-name
按照文件名查找文件。        
-perm
按照文件权限来查找文件。        
-prune
使用这一选项可以使find命令不在当前指定的目录中查找，如果同时使用-depth选项，那么-prune将被find命令忽略。             
-user
按照文件属主来查找文件。          
-group
按照文件所属的组来查找文件。            
-mtime -n +n
按照文件的更改时间来查找文件， - n表示文件更改时间距现在n天以内，+ n表示文件更改时间距现在n天以前。find命令还有-atime和-ctime 选项，但它们都和-m time选项。             
-nogroup
查找无有效所属组的文件，即该文件所属的组在/etc/groups中不存在。                
-nouser
查找无有效属主的文件，即该文件的属主在/etc/passwd中不存在。              
-newer file1 ! file2
查找更改时间比文件file1新但比文件file2旧的文件。            
-type
查找某一类型的文件，诸如：          
b - 块设备文件。      
d - 目录。         
c - 字符设备文件。         
p - 管道文件。           
l - 符号链接文件。         
f - 普通文件。          
-size n：[c] 查找文件长度为n块的文件，带有c时表示文件长度以字节计。         
-depth：在查找文件时，首先查找当前目录中的文件，然后再在其子目录中查找。              
-fstype：查找位于某一类型文件系统中的文件，这些文件系统类型通常可以在配置文件/etc/fstab中找到，该配置文件中包含了本系统中有关文件系统的信息。              
-mount：在查找文件时不跨越文件系统mount点。          
-follow：如果find命令遇到符号链接文件，就跟踪至链接所指向的文件。          
-cpio：对匹配的文件使用cpio命令，将这些文件备份到磁带设备中。           
另外,下面三个的区别:           
   -amin n
　　查找系统中最后N分钟访问的文件          
-atime n
　　查找系统中最后nx24小时访问的文件          
-cmin n
　　查找系统中最后N分钟被改变文件状态的文件            
-ctime n
　　查找系统中最后nx24小时被改变文件状态的文件       
-mmin n
　　查找系统中最后N分钟被改变文件数据的文件          
-mtime n
　　查找系统中最后n*24小时被改变文件数据的文件         

* **使用exec或ok来执行shell命令**            
使用find时，只要把想要的操作写在一个文件里，就可以用exec来配合find查找.       
在有些操作系统中只允许`-exec`选项执行诸如`l s`或`ls -l`这样的命令。大多数用户使用这一选项是为了查找旧文件并删除它们。建议在真正执行rm命令删除文件之前，最好先用ls命令看一下，确认它们是所要删除的文件。                  
exec选项后面跟随着所要执行的命令或脚本，然后是一对儿{ }，一个空格和一个\，最后是一个分号。为了使用exec选项，必须要同时使用print选项。如果验证一下find命令，会发现该命令只输出从当前路径起的相对路径及文件名。         
例如：为了用`ls -l`命令列出所匹配到的文件，可以把`ls -l`命令放在find命令的-exec选项中
 `# find . -type f -exec ls -l {  } \;`            
上面的例子中，find命令匹配到了当前目录下的所有普通文件，并在`-exec`选项中使用`ls -l`命令将它们列出。         
在/logs目录中查找更改时间在5日以前的文件并删除它们：     
`$ find logs -type f -mtime +5 -exec rm {  } \;`
_注意：_在shell中用任何方式删除文件之前，应当先查看相应的文件，一定要小心！当使用诸如mv或rm命令时，可以使用`-exec`选项的安全模式。它将在对每个匹配到的文件进行操作之前提示你。      
在下面的例子中， find命令在当前目录中查找所有文件名以.LOG结尾、更改时间在5日以上的文件，并删除它们，只不过在删除之前先给出提示。         
`$ find . -name "*.conf"  -mtime +5 -ok rm {  } \;`
任何形式的命令都可以在-exec选项中使用。        
在下面的例子中我们使用grep命令。find命令首先匹配所有文件名为“ passwd*”的文件，例如passwd、passwd.old、passwd.bak，然后执行grep命令看看在这些文件中是否存在一个sam用户。   
         
 `# find /etc -name "passwd*" -exec grep "sam" {  } \;
sam:x:501:501::/usr/sam:/bin/bash`

####xargs:

在使用find命令的-exec选项处理匹配到的文件时， find命令将所有匹配到的文件一起传递给exec执行。但有些系统对能够传递给exec的命令长度有限制，这样在find命令运行几分钟之后，就会出现 溢出错误。错误信息通常是“参数列太长”或“参数列溢出”。这就是xargs命令的用处所在，特别是与find命令一起使用。         

find命令把匹配到的文件传递给xargs命令，而xargs命令每次只获取一部分文件而不是全部，不像-exec选项那样。这样它可以先处理最先获取的一部分文件，然后是下一批，并如此继续下去。           

在有些系统中，使用-exec选项会为处理每一个匹配到的文件而发起一个相应的进程，并非将匹配到的文件全部作为参数一次执行；这样在有些情况下就会出现进程过多，系统性能下降的问题，因而效率不高；           

而使用xargs命令则只有一个进程。另外，在使用xargs命令时，究竟是一次获取所有的参数，还是分批取得参数，以及每一次获取参数的数目都会根据该命令的选项及系统内核中相应的可调参数来确定。

###touch:
linux的touch命令不常用，一般在使用make的时候可能会用到，用来修改文件时间戳，或者新建一个不存在的文件。touch命令参数可更改文档或目录的日期时间，包括存取时间和更改时间。          

* **命令格式：**          
`touch [选项]... 文件...`
* **参数：**           
-a   或--time=atime或--time=access或--time=use 　只更改存取时间。            
-c   或--no-create 　仅修改时间，不建立任何文档。         
-d 　使用指定的日期时间，而非现在的时间。           
-f 　此参数将忽略不予处理，仅负责解决BSD版本touch指令的兼容性问题。           
-m   或--time=mtime或--time=modify 　只更改变动时间。         
-r 　把指定文档或目录的日期时间，统统设成和参考文档或目录的日期时间相同。         
-t 　使用指定的日期时间，而非现在的时间。后面可以接时间，格式为 [[CC]YY]MMDDhhmm[.SS] 如198408250310.20         

###chmod:
chmod是Linux下设置文件权限的命令，后面的数字表示不同的用户或用户组的权限。   
         
* **一般是三个数字：**      
第一个数字表示文件所有者的权限        
第二个数字表示与文件所有者同属一个用户组的其他用户的权限            
第三个数字表示其它用户组的权限             
* **权限分三种：**        
读 r=4      
写 w=2          
执行 x=1           
* **综合起来：**           
rx=5 rw=6 rwx=7              
所以chmod 755表示用户对该文件拥有读，写，执行的权限，同组其他人员拥有执行和读的权限，没有写的权限，其他用户的权限和同组人员权限一样.           
* **使用方式 :**     
`chmod [-cfvR] [--help] [--version] mode file...`
* **参数 :**           
mode : 权限设定字串，格式如下 : [ugoa...][[+-=][rwxX]...][,...]，其中            
u 表示该档案的拥有者，          
g 表示与该档案的拥有者属于同一个群体(group)者，          
o 表示其他以外的人，         
a 表示这三者皆是。        
"+" 表示增加权限、          
"-" 表示取消权限、            
"=" 表示唯一设定权限。                  
r 表示可读取，            
w 表示可写入，       
x 表示可执行，        
X 表示只有当该档案是个子目录或者该档案已经被设定过为可执行。           
-c : 若该档案权限确实已经更改，才显示其更改动作           
-f : 若该档案权限无法被更改也不要显示错误讯息         
-v : 显示权限变更的详细资料           
-R : 对目前目录下的所有档案与子目录进行相同的权限变更(即以递回的方式逐个变更)           
--help : 显示辅助说明           
--version : 显示版本            

###scp:           
scp 可以在 2个 linux 主机间复制文件；          

* **命令基本格式：**
  `scp [可选参数] file_source file_target`
* **从本地复制到远程**
 1. 复制文件：          
    命令格式：
       `scp local_file `
   remote_username@remote_ip:remote_folder        
                或者        
                scp local_file remote_username@remote_ip:remote_file        
                或者          
                scp local_file remote_ip:remote_folder                  
                或者       
                scp local_file remote_ip:remote_file              

  第1,2个指定了用户名，命令执行后需要再输入密码，第1个仅指定了远程的目录，文件名字不变，第2个指定了文件名；         
       第3,4个没有指定用户名，命令执行后需要输入用户名和密码，第3个仅指定了远程的目录，文件名字不变，第4个指定了文件名；         
   例子：           
        scp /home/space/music/1.mp3 root@www.cumt.edu.cn:/home/root/others/music           
                scp /home/space/music/1.mp3 root@www.cumt.edu.cn:/home/root/others/music/001.mp3
                scp /home/space/music/1.mp3            www.cumt.edu.cn:/home/root/others/music         
                scp /home/space/music/1.mp3 www.cumt.edu.cn:/home/root/others/music/001.mp3           

 2. 复制目录：        
    命令格式：       
   `scp -r local_folder `
   remote_username@remote_ip:remote_folder          
                或者            
                scp -r local_folder remote_ip:remote_folder               

 第1个指定了用户名，命令执行后需要再输入密码；        
 第2个没有指定用户名，命令执行后需要输入用户名和密码；        
   例子：       
      scp -r /home/space/music/ root@www.cumt.edu.cn:/home/root/others/          
      scp -r /home/space/music/ www.cumt.edu.cn:/home/root/others/           

  上面命令将本地music目录复制到远程others目录下，即复制后有远程 有 ../others/music/ 目录       

* **从远程 复制到本地**
从远程复制到本地，只要将从本地复制到远程的命令的后2个参数调换顺序 即可；       
例如：     
        scp root@www.cumt.edu.cn:/home/root/others/music /home/space/music/1.mp3          
        scp -r www.cumt.edu.cn:/home/root/others/ /home/space/music/          
最简单的应用如下 :        
`scp 本地用户名 @IP 地址 : 文件名 1 远程用户名 @IP 地址 : 文件名 2`             
[ 本地用户名 @IP 地址 :] 可以不输入 , 可能需要输入远程用户名所对应的密码 .           

* **可能有用的几个参数 :**    
-v 和大多数 linux 命令中的 -v 意思一样 , 用来显示进度 . 可以用来查看连接 , 认证 , 或是配置错误 .      
-C 使能压缩选项 .        
-P 选择端口 . 注意 -p 已经被 rcp 使用 .       
-4 强行使用 IPV4 地址 .       
-6 强行使用 IPV6 地址 .         


