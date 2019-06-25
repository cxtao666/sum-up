# vue和node总结

## js代码注意事项

.

 当你采用了无分号的代码风格的时候，只需要注意以下情况就不会有上面的问题了：
    当一行代码是以：
        (
        [
        `
        开头的时候，则在前面补上一个分号用以避免一些语法解析错误。
    所以你会发现在一些第三方的代码中能看到一上来就以一个 ; 开头。
  结论：
    无论你的代码是否有分号，都建议如果一行代码是以 (、[、` 开头的，则最好都在其前面补上一个分号。
    有些人也喜欢玩儿一些花哨的东西，例如可以使用 ! ~ 等。



## centos常用命令

安装yum,vim,nvm,wget

### 其它命令

`sudo chmod 755 -R node` 修改目录权限
`sudo lsof -nP -iTCP -sTCP:LISTEN` 查看本地服务
`ps -ef | grep websocket` 查看websocket进程
`ps aux | grep mysql` 查看mysql进程
`sudo kill 443` 杀掉进程

### 给目录权限

```
sudo chmod -R 777 目录
```

### 搜索

```
find path -option [-print] [-exec -ok command] { }\;
```

- pathname: find命令所查找的目录路径。例如用`.`来表示当前目录，用`/`来表示系统根目录。
- `-print`: find命令将匹配的文件输出到标准输出。
- `-exec`: find命令对匹配的文件执行该参数所给出的shell命令。相应命令的形式为`'command' { } \;`，注意`{ }`和`\;`之间的空格。
- `-ok`： 和`-exec`的作用相同，只不过以一种更为安全的模式来执行该参数所给出的shell命令，在执行每一个命令之前，都会给出提示，让用户来确定是否执行。

```
$ find ~ -name "*.txt"  -print   #在$HOME中查.txt文件并显示
$ find . -name "*.txt"  -print
$ find . -name "[A-Z]*" -print   #查以大写字母开头的文件
$ find /etc -name "host*"  -print  #查以host开头的文件
# 查以两个小写字母和两个数字开头的txt文件
$ find .   -name   "[a-z][a-z][0–9][0–9].txt" -print   
$ ind . -perm   755   -print
$ ind . -perm -007   -exec ls -l {} \;   #查所有用户都可读写执行的文件同-perm 777
$ ind . -type d   -print
$ ind . !  -type d   -print 
$ ind . -type l   -print
```

### ls

> 类似于dos下的dir命令

ls最常用的参数有三个： -a -l -F。

ls –a

Linux上的文件以.开头的文件被系统视为隐藏文件，仅用ls命令是看不到他们的，而用ls - a除了显示一般文件名外，连隐藏文件也会显示出来。 ls –l 该参数显示更详细的文件信息。 ls –F 使用这个参数表示在文件的后面多添加表示文件类型的符号，例如*表示可执行，/表示目录，@表示连结文件，这都是因为使用了-F这个参数。但是现在基本上所有的Linux发行版本的ls都已经内建了-F参数，也就是说，不用输入这个参数，我们也能看到各种分辨符号。

### cd

> 用于切换用户当前工作目录

cd aaa 进入aaa目录 cd 命令后不指定目录，会切换到当前用户的home 目录 cd ~ 作用同cd后不指定目录，切换到当前用户的home 目录 cd - 命令后跟一个减号，则会退回到切换前的目录 cd .. 返回到当前目录下的上一级目录

### pwd

> 用于显示用户当前工作目录

### mkdir 和 rmdir

> midir:创建目录 / rmdir:删除目录

两个命令都支持-p参数，对于mkdir命令若指定路径的父目录不存在则一并创建，对于rmdir命令则删除指定路径的所有层次目录，如果文件夹里有内容，则不能用rmdir命令

如下：

```
mkdir -p 1/2/3
rmdir -p 1/2/3 
```

### mkdir循环创建目录

[How do I make multiple directories at once in a directory?](http://unix.stackexchange.com/questions/636/how-do-i-make-multiple-directories-at-once-in-a-directory)

```
for char in {A..Z}; do
    mkdir $char
done

for num in {1..100}; do
    mkdir $num
done
```

#### 创建文件命令

```
touch 文件名
```

### cp

> 复制命令

- 复制一个文件到另一目录：`cp 1.txt ../test2`
- 复制一个文件到本目录并改名：`cp 1.txt 2.txt`
- 复制一个文件夹a并改名为b，-r或-R 选项表明递归操作：`cp -r a b`
- 同时拷贝多个文件，我们只需要将多个文件用空格隔开。`cp file_1.txt file_2.txt file_3.txt /home/pungki/office`

### mv

> 移动命令

将一个文件移动到另一个目录：mv 1.txt ../test1 将一个文件在本目录改名：mv 1.txt 2.txt 将一个文件一定到另一个目录并改名：mv 1.txt ../test1/2.txt

### rm命令

> 命令用于删除文件，与dos下的del/erase命令相似，rm命令常用的参数有三个：-i，-r，-f。

1. –i ：系统在删除文件之前会先询问确认，用户回车之后，文件才会真的被删除。需要注意，linux下删除的文件是不能恢复的，删除之前一定要谨慎确认。
2. –r：该参数支持目录删除，功能和rmdir命令相似。
3. –f：和-i参数相反，-f表示强制删除

### find

> find 查找目录和文件

```
-name   filename   #查找名为filename的文件
-perm              #按执行权限来查找
-user    username  #按文件属主来查找
-group groupname   #按组来查找
-mtime   -n +n     #按文件更改时间来查找文件，-n指n天以内，+n指n天以前
-atime    -n +n    #按文件访问时间来查GIN: 0px">

-ctime    -n +n    #按文件创建时间来查找文件，-n指n天以内，+n指n天以前

-nogroup           #查无有效属组的文件，即文件的属组在/etc/groups中不存在
-nouser            #查无有效属主的文件，即文件的属主在/etc/passwd中不存
-newer   f1 !f2    #找文件，-n指n天以内，+n指n天以前 
-ctime    -n +n    #按文件创建时间来查找文件，-n指n天以内，+n指n天以前 
-nogroup           #查无有效属组的文件，即文件的属组在/etc/groups中不存在
-nouser            #查无有效属主的文件，即文件的属主在/etc/passwd中不存
-newer   f1 !f2    #查更改时间比f1新但比f2旧的文件
-type    b/d/c/p   #查是块设备、目录、字符设备、管道、符号链接、普通文件
-size      n[c]    #查长度为n块[或n字节]的文件
-depth             #使查找在进入子目录前先行查找完本目录
-fstype            #查更改时间比f1新但比f2旧的文件
-type    b/d/c/p   #查是块设备、目录、字符设备、管道、符号链接、普通文件
-size      n[c]    #查长度为n块[或n字节]的文件
-depth             #使查找在进入子目录前先行查找完本目录
-fstype            #查位于某一类型文件系统中的文件，这些文件系统类型通常可 在/etc/fstab中找到
-mount             #查文件时不跨越文件系统mount点
-follow            #如果遇到符号链接文件，就跟踪链接所指的文件
-cpio %;           #查位于某一类型文件系统中的文件，这些文件系统类型通常可 在/etc/fstab中找到
-mount             #查文件时不跨越文件系统mount点
-follow            #如果遇到符号链接文件，就跟踪链接所指的文件
-cpio              #对匹配的文件使用cpio命令，将他们备份到磁带设备中
-prune             #忽略某个目录
```

例子：

- ~ 代表的是$home目录，

```
$ find . -name '*.DS_Store' -type f -delete # 删除所有.DS_Store文件
$ find ~ -name "*.txt" -print       # 在$HOME中查.txt文件并显示
$ find . -size +1000000c -print     # 查长度大于1Mb的文件
$ find . -size 100c -print          # 查长度为100c的文件
$ find . -size +10 -print           # 查长度超过期作废10块的文件（1块=512字节）
$ find -name april*                 # 在当前目录下查找以april开始的文件
$ find -name april* fprint file     # 在当前目录下查找以april开始的文件，并把结果输出到file中
$ find -name ap* -o -name may*          # 查找以ap或may开头的文件
$ find /mnt -name tom.txt -ftype vfat   # 在/mnt下查找名称为tom.txt且文件系统类型为vfat的文件
$ find /mnt -name t.txt ! -ftype vfat   # 在/mnt下查找名称为tom.txt且文件系统类型不为vfat的文件
$ find /tmp -name wa* -type l           # 在/tmp下查找名为wa开头且类型为符号链接的文件
$ find ~ -mtime -2                  # 在/home下查最近两天内改动过的文件
$ find ~ -atime -1                  # 查1天之内被存取过的文件
$ find ~ -mmin +60                  # 在/home下查60分钟前改动过的文件
$ find ~ -amin +30                  # 查最近30分钟前被存取过的文件
$ find ~ -newer tmp.txt             # 在/home下查更新时间比tmp.txt近的文件或目录
$ find ~ -anewer tmp.txt            # 在/home下查存取时间比tmp.txt近的文件或目录
$ find ~ -used -2                   # 列出文件或目录被改动过之后，在2日内被存取过的文件或目录
$ find ~ -user cnscn                # 列出/home目录内属于用户cnscn的文件或目录
$ find ~ -uid +501                  # 列出/home目录内用户的识别码大于501的文件或目录
$ find ~ -group cnscn               # 列出/home内组为cnscn的文件或目录
$ find ~ -gid 501                   # 列出/home内组id为501的文件或目录
$ find ~ -nouser                    # 列出/home内不属于本地用户的文件或目录
$ find ~ -nogroup                   # 列出/home内不属于本地组的文件或目录
$ find ~ -name tmp.txt -maxdepth 4  # 列出/home内的tmp.txt 查时深度最多为3层
$ find ~ -name tmp.txt -mindepth 3  # 从第2层开始查
$ find ~ -empty                     # 查找大小为0的文件或空目录
$ find ~ -size   +512k              # 查大于512k的文件
$ find ~ -size   -512k              # 查小于512k的文件
$ find ~ -links   +2                # 查硬连接数大于2的文件或目录
$ find ~ -perm 0700                 # 查权限为700的文件或目录
$ find ~ -perm 755 -print | more    # 查找权限为755的文件
$ find /tmp -name tmp.txt -exec cat {} \;
$ find /tmp -name tmp.txt ok rm {} \;

$ find / -amin    -10      # 查找在系统中最后10分钟访问的文件
$ find / -atime   -2       # 查找在系统中最后48小时访问的文件
$ find / -empty            # 查找在系统中为空的文件或者文件夹
$ find / -group   cat      # 查找在系统中属于 groupcat的文件
$ find / -mmin   -5        # 查找在系统中最后5分钟里修改过的文件
$ find / -mtime   -1       # 查找在系统中最后24小时里修改过的文件
$ find / -nouser           # 查找在系统中属于作废用户的文件
$ find / -user    fred     # 查找在系统中属于FRED这个用户的文件
```

### du、df命令

> du命令可以显示目前的目录所占用的磁盘空间，df命令可以显示目前磁盘剩余空间。

如果du命令不加任何参数，那么返回的是整个磁盘的使用情况，如果后面加了目录的话，就是这个目录在磁盘上的使用情况。

1. `du -hs` 指定目录 查看指定目录的总大小
2. `du -hs ./*` 查看当前目录下的所有文件夹和文件的大小

这两个命令都支持-k，-m和-h参数，-k和-m类似，都表示显示单位，一个是k字节一个是兆字节，-h则表示human-readable，即友好可读的显示方式。

### cat命令

> cat命令的功能是显示或连结一般的ascii文本文件。cat是concatenate的简写，类似于dos下面的type命令。用法如下：

1. `cat file1` 显示file1文件内容
2. `cat file1 file2` 依次显示file1,file2的内容
3. `cat file1 file2 > file3` 把file1, file2的内容结合起来，再“重定向（>）”到file3文件中。
4. `>`是右重定向符，表示将左边命令结果当成右边命令的输入，注意：如果右侧文件是一个已存在文件，其原有内容将会被清空，而变成左侧命令输出内容。如果希望以追加方式写入，请改用">>"重定向符。

如果">"左边没有指定文件，如： cat >file1，将会等用户输入，输入完毕后再按[Ctrl]+[c]或[Ctrl]+[d]，就会将用户的输入内容写入file1。

### echo命令

> echo命令的使用频率不少于ls和cat，尤其是在shell脚本编写中。 语法：echo [-ne][字符串] 功能：echo会将输入的字符串送往标准输出，输出的字符串间以空白字符隔开， 并在最后加上换行符。

参数：

- `-n` 显示字串时在最后自动换行
- `-e` 支持以下格式的转义字符， -E 不支持以下格式的转义字符
- `/a` 发出警告声；
- `/b` 删除前一个字符；
- `/c` 最后不加上换行符号；
- `/f` 换行但光标仍旧停留在原来的位置；
- `/n` 换行且光标移至行首；
- `/r` 光标移至行首，但不换行；
- `/t` 插入tab；
- `/v` 与/f相同；
- `//` 插入/字符；
- `/nnn` 插入nnn（八进制）所代表的ASCII字符；

示例：

```
kenny@jstest:~/hgd> echo "123" "456"
123 456
kenny@jstest:~/hgd> echo "123/n456"
123/n456
kenny@jstest:~/hgd> echo -e "123/n456"
123
456
kenny@jstest:~/hgd> echo -E "123/n456"
123/n456
kenny@jstest:~/hgd> echo -E "123///456"
123//456
kenny@jstest:~/hgd> echo -e "123///456"
123/456
kenny@jstest:~/hgd> echo -e "123/100456"
123@456
```

注意事项： 在Linux使用的bash下，单引号’’和双引号是有区别的，单引号忽略所有的转义，双引号不会忽略以下特殊字符： Dollar signs ($)，Back quotes (`)，Backslashes (/)，Excalmatory mark(!)

示例如下：

```
kenny@jstest:~> echo "`TEST`"
-bash: TEST: command not found
kenny@jstest:~> echo '`TEST`'
`TEST`
kenny@jstest:~> echo "$TEST"
        
kenny@jstest:~> echo '$TEST'
$TEST
kenny@jstest:~> echo "//TEST"
/TEST
kenny@jstest:~> echo '//TEST'
//TEST
kenny@jstest:~> echo "Hello!"
echo "Hello"
Hello
kenny@jstest:~> echo 'Hello!'
Hello!
```

### more，less，clear

> more，less命令

```
这两个命令用于查看文件，如果一个文件太长，显示内容超出一个屏幕，用cat命令只能看到最后的内容，用more和less两个命令可以分页查看。more指令可以使超过一页的文件内容分页暂停显示，用户按键后才继续显示下一页。而less除了有more的功能以外，还可以用方向键往上或往下的滚动文件，更方便浏览阅读。
```

less的常用动作命令：

- 回车键 向下移动一行；
- `y` 向上移动一行；
- 空格键 向下滚动一屏；
- `b` 向上滚动一屏；
- `d` 向下滚动半屏；
- `h` less的帮助；
- `u` 向上洋动半屏；
- `w` 可以指定显示哪行开始显示，是从指定数字的下一行显示；比如指定的是6，那就从第7行显示；
- `g` 跳到第一行；
- `G` 跳到最后一行；
- `p n%` 跳到n%，比如 10%，也就是说比整个文件内容的10%处开始显示；
- `/pattern` 搜索pattern ，比如 /MAIL表示在文件中搜索MAIL单词；
- `v` 调用vi编辑器；
- `q` 退出less
- `!command` 调用SHELL，可以运行命令；比如!ls 显示当前列当前目录下的所有文件；
- `clear`命令 clear命令是用来清除当前屏幕显示的，不需任何参数，和dos下的cls命令功能相同。

### head，tail

- head和tail命令都用于查看文本文件，区别在于： head显示文件的头n行，tail显示文件的尾n行，缺省情况n都为10行。可以通过-n方式指定行数，如：head -100 file和tail -100 file分别表示显示文件头100行和尾100行内容。
- tail -f命令可以实时查看文件新增内容。

### wc命令

该命令用于统计指定文件中的字节数、字数、行数。该命令各选项含义如下：

- -l 统计行数
- -w 统计字数
- -c 统计字节数

这些选项可以组合使用。输出列的顺序和数目不受选项的顺序和数目的影响。总是按下述顺序显示并且每项最多一列。 行数、字数、字节数、文件名 如果命令行中没有文件名，则输出中不出现文件名。

例如：

```
oracle@hjtest:~> wc 1.txt 2.txt
  460  1679 16353 1.txt
  300  1095 10665 2.txt
  760  2774 27018 总用量
oracle@hjtest:~> wc -l 1.txt
460 1.txt
```

缺省参数为-lcw，即wc file1 file2命令的执行结果与上面一样。

### grep 命令

> grep是（global search regular expression(RE) and print out the line的缩写，用于从文件面搜索包含指定模式的行并打印出来，它是一种强大的文本搜索工具，支持使用正则表达式搜索文本。grep的工作方式是这样的，它在一个或多个文件中搜索字符串模板。如果模板包括空格，则必须被””引用，模板后的所有字符串被看作文件名。搜索结果送到屏幕，不影响原文件内容。

grep可用于shell脚本，因为grep通过返回一个状态值来说明搜索的状态，如果模板搜索成功，则返回0，如果搜索不成功，则返回1，如果搜索的文件不存在，则返回2。我们利用这些返回值就可进行一些自动化的文本处理工作。 示例：

```
$ ls -l | grep '^a'
通过管道过滤ls -l输出的内容，只显示以a开头的行。
$ grep 'test' d*
显示所有以d开头的文件中包含test的行。
$ grep 'test' aa bb cc
显示在aa，bb，cc文件中匹配test的行。
$ grep '[a-z]/{5/}' aa
显示所有包含每个字符串至少有5个连续小写字符的字符串的行。
$ grep 'w/(es/)t.*/1' aa
如果west被匹配，则es就被存储到内存中，并标记为1，然后搜索任意个字符（.*），这些字符后面紧跟着另外一个es（/1），找到就显示该行。如果用egrep或grep -E，就不用"/"号进行转义，直接写成'w(es)t.*/1'就可以了。
```

### man，logout命令

> man命令，man是manual的缩写，相当于Unix/Linux的联机Help，每个系统命令和调用都有非常详细的说明，绝大多数都是英文。如：man ls即是查看ls命令的使用说明，一般还有另一种方法用来查看帮助，如：ls –help，这种方式绝大多数命令都支持。

> logout命令，该命令用于退出系统，与login命令对应。

### 管道和xargs

#### 管道

利用Linux所提供的管道符“|”将两个命令隔开，管道符左边命令的输出就会作为管道符右边命令的输入。连续使用管道意味着第一个命令的输出会作为第二个命令的输入，第二个命令的输出又会作为第三个命令的输入，依此类推。 注意：管道左边命令的输入作为管道右边命令的输入(命令的输入是一定的)，不是参数，并不是所有命令都支持管道 例子：ls | grep a 查看当前目录下名称包含a的文件或文件夹

#### xargs

大多数 Linux 命令都会产生输出：文件列表、字符串列表等。但如果要使用其他某个命令并将前一个命令的输出作为参数该怎么办？例如，file 命令显示文件类型（可执行文件、ascii 文本等）；你能处理输出，使其仅显示文件名，目前你希望将这些名称传递给 ls -l 命令以查看时间戳记。xargs 命令就是用来完成此项工作的。 注意：find命令把匹配到的文件传递给xargs命令，而xargs命令每次只获取一部分文件而不是全部，不像-exec选项那样。这样它可以先处理最先获取的一部分文件，然后是下一批，并如此继续下去

例子：

1. 在整个系统中查找内存信息转储文件(core dump) ，然后把结果保存到/tmp/core.log 文件中：

```
$ find / -name "core" -print | xargs echo "" >/tmp/core.log
```

1. 当一个目录下文件太多时，直接用rm * 命令会包参数过长,用如下方法可以全部删除

```
$ls | xargs rm
```

### basename 和 dirname

basename用于查看文件不含路径的名字，dirname则用于查看文件路径，使用效果我们测试一下便知：

```
> basename /home/hj/1.txt
1.txt
> dirname  /home/hj/1.txt
/home/hj
> basename 1.txt
1.txt
> dirname 1.txt
.
```



## 包管理工具npm

首先安装nvm，然后再这基础上安装node和npm

- package.json 包描述文件
  - 就是产品的说明书
  - `dependencies` 属性，用来保存项目的第三方包依赖项信息
  - 所以建议每个项目都要有且只有一个 package.json (存放在项目的根目录)
  - 我们可以通过 `npm init [--yes]` 来生成 package.json 文件
  - 同样的，为了保存依赖项信息，我们每次安装第三方包的时候都要加上：`--save` 选项。
  
- npm 常用命令
  - install
  
  - uninstall
  
    #### npm更改镜像
  
  ### 方法一： 直接编辑npm的配置文件
  
  ```
  npm config edit
  ```
  
  ![img](https://images2018.cnblogs.com/blog/1416090/201806/1416090-20180621111355013-1113191392.png)
  
  直接修改registry的地址
  
  sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
  phantomjs_cdnurl=https://npm.taobao.org/mirrors/phantomjs/
  electron_mirror=https://npm.taobao.org/mirrors/electron/
  registry=https://registry.npm.taobao.org
  
   
  
  ### 方法二：用代码更改npm的配置文件
  
  ```
  npm config set registry http://registry.npm.taobao.org
  ```
  
  这段代码即将镜像改为淘宝镜像
  
   
  
  ### 方法三： 使用nrm管理registry地址
  
  **安装nrm**
  
  ```
  npm install -g nrm
  ```
  
  **查看镜像列表**
  
  ```
  nrm ls
  ```
  
  ![img](https://images2018.cnblogs.com/blog/1416090/201806/1416090-20180621140442524-135518017.png)
  
  **切换镜像**
  
  ```
  nrm use taobao
  ```
  
   
  
   
  
  ------
  
   
  
  ps：r_name镜像名字， r_url镜像地址
  
  **在nrm添加自己的镜像地址**
  
  ```
  nrm add r_name r_url
  ```
  
  **删除**
  
  ```
  nrm del r_name
  ```
  
  **测试镜像的相应速度**
  
  ```
  nrm test r_name
  ```

## node

### 基础介绍

在 Node 中，采用 EcmaScript 进行编码

没有 BOM、DOM

和浏览器中的 JavaScript 不一样

浏览器中的 JavaScript 是没有文件操作的能力的

但是 Node 中的 JavaScript 具有文件操作的能力

### 模块化

使用 require 方法加载 fs 核心模块

- - 在 Node 中没有全局作用域的概念
  - 在 Node 中，只能通过 require 方法来加载执行多个 JavaScript 脚本文件
  - require 加载只能是执行其中的代码，文件与文件之间由于是模块作用域，所以不会有污染的问题
    - 模块完全是封闭的
    - 外部无法访问内部
    - 内部也无法访问外部
  - 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突污染的问题
  - 但是某些情况下，模块与模块是需要进行通信的
  - 在每个模块中，都提供了一个对象：`exports`
  - 该对象默认是一个空对象
  - 你要做的就是把需要被外部访问使用的成员手动的挂载到 `exports` 接口对象中
  - 然后谁来 `require` 这个模块，谁就可以得到模块内部的 `exports` 接口对象
  - 还有其它的一些规则，具体后面讲，以及如何在项目中去使用这种编程方式，会通过后面的案例来处理
- 核心模块
  - 核心模块是由 Node 提供的一个个的具名的模块，它们都有自己特殊的名称标识，例如
    - fs 文件操作模块
    - http 网络服务构建模块
    - os 操作系统信息模块
    - path 路径处理模块
    - 。。。。
  - 所有核心模块在使用的时候都必须手动的先使用 `require` 方法来加载，然后才可以使用，例如：
    - `var fs = require('fs')

#### 读写模块

```javascript
var fs = require("fs")
```

fs 是 file-system 的简写，就是文件系统的意思

在 Node 中如果想要进行文件操作，就必须引入 fs 这个核心模块

在 fs 这个核心模块中，就提供了所有的文件操作相关的 API

##### fs.readFile的使用

fs.readFile 就是用来读取文件的

```javascript
fs.readFile('.dataa.txt', function (error, data) {
 if (error) {
    console.log('读取文件失败了')
  } else {
    console.log(data.toString())
  }
})
```

2. 读取文件

 第一个参数就是要读取的文件路径

第二个参数是一个回调函数

######   成功

​       data 数据

​        error null

######   失败

​       data undefined没有数据

​         error 错误对象

<Buffer 68 65 6c 6c 6f 20 6e 6f 64 65 6a 73 0d 0a>

文件中存储的其实都是二进制数据 0 1

这里为什么看到的不是 0 和 1 呢？原因是二进制转为 16 进制了

但是无论是二进制01还是16进制，人类都不认识

所以我们可以通过 toString 方法把其转为我们能认识的字符

console.log(data)

console.log(error)

 console.log(data)

 在这里就可以通过判断 error 来确认是否有错误发生

##### fs.writeFile使用

```javascript
fs.writeFile('.data你好.md', '大家好，给大家介绍一下，我是Node.js', function (error)  if (error) {
    console.log('写入失败')
  } else {
    console.log('写入成功了')
  }
})
```

第一个参数：文件路径

 第二个参数：文件内容

 第三个参数：回调函数

​    erro

​    成功：

 文件写入成功

error 是 null

  失败：

文件写入失败

error 就是错误对象

#### http模块

```javascript
var http = require('http')
var server = http.createServer()
server.on('request', function () {
  console.log('收到客户端的请求了')
})
server.listen(3000, function () {
  console.log('服务器启动成功了，可以通过 http:127.0.0.1:3000 来进行访问')
})
```

##### 服务器要干嘛

   提供服务：对 数据的服务

   发请求

   接收请求

   处理请求

   给个反馈（发送响应）

   注册 request 请求事件

   当客户端请求过来，就会自动触发服务器的 request 请求事件，然后执行

##### http模块参数

   request 请求事件处理函数，需要接收两个参数：

######   Request 请求对象

   请求对象可以用来获取客户端的一些请求信息，例如请求路径

###### Response 响应对象

​      响应对象可以用来给客户端发送响应消息

###### response步骤

response 对象有一个方法：write 可以用来给客户端发送响应数据

write 可以使用多次，但是最后一定要使用 end 来结束响应，否则客户端会一直等待

告诉客户端，我的话说完了，你可以呈递给用户了

上面的方式比较麻烦，推荐使用更简单的方式，直接 end 的同时发送响应数据

 res.end('hello nodejs')

根据不同的请求路径发送不同的响应结果

\1. 获取请求路径

​     req.url 获取到的是端口号之后的那一部分路径

​     也就是说所有的 url 都是以  开头的

  \2. 判断路径处理响应

 响应内容只能是二进制数据或者字符串

​     数字

​     对象

​     数组

​     布尔值

##### path模块

- path 模块
- __dirname 和 __filename
  - **动态的** 获取当前文件或者文件所处目录的绝对路径
  - 用来解决文件操作路劲的相对路径问题
  - 因为在文件操作中，相对路径相对于执行 `node` 命令所处的目录
  - 所以为了尽量避免这个问题，都建议文件操作的相对路劲都转为：**动态的绝对路径**
  - 方式：`path.join(__dirname, '文件名')

##### 端口

ip 地址用来定位计算机

端口号用来定位具体的应用程序

 所有需要联网通信的应用程序都会占用一个端口号

```javascript
server.on('request', function (req, res) {
  console.log('收到请求了，请求路径是：' + req.url)
  console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)

  res.end('hello nodejs')
})
```

```javascript
 res.setHeader('Content-Type', 'textplain; charset=utf-8')
  res.end('hello 世界')
```

 在服务端默认发送的数据，其实是 utf8 编码的内容

  但是浏览器不知道你是 utf8 编码的内容

  浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析

  中文操作系统默认是 gbk

  解决方法就是正确的告诉浏览器我给你发送的内容是什么编码的

  在 http 协议中，Content-Type 就是用来告知对方我给你发送的数据内容是什么类型

######  关于Content-Type的类型

[Content-Type]: https:developer.mozilla.orgzh-CN/docs/Web/HTTP/Headers/Content-Type	"HTML"

![ip地址和端口](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\01\ip地址和端口号.png)

#### 重定向

如何在 Node 中实现服务器重定向

- header('location')
  - 301 永久重定向 浏览器会记住
    - a.com b.com
    - a 浏览器不会请求 a 了
    - 直接去跳到 b 了
  - 302 临时重定向 浏览器不记忆
    - a.com b.com
    - a.com 还会请求 a
    - a 告诉浏览器你往 b

### 模板引擎的使用

#### art -template的引入

 art-template
 art-template 不仅可以在浏览器使用，也可以在 node 中使用

 安装：
```javascript
    npm install art-template
```
    该命令在哪执行就会把包下载到哪里。默认会下载到 node_modules 目录中
    node_modules 不要改，也不支持改。

 在 Node 中使用 art-template 模板引擎
 模板引起最早就是诞生于服务器领域，后来才发展到了前端。

 1. 安装 npm install art-template
 2. 在需要使用的文件模块中加载 art-template
    只需要使用 require 方法加载就可以了：require('art-template')
    参数中的 art-template 就是你下载的包的名字
    也就是说你 isntall 的名字是什么，则你 require 中的就是什么
 3. 查文档，使用模板引擎的 API
      默认读取到的 data 是二进制数据
      而模板引擎的 render 方法需要接收的是字符串
      所以我们在这里需要把 data 二进制数据转为 字符串 才可以给模板引擎使用
  4. ![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\02\code\服务端渲染.png)
  5. ![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\02\code\客户端渲染.png)
  ```javascript
  var template = require('art-template')
var fs = require('fs')
 var tplStr = `
 <!DOCTYPE html>
 <html lang="en">
 <head>
   <meta charset="UTF-8">
   <title>Document<title>
 <head>
 <body>
   <p>大家好，我叫：{{ name }}<p>
   <p>我今年 {{ age }} 岁了<p>
   <h1>我来自 {{ province }}<h1>
   <p>我喜欢：{{each hobbies}} {{ $value }} {{each}}<p>
 <body>
 <html>
 `
  fs.readFile('.tpl.html', function (err, data) {
  if (err) {
    return console.log('读取文件失败了')
  }
  var ret = template.render(data.toString(), {
    name: 'Jack',
    age: 18,
    province: '北京市',
    hobbies: [
      '写代码',
      '唱歌',
      '打游戏'
    ],
    title: '个人'
  })

  console.log(ret)
})
![服务端渲染](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\02\服务端渲染.png)
  ```



#### 前端渲染和后端渲染

- 代码风格
- 无分号
  - `(`
  - `[`
  - `
  - 最好前面补分号，避免一些问题
  - 《编写可维护的 JavaScript》
  - 不仅是功能，还要写的漂亮
- 服务端渲染
  - 说白了就是在服务端使用模板引擎
  - 模板引擎最早诞生于服务端，后来才发展到了前端
- 服务端渲染和客户端渲染的区别
  - 客户端渲染不利于 SEO 搜索引擎优化
  - 服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的
  - 所以你会发现真正的网站既不是纯异步也不是纯服务端渲染出来的
  - 而是两者结合来做的
  - 例如京东的商品列表就采用的是服务端渲染，目的了为了 SEO 搜索引擎优化
  - 而它的商品评论列表为了用户体验，而且也不需要 SEO 优化，所以采用是客户端渲染

## 

###  模块化

#### module.exports和exports的区分

 在 Node 中，每个模块内部都有一个自己的 module 对象
 该 module 对象中，有一个成员叫：exports 也是一个对象
 也就是说如果你需要对外导出成员，只需要把导出的成员挂载到 module.exports 中

 我们发现，每次导出接口成员的时候都通过 module.exports.xxx = xxx 的方式很麻烦，点儿的太多了
 所以，Node 为了简化你的操作，专门提供了一个变量：exports 等于 module.exports

 var module = {
   exports: {
     foo: 'bar',
     add: function
   }
 }

 也就是说在模块中还有这么一句代码
 var exports = module.exports

 module.exports.foo = 'bar'

 module.exports.add = function (x, y) {
   return x + y
 }

 两者一致，那就说明，我可以使用任意一方来导出内部成员
 console.log(exports === module.exports)

 exports.foo = 'bar'
 module.exports.add = function (x, y) {
   return x + y
 }

 当一个模块需要导出单个成员的时候
 直接给 exports 赋值是不管用的

 exports.a = 123

 exports = {}
 exports.foo = 'bar'

 module.exports.b = 456

 给 exports 赋值会断开和 module.exports 之间的引用
 同理，给 module.exports 重新赋值也会断开

 这里导致 exports !== module.exports
 module.exports = {
   foo: 'bar'
 }

  但是这里又重新建立两者的引用关系
 exports = module.exports

 exports.foo = 'hello'

 {foo: bar}
exports.foo = 'bar'


 {foo: bar, a: 123}
module.exports.a = 123

 exports !== module.exports
 最终 return 的是 module.exports
 所以无论你 exports 中的成员是什么都没用
exports = {
  a: 456
}

 {foo: 'haha', a: 123}
module.exports.foo = 'haha'

 没关系，混淆你的
exports.c = 456

 重新建立了和 module.exports 之间的引用关系了
exports = module.exports

 由于在上面建立了引用关系，所以这里是生效的
 {foo: 'haha', a: 789}
exports.a = 789

 前面再牛逼，在这里都全部推翻了，重新赋值
 最终得到的是 Function
module.exports = function () {
  console.log('hello')
}

------

 真正去使用的时候：
    导出多个成员：exports.xxx = xxx
    导出多个成员也可以：module.exports = {
                        }
    导出单个成员：module.exports

 谁来 require 我，谁就得到 module.exports
 默认在代码的最后有一句：
 一定要记住，最后 return 的是 module.exports
 不是 exports
 所以你给 exports 重新赋值不管用，
 return module.exports

#### 模块化加载

 如果是非路径形式的模块标识

 路径形式的模块：

  ./ 当前目录，不可省略

  ../ 上一级目录，不可省略

  /xxx 几乎不用

  d:/a/foo.js 几乎不用

  首位的 / 在这里表示的是当前文件模块所属磁盘根路径

  .js 后缀名可以省略

 require('./foo.js')

 核心模块的本质也是文件

 核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了

 require('fs')

 require('http')

 第三方模块

 凡是第三方模块都必须通过 npm 来下载

 使用的时候就可以通过 require('包名') 的方式来进行加载才可以使用

 不可能有任何一个第三方包和核心模块的名字是一样的

 既不是核心模块、也不是路径形式的模块

​    先找到当前文件所处目录中的 node_modules 目录

​    node_modules/art-template

​    node_modules/art-template/package.json 文件

​    node_modules/art-template/package.json 文件中的 main 属性

​    main 属性中就记录了 art-template 的入口模块

​    然后加载使用这个第三方包

​    实际上最终加载的还是文件

​    如果 package.json 文件不存在或者 main 指定的入口模块是也没有

​    则 node 会自动找该目录下的 index.js

​    也就是说 index.js 会作为一个默认备选项

​    

​    如果以上所有任何一个条件都不成立，则会进入上一级目录中的 node_modules 目录查找

​    如果上一级还没有，则继续往上上一级查找

​    。。。

​    如果直到当前磁盘根目录还找不到，最后报错：

​      can not find module xxx

 var template = require('art-template')

 

 注意：我们一个项目有且只有一个 node_modules，放在项目根目录中，这样的话项目中所有的子目录中的代码都可以加载到第三方包

 不会出现有多个 node_modules

 模块查找机制

​    优先从缓存加载

​    核心模块

​    路径形式的文件模块

​    第三方模块

​      node_modules/art-template/

​      node_modules/art-template/package.json

​      node_modules/art-template/package.json main

​      index.js 备选项

​      进入上一级目录找 node_modules

​      按照这个规则依次往上找，直到磁盘根目录还找不到，最后报错：Can not find moudle xxx

​    一个项目有且仅有一个 node_modules 而且是存放到项目的根目录

#### 模块化注意

​     咱们所使用的所有文件操作的 API 都是异步的
 就像你的 ajax 请求一样
 文件操作中的相对路径可以省略 ./
 fs.readFile('data/a.txt', function (err, data) {
   if (err) {
​     return console.log('读取失败')
   }
   console.log(data.toString())
 })

 在模块加载中，相对路径中的 ./ 不能省略
 Error: Cannot find module 'data/foo.js'
 require('data/foo.js')

 require('./data/foo.js')('hello')

 在文件操作的相对路径中
    ./data/a.txt 相对于当前目录
    data/a.txt   相对于当前目录
    /data/a.txt  绝对路径，当前文件模块所处磁盘根目录
    c:/xx/xx...  绝对路径
 fs.readFile('./data/a.txt', function (err, data) {
   if (err) {
     console.log(err)
     return console.log('读取失败')
   }
   console.log(data.toString())
 })

 这里如果忽略了 . 则也是磁盘根目录

**在 Node 没有全局作用域，它是文件模块作用域**

**模块是独立，不能因为 a 加载过 fs 了 b 就不需要，这是错误的理解**

 **正确的做法应该是，a 需要 fs 则 a 就加载 fs ，b 需要 fs 则 b 就加载 fs**

### express的使用

 0. 安装

 1. 引包
```javascript
var express = require('express')
var app = express()

app.use('/public/', express.static('./public/'))

app.use('/static/', express.static('./static/'))

app.use('/node_modules/', express.static('./node_modules/'))

app.get('/about', function (req, res) {

   在 Express 中可以直接 req.query 来获取查询字符串参数

  console.log(req.query)

  res.send('你好，我是 Express!')
})

app.get('/pinglun', function (req, res) {

   req.query

   在 Express 中使用模板引擎有更好的方式：res.render('文件名， {模板对象})

   可以自己尝试去看 art-template 官方文档：如何让 art-template 结合 Express 来使用

})
app.get('/', function (req, res) {

  res.send(`

<!DOCTYPE html>

<html lang="en">

  <head>

    <meta charset="UTF-8" />

​    <title>Document</title>

  </head>

<body>

  <h1>hello Express！你好</h1>

</body>

</html>

`)

})
app.listen(3000, function () {

  console.log('app is running at port 3000.')

})
})
```


 2. 创建你服务器应用程序

​    也就是原来的 http.createServer

 3. 在 Express 中开放资源就是一个 API 的事儿

 公开指定目录

 只要这样做了，你就可以直接通过 /public/xx 的方式访问 public 目录中的所有资源了

4. 模板引擎，在 Express 也是一个 API 的事儿

 得到路径

 当服务器收到 get 请求 / 的时候，执行回调处理函数

 5. app.listen相当于 server.listen

  #### 路由模块

  router.js 路由模块
  职责：
  处理路由
  根据不同的请求方法+请求路径设置具体的请求处理函数
 模块职责要单一，不要乱写
  我们划分模块的目的就是为了增强项目代码的可维护性,提升开发效率

Express 提供了一种更好的方式
 专门用来包装路由的
var express = require('express')

1. 创建一个路由容器
   var router = express.Router()
2. 把路由都挂载到 router 路由容器中,router.get或router.post 处理请求

3. 最后把router.js导入app.js中     var router = require(‘./router’)，采用app.use(router)方式进行挂在app.js中

4. 浏览器收到 HTML 响应内容之后，就要开始从上到下依次解析，

   ​    当在解析的过程中，如果发现：

   ​      link

   ​      script

   ​      img

   ​      iframe

   ​      video

   ​      audio

   ​    等带有 src 或者 href（link） 属性标签（具有外链的资源）的时候，浏览器会自动对这些资源发起新的请求。

      -->

      <!-- 

   ​      注意：在服务端中，文件中的路径就不要去写相对路径了。

   ​      因为这个时候所有的资源都是通过 url 标识来获取的

   ​      我的服务器开放了 /public/ 目录

   ​      所以这里的请求路径都写成：/public/xxx

   ​      / 在这里就是 url 根路径的意思。

   ​      浏览器在真正发请求的时候会最终把 http:127.0.0.1:3000 拼上

   ​      不要再想文件路径了，把所有的路径都想象成 url 地址

   ​    -->

   5. 以前表单是如何提交的？

   ​      表单中需要提交的表单控件元素必须具有 name 属性

   ​      表单提交分为：

   ​        \1. 默认的提交行为

   ​        \2. 表单异步提交

   ​        action 就是表单提交的地址，说白了就是请求的 url 地址

   ​        method 请求方法

   ​            get

   ​            post

   ​     -->

#### 入口js的作用

  app.js 入门模块

   职责：

  **创建服务**

​    **做一些服务相关配置**

   **模板引擎**

   **body-parser 解析表单 post 请求体**

  **提供静态资源服务**

​    **挂载路由**

  **监听端口启动服务**

#### express中使用模板引擎进行

 配置使用 art-template 模板引擎

 第一个参数，表示，当渲染以 .art 结尾的文件的时候，使用 art-template 模板引擎

 express-art-template 是专门用来在 Express 中把 art-template 整合到 Express 中

 虽然外面这里不需要记载 art-template 但是也必须安装

 原因就在于 express-art-template 依赖了 art-template

 Express 为 Response 相应对象提供了一个方法：render

 render 方法默认是不可以使用，但是如果配置了模板引擎就可以使用了

 res.render('html模板名', {模板数据})

 第一个参数不能写路径，默认会去项目中的 views 目录查找该模板文件

 也就是说 Express 有一个约定：开发人员把所有的视图文件都放到 views 目录中

 如果想要修改默认的 views 目录，则可以

 app.set('views', render函数的默认路径)

 配置 body-parser 中间件（插件，专门用来解析表单 POST 请求体）

 parse application/x-www-form-urlencoded

```javascript
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

app.use('/public/', express.static('./public/'))
app.engine('html', require('express-art-template'))
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
var comments = [{
    name: '张三',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三2',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三3',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三4',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三5',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  }
]

app.get('/', function (req, res) {
  res.render('index.html', {
    comments: comments
  })
})

app.get('/post', function (req, res) {
  res.render('post.html')
})

app.post('/post', function (req, res) {
   1. 获取表单 POST 请求体数据
   2. 处理
   3. 发送响应

   req.query 只能拿 get 请求参数
   console.log(req.query)

  var comment = req.body
  comment.dateTime = '2017-11-5 10:58:51'
  comments.unshift(comment)

   res.send
   res.redirect
   这些方法 Express 会自动结束响应
  res.redirect('/')
   res.statusCode = 302
   res.setHeader('Location', '/') 
})

 app.get('/pinglun', function (req, res) {
   var comment = req.query
   comment.dateTime = '2017-11-5 10:58:51'
   comments.unshift(comment)
   res.redirect('/')
    res.statusCode = 302
    res.setHeader('Location', '/')
 })

app.listen(3000, function () {
  console.log('running...')
})


```



#### **crud**的使用

  数据操作文件模块

 职责：操作文件中的数据，只处理数据，不关心业务

  这里才是我们学习 Node 的精华部分：奥义之所在

  封装异步 API

 咱们所使用的所有文件操作的 API 都是异步的

 就像你的 ajax 请求一样

 文件操作中的相对路径可以省略 ./

 fs.readFile('data/a.txt', function (err, data) {

   if (err) {

​     return console.log('读取失败')

   }

   console.log(data.toString())

 })

 在模块加载中，相对路径中的 ./ 不能省略

 Error: Cannot find module 'data/foo.js'

 require('data/foo.js')

 require('./data/foo.js')('hello')

 在文件操作的相对路径中

​    ./data/a.txt 相对于当前目录

​    data/a.txt   相对于当前目录

​    /data/a.txt  绝对路径，当前文件模块所处磁盘根目录

​    c:/xx/xx...  绝对路径

 fs.readFile('./data/a.txt', function (err, data) {

   if (err) {

​     console.log(err)

​     return console.log('读取失败')

   }

   console.log(data.toString())

 })

 这里如果忽略了 . 则也是磁盘根目录



#### 中间件的使用

##### 中间件的作用

   解析表单 get 请求体

   解析表单 post 请求体

   解析 Cookie

   处理 Session

  使用模板引擎

```
var http = require('http')
var url = require('url')

var cookie = require('./middlewares/cookie')
var postBody = require('./middlewares/post-body')
var query = require('./middlewares/query')
var session = require('./middlewares/session')

var server = http.createServer(function (req, res) {
   解析表单 get 请求体
   解析表单 post 请求体
   解析 Cookie
   处理 Session
   使用模板引擎
   console.log(req.query)
   console.log(req.body)
   console.log(req.cookies)
   console.log(req.session)

   解析请求地址中的 get 参数
   var urlObj = url.parse(req.url, true)
   req.query = urlObj.query
  query(req, res)

   解析请求地址中的 post 参数
   req.body = {
     foo: 'bar'
   }
  postBody(req, res)

   解析 Cookie
   req.cookies = {
     isLogin: true
   }
  cookie(req, res)

   配置 Session
   req.session = {}
  session(req, res)

   配置模板引擎
  res.render = function () {
    
  }

  if (req.url === 'xxx') {
     处理
     query、body、cookies、session、render API 成员
  } else if (url === 'xx') {
     处理
  }


   上面的过程都是了为了在后面做具体业务操作处理的时候更方便
})

server.listen(3000, function () {
  console.log('3000. running...')
})

```

##### 中间件中next的使用

 中间件：处理请求的，本质就是个函数

 在 Express 中，对中间件有几种分类

 当请求进来，会从第一个中间件开始进行匹配

​    如果匹配，则进来

​       如果请求进入中间件之后，没有调用 next 则代码会停在当前中间件

​       如果调用了 next 则继续向后找到第一个匹配的中间件

​    如果不匹配，则继续判断匹配下一个中间件

​    

 不关心请求路径和请求方法的中间件

 也就是说任何请求都会进入这个中间件

 中间件本身是一个方法，该方法接收三个参数：

​    Request 请求对象

​    Response 响应对象

​    next     下一个中间件

 当一个请求进入一个中间件之后，如果不调用 next 则会停留在当前中间件

 所以 next 是一个方法，用来调用下一个中间件的

 调用 next 方法也是要匹配的（不是调用紧挨着的那个）

##### next传参

​      return res.status(500).send('Server Error')

​       当调用 next 的时候，如果传递了参数，则直接往后找到带有 四个参数的应用程序级别中间件

​       当发生错误的时候，我们可以调用 next 传递错误对象

​       然后就会被全局错误处理中间件匹配到并处理之

```javascript
var express = require('express')
var fs = require('fs')

var app = express()

 app.get('/abc', function (req, res, next) {
   console.log('abc')
    req.foo = 'bar'
   req.body = {}
   next()
 })

 app.get('/abc', function (req, res, next) {
   console.log(req.body)
   console.log('abc 2')
 })

app.get('/', function (req, res, next) {
  fs.readFile('.d/sa./d.sa/.dsa', function (err, data) {
    if (err) {
       return res.status(500).send('Server Error')
       当调用 next 的时候，如果传递了参数，则直接往后找到带有 四个参数的应用程序级别中间件
       当发生错误的时候，我们可以调用 next 传递错误对象
       然后就会被全局错误处理中间件匹配到并处理之
      next(err)
    }
  })
})

app.get('/', function (req, res, next) {
  console.log('/ 2')
})



app.get('/a', function (req, res, next) {
  fs.readFile('./abc', function (err, data) {
    if (err) {
       return res.status(500).send('Server Error') 
      next(err)
    }
  })
})

app.use(function (req, res, next) {
  res.send('404')
})

 配置错误处理中间件
app.use(function (err, req, res, next) {
  res.status(500).send(err.message)
})

app.listen(3000, function () {
  console.log('app is running at port 3000.')
})


```



### promise解决异步问题
#### promise的使用

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\promiseAPI代码图示.png)

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\promise链式调用.png)

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\promise容器概念.png)

```
var fs = require('fs')

var p1 = new Promise(function (resolve, reject) {
  fs.readFile('./data/a.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p2 = new Promise(function (resolve, reject) {
  fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p3 = new Promise(function (resolve, reject) {
  fs.readFile('./data/c.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

p1
  .then(function (data) {
    console.log(data)
     当 p1 读取成功的时候
     当前函数中 return 的结果就可以在后面的 then 中 function 接收到
     当你 return 123 后面就接收到 123
          return 'hello' 后面就接收到 'hello'
          没有 return 后面收到的就是 undefined
     上面那些 return 的数据没什么卵用
     真正有用的是：我们可以 return 一个 Promise 对象
     当 return 一个 Promise 对象的时候，后续的 then 中的 方法的第一个参数会作为 p2 的 resolve
     
    return p2
  }, function (err) {
    console.log('读取文件失败了', err)
  })
  .then(function (data) {
    console.log(data)
    return p3
  })
  .then(function (data) {
    console.log(data)
    console.log('end')
  })

```



```
var fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./data/a.txt')
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/b.txt')
  })
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/c.txt')
  })
  .then(function (data) {
    console.log(data)
  })

```



#### 异步封装API

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\回调函数.png)

在crud中对文件进行读取，数据处理api的封装，后导给router.js进行调用

## mongodb的使用

- MongoDB 数据库
  - MongoDB 的数据存储结构
    - 数据库
    - 集合（表）
    - 文档（表记录）
- MongoDB 官方有一个 mongodb 的包可以用来操作 MongoDB 数据库
  - 这个确实和强大，但是比较原始，麻烦，所以咱们不使用它
- mongoose
  - 真正在公司进行开发，使用的是 mongoose 这个第三方包
  - 它是基于 MongoDB 官方的 mongodb 包进一步做了封装
  - 可以提高开发效率
  - 让你操作 MongoDB 数据库更方便

### mongodb的使用步骤

 **创建一个模型**

 **就是在设计数据库**

 **MongoDB 是动态的，非常灵活，只需要在代码中设计你的数据库就可以了**

 **mongoose 这个包就可以让你的设计编写过程变的非常的简单**

1. 连接数据库，指定连接的数据库不需要存在，当你插入第一条数据之后就会自动被创建出来

2.  设计文档结构（表结构），字段名称就是表结构中的属性名称，约束的目的是为了保证数据的完整性，不要有脏数据

3.  将文档结构发布为模型

      mongoose.model 方法就是用来将一个架构发布为 model

      第一个参数：传入一个大写名词单数字符串用来表示你的数据库名称

   ​                mongoose 会自动将大写名词的字符串生成 小写复数 的集合名称

   ​                例如这里的 User 最终会变为 users 集合名称

      第二个参数：架构 Schema

     

      返回值：模型构造函数

   4.当我们有了模型构造函数之后，就可以使用这个构造函数对 users 集合中的数据为所欲为了（增删改查）

   ```javascript
   var mongoose = require('mongoose')
   
   var Schema = mongoose.Schema
   mongoose.connect('mongodb:localhost/itcast')
   
   var userSchema = new Schema({
     username: {
       type: String,
       required: true  必须有
     },
     password: {
       type: String,
       required: true
     },
     email: {
       type: String
     }
   })
   
   var User = mongoose.model('User', userSchema)
   
   #region /新增数据
   **********************
   var admin = new User({
     username: 'zs',
     password: '123456',
     email: 'admin@admin.com'
   })
   
   admin.save(function (err, ret) {
     if (err) {
       console.log('保存失败')
     } else {
       console.log('保存成功')
       console.log(ret)
     }
   })
   **********************
   #endregion /新增数据
   **********************
   
   
   
   
   **********************
   #region /查询数据
   **********************
   
   User.find({
     username: 'zs'
   }, function (err, ret) {
     if (err) {
       console.log('查询失败')
     } else {
       console.log(ret)
     }
   })
   
   User.findOne({
     username: 'zs'
   }, function (err, ret) {
     if (err) {
       console.log('查询失败')
     } else {
       console.log(ret)
     }
   })
   **********************
   #endregion /查询数据
   **********************
   
   
   
   **********************
   #region /删除数据
   **********************
   User.remove({
     username: 'zs'
   }, function (err, ret) {
     if (err) {
       console.log('删除失败')
     } else {
       console.log('删除成功')
       console.log(ret)
     }
   })
   **********************
   #endregion /删除数据
   **********************
   
   
   **********************
   #region /更新数据
   **********************
   User.findByIdAndUpdate('5a001b23d219eb00c8581184', {
     password: '123'
   }, function (err, ret) {
     if (err) {
       console.log('更新失败')
     } else {
       console.log('更新成功')
     }
   })
   **********************
   #endregion /更新数据
   **********************
   
   ```

   

```javascript
User.findOne({ username: 'aaa' }, function (user) {
  if (user) {
    console.log('已存在')
  } else {
    new User({
      username: 'aaa',
      password: '123',
      email: 'dsadas'
    }).save(function () {
      
    })
  }
})

User.findOne({
    username: 'aaa'
  })
  .then(function (user) {
    if (user) {
       用户已存在，不能注册
      console.log('用户已存在')
    } else {
       用户不存在，可以注册
      return new User({
        username: 'aaa',
        password: '123',
        email: 'dsadas'
      }).save()
    }
  })
  .then(function (ret) {
  })

User.find({
  username: 'zs'
}, function (err, ret) {
  if (err) {
    console.log('查询失败')
 } else {
    console.log(ret)
  }
})
```

## vue

### mvvm框架

![](D:\后台\15--Vuejs（11天）\资料\day1\笔记\01.MVC和MVVM的关系图解.png)

### 为什么要学vue

企业中，使用框架，能够提高开发的效率；

提高开发效率的发展历程：原生JS -> Jquery之类的类库 -> 前端模板引擎 -> Angular.js / Vue.js（能够帮助我们减少不必要的DOM操作；提高渲染效率；双向数据绑定的概念【通过框架提供的指令，我们前端程序员只需要关心数据的业务逻辑，不再关心DOM是如何渲染的了】）

在Vue中，一个核心的概念，就是让用户不再操作DOM元素，解放了用户的双手，让程序员可以更多的时间去关注业务逻辑；框架和库的区别

### 框架和库的区别

- 框架：是一套完整的解决方案；对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。

- node 中的 express；



- 库（插件）：提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。

- 1. 从Jquery 切换到 Zepto
- 2. 从 EJS 切换到 art-template



### vue的基本使用和语法

```
<!-- 将来 new 的Vue实例，会控制这个 元素中的所有内容 -->
  <!-- Vue 实例所控制的这个元素区域，就是我们的 V  -->
  <div id="app">
    <p>{{ msg }}</p>
  </div>

  <script>
    // 2. 创建一个Vue的实例
    // 当我们导入包之后，在浏览器的内存中，就多了一个 Vue 构造函数
    //  注意：我们 new 出来的这个 vm 对象，就是我们 MVVM中的 VM调度者
    var vm = new Vue({
      el: '#app',  // 表示，当前我们 new 的这个 Vue 实例，要控制页面上的哪个区域
      // 这里的 data 就是 MVVM中的 M，专门用来保存 每个页面的数据的
      data: { // data 属性中，存放的是 el 中要用到的数据
        msg: '欢迎学习Vue' // 通过 Vue 提供的指令，很方便的就能把数据渲染到页面上，程序员不再手动操作DOM元素了【前端的Vue之类的框架，不提倡我们去手动操作DOM元素了】
      }
    })
```

在 VM实例中，如果想要获取 data 上的数据，或者 想要调用 methods 中的 方法，必须通过 this.数据属性名  或  this.方法名 来进行访问，这里的this，就表示 我们 new 出来的  VM 实例对象;

VM实例，会监听自己身上 data 中所有数据的改变，只要数据一发生变化，就会自动把 最新的数据，从data 上同步到页面中去；【好处：程序员只需要关心数据，不需要考虑如何重新渲染DOM页面】

#### vue中事件的冒泡和阻止默认行为

**使用  .stop  阻止冒泡**

**使用 .prevent 阻止默认行为**

**使用  .capture 实现捕获触发事件的机制**

**使用 .self 实现只有点击当前元素时候，才会触发事件处理函数**

**使用 .once 只触发一次事件处理函数**

#### 插值表达式

#### v-html

#### v-cloak

#### v-text

 v-text和插值表达式的区别<!-- v-text会覆盖元素中原本的内容，但是 插值表达式  只会替换自己的这个占位符，不会把 整个元素的内容清空 -->

#### v-bind

是 Vue中，提供的用于绑定属性的指令

<input type="button" value="按钮" v-bind:title="mytitle + '123'"> 

mytitle是vue中的变量值

title是原先html元素自带的属性

v-bind: 指令可以被简写为 :要绑定的属性

<!--  在vue中绑定样式两种方式  v-bind:class   v-bind:style -->

#### v-on

 <!-- Vue 中提供了 v-on: 事件绑定机制 -->

 <!-- <input type="button" value="按钮" :title="mytitle + '123'" v-      on:click="show"> -->

show是VUE中的方法

click是html元素的点击事件

v-on: 指令可以被简写为@要绑定的属性

#### v-model

  <!-- v-bind 只能实现数据的单向绑定，从 M 自动绑定到 V， 无法实现数据的双向绑定  -->

​    <!-- <input type="text" v-bind:value="msg" style="width:100%;"> -->

​    <!-- 使用  v-model 指令，可以实现 表单元素和 Model 中数据的双向数据绑定 -->

​    <!-- 注意： v-model 只能运用在 表单元素中 -->

#### v-for

```javascript
<p v-for="(item, i) in list">索引值：{{i}} --- 每一项：{{item}}</p>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        list: [1, 2, 3, 4, 5, 6]
      },
      methods: {}
    });
  </script>
```

```javascript
 <div id="app">
    <p v-for="(user, i) in list">Id：{{ user.id }} --- 名字：{{ user.name }} --- 索引：{{i}}</p>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        list: [
          { id: 1, name: 'zs1' },
          { id: 2, name: 'zs2' },
          { id: 3, name: 'zs3' },
          { id: 4, name: 'zs4' }
        ]
      },
      methods: {}
    });
  </script>
```

```javascript
<div id="app">
    <!-- 注意：在遍历对象身上的键值对的时候， 除了 有  val  key  ,在第三个位置还有 一个 索引  -->
    <p v-for="(val, key, i) in user">值是： {{ val }} --- 键是： {{key}} -- 索引： {{i}}</p>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        user: {
          id: 1,
          name: '托尼·屎大颗',
          gender: '男'
        }
      },
      methods: {}
    });
  </script>
```

```javascript
<div id="app">
    <!-- in 后面我们放过  普通数组，对象数组，对象， 还可以放数字 -->
    <!-- 注意：如果使用 v-for 迭代数字的话，前面的 count 值从 1 开始 -->
    <p v-for="count in 10">这是第 {{ count }} 次循环</p>
  </div>
```

```javascript
<div id="app">

    <div>
      <label>Id:
        <input type="text" v-model="id">
      </label>

      <label>Name:
        <input type="text" v-model="name">
      </label>

      <input type="button" value="添加" @click="add">
    </div>

    <!-- 注意： v-for 循环的时候，key 属性只能使用 number获取string -->
    <!-- 注意： key 在使用的时候，必须使用 v-bind 属性绑定的形式，指定 key 的值 -->
    <!-- 在组件中，使用v-for循环的时候，或者在一些特殊情况中，如果 v-for 有问题，必须 在使用 v-for 的同时，指定 唯一的 字符串/数字 类型 :key 值 -->
    <p v-for="item in list" :key="item.id">
      <input type="checkbox">{{item.id}} --- {{item.name}}
    </p>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        id: '',
        name: '',
        list: [
          { id: 1, name: '李斯' },
          { id: 2, name: '嬴政' },
          { id: 3, name: '赵高' },
          { id: 4, name: '韩非' },
          { id: 5, name: '荀子' }
        ]
      },
      methods: {
        add() { // 添加方法
          this.list.unshift({ id: this.id, name: this.name })
        }
      }
    });
  </script>
```

#### v-if

```html
<h3 v-if="flag">这是用v-if控制的元素</h3>
```

flag是定义在vue中的变量属性，当flag是false时,h3不会显示

#### v-show

```
 <h3 v-show="flag">这是用v-show控制的元素</h3>
```

flag是定义在vue中的变量属性，当flag是false时,h3不会显示

区别:

 <!-- v-if 的特点：每次都会重新删除或创建元素 -->

​    <!-- v-show 的特点： 每次不会重新进行DOM的删除和创建操作，只是切换了元素的 display:none 样式 -->

​    <!-- v-if 有较高的切换性能消耗 -->

​    <!-- v-show 有较高的初始渲染消耗 -->

### vue中的过滤器

```javascript
<div id="app">
    <p>{{ msg | msgFormat('疯狂+1', '123') | test }}</p>
  </div>

  <script>
    // 定义一个 Vue 全局的过滤器，名字叫做  msgFormat
    Vue.filter('msgFormat', function (msg, arg, arg2) {
      // 字符串的  replace 方法，第一个参数，除了可写一个 字符串之外，还可以定义一个正则
      return msg.replace(/单纯/g, arg + arg2)
    })

    Vue.filter('test', function (msg) {
      return msg + '========'
    })


    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '曾经，我也是一个单纯的少年，单纯的我，傻傻的问，谁是世界上最单纯的男人'
      },
      methods: {}
    });
  </script>
```

Vue.js 允许你自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：**双花括号插值和 v-bind 表达式** (后者从 2.1.0+ 开始支持)。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符号指示：

```
<!-- 在双花括号中 -->
{{ message | capitalize }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>
```

你可以在一个组件的选项中定义本地的过滤器：

```
filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
```

或者在创建 Vue 实例之前全局定义过滤器：

```
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})

new Vue({
  // ...
})
```

当全局过滤器和局部过滤器重名时，会采用局部过滤器。

下面这个例子用到了 `capitalize` 过滤器：

John

过滤器函数总接收表达式的值 (之前的操作链的结果) 作为第一个参数。在上述例子中，`capitalize` 过滤器函数将会收到 `message` 的值作为第一个参数。

过滤器可以串联：

```
{{ message | filterA | filterB }}
```

在这个例子中，`filterA` 被定义为接收单个参数的过滤器函数，表达式 `message` 的值将作为参数传入到函数中。然后继续调用同样被定义为接收单个参数的过滤器函数 `filterB`，将 `filterA` 的结果传递到 `filterB` 中。

过滤器是 JavaScript 函数，因此可以接收参数：

```
{{ message | filterA('arg1', arg2) }}
```

这里，`filterA` 被定义为接收三个参数的过滤器函数。其中 `message` 的值作为第一个参数，普通字符串 `'arg1'` 作为第二个参数，表达式 `arg2` 的值作为第三个参数。

### 自定义指令

 <!-- 注意： Vue中所有的指令，在调用的时候，都以 v- 开头 -->

```javascript
 // 使用  Vue.directive() 定义全局的指令  v-focus
    // 其中：参数1 ： 指令的名称，注意，在定义的时候，指令的名称前面，不需要加 v- 前缀, 
    // 但是： 在调用的时候，必须 在指令名称前 加上 v- 前缀来进行调用
    //  参数2： 是一个对象，这个对象身上，有一些指令相关的函数，这些函数可以在特定的阶段，执行相关的操作
    Vue.directive('focus', {
      bind: function (el) { // 每当指令绑定到元素上的时候，会立即执行这个 bind 函数，只执行一次
        // 注意： 在每个 函数中，第一个参数，永远是 el ，表示 被绑定了指令的那个元素，这个 el 参数，是一个原生的JS对象
        // 在元素 刚绑定了指令的时候，还没有 插入到 DOM中去，这时候，调用 focus 方法没有作用
        //  因为，一个元素，只有插入DOM之后，才能获取焦点
        // el.focus()
      },
      inserted: function (el) {  // inserted 表示元素 插入到DOM中的时候，会执行 inserted 函数【触发1次】
        el.focus()
        // 和JS行为有关的操作，最好在 inserted 中去执行，放置 JS行为不生效
      },
      updated: function (el) {  // 当VNode更新的时候，会执行 updated， 可能会触发多次

      }
    })
```

```javascript
// 自定义一个 设置字体颜色的 指令
    Vue.directive('color', {
      // 样式，只要通过指令绑定给了元素，不管这个元素有没有被插入到页面中去，这个元素肯定有了一个内联的样式
      // 将来元素肯定会显示到页面中，这时候，浏览器的渲染引擎必然会解析样式，应用给这个元素
      bind: function (el, binding) {
        // el.style.color = 'red'
        // console.log(binding.name)
        // 和样式相关的操作，一般都可以在 bind 执行

        // console.log(binding.value)
        // console.log(binding.expression)

        el.style.color = binding.value
      }
    })
```

#### 钩子函数参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。

- ```
  binding
  ```

  ：一个对象，包含以下属性：

  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。

- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。

- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。



### 生命周期函数

- 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！
- [生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)：就是生命周期事件的别名而已；
- 生命周期钩子 = 生命周期函数 = 生命周期事件
- 主要的生命周期函数分类：

- 创建期间的生命周期函数：

- beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
- created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
- beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
- mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示

- 运行期间的生命周期函数：

- beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
- updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！

- 销毁期间的生命周期函数：

- beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
- destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

```javascript
   beforeCreate() { // 这是我们遇到的第一个生命周期函数，表示实例完全被创建出来之前，会执行它
        // console.log(this.msg)
        // this.show()
        // 注意： 在 beforeCreate 生命周期函数执行的时候，data 和 methods 中的 数据都还没有没初始化
      },
      created() { // 这是遇到的第二个生命周期函数
        // console.log(this.msg)
        // this.show()
        //  在 created 中，data 和 methods 都已经被初始化好了！
        // 如果要调用 methods 中的方法，或者操作 data 中的数据，最早，只能在 created 中操作
      },
      beforeMount() { // 这是遇到的第3个生命周期函数，表示 模板已经在内存中编辑完成了，但是尚未把 模板渲染到 页面中
        // console.log(document.getElementById('h3').innerText)
        // 在 beforeMount 执行的时候，页面中的元素，还没有被真正替换过来，只是之前写的一些模板字符串
      },
      mounted() { // 这是遇到的第4个生命周期函数，表示，内存中的模板，已经真实的挂载到了页面中，用户已经可以看到渲染好的页面了
        // console.log(document.getElementById('h3').innerText)
        // 注意： mounted 是 实例创建期间的最后一个生命周期函数，当执行完 mounted 就表示，实例已经被完全创建好了，此时，如果没有其它操作的话，这个实例，就静静的 躺在我们的内存中，一动不动
      },


      // 接下来的是运行中的两个事件
      beforeUpdate() { // 这时候，表示 我们的界面还没有被更新【数据被更新了吗？  数据肯定被更新了】
        /* console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
        console.log('data 中的 msg 数据是：' + this.msg) */
        // 得出结论： 当执行 beforeUpdate 的时候，页面中的显示的数据，还是旧的，此时 data 数据是最新的，页面尚未和 最新的数据保持同步
      },
      updated() {
        console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
        console.log('data 中的 msg 数据是：' + this.msg)
        // updated 事件执行的时候，页面和 data 数据已经保持同步了，都是最新的
      }
    });
```

![](D:\后台\15--Vuejs（11天）\资料\day2\笔记\lifecycle.png)

### vue-resource 实现 get, post, jsonp请求

除了 vue-resource 之外，还可以使用 `axios` 的第三方包实现实现数据的请求

1. 之前的学习中，如何发起数据请求？
2. 常见的数据请求类型？  get  post jsonp
3. 测试的URL请求资源地址：

- get请求地址： http://vue.studyit.io/api/getlunbo
- post请求地址：http://vue.studyit.io/api/post
- jsonp请求地址：http://vue.studyit.io/api/jsonp

4. JSONP的实现原理

- 由于浏览器的安全性限制，不允许AJAX访问 协议不同、域名不同、端口号不同的 数据接口，浏览器认为这种访问不安全；
- 可以通过动态创建script标签的形式，把script标签的src属性，指向数据接口的地址，因为script标签不存在跨域限制，这种数据获取方式，称作JSONP（注意：根据JSONP的实现原理，知晓，JSONP只支持Get请求）；
- 具体实现过程：

- 先在客户端定义一个回调方法，预定义对数据的操作；
- 再把这个回调方法的名称，通过URL传参的形式，提交到服务器的数据接口；
- 服务器数据接口组织好要发送给客户端的数据，再拿着客户端传递过来的回调方法名称，拼接出一个调用这个方法的字符串，发送给客户端去解析执行；
- 客户端拿到服务器返回的字符串之后，当作Script脚本去解析执行，这样就能够拿到JSONP的数据了；

- 带大家通过 Node.js ，来手动实现一个JSONP的请求例子

```javascript
const http = require('http');
    // 导入解析 URL 地址的核心模块
    const urlModule = require('url');

    const server = http.createServer();
    // 监听 服务器的 request 请求事件，处理每个请求
    server.on('request', (req, res) => {
      const url = req.url;

      // 解析客户端请求的URL地址
      var info = urlModule.parse(url, true);

      // 如果请求的 URL 地址是 /getjsonp ，则表示要获取JSONP类型的数据
      if (info.pathname === '/getjsonp') {
        // 获取客户端指定的回调函数的名称
        var cbName = info.query.callback;
        // 手动拼接要返回给客户端的数据对象
        var data = {
          name: 'zs',
          age: 22,
          gender: '男',
          hobby: ['吃饭', '睡觉', '运动']
        }
        // 拼接出一个方法的调用，在调用这个方法的时候，把要发送给客户端的数据，序列化为字符串，作为参数传递给这个调用的方法：
        var result = `${cbName}(${JSON.stringify(data)})`;
        // 将拼接好的方法的调用，返回给客户端去解析执行
        res.end(result);
      } else {
        res.end('404');
      }
    });

    server.listen(3000, () => {
      console.log('server running at http://127.0.0.1:3000');
    });
```

5. vue-resource 的配置步骤：

- 直接在页面中，通过`script`标签，引入 `vue-resource` 的脚本文件；
- 注意：引用的先后顺序是：先引用 `Vue` 的脚本文件，再引用 `vue-resource` 的脚本文件；

6. 发送get请求：

```javascript
getInfo() { // get 方式获取数据
  this.$http.get('http://127.0.0.1:8899/api/getlunbo').then(res => {
    console.log(res.body);
  })
}
```

7. 发送post请求：

   ```javascript
   postInfo() {
     var url = 'http://127.0.0.1:8899/api/post';
     // post 方法接收三个参数：
     // 参数1： 要请求的URL地址
     // 参数2： 要发送的数据对象
     // 参数3： 指定post提交的编码类型为 application/x-www-form-urlencoded
     this.$http.post(url, { name: 'zs' }, { emulateJSON: true }).then(res => {
       console.log(res.body);
     });
   }
   ```

   

8. 发送JSONP请求获取数据：

   ```javascript
   jsonpInfo() { // JSONP形式从服务器获取数据
     var url = 'http://127.0.0.1:8899/api/jsonp';
     this.$http.jsonp(url).then(res => {
       console.log(res.body);
     });
   }
   ```

### 组件

```javascript
<div id="app">
    <!-- 如果要使用组件，直接，把组件的名称，以 HTML 标签的形式，引入到页面中，即可 -->
    <mycom1></mycom1>
  </div>

  <script>
    // 1.1 使用 Vue.extend 来创建全局的Vue组件
    // var com1 = Vue.extend({
    //   template: '<h3>这是使用 Vue.extend 创建的组件</h3>' // 通过 template 属性，指定了组件要展示的HTML结构
    // })
    // 1.2 使用 Vue.component('组件的名称', 创建出来的组件模板对象)
    // Vue.component('myCom1', com1)
    // 如果使用 Vue.component 定义全局组件的时候，组件名称使用了 驼峰命名，则在引用组件的时候，需要把 大写的驼峰改为小写的字母，同时，两个单词之前，使用 - 链接；
    // 如果不使用驼峰,则直接拿名称来使用即可;
    // Vue.component('mycom1', com1)

    // Vue.component 第一个参数:组件的名称,将来在引用组件的时候,就是一个 标签形式 来引入 它的
    // 第二个参数: Vue.extend 创建的组件  ,其中 template 就是组件将来要展示的HTML内容
    Vue.component('mycom1', Vue.extend({
      template: '<h3>这是使用 Vue.extend 创建的组件</h3>'
    }))


    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {}
    });
  </script>
```

  注意:不论是哪种方式创建出来的组件,组件的 template 属性指向的模板内容,必须有且只能有唯一的一个根元素

```javascript
<div id="app">
    <mycom3></mycom3>
    <!-- <login></login> -->
  </div>


  <div id="app2">
    <mycom3></mycom3>
    <login></login>
  </div>

  <!-- 在 被控制的 #app 外面,使用 template 元素,定义组件的HTML模板结构  -->
  <template id="tmpl">
    <div>
      <h1>这是通过 template 元素,在外部定义的组件结构,这个方式,有代码的只能提示和高亮</h1>
      <h4>好用,不错!</h4>
    </div>
  </template>

  <template id="tmpl2">
    <h1>这是私有的 login 组件</h1>
  </template>

  <script>
    Vue.component('mycom3', {
      template: '#tmpl'
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {}
    });


    var vm2 = new Vue({
      el: '#app2',
      data: {},
      methods: {},
      filters: {},
      directives: {},
      components: { // 定义实例内部私有组件的
        login: {
          template: '#tmpl2'
        }
      },
      beforeCreate() { },
      created() { },
      beforeMount() { },
      mounted() { },
      beforeUpdate() { },
      updated() { },
      beforeDestroy() { },
      destroyed() { }
    })
  </script>
```

1. 组件可以有自己的 data 数据

​     2. 组件的 data 和 实例的 data 有点不一样,实例中的 data 可以为一个对象,但是 组件中的 data 必须是一个方法

​    3. 组件中的 data 除了必须为一个方法之外,这个方法内部,还必须返回一个对象才行;

​     4. 组件中 的data 数据,使用方式,和实例中的 data 使用方式完全一样!!!

```javascript
 Vue.component('mycom1', {
      template: '<h1>这是全局组件 --- {{msg}}</h1>',
      data: function () {
        return {
          msg: '这是组件的中data定义的数据'
        }
      }
    })
```

```javascript
Vue.component('counter', {
      template: '#tmpl',
      data: function () {
        // return dataObj
        return { count: 0 }
      },
      methods: {
        increment() {
          this.count++
        }
      }
    })
```

#### 组件切换

```javascript
<div id="app">
    <a href="" @click.prevent="flag=true">登录</a>
    <a href="" @click.prevent="flag=false">注册</a>

    <login v-if="flag"></login>
    <register v-else="flag"></register>

  </div>

  <script>
    Vue.component('login', {
      template: '<h3>登录组件</h3>'
    })

    Vue.component('register', {
      template: '<h3>注册组件</h3>'
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        flag: false
      },
      methods: {}
    });
```

#### 父子组件的传值

##### 父组件传值给子组件

```javascript
 <div id="app">
    <!-- 父组件，可以在引用子组件的时候， 通过 属性绑定（v-bind:） 的形式, 把 需要传递给 子组件的数据，以属性绑定的形式，传递到子组件内部，供子组件使用 -->
    <com1 v-bind:parentmsg="msg"></com1>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '123 啊-父组件中的数据'
      },
      methods: {},

      components: {
        // 结论：经过演示，发现，子组件中，默认无法访问到 父组件中的 data 上的数据 和 methods 中的方法
        com1: {
          data() { // 注意： 子组件中的 data 数据，并不是通过 父组件传递过来的，而是子组件自身私有的，比如： 子组件通过 Ajax ，请求回来的数据，都可以放到 data 身上；
            // data 上的数据，都是可读可写的；
            return {
              title: '123',
              content: 'qqq'
            }
          },
          template: '<h1 @click="change">这是子组件 --- {{ parentmsg }}</h1>',
          // 注意： 组件中的 所有 props 中的数据，都是通过 父组件传递给子组件的
          // props 中的数据，都是只读的，无法重新赋值
          props: ['parentmsg'], // 把父组件传递过来的 parentmsg 属性，先在 props 数组中，定义一下，这样，才能使用这个数据
          directives: {},
          filters: {},
          components: {},
          methods: {
            change() {
              this.parentmsg = '被修改了'
            }
          }
        }
      }
    });
  </script>
```

##### 父组件方法传递给子组件

```javascript
<div id="app">
    <!-- 父组件向子组件 传递 方法，使用的是 事件绑定机制； v-on, 当我们自定义了 一个 事件属性之后，那么，子组件就能够，通过某些方式，来调用 传递进去的 这个 方法了 -->
    <com2 @func="show"></com2>
  </div>

  <template id="tmpl">
    <div>
      <h1>这是 子组件</h1>
      <input type="button" value="这是子组件中的按钮 - 点击它，触发 父组件传递过来的 func 方法" @click="myclick">
    </div>
  </template>

  <script>

    // 定义了一个字面量类型的 组件模板对象
    var com2 = {
      template: '#tmpl', // 通过指定了一个 Id, 表示 说，要去加载 这个指定Id的 template 元素中的内容，当作 组件的HTML结构
      data() {
        return {
          sonmsg: { name: '小头儿子', age: 6 }
        }
      },
      methods: {
        myclick() {
          // 当点击子组件的按钮的时候，如何 拿到 父组件传递过来的 func 方法，并调用这个方法？？？
          //  emit 英文原意： 是触发，调用、发射的意思
          // this.$emit('func123', 123, 456)
          this.$emit('func', this.sonmsg)
        }
      }
    }


    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        datamsgFormSon: null
      },
      methods: {
        show(data) {
          // console.log('调用了父组件身上的 show 方法: --- ' + data)
          // console.log(data);
          this.datamsgFormSon = data
        }
      },

      components: {
        com2
        // com2: com2
      }
    });
  </script>
```

#### ref获取组件和DOM元素

```javascript
 <div id="app">
    <input type="button" value="获取元素" @click="getElement" ref="mybtn">

    <h3 id="myh3" ref="myh3">哈哈哈， 今天天气太好了！！！</h3>

    <hr>

    <login ref="mylogin"></login>
  </div>

  <script>

    var login = {
      template: '<h1>登录组件</h1>',
      data() {
        return {
          msg: 'son msg'
        }
      },
      methods: {
        show() {
          console.log('调用了子组件的方法')
        }
      }
    }

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        getElement() {

          //  ref  是 英文单词 【reference】   值类型 和 引用类型  referenceError
          // console.log(this.$refs.myh3.innerText)

          // console.log(this.$refs.mylogin.msg)
          // this.$refs.mylogin.show()
        }
      },
      components: {
        login
      }
    });
  </script>
```

### 路由

#### 什么是路由

1. 后端路由：**对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源；
2. **前端路由：**对于单页面应用程序来说，主要通过URL中的hash(#号)来实现不同页面之间的切换，同时，hash有一个特点：HTTP请求中不会包含hash相关的内容；所以，单页面程序中的页面跳转主要用hash实现；
3. 在单页面应用程序中，这种通过hash改变来切换页面的方式，称作前端路由（区别于后端路由）；

#### 在 vue 中使用 vue-router

1. 导入 vue-router 组件类库：

```
<!-- 1. 导入 vue-router 组件类库 -->
  <script src="./lib/vue-router-2.7.0.js"></script>
```

2. 使用 router-link 组件来导航

```
<!-- 2. 使用 router-link 组件来导航 -->
<router-link to="/login">登录</router-link>
<router-link to="/register">注册</router-link>
```

3. 使用 router-view 组件来显示匹配到的组件

```
<!-- 3. 使用 router-view 组件来显示匹配到的组件 -->
<router-view></router-view>
```

4. 创建使用`Vue.extend`创建组件

```
    // 4.1 使用 Vue.extend 来创建登录组件
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    // 4.2 使用 Vue.extend 来创建注册组件
    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });
```

5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则

```
// 5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
    var router = new VueRouter({
      routes: [
        { path: '/login', component: login },
        { path: '/register', component: register }
      ]
    });
```

6. 使用 router 属性来使用路由规则

```
// 6. 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      router: router // 使用 router 属性来使用路由规则
    });
```

#### 使用tag属性指定router-link渲染的标签类型

#### 设置路由重定向

#### 设置路由高亮

#### 设置路由切换动效

#### 在路由规则中定义参数

1. 在规则中定义参数：

```
{ path: '/register/:id', component: register }
```

2. 通过 `this.$route.params`来获取路由中的参数：

```
var register = Vue.extend({
      template: '<h1>注册组件 --- {{this.$route.params.id}}</h1>'
    });
```

```html
<div id="app">

    <!-- <a href="#/login">登录</a> -->
    <!-- <a href="#/register">注册</a> -->

    <!-- router-link 默认渲染为一个a 标签 -->
    <router-link to="/login" tag="span">登录</router-link>
    <router-link to="/register">注册</router-link>


    <!-- 这是 vue-router 提供的元素，专门用来 当作占位符的，将来，路由规则，匹配到的组件，就会展示到这个 router-view 中去 -->
    <!-- 所以： 我们可以把 router-view 认为是一个占位符 -->
    <transition mode="out-in">
      <router-view></router-view>
    </transition>

  </div>

  <script>
    // 组件的模板对象
    var login = {
      template: '<h1>登录组件</h1>'
    }

    var register = {
      template: '<h1>注册组件</h1>'
    }


    /*  Vue.component('login', {
       template: '<h1>登录组件</h1>'
     }) */

    // 2. 创建一个路由对象， 当 导入 vue-router 包之后，在 window 全局对象中，就有了一个 路由的构造函数，叫做 VueRouter
    // 在 new 路由对象的时候，可以为 构造函数，传递一个配置对象
    var routerObj = new VueRouter({
      // route // 这个配置对象中的 route 表示 【路由匹配规则】 的意思
      routes: [ // 路由匹配规则 
        // 每个路由规则，都是一个对象，这个规则对象，身上，有两个必须的属性：
        //  属性1 是 path， 表示监听 哪个路由链接地址；
        //  属性2 是 component， 表示，如果 路由是前面匹配到的 path ，则展示 component 属性对应的那个组件
        // 注意： component 的属性值，必须是一个 组件的模板对象， 不能是 组件的引用名称；
        // { path: '/', component: login },
        { path: '/', redirect: '/login' }, // 这里的 redirect 和 Node 中的 redirect 完全是两码事
        { path: '/login', component: login },
        { path: '/register', component: register }
      ],
      linkActiveClass: 'myactive'   linkActiveClass: 'myactive' // 和激活相关的类
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router: routerObj // 将路由规则对象，注册到 vm 实例上，用来监听 URL 地址的变化，然后展示对应的组件
    });
  </script>
```

#### 通过路由传参

```html
<div id="app">

    <!-- 如果在路由中，使用 查询字符串，给路由传递参数，则 不需要修改 路由规则的 path 属性 -->
    <router-link to="/login?id=10&name=zs">登录</router-link>
    <router-link to="/register">注册</router-link>

    <router-view></router-view>

  </div>

  <script>

    var login = {
      template: '<h1>登录 --- {{ $route.query.id }} --- {{ $route.query.name }}</h1>',
      data(){
        return {
          msg: '123'
        }
      },
      created(){ // 组件的生命周期钩子函数
        // console.log(this.$route)
        // console.log(this.$route.query.id)
      }
    }

    var register = {
      template: '<h1>注册</h1>'
    }

    var router = new VueRouter({
      routes: [
        { path: '/login', component: login },
        { path: '/register', component: register }
      ]
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      // router: router
      router
    });
  </script>
```

```javascript
<div id="app">

    <!-- 如果在路由中，使用 查询字符串，给路由传递参数，则 不需要修改 路由规则的 path 属性 -->
    <router-link to="/login/12/ls">登录</router-link>
    <router-link to="/register">注册</router-link>

    <router-view></router-view>

  </div>

  <script>

    var login = {
      template: '<h1>登录 --- {{ $route.params.id }} --- {{ $route.params.name }}</h1>',
      data(){
        return {
          msg: '123'
        }
      },
      created(){ // 组件的生命周期钩子函数
        console.log(this.$route.params.id)
      }
    }

    var register = {
      template: '<h1>注册</h1>'
    }

    var router = new VueRouter({
      routes: [
        { path: '/login/:id/:name', component: login },
        { path: '/register', component: register }
      ]
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      // router: router
      router
    });
  </script>
```

#### 路由嵌套和子路由

```javascript
  <div id="app">

    <router-link to="/account">Account</router-link>

    <router-view></router-view>

  </div>

  <template id="tmpl">
    <div>
      <h1>这是 Account 组件</h1>

      <router-link to="/account/login">登录</router-link>
      <router-link to="/account/register">注册</router-link>

      <router-view></router-view>
    </div>
  </template>

  <script>

    // 组件的模板对象
    var account = {
      template: '#tmpl'
    }

    var login = {
      template: '<h3>登录</h3>'
    }

    var register = {
      template: '<h3>注册</h3>'
    }

    var router = new VueRouter({
      routes: [
        {
          path: '/account',
          component: account,
          // 使用 children 属性，实现子路由，同时，子路由的 path 前面，不要带 / ，否则永远以根路径开始请求，这样不方便我们用户去理解URL地址
          children: [
            { path: 'login', component: login },
            { path: 'register', component: register }
          ]
        }
        // { path: '/account/login', component: login },
        // { path: '/account/register', component: register }
      ]
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router
    });
  </script>
```

### watch,computed的使用

// 在 computed 中，可以定义一些 属性，这些属性，叫做 【计算属性】， 计算属性的，本质，就是 一个方法，只不过，我们在使用 这些计算属性的时候，是把 它们的 名称，直接当作 属性来使用的；并不会把 计算属性，当作方法去调用；

​        // 注意1： 计算属性，在引用的时候，一定不要加 () 去调用，直接把它 当作 普通 属性去使用就好了；

​        // 注意2： 只要 计算属性，这个 function 内部，所用到的 任何 data 中的数据发送了变化，就会 立即重新计算 这个 计算属性的值

​        // 注意3： 计算属性的求值结果，会被缓存起来，方便下次直接使用； 如果 计算属性方法中，所以来的任何数据，都没有发生过变化，则，不会重新对 计算属性求值；

// watch 使用这个 属性，可以监视 data 中指定数据的变化，然后触发这个 watch 中对应的 function 处理函数

#### watch`属性的使用

考虑一个问题：想要实现 `名` 和 `姓` 两个文本框的内容改变，则全名的文本框中的值也跟着改变；（用以前的知识如何实现？？？）

1. 监听`data`中属性的改变：

```
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen',
        fullName: 'jack - chen'
      },
      methods: {},
      watch: {
        'firstName': function (newVal, oldVal) { // 第一个参数是新数据，第二个参数是旧数据
          this.fullName = newVal + ' - ' + this.lastName;
        },
        'lastName': function (newVal, oldVal) {
          this.fullName = this.firstName + ' - ' + newVal;
        }
      }
    });
  </script>
```

2. 监听路由对象的改变：

```
<div id="app">
    <router-link to="/login">登录</router-link>
    <router-link to="/register">注册</router-link>

    <router-view></router-view>
  </div>

  <script>
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });

    var router = new VueRouter({
      routes: [
        { path: "/login", component: login },
        { path: "/register", component: register }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router: router,
      watch: {
        '$route': function (newVal, oldVal) {
          if (newVal.path === '/login') {
            console.log('这是登录组件');
          }
        }
      }
    });
  </script>
```

#### `computed`计算属性的使用

1. 默认只有`getter`的计算属性：

```
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen'
      },
      methods: {},
      computed: { // 计算属性； 特点：当计算属性中所以来的任何一个 data 属性改变之后，都会重新触发 本计算属性 的重新计算，从而更新 fullName 的值
        fullName() {
          return this.firstName + ' - ' + this.lastName;
        }
      }
    });
  </script>
```

2. 定义有`getter`和`setter`的计算属性：

```
<div id="app">
    <input type="text" v-model="firstName">
    <input type="text" v-model="lastName">
    <!-- 点击按钮重新为 计算属性 fullName 赋值 -->
    <input type="button" value="修改fullName" @click="changeName">

    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen'
      },
      methods: {
        changeName() {
          this.fullName = 'TOM - chen2';
        }
      },
      computed: {
        fullName: {
          get: function () {
            return this.firstName + ' - ' + this.lastName;
          },
          set: function (newVal) {
            var parts = newVal.split(' - ');
            this.firstName = parts[0];
            this.lastName = parts[1];
          }
        }
      }
    });
  </script>
```

#### `watch`、`computed`和`methods`之间的对比

1. `computed`属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。主要当作属性来使用；
2. `methods`方法表示一个具体的操作，主要书写业务逻辑；
3. `watch`一个对象，键是需要观察的表达式，值是对应回调函数。主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作；可以看作是`computed`和`methods`的结合体；

### webpack

#### 在网页中会引用哪些常见的静态资源？

- JS

- .js  .jsx  .coffee  .ts（TypeScript  类 C# 语言）

- CSS

- .css  .less   .sass  .scss

- Images

- .jpg   .png   .gif   .bmp   .svg

- 字体文件（Fonts）

- .svg   .ttf   .eot   .woff   .woff2

- 模板文件

- .ejs   .jade  .vue【这是在webpack中定义组件的方式，推荐这么用】

#### 网页中引入的静态资源多了以后有什么问题？？？

1. 网页加载速度慢， 因为 我们要发起很多的二次请求；
2. 要处理错综复杂的依赖关系

#### 如何解决上述两个问题

1. 合并、压缩、精灵图、图片的Base64编码
2. 可以使用之前学过的requireJS、也可以使用webpack可以解决各个包之间的复杂依赖关系；

#### 什么是webpack?

webpack 是前端的一个项目构建工具，它是基于 Node.js 开发出来的一个前端工具；

#### 如何完美实现上述的2种解决方案

1. 使用Gulp， 是基于 task 任务的；
2. 使用Webpack， 是基于整个项目进行构建的；

- 借助于webpack这个前端自动化构建工具，可以完美实现资源的合并、打包、压缩、混淆等诸多功能。
- 根据官网的图片介绍webpack打包的过程
- [webpack官网](http://webpack.github.io/)

#### webpack安装的两种方式

1. 运行`npm i webpack -g`全局安装webpack，这样就能在全局使用webpack的命令
2. 在项目根目录中运行`npm i webpack --save-dev`安装到项目依赖中

#### 初步使用webpack打包构建列表隔行变色案例

1. 运行`npm init`初始化项目，使用npm管理项目中的依赖包
2. 创建项目基本的目录结构
3. 使用`cnpm i jquery --save`安装jquery类库
4. 创建`main.js`并书写各行变色的代码逻辑：

```
	// 导入jquery类库
    import $ from 'jquery'

    // 设置偶数行背景色，索引从0开始，0是偶数
    $('#list li:even').css('backgroundColor','lightblue');
    // 设置奇数行背景色
    $('#list li:odd').css('backgroundColor','pink');
```

5. 直接在页面上引用`main.js`会报错，因为浏览器不认识`import`这种高级的JS语法，需要使用webpack进行处理，webpack默认会把这种高级的语法转换为低级的浏览器能识别的语法；
6. 运行`webpack 入口文件路径 输出文件路径`对`main.js`进行处理：

```
webpack src/js/main.js dist/bundle.js
```

#### 使用webpack的配置文件简化打包时候的命令

1. 在项目根目录中创建`webpack.config.js`
2. 由于运行webpack命令的时候，webpack需要指定入口文件和输出文件的路径，所以，我们需要在`webpack.config.js`中配置这两个路径：

```
    // 导入处理路径的模块
    var path = require('path');

    // 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js，并读取这个文件中导出的配置对象，来进行打包处理
    module.exports = {
        entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        }
    }
```

#### 实现webpack的实时打包构建

1. 由于每次重新修改代码之后，都需要手动运行webpack打包的命令，比较麻烦，所以使用`webpack-dev-server`来实现代码实时打包编译，当修改代码之后，会自动进行打包构建。
2. 运行`cnpm i webpack-dev-server --save-dev`安装到开发依赖
3. 安装完成之后，在命令行直接运行`webpack-dev-server`来进行打包，发现报错，此时需要借助于`package.json`文件中的指令，来进行运行`webpack-dev-server`命令，在`scripts`节点下新增`"dev": "webpack-dev-server"`指令，发现可以进行实时打包，但是dist目录下并没有生成`bundle.js`文件，这是因为`webpack-dev-server`将打包好的文件放在了内存中

- 把`bundle.js`放在内存中的好处是：由于需要实时打包编译，所以放在内存中速度会非常快
- 这个时候访问webpack-dev-server启动的`http://localhost:8080/`网站，发现是一个文件夹的面板，需要点击到src目录下，才能打开我们的index首页，此时引用不到bundle.js文件，需要修改index.html中script的src属性为:`<script src="../bundle.js"></script>`
- 为了能在访问`http://localhost:8080/`的时候直接访问到index首页，可以使用`--contentBase src`指令来修改dev指令，指定启动的根目录：

```
 "dev": "webpack-dev-server --contentBase src"
```

 同时修改index页面中script的src属性为`<script src="bundle.js"></script>`

使用`html-webpack-plugin`插件配置启动页面

由于使用`--contentBase`指令的过程比较繁琐，需要指定启动的目录，同时还需要修改index.html中script标签的src属性，所以推荐大家使用`html-webpack-plugin`插件配置启动页面.

1. 运行`cnpm i html-webpack-plugin --save-dev`安装到开发依赖
2. 修改`webpack.config.js`配置文件如下：

```
    // 导入处理路径的模块
    var path = require('path');
    // 导入自动生成HTMl文件的插件
    var htmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {
        entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
        output: { // 配置输出选项
            path: path.resolve(__dirname, 'dist'), // 配置输出的路径
            filename: 'bundle.js' // 配置输出的文件名
        },
        plugins:[ // 添加plugins节点配置插件
            new htmlWebpackPlugin({
                template:path.resolve(__dirname, 'src/index.html'),//模板路径
                filename:'index.html'//自动生成的HTML文件的名称
            })
        ]
    }
```

3. 修改`package.json`中`script`节点中的dev指令如下：

```
"dev": "webpack-dev-server"
```

4. 将index.html中script标签注释掉，因为`html-webpack-plugin`插件会自动把bundle.js注入到index.html页面中！

#### 实现自动打开浏览器、热更新和配置浏览器的默认端口号

**注意：热更新在JS中表现的不明显，可以从一会儿要讲到的CSS身上进行介绍说明！**

##### 方式1：

- 修改`package.json`的script节点如下，其中`--open`表示自动打开浏览器，`--port 4321`表示打开的端口号为4321，`--hot`表示启用浏览器热更新：

```
"dev": "webpack-dev-server --hot --port 4321 --open"
```

##### 方式2：

1. 修改`webpack.config.js`文件，新增`devServer`节点如下：

```
devServer:{
        hot:true,
        open:true,
        port:4321
    }
```

2. 在头部引入`webpack`模块：

```
var webpack = require('webpack');
```

3. 在`plugins`节点下新增：

```
new webpack.HotModuleReplacementPlugin()
```

#### 使用webpack打包css文件

1. 运行`cnpm i style-loader css-loader --save-dev`
2. 修改`webpack.config.js`这个配置文件：

```
module: { // 用来配置第三方loader模块的
        rules: [ // 文件的匹配规则
            { test: /\.css$/, use: ['style-loader', 'css-loader'] }//处理css文件的规则
        ]
    }
```

3. 注意：`use`表示使用哪些模块来处理`test`所匹配到的文件；`use`中相关loader模块的调用顺序是从后向前调用的；

#### 使用webpack打包less文件

1. 运行`cnpm i less-loader less -D`
2. 修改`webpack.config.js`这个配置文件：

```
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
```

#### 使用webpack打包sass文件

1. 运行`cnpm i sass-loader node-sass --save-dev`
2. 在`webpack.config.js`中添加处理sass文件的loader模块：

```
{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
```

#### 使用webpack处理css中的路径

1. 运行`cnpm i url-loader file-loader --save-dev`
2. 在`webpack.config.js`中添加处理url路径的loader模块：

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader' }
```

3. 可以通过`limit`指定进行base64编码的图片大小；只有小于指定字节（byte）的图片才会进行base64编码：

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=43960' },
```

#### 使用babel处理高级JS语法

1. 运行`cnpm i babel-core babel-loader babel-plugin-transform-runtime --save-dev`安装babel的相关loader包
2. 运行`cnpm i babel-preset-es2015 babel-preset-stage-0 --save-dev`安装babel转换的语法
3. 在`webpack.config.js`中添加相关loader模块，其中需要注意的是，一定要把`node_modules`文件夹添加到排除项：

```
{ test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
```

4. 在项目根目录中添加`.babelrc`文件，并修改这个配置文件如下：

```
{
    "presets":["es2015", "stage-0"],
    "plugins":["transform-runtime"]
}
```

5. **注意：语法插件`babel-preset-es2015`可以更新为`babel-preset-env`，它包含了所有的ES相关的语法；**



#### 在普通页面中使用render函数渲染组件



#### 在webpack中配置.vue组件页面的解析

1. 运行`cnpm i vue -S`将vue安装为运行依赖；
2. 运行`cnpm i vue-loader vue-template-compiler -D`将解析转换vue的包安装为开发依赖；
3. 运行`cnpm i style-loader css-loader -D`将解析转换CSS的包安装为开发依赖，因为.vue文件中会写CSS样式；
4. 在`webpack.config.js`中，添加如下`module`规则：

```
module: {

    rules: [

      { test: /\.css$/, use: ['style-loader', 'css-loader'] },

      { test: /\.vue$/, use: 'vue-loader' }

    ]

  }

```

5. 创建`App.js`组件页面：

```
    <template>

      <!-- 注意：在 .vue 的组件中，template 中必须有且只有唯一的根元素进行包裹，一般都用 div 当作唯一的根元素 -->

      <div>

        <h1>这是APP组件 - {{msg}}</h1>

        <h3>我是h3</h3>

      </div>

    </template>



    <script>

    // 注意：在 .vue 的组件中，通过 script 标签来定义组件的行为，需要使用 ES6 中提供的 export default 方式，导出一个vue实例对象

    export default {

      data() {

        return {

          msg: 'OK'

        }

      }

    }

    </script>



    <style scoped>

    h1 {

      color: red;

    }

    </style>

```

6. 创建`main.js`入口文件：

```
    // 导入 Vue 组件

    import Vue from 'vue'



    // 导入 App组件

    import App from './components/App.vue'



    // 创建一个 Vue 实例，使用 render 函数，渲染指定的组件

    var vm = new Vue({

      el: '#app',

      render: c => c(App)

    });

```

#### 在使用webpack构建的Vue项目中使用模板对象？

1. 在`webpack.config.js`中添加`resolve`属性：

```
resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  }
```



#### ES6中语法使用总结

1. 使用 `export default` 和 `export` 导出模块中的成员; 对应ES5中的 `module.exports` 和 `export`
2. 使用 `import ** from **` 和 `import '路径'` 还有 `import {a, b} from '模块标识'` 导入其他模块
3. 使用箭头函数：`(a, b)=> { return a-b; }`



#### 在vue组件页面中，集成vue-router路由模块

[vue-router官网](https://router.vuejs.org/)

1. 导入路由模块：

```
import VueRouter from 'vue-router'

```

2. 安装路由模块：

```
Vue.use(VueRouter);

```

3. 导入需要展示的组件:

```
import login from './components/account/login.vue'

import register from './components/account/register.vue'

```

4. 创建路由对象:

```
var router = new VueRouter({

  routes: [

    { path: '/', redirect: '/login' },

    { path: '/login', component: login },

    { path: '/register', component: register }

  ]

});

```

5. 将路由对象，挂载到 Vue 实例上:

```
var vm = new Vue({

  el: '#app',

  // render: c => { return c(App) }

  render(c) {

    return c(App);

  },

  router // 将路由对象，挂载到 Vue 实例上

});

```

6. 改造App.vue组件，在 template 中，添加`router-link`和`router-view`：

```
    <router-link to="/login">登录</router-link>

    <router-link to="/register">注册</router-link>



    <router-view></router-view>

```



#### 组件中的css作用域问题



#### 抽离路由为单独的模块

### vuex

概念：
vuex 是 Vue 配套的 公共数据管理工具，它可以把一些共享的数据，保存到 vuex 中，方便 整个程序中的任何组件直接获取或修改我们的公共数据；

```javascript
// 入口文件
import Vue from 'vue'
// 配置vuex的步骤
// 1. 运行 cnpm i vuex -S 
// 2. 导入包
import Vuex from 'vuex'
// 3. 注册vuex到vue中
Vue.use(Vuex)
// 4. new Vuex.Store() 实例，得到一个 数据仓储对象
var store = new Vuex.Store({
  state: {
    // 大家可以把 state 想象成 组件中的 data ,专门用来存储数据的
    // 如果在 组件中，想要访问，store 中的数据，只能通过 this.$store.state.*** 来访问
    count: 0
  },
  mutations: {
    // 注意： 如果要操作 store 中的 state 值，只能通过 调用 mutations 提供的方法，才能操作对应的数据，不推荐直接操作 state 中的数据，因为 万一导致了数据的紊乱，不能快速定位到错误的原因，因为，每个组件都可能有操作数据的方法；
    increment(state) {
      state.count++
    },
    // 注意： 如果组件想要调用 mutations 中的方法，只能使用 this.$store.commit('方法名')
    // 这种 调用 mutations 方法的格式，和 this.$emit('父组件中方法名')
    subtract(state, obj) {
      // 注意： mutations 的 函数参数列表中，最多支持两个参数，其中，参数1： 是 state 状态； 参数2： 通过 commit 提交过来的参数；
      console.log(obj)
      state.count -= (obj.c + obj.d)
    }
  },
  getters: {
    // 注意：这里的 getters， 只负责 对外提供数据，不负责 修改数据，如果想要修改 state 中的数据，请 去找 mutations
    optCount: function (state) {
      return '当前最新的count值是：' + state.count
    }
    // 经过咱们回顾对比，发现 getters 中的方法， 和组件中的过滤器比较类似，因为 过滤器和 getters 都没有修改原数据， 都是把原数据做了一层包装，提供给了 调用者；
    // 其次， getters 也和 computed 比较像， 只要 state 中的数据发生变化了，那么，如果 getters 正好也引用了这个数据，那么 就会立即触发 getters 的重新求值；
  }
})

// 总结：
// 1. state中的数据，不能直接修改，如果想要修改，必须通过 mutations
// 2. 如果组件想要直接 从 state 上获取数据： 需要 this.$store.state.***
// 3. 如果 组件，想要修改数据，必须使用 mutations 提供的方法，需要通过 this.$store.commit('方法的名称'， 唯一的一个参数)
// 4. 如果 store 中 state 上的数据， 在对外提供的时候，需要做一层包装，那么 ，推荐使用 getters, 如果需要使用 getters ,则用 this.$store.getters.***


import App from './App.vue'

const vm = new Vue({
  el: '#app',
  render: c => c(App),
  store // 5. 将 vuex 创建的 store 挂载到 VM 实例上， 只要挂载到了 vm 上，任何组件都能使用 store 来存取数据
})
```

![](D:\后台\15--Vuejs（11天）\资料\day10\笔记\vuex概念图.png)





