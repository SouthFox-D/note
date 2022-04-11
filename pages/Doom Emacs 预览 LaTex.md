- 安装 `LaTex` 解析器
	- ```shell
	  yay -S texlive-latexextra
	  ```
- 在 `~/.doom.d/init.el` 启用对应的包
	- ```lisp
	  (latex                       ; writing papers in Emacs has never been so fun
	   +latexmk                    ; what else would you use?
	   +cdlatex                    ; quick maths symbols
	   +fold)                      ; fold the clutter away nicities
	  ```
	- 参考：https://tecosaur.github.io/emacs-config/config.html