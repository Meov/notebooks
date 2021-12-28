[Markdown语法参考,点我](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/)

# 这是 <h1> 一级标题
## 这是 <h2> 二级标题
### 这是 <h3> 三级标题
*这是斜体文字*
**这是粗体文字**
__这也是粗体文字__
_你也可以**组合**这些符号,让文字变得**又粗又斜**_

__无序列表：__
- Item1
- Item2
  - Item2a
  - Item2b


__无序列表：__
1. Item1
1. Item2
    1. Item 2a
    1. Item 2b

__添加图片__
![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)

https://github.com - 自动生成！
[GitHub](https://github.com) __*也可以这样*__

__引用__
> to be or not to be...
> that is a question

__行内代码__
应该是这样`<addr>` 才对，这个符号是英文状态下按 ～ 键产生的。 

__代码块__
```c++
int main(){
    printf("hehehe");
}
```
*其中 c++ 代表使用的语言的类型*

__显示代码行数__
```c++ {.line-numbers}
int main(){
    printf("hehehe");
}
```
*使用 **{.line-numbers}** 来显示代码行数*

__表格__
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

$f(x)=sin(x)+b$
$$f(x)=sin(x)+cos(y)$$ 
*这是块状的公式*

__字体颜色__

<font color=#FF0000>  这样字体改成红色了 </font>  
**<font color=#FF0000>  可以这样让字体字体变得又红又粗 </font>** 
_**<font color=#FF0000>  可以这样让字体字体变得又红又粗又斜 </font>**_

__换行__

如果你想换行，打一个回车
可以发现，明显是不行的

正确的做法是在需要换行的地方，比如说这里插入“：</br> 他就换行了 :)
