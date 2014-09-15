# Ant

简单介绍ant的语法和使用方式

##	目录

*	[ant对于前端作用](#ant对于前端作用)
*	[ant语法](#ant常用语法)

##	ant对于前端作用

1.  克服静态代码弱点，自动化完善、优化代码，前端架构的好帮手。
2.	自动完成一些必要而又繁杂的操作，提高工作效率

## ant语法

<project name="demo" default="all" basedir="."></project>
project：根元素，必须设定。
(1)name--项目名称
(2)default--默认执行的target的名称
(3)basedir--用于计算所有其他路径的基路径，默认是“./”

<target name="_develep" depends="init" description="test"></target>
target:任务的集合名称
(1)name--target名称（必须）
(2)depends--依赖的target，注意：被依赖的target只能执行一次
(3)description--target作用描述，其经常被用于显示过滤。


<copy todir="${dir.output}">
    <fileset dir="web">
    <exclude name="build/"></exclude>
    <include name="app.js"/>
    <include name="**/*css"/>
    <include name="**/*css"/>
    <include name="/**/*css"/>
    </fileset>
</copy>
copy:复制文件或文件夹
(1)todir--要复制到得目录
fileset:文件设置
(1)dir--文件目录
(2)exclude name--不包含的文件或文件夹，可以使用通配符
(3)include name--包含的文件或文件夹，可以使用通配符
通配符介绍：
？匹配任何单字符
*匹配0或者任意数量的字符
**匹配0或者更多的目录
示例：
<include name="**/*css"/> 递归web下所有css文件，包含子目录的的css文件,并安源目录结构存放
<include name="*css"/> web目录所有css文件，不包含子目录下的css文件
<include name="public/**/*.css"/>  web/public下所有css文件，包含子目录的css文件，注意是按web的目录结构存放

<delete dir="${dir.output}"/>
delete:删除文件或文件夹，可以嵌套fileset
(1)dir--要删除的目录
(2)file--要删除的文件

<replaceregexp match="v=\d+" replace="v=${dateTime}" byline="false" flags="g" encoding="utf-8"></replaceregexp>
replaceregexp:正则表达式替换文件内容，可以嵌套fileset
(1)match--正则表达式内容(必须)
(2)replace--被替换的内容(必须)
(3)byline--true:替换所有，false:替换匹配到得第一个，默认flase，可以用flags替换
(4)flags--正则表达式修饰符，i:不区分大小写，g:替换所有
(5)encoding--替换后存储的文件格式

<replace token="123" value="121113" file="output/index.css" encoding="utf-8"/>
replace:文本全局替换，可以嵌套css
(1)token--要替换的文本(必须)
(2)value--替换后的值（必须）
(3)file--要替换的文件（必须，可以使用fileset替换）


<echo message="test"/>
echo:输出文本信息
(1)message--输出的文本内容（必须）

<zip destfile="${dir.zip}/ad-backoffice.zip" basedir="${dir.output}"/>
zip:压缩文件
(1)destfile--目标zip文件(必须)
(2)basedir--要压缩的目录(可以使用fileset代替)


<antcall target="echoTestTest"/>
antcall: 调用target
(1)target--被调用的target名称(必须)

<scp todir="${baolei.user}:${baolei.pwd}@123.150.172.198:." port="63008" trust="true" verbose="true"></scp>
scp:传输文件
(1)todir--要传到得服务器目标(必须)
(2)port--服务器端口名称
(3)trust--通常设置为true 默认false ，假如为默认值false时,那么就要求你所连接的host必须存在于你的knownhosts文件中，并且 这个文件也必须是存在的。
(4)verbose--显示传输进度

<script type="build/html">
<sshexec host="123.150.172.198" username="${baolei.user}" password="${baolei.pwd}" port="63008" command="cd /home/${baolei.user};expect aa.sh" timeout="20000" trust="true"/>
</script>
sshexec:远程执行命令
(1)host--服务器地址(必须)
(2)username--用户名(必须)
(3)password--密码
(4)port--端口 默认22
(5)command--执行的命令(必须)
(6)timeout--强制断开时间
(7)trust--同scp.trust