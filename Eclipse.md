Mac下eclipse的快捷键

command+option+S: 调出快速生成代码会话框，可以选择为成员变量生成Setter/Getter方法，重写toString,hashCode,equals方法，生成constructor等
tab: 调用一个有多个参数的方法的时候，从一个参数跳到另外一个参数。比如Hashtable的put方法，输入string key,需要跳到string value的时候。
command+option+M: 将某段代码抽出放在一个单独的方法里(对应Refactor->Extract Method)
command+option+R: 批量重命名某个变量名或者字段(field)

阅读代码：
command+[: 返回前一个位置
command+单击: 查看源码，也可以使用F3实现
command+shift+T: 调出OpenType对话框，可以输入类名，查看类的实现源码
command+option+W: 快速定位当前文件在工程中的位置,即在package视图中的位置,在弹出的对话框中选择"package explorer"

代码整理：
command+shift+O: 整理包，去掉多余的import语句，补足未导入的包
command+／: 注释或反注释所选中的所有行，没选默认只注释当前行
command+1: 快速修复
command+d: 删除当前行

其它：
command+option+↓: 复制当前行到下一行
command+option+↑: 复制当前行到上一行
command+←: 移动光标到当前行的行首，Mac系统通用
command+→: 移动光标到当前行的行尾
command+O: 在某个类文件，可以快速定位到当前文件的属性和方法
command+Z: 撤销刚才的操作，undo
option+↑: 向上移动当前行
option+↓: 向下移动当前行
option+→: 下一单词
option+←: 上一单词
option+↩︎: 显示当前选择资源的属性
option+/: 代码联想提示，如果没设置代码联想快捷键，需要先设置，详情见参考文献3
option+shift+→: 选中一段连续的内容，比如一个字符串
shift+↩︎: 光标移动到下一行开始位置
Ctrl+H: 搜索，可以在Customize中将File Search以外的搜索选项去掉，只保留最有用的File Search.

