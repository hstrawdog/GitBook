## 快捷键

 1. #### 查找引用    edit -> find usages  -> Show Usages 

    设置成 command + F7   与原功能对调使用 

 2. #### 移除无用的导入

    - 描述 移除顶部冗余的导入/引用
    - 快捷键 control + option +O

3. #### 提取方法（Extract Method）
    - 描述：提取一段代码块，生成一个新的方法。当你发现某个方法里面过于复杂，需要将某一段代码提取成单独的方法时，该技巧是很有用的。
    - 调用：Menu → Refactor → Extract → Method
    - 快捷键：Cmd + Alt + M(OS X)、Ctrl + Alt + M(Windows/Linux)；shift+ Alt + M
    - 更多：在提取代码的对话框，你可以更改方法的修饰符和参数的变量名。

    

4. #### 书签（Bookmarks）

    - 描述：这是一个很有用的功能，让你可以在某处做个标记（书签），方便后面再跳转到此处。
    - 调用：Menu → Navigate → Bookmarks
    - 快捷键：
      - 添加/移除书签：F3(OS X) 、F11(Windows/Linux);
      - 添加/移除书签(带标记)：Alt + F3(OS X)、Ctrl + F11(Windows/Linux);
      - 显示全部书签：Cmd + F3(OS X) 、Shift + F11(Windows/Linux)，显示所有的书签列表，并且是可以搜索的。
      - 上一个/下一个书签：无，可以在设置中设置快捷键。
    - 更多：当你为某个书签指定了标记，你可以使用快捷键 Ctrl + 标记 来快速跳转到标记处，比如输入Ctrl + 1，跳到标记为1的书签处。



4. #### 折叠/展开代码块（Collapse Expand Code Block）

    - 描述：该操作提供一种方法，让你隐藏你不关心的部分代码，以一种较为简洁的格式显示关键代码。一个有意思的用法是隐藏匿名内部类的代码，让其看起来像一个Lambda表达式。

    - 快捷键：Cmd + “+”/”-“(OS X)、Ctrl + Shift + “+”/”-“(Windows/Linux);

    - 更多：可以在Settig → Editor → General → Code Folding 中设置折叠规则。

      

5. #### 最近访问（Recents）

    - 描述：该操作可以得到一个最近访问文件的可搜索的列表。

    - 快捷键：Cmd + E(OS X)、Ctrl + E(Windows/Linux)

      

6. #### 折叠/展开代码块（Collapse Expand Code Block）

    - **描述：**该操作提供一种方法，让你隐藏你不关心的部分代码，以一种较为简洁的格式显示关键代码。一个有意思的用法是隐藏匿名内部类的代码，让其看起来像一个Lambda表达式。

    - **快捷键：**Cmd + “+”/”-“(OS X)、Ctrl + Shift + “+”/”-“(Windows/Linux);

    - **更多：**可以在Settig → Editor → General → Code Folding 中设置折叠规则。

      

7. #### 上一个编辑位置（Last Edit Location）

    - **描述：**该操作将使得你导航到上一处你改动过的地方，这与点击工具栏上的返回箭头回到上一个定位位置是不一样的，该操作将会返回到上一个编辑的位置。
    - **快捷键：** Cmd + Shift + Delete(OS X)、Ctrl + Shift + Backspace﻿(Windows/Linux);

8. ####  最近修改的文件（Recently Changed Files）

    - **描述：**该操作类似于“最近访问（Recents）”弹窗，会显示最近本地修改过的文件列表，根据修改时间排列。可以输入字符来过滤列表结果。
    - **快捷键：**Cmd + Shift + E(OS X)、Ctrl + Shift + E(Windows/Linux)

9. #### 提取方法（Extract Method）

    - **描述：**提取一段代码块，生成一个新的方法。当你发现某个方法里面过于复杂，需要将某一段代码提取成单独的方法时，该技巧是很有用的。
    - **调用：**Menu → Refactor → Extract → Method
    - **快捷键：**Cmd + Alt + M(OS X)、Ctrl + Alt + M(Windows/Linux)；
    - **更多：**在提取代码的对话框，你可以更改方法的修饰符和参数的变量名。

10. ####  提取参数（Extract Parameter）

    - **描述：**这是一个提取参数的快捷操作。当你觉得可以通过提取参数来优化某个方法的时候，这个技巧将很有用。该操作会将当前值作为一个方法的参数，将旧的值放到方法调用的地方，作为传进来的参数。
    - **调用：**Menu → Refactor → Extract → Parameter
    - **快捷键：**Cmd + Alt + P(OS X)、Ctrl + Alt + P(Windows/Linux)；
    - **更多：**通过勾选“delegate”，可以保持旧的方法，重载生成一个新方法。

11. #### 提取变量（Extract Variable）

     - **描述：**这是一个提取变量的快捷操作。当你在没有写变量声明的直接写下值的时候，这是一个很方便生成变量声明的操作，同时还会给出一个建议的变量命名。
     - **调用：**Menu → Refactor → Extract → Variable
     - **快捷键：**Cmd + Alt + V(OS X)、Ctrl + Alt + V(Windows/Linux)；
     - **更多：**当你需要改变变量声明的类型，例如使用 List 替代 ArrayList，可以按下Shift + Tab，就会显示所有可用的变量类型。

12. #### 包裹代码（Surround With）

     - **描述：** 该操作可以用特定代码结构包裹住选中的代码块，通常是if语句，循环，try/catch语句或者runnable语句。 如果你没有选中任何东西，该操作会包裹当前一整行。
     - **快捷键：**Cmd + Alt + T(OS X)、Ctrl + Alt + T(Windows/Linux)