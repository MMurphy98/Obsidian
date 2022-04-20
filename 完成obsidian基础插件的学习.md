## Plug-in

### Advanced Table
|  C_para   | ΔVgs | V_cap0 |
|:---------:|:----:|:------:|
| C_p(G->S) |  -   | fdjkf  |
|    fdf    | fdf  |  fdf   |

体验不错，`tab` 回退，`Enter` 直接换行

### Admonition
```ad-note
title: Title
collapse: open

This is a note，这是一篇笔记
```

```ad-summary
title: summary

This is a note，这是一篇笔记
```

```ad-info
title: Information

这是Info
```

```ad-important
Admonition 多元化了markdown的笔记内容，让形式更丰富了；
```

```ad-abstract

```


### Calender
![[Pasted image 20220419112212.png]]

非常重要且美观；  

### Footnotes

插入脚注 [^1]， 但是感觉插入脚注的场景，并不是很多，没有必要；


[^1]:这是一条脚注，但是感觉插入脚注的场景使用的并不多；

### Checklist
#todo
- [ ] [[完成obsidian基础插件的学习]]；
- [ ] 实现obsidian与zotero的联动；
- [ ] 子任务是没法实现的；

**Checklist** 可以根据自定义的 `tag` 识别todo的任务，并且按照文件名分类，但是有个问题是无法实现**任务与子任务**的拆分；

### `ris:CodeSSlash` Icon
快捷键`ctrl+shift+i` 插入图表，只能在预览模式中使用，但是效果还可以，可以起到一定的美化效果；

`ris:Book2`

### Editor Syntax Highlight

``` C
#include <iostream>

int main(){
	for (int i = 0; i < 10; i++){
		std::cout << i ;
	}
}
```

好吃就是在编辑区能实现色彩的高亮，也不是说完全没有用，可以保留着；
![[Pasted image 20220419114903.png]]

```verilog
always @(posedge clk or negedge rstn) begin
	if (~rstn) begin
	end 
	esle begin
		...
	end
end
```

### Paste URL into selection

- 这是原本的链接：https://github.com/
- 使用插件之后，将URL粘贴至文本中，如：[Github](https://github.com/), 直接使用快捷键`Ctrl + V` 即可；


使用体验不错，**可以保留**；


### Excalidraw

漂亮，但是感觉并不是很值得这样做；

### cMenu
![[Pasted image 20220419145910.png]]

添加一个快捷方式的浮窗，感觉还可以<sup>2</sup>，方便使用

### Quick LaTex for Obsidian

$$x+b=c$$

$(a+b)=c+d$

$$\sum\limits_{a}^{b}$$

$$\frac{x-\mu}{\sigma}$$

$$\frac{e}{2}$$

$$
\begin{align*}
\pi\\
&\omega \\
&\psi \kappa
\end{align*}
$$

总体的使用感受还是很流畅的，很方便；

### Kanban
可以通过代码实现关于子任务的设置，但是感觉不是很方便，可以配合checklist使用；

