- ## 参考资料
	- https://www.codeplayer.org/Wiki/Emacs/org-mode-tutorial.html
- ## 基本语法-列表
	- 列表： `*` + 空格
	- 多个 `*` 即为多级列表……
	- 可以用 `Tab` 展开 / 收起。
	- `S+Tab`  为全部展开 / 收起。
	- `M-Ret` 新建同级列表。
- ## 基本语法-链接
	- 使用 `[[ ]]` 括起来一段文字，可以链接到任意一段标题。
	- `SPC-m-l` 制作连接。
		- `::` 指定文件连接(可和描述分开)。
		- `::` 后跟数字既是行号。
		- 复制粘贴网址即可制作超链接。
		- `elisp:` 后可跟代码。
			- 也可跟函数。
- ## 基本语法-代码
	- `<s` 然后加 `TAB` 即可创建一个代码快。
- ## 基本语法-任务
	- `SPC-m-q` 设置标签。
	-