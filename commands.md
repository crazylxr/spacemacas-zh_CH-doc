## 14 Commands
### 14.1 Vim key bindings
spacemacs 是基于 vim 模式的用户界面来导航和编辑文本。如果你不熟悉 vim 编辑文本的方式，你可以随时按下 SPC h T 来试试这个 [evil-tutor](https://github.com/syl20bnr/evil-tutor) 教程。

#### 14.1.1 Escaping
spacemacs 通过快速按下 fd 键，使用 evil-escape 来轻松切换插入状态和正常状态。

fd 的选择使得能够使用相同的序列从 emacs 中的 “everything”:
- 从一切 evil 状态摆脱到正常的状态
- 从 evil-lisp-state 到正常状态
- 从 evil-iedit-state 到正常状态
- 放弃 evil 的命令
- 退出 minibuffer
- 放弃 isearch
- 退出 magit buffers
- 退出 help buffers
- 退出 apropos buffers
- 退出 ert buffers
- 退出 undo-tree buffer
- 退出 paradox
- 退出 gist-list menu
- 退出 helm-ag-edit
- 隐藏 neotree buffer

如果您发现自己处于 Spacemacs（SPC）或 vim键 绑定不起作用的缓冲区中，则可以使用它恢复到正常状态（例如，在 SPC SPC customize 按 fd 以使 SPC b b再次运行）。

这个序列可以在你的 〜/.spacemacs 中定制。例如将其设置为jj：

```lisp
(defun dotspacemacs/user-config ()
  (setq-default evil-escape-key-sequence "jj"))
```
> 注意：尽管 jj 或 jk 是 vim 用户的流行选择，但这些关键序列对于 spacemacs 并不是最优的。事实上，在 visual 状态下很快就会很快地按下，不经意地逃到 normal 状态。

#### 14.1.2 Executing Vim and Emacs ex/M-x commands

Command | Key Binding
---|---
Vim (ex-command) | ：
Emacs (M-x)| SPC SPC

可以使用 〜/.spacemacs 的变量 dotspacemacs-emacs-command-key 来更改 emacs 命令键 SPC（在leader key后面执行）。

#### 14.1.3 Leader key
在 vim 模式之上（模式被称为 spacemacs 中的状态），有一个特殊的键被称为 leader 键，它曾经被按下给出一个全新的键盘层。leader 键是默认的 SPC（空格）。可以用变量 dotspacemacs-leader-key 来改变这个键。
#### 14.1.4 Additional text objects
在spacemacs中定义了额外的文本对象：

Object | Description
---|---
a |	an argument
g|	the entire buffer
$|	text between $
*|	text between *
8|	text between /* and */
%|	text between %
\vert|	text between \vert

### 14.2为用户保留前缀命令
SPC o 和 SPC m o 是为用户保留的。在这些背后设置键绑定保证不会与 spacemacs 默认键绑定冲突。

例如：在你的 〜/.spacemacs 文件里放置（spacesmacs/ set-leader-keys“oc”'org-capture）到 dotspacemacs/user-config 中，以便能够使用 SPC o c 来运行组织模式捕获。

### 14.3 Completion
spacemacs 由两个增量完成和选择缩小框架之一驱动：helm（默认）或 ivy。要使用 ivy，请将 ivy layer 添加到启用的 layer 列表中。如果 ivy layer 没有启用，helm 将自动启用。（请注意，由于 Helm 是两者中较为成熟的，所以如果选择 ivy，某些功能可能无法使用。）

这些完成系统是 spacemacs 的中央控制塔，他们被用来管理缓冲区(buffers)，项目(projects)，搜索结果(search results)，配置层(configuration)，切换(toggles)和更多...

掌握你完成系统的选择将会使你成为一名超级 Spacemacs 用户。

#### 14.3.1 Helm
不要犹豫来阅读[Helm wiki 文档](https://github.com/emacs-helm/helm/wiki)。

#### 14.3.1.1 C-z and Tab switch
绑定到 C-z 的命令比绑定到 Tab 的命令更有用，所以交换它们是有意义的。[这里](http://tuhdo.github.io/helm-intro.html)也推荐。

#### 14.3.1.2 Helm focus
如果您发现自己无法将焦点返回到 Helm（例如粗心的点击鼠标之后），请使用 SPC w b 将焦点返回到 minibuffer。

#### 14.3.1.3 Helm transient state
Spacemacs 为 Helm 定义了一个[临时状态](http://spacemacs.org/doc/DOCUMENTATION.html#transient-states)，使其像 [Vim's Unite](https://github.com/Shougo/unite.vim) 插件一样工作。

在 Helm 缓冲区中用 M-SPC 或 s-M-SPC 启动临时状态。


Key Binding | Description
---|---
M-SPC or s-M-SPC|	initiate the transient state
q|	quit transient state
TAB	|switch to actions page and leave the transient state
1|	execute action 0
2|	execute action 1
3|	execute action 2
4|	execute action 3
5|	execute action 4
6|	execute action 5
7|	execute action 6
8|	execute action 7
9|	execute action 8
0|	execute action 9
a|	switch to actions page
g|	go to first candidate
G|	go to last candidate
h|	go to previous source
j|	select next candidate
k|	select previous candidate
l|	go to next source
t|	mark current candidate
T|	mark all candidates
v|	execute persistent action

### 14.4 Discovering
#### 14.4.1 Key bindings
##### 14.4.1.1 Which-key

每次在正常模式下按下 SPC 键时都会显示帮助缓冲区。它列出了可用的键绑定及其相关的命令。

默认情况下，在键被按下后，which-key 缓冲器将被快速显示。你可以通过设置你喜欢的变量 dotspacemacs-which-key-delay 来改变延迟（值在秒）。

##### 14.4.1.2 Helm describe key bindings
可以通过按 SPC ？. 搜索特定的键绑定。

通过使用 leader 键类型来将列表缩小到某些键绑定，例如这个正则表达式：SPC\ b，它将列出所有与缓冲区有关的绑定。

#### 14.4.2 Getting help
Describe functions 是强大的 emacs introspection 命令来获取有关函数(functions)，变量(variables)，模式(modes)等信息，因此这些命令是绑定的：

Key Binding | Description
---|---
SPC h d b|	describe bindings in a helm buffer
SPC h d c|	describe current character under point
SPC h d d|   describe current expression under point
SPC h d f|	describe a function
SPC h d F|	describe a face
SPC h d k|	describe a key
SPC h d K|	describe a keymap
SPC h d l|	copy last pressed keys that you can paste in gitter chat
SPC h d m|	describe current modes
SPC h d p|	describe a package (Emacs built-in function)
SPC h d P|	describe a package (Spacemacs layer information)
SPC h d s|	copy system information that you can paste in gitter chat
SPC h d t|	describe a theme
SPC h d v|	describe a variable

其他 help 键绑定：

Key Binding	 | Description
---|---
SPC h SPC|	discover Spacemacs documentation, layers and packages using helm
SPC h i	|search in info pages with the symbol at point
SPC h k	|show top-level bindings with which-key
SPC h m	|search available man pages
SPC h n	|browse emacs news

在 help-mode 下导航键绑定：
Key Binding|	Description
-- | --
g b |or [	go back (same as clicking on [back] button)
g f |or ]	go forward (same as clicking on [forward] button)
g h	|go to help for symbol under point

报告问题：

Key Binding | Description
---|---
SPC h I	|Open Spacemacs GitHub issue page with pre-filled information
SPC u SPC h I|	Open Spacemacs GitHub issue page with pre-filled information - include last pressed keys

> 注意：如果这两个绑定与 *Backtrace* 缓冲区打开使用，则自动包括 backtrace

#### 14.4.3 Available layers
所有的层可以很容易地发现通过 helm-spacemacs-help 可访问的 SPC h SPC。
 。
 
 下面的 helm actions 是可用的：
 - 默认：打开图层 readme.org
 - 第二：打开图层 packages.el

##### 14.4.3.1 Available packages in Spacemacs
helm-spacemacs-help 还列出了 Spacemacs 中可用的所有软件包。入口格式是（layer）包。如果你输入 flycheck，你将能够看到所有使用 flycheck 的 layers。

软件包中有以下 helm 操作：
- 默认：去包初始化函数

##### 14.4.3.2 New packages from ELPA repositories
package-list-packages 是您可以在不同的 Elpa 软件仓库中浏览所有可用软件包的地方。可以从那里升级软件包，但不建议使用 spacemacs 启动页面上的 [Update Packages] 链接。

Spacemacs 使用 [Paradox](https://github.com/Malabarba/paradox) 而不是 package-list-packages 来列出可用的 ELPA 包。Paradox 增强了更好的反馈，新的过滤器和 github 信息，如星星数量的软件包列表缓冲区。也可以选择直接在缓冲区中打包。

> 重要的注意事项1：从 **Paradox** 安装一个新的包不会使其持久。要持久地安装软件包，必须将其明确添加到配置层。

> 重要说明2：不要从  **Paradox** 或 **package-list-packages** 更新软件包，因为它们不支持 Spacemacs 的回滚功能。


Key Binding | Description
---|---
SPC a k|	launch paradox
/|	evil-search
f k	|filter by keywords
f r|	filter by regexp
f u|	display only installed package with updates available
h|	go left
H|	show help (not accurate)
j|	go down
k|	go up
l|	go right
L|	show last commits
n|	next search occurrence
N|	previous search occurrence
o|	open package homepage
r|	refresh
S P|	sort by package name
S S|	sort by status (installed, available, etc…)
S *|	sort by Github stars
v|	visual state
V|	visual-line state
x|	execute (action flags)

#### 14.4.4 Toggles
helm-spacemacs-help 也是发现可用切换的中心位置。只显示切换源按下 C-l（或在[ helm 临时状态](http://spacemacs.org/doc/DOCUMENTATION.html#helm-transient-state)下按 l）。

软件包中有以下 helm 操作：
- 默认值：打开/关闭

提示使用 SPC h l 来恢复最后的 helm 会话。快速打开和关闭切换是很方便的。

### 14.5 Navigating
#### 14.5.1 Point/Cursor
导航是使用 Vi 键绑定 hjkl 来执行的。

Key Binding | Description
---|---
h|	move cursor left
j|	move cursor down
k|	move cursor up
l|	move cursor right
H|	move cursor to the top of the screen
L|	move cursor to the bottom of the screen
SPC j 0|	go to the beginning of line (and set a mark at the previous location in the line)
SPC j $	|go to the end of line (and set a mark at the previous location in the line)
SPC t -|	lock the cursor at the center of the screen

##### 14.5.1.1 Smooth scrolling
[smooth-scrolling](https://github.com/aspiers/smooth-scrolling) 防止点到达屏幕的顶部或底部时跳转。它是默认启用的。

在 Windows 上，你可能想禁用它。禁用平滑滚动，将 〜/.spacemacs 中的 dotspacemacs-smooth-scrolling 变量设置为nil：

```lisp
(setq-default dotspacemacs-smooth-scrolling nil)
```

您也可以使用 SPC t v 切换平滑滚动。

#### 14.5.2 Vim motions with avy
Spacemacs 使用 avy 的 evil 的整合，使运行期间 avy 的调用。

例如，从当前行删除一组视觉线是有用的。在包含一些文本的缓冲区中尝试以下顺序：d SPC j l，然后选择一个 avy 候选项。

Key Binding	 | Description
---|---
SPC j b|	go back to the previous location (before the jump)
SPC j j|	initiate avy jump char
SPC j w| initiate avy jump word
SPC j l| initiate avy jump line

##### 14.5.2.1 ace-link mode
类似于 avy，ace-link 允许用户通过两个按键跳转到 help-mode 和 info-mode 下的任何链接。

Key Binding	 | Description
---|---
o| 在 help-mode 和 info-mode 下启动 ace-link
 
#### 14.5.3 Unimpaired bindings
Spacemacs 带有一个内置的 [tpope's vim-unimpaired](https://github.com/tpope/vim-unimpaired) 端口。

这个插件提供了几对括号映射，使用 [ 表示前一个，] 表示下一个。


KeyBindings | Description
---|---
[ SPC|	Insert space above
] SPC|	Insert space below
[ b	|Go to previous buffer
] b	|Go to next buffer
[ f	|Go to previous file in directory
] f	|Go to next file in directory
[ l	|Go to the previous error
] l	|Go to the next error
[ h	|Go to the previous vcs hunk
] h	|Go to the next vcs hunk
[ q	|Go to the previous error
] q	|Go to the next error
[ t	|Go to the previous frame
] t	|Go to the next frame
[ w	|Go to the previous window
] w	|Go to the next window
[ e	|Move line up
] e	|Move line down
[ p	|Paste above current line
] p	|Paste below current line
g p	|Select pasted text

#### 14.5.4 Jumping, Joining and Splitting
SPC j 前缀用于跳转(jumping)，连接(joining)和分割(splitting)。

##### 14.5.4.1 Jumping

Key Binding |	Description
---|---
SPC j 0	|go to the beginning of line (and set a mark at the previous location in the line)
SPC j $|	go to the end of line (and set a mark at the previous location in the line)
SPC j b|	undo a jump (go back to previous location)
SPC j d|	jump to a listing of the current directory
SPC j D	|jump to a listing of the current directory (other window)
SPC j f|	jump to the definition of an Emacs Lisp function
SPC j i|	jump to a definition in buffer (imenu)
SPC j I|	jump to a definition in any buffer (imenu)
SPC j j|	jump to a character in the buffer (works as an evil motion)
SPC j J|	jump to a suite of two characters in the buffer (works as an evil motion)
SPC j k|	jump to next line and indent it using auto-indent rules
SPC j l|	jump to a line with avy (works as an evil motion)
SPC j q|	show the dumb-jump quick look tooltip
SPC j u|	jump to a URL in the current buffer
SPC j v|	jump to the definition/declaration of an Emacs Lisp variable
SPC j w|	jump to a word in the current buffer (works as an evil motion)

##### 14.5.4.2 Joining and splitting

Key Binding | Description
---|---
J|	join the current line with the next line
SPC j k|	go to next line and indent it using auto-indent rules
SPC j n|	split the current line at point, insert a new line and auto-indent
SPC j s|	split a quoted string or s-expression in place
SPC j S|	split a quoted string or s-expression, insert a new line and auto-indent
#### 14.5.5 Window manipulation
##### 14.5.5.1 Window manipulation key bindings
每个窗口都有一个 在mode-line 开始处显示的数字，可以使用 SPC number 快速访问。

Key Binding	 | Description
---|---
SPC 1|	go to window number 1
SPC 2|	go to window number 2
SPC 3|	go to window number 3
SPC 4|	go to window number 4
SPC 5|	go to window number 5
SPC 6|	go to window number 6
SPC 7|	go to window number 7
SPC 8|	go to window number 8
SPC 9|	go to window number 9
SPC 0|	go to window number 0

Windows操作命令（以 w 开头）：

Key Binding	| Description
---|---
SPC w =	|balance split windows
SPC w b	|force the focus back to the minibuffer (usefull with helm popups)
SPC w c	|maximize/minimize a window and center it
SPC w C	|maximize/minimize a window and center it using ace-window
SPC w d	|delete a window
SPC u SPC w d	|delete a window and its current buffer (does not delete the file)
SPC w D	|delete another window using ace-window
SPC u SPC w D	|delete another window and its current buffer using ace-window
SPC w t	|toggle window dedication (dedicated window cannot be reused by a mode)
SPC w f	|toggle follow mode
SPC w F|	create new frame
SPC w h	|move to window on the left
SPC w H	|move window to the left
SPC w j	|move to window below
SPC w J	|move window to the bottom
SPC w k	|move to window above
SPC w K	|move window to the top
SPC w l	|move to window on the right
SPC w L	|move window to the right
SPC w m	|maximize/minimize a window (maximize is equivalent to delete other windows)
SPC w M	|swap windows using ace-window
SPC w o	|cycle and focus between frames
SPC w p m	|open messages buffer in a popup window
SPC w p p	|close the current sticky popup window
SPC w r	|rotate windows forward
SPC w R	|rotate windows backward
SPC w s or SPC w -|	horizontal split
SPC w S	|horizontal split and focus new window
SPC w u	|undo window layout (used to effectively undo a closed window)
SPC w U	|redo window layout
SPC w v or SPC w /|	vertical split
SPC w V|	vertical split and focus new window
SPC w w	|cycle and focus between windows
SPC w W	|select window using ace-window

##### 14.5.5.2 Window manipulation transient state
一个方便的窗口操作临时状态允许执行上面列出的大部分操作临时状态允许额外的行为，如窗口大小调整。

Key Binding	| Description
---|---
SPC w .	|initiate transient state
?	|display the full documentation in minibuffer
0	|go to window number 0
1	|go to window number 1
2	|go to window number 2
3	|go to window number 3
4	|go to window number 4
5	|go to window number 5
6	|go to window number 6
7	|go to window number 7
8	|go to window number 8
9	|go to window number 9
/	|vertical split
-	|horizontal split
[	|shrink window horizontally
]	|enlarge window horizontally
{	|shrink window vertically
}	|enlarge window vertically
d	|delete window
D	|delete other windows
g	|toggle golden-ratio on and off
h	|go to window on the left
j	|go to window below
k	|go to window above
l	|go to window on the right
H	|move window to the left
J	|move window to the bottom
K	|move bottom to the top
L	|move window to the right
o	|focus other frame
r	|rotate windows forward
R	|rotate windows backward
s	|horizontal split
S	|horizontal split and focus new window
u	|undo window layout (used to effectively undo a closed window)
U	|redo window layout
v	|vertical split
V	|horizontal split and focus new window
w	|focus other window
Any other key	|leave the transient state

##### 14.5.5.3 Golden ratio
如果你像疯了一样调整窗口大小，你可能想尝试一下[黄金比例](https://github.com/roman/golden-ratio.el)。

黄金比例动态调整窗口的大小，取决于它们是否被选中。默认情况下，黄金比例关闭。

可以使用 SPC t g 来打开和关闭模式。

#### 14.5.6 Buffers and Files
默认情况下，Spacemacs 使用 helm 来打开文件。

##### 14.5.6.1 Buffers manipulation key bindings
缓冲区操作命令（以 b 开头）：

Key Binding	| Description
---|---
SPC TAB	|switch to alternate buffer in the current window (switch back and forth)
SPC b b	|switch to a buffer using helm
SPC b d	|kill the current buffer (does not delete the visited file)
SPC u SPC b d	|kill the current buffer and window (does not delete the visited file)
SPC b D	|kill a visible buffer using ace-window
SPC u SPC b D	|kill a visible buffer and its window using ace-window
SPC b C-d	|kill buffers using a regular expression
SPC b e	|erase the content of the buffer (ask for confirmation)
SPC b h	|open *spacemacs* home buffer
SPC b n	|switch to next buffer avoiding special buffers
SPC b m	|kill all buffers except the current one
SPC u SPC b m	|kill all buffers and windows except the current one
SPC b M	|kill all buffers matching the regexp
SPC b p	|switch to previous buffer avoiding special buffers
SPC b P	|copy clipboard and replace buffer (useful when pasting from a browser)
SPC b R	|revert the current buffer (reload from disk)
SPC b s	|switch to the *scratch* buffer (create it if needed)
SPC b w	|toggle read-only (writable state)
SPC b Y	|copy whole buffer to clipboard (useful when copying to a browser)
z f	|Make current function or comments visible in buffer as much as possible
##### 14.5.6.2 Buffers manipulation transient state
一个方便的缓冲区操作瞬态允许通过打开的缓冲区快速循环并杀死它们。

Key Binding	| Description
---|---
SPC b .	|initiate transient state
K	|kill current buffer
n	|go to next buffer (avoid special buffers)
N	|go to previous buffer (avoid special buffers)
Any other key	|leave the transient state

##### 14.5.6.3 Special Buffers
不像 vim，emacs 创建了大多数人不需要看的缓冲区。一些例子是 *messages* 和 *compile-log*。Spacemacs 会尝试自动忽略无用的缓冲区。不过，您可能需要更改 spacemacs 将缓冲区标记为有用的方式。有关说明，请参阅[特殊缓冲区 howto](http://spacemacs.org/doc/FAQ.html#MissingReference)。

##### 14.5.6.4 Files manipulations key bindings
文件操作命令（以f开头）：

Key Binding	| Description
---|---
SPC f b	|go to file bookmarks
SPC f c	|copy current file to a different location
SPC f C d	|convert file from unix to dos encoding
SPC f C u	|convert file from dos to unix encoding
SPC f D	|delete a file and the associated buffer (ask for confirmation)
SPC f E	|open a file with elevated privileges (sudo edit)
SPC f f	|open file with helm
SPC f F	|try to open the file under point helm
SPC f h	|open binary file with hexl (a hex editor)
SPC f j	|jump to the current buffer file in dired
SPC f J	|open a junk file, in mode determined by the file extension provided (defaulting to fundamental mode), using helm (or ivy)
SPC f l	|open file literally in fundamental mode
SPC f L	|Locate a file (using locate)
SPC f o	|open a file using the default external program
SPC f R	|rename the current file
SPC f s	|save a file
SPC f S	|save all files
SPC f r	|open a recent file with helm
SPC f t	|toggle file tree side bar using NeoTree
SPC f v d	|add a directory variable
SPC f v f	|add a local variable to the current file
SPC f v p	|add a local variable to the first line of the current file
SPC f y	|show and copy current file absolute path in the minibuffer
##### 14.5.6.5 Emacs and Spacemacs files
方便的键绑定位于前缀 SPC f e 下，以便在 emacs 和 spacemacs 特定文件之间快速导航。


Key Binding	| Description
---|---
SPC f e d	|open the spacemacs dotfile (~/.spacemacs)
SPC f e D	|open ediff buffer of ~/.spacemacs and .spacemacs.template
SPC f e f	|discover the FAQ using helm
SPC f e i	|open the all mighty init.el
SPC f e l	|locate an Emacs library
SPC f e R	|resync the dotfile with spacemacs
SPC f e v	|display and copy the spacemacs version
##### 14.5.6.6 Browsing files with Helm
在 vim 和 hybrid 风格中，Spacemacs 重映射 Helm 查找文件中的导航，以保持在主行上。 

Key Binding	| Description
---|---
C-h |go up one level (parent directory
C-H	|describe key (replace C-h)
C-j	|go to previous candidate
C-k	|go to next candidate
C-l	|enter current directory
#### 14.5.7 Ido
Spacemacs 垂直显示 ido minibuffer 感谢 [ido-vertical-mode](https://github.com/gempesaw/ido-vertical-mode.el).

基本的 ido 操作可以用 Ctrl 键完成：

Key Binding	| Description
---|---
C-<return>	|open a dired buffer
M-<return>	|open a dired buffer in terminal
C-d	|delete selected file (ask for confirmation)
C-h	|go to parent directory
C-j	|select next file or directory
C-k	|select previous file or directory
C-l	|open the selected file
C-n	|select next file or directory
C-o	|open selected file in other window
C-p	|select previous file or directory
C-s	|open selected file in a vertically split window
C-t	|open selected file in a new frame
C-v	|open selected file in a horizontally split window
C-S-h	|go to previous directory
C-S-j or C-S-n	|next history element
C-S-k or C-S-p	|previous history element
C-S-l	|go to next directory

#### 14.5.8 Ido transient state
Spacemacs 为 ido定义了一个[临时装态](http://spacemacs.org/doc/DOCUMENTATION.html#transient-states)。

在一个 ido 缓冲区中用 M-SPC 或 s-M-SPC 启动临时装态。

Key Binding	| Description
---|---
M-SPC or s-M-SPC	|initiate or leave the transient state
?	|display help
e	|open dired
h	|delete backward or parent directory
j	|next match
J	|sub directory
k	|previous match
K	|parent directory
l	|select match
n	|next directory in history
o	|open in other window
p	|previous directory in history
q	|quit transient state
s	|open in a new horizontal split
t	|open in other frame
v	|open in a new vertical split
#### 14.5.9 NeoTree file tree
Spacemacs 提供了一个快速和简单的方法来在 [NeoTree](https://github.com/jaypei/emacs-neotree) 中导航未知的项目文件树。

切换 NeoTree 缓冲区按 SPC f t 或 SPC p t（后者打开 NeoTree，根目录设置为子弹项目根目录）。

NeoTree 窗口始终有数字 0，所以它不会移动其他窗口的当前数量。选择 NeoTree 窗口然后使用 spc 0。

支持 VSC 集成，文件颜色将根据当前状态而改变。用默认的 spacemacs-dark 主题：
- 绿色: 新文件
- 紫色: 修改过的文件

##### 14.5.9.1 NeoTree navigation
导航以 hjkl 键为中心，希望能提供像 [ranger](http://ranger.nongnu.org/) 一样的快速导航体验：

Key Binding	| Description
---|---
h	|collapse expanded directory or go to parent node
H	|select previous sibling
j	|select next file or directory
J	|select next expanded directory on level down
k	|select previous file or directory
K	|select parent directory, when reaching the root change it to parent directory
l or RET	|expand directory
L	|select next sibling
R	|make a directory the root directory
> 注意：点自动设置为节点的第一个字母，以获得更流畅的体验。

##### 14.5.9.2 Opening files with NeoTree
默认情况下在最后一个活动窗口中打开一个文件。可以通过使用数字参数来选择要打开文件的窗口号，例如 2 l 或 2 RET 将打开窗口 2 中的当前文件。也可以使用 | 和 - ：

Key Binding	| Description
---|---
l or RET	|open file in last active window
# l or # RET	|open file in window number #
¦	|open file in an vertically split window
-	|open file in an horizontally split window

##### 14.5.9.3 Other NeoTree key bindings

Key Binding	| Description
---|---
TAB	|toggle stretching of the buffer
c	|create a node
d	|delete a node
gr	|refresh
s	|toggle showing of hidden files
q or fd	|hide NeoTree buffer
r	|rename a node
?	|show help
##### 14.5.9.4 NeoTree mode-line
mode-line 具有以下格式 [x/y] d（d：a，f：b）其中：
- x是当前所选文件或目录的索引
- y当前目录中项目（文件和目录）的总数
- d当前目录的名称
- a当前目录中的目录数量
- b当前目录中的文件数量

##### 14.5.9.5 NeoTree Source Control Integration
如果你想 NeoTree 显示源控制信息，你可以使用 neo-vc-integration 设置。它是一个包含可能值的列表：

Setting	| Description
---|---
face	|通过改变文件/目录名称的颜色来显示信息。
char	|在文件/目录名称的左侧显示带有字符的信息。

默认是 nil（不显示源控制信息），这是推荐的。

例如，

```lisp
(setq neo-vc-integration 'face)
```
> 注意：目前，不建议将其设置为除 nil 之外的任何值。否则，源码树越大，速度越慢。有关更多信息，请参阅 [https://github.com/jaypei/emacs-neotree/issues/126](https://github.com/jaypei/emacs-neotree/issues/126)。

##### 14.5.9.6 NeoTree Theme
你可以使用设置 neo-theme 来改变 NeoTree 主题。可能的值是：

Setting |	Description
---|---
classic	|使用图标显示项目 - 只适用于 gui 模式。
ascii	|最简单的样式，它将使用x， - 来显示折叠状态。
arrow	|使用 unicode 箭头来显示折叠状态。
nerd	|使用 NERDTree 缩进模式和箭头。

默认是 classic。
使用 nerd ，如果你想在 VIM 看起来最像 NERDTree。例如：

```lisp
(setq neo-theme 'nerd)
```
#### 14.5.10 Bookmarks
书签可以在文件的任何地方设置。书签是持久的。他们是非常有用的跳转到/打开一个已知的项目。Spacemacs 使用 helm-bookmarks 来管理它们。

按下：SPC f b，打开当前书签的 helm 窗口

然后在 helm-bookmarks 缓冲区中：

Key Binding	| Description
---|---
C-d	|删除选中的书签
C-e	|编辑选定的书签
C-f	|切换文件名位置
C-o	|在另一个窗口中打开选定的书签

要保存新的书签，只需输入书签的名称，然后按下 RET。

#### 14.5.11 DocView mode
doc-view-mode 是一个内置的主要模式来查看 DVI，PostScript (PS), PDF，OpenDocument 和 Microsoft Office 文档。

Key Binding	| Description
---|---
/	|search forward
?	|search backward
+	|enlarge
-	|shrink
gg	|go to first page
G	|go to last page
gt	|go to page number
h	|previous page
H	|adjust to height
j	|next line
k	|previous line
K	|kill proc and buffer
l	|next page
n	|go to next search occurrence
N	|go to previous search occurrence
P	|fit page to window
r	|revert
W	|adjust to width
C-d	|scroll down
C-k	|kill proc
C-u	|scroll up
C-c C-c	|toggle display text and image display
C-c C-t	|open new buffer with doc's text contents
### 14.6 Auto-saving
#### 14.6.1 Frequency of auto-saving
默认情况下，每300个字符和每30秒的空闲时间执行文件自动保存，可以通过分别将变量 auto-save-inteval 和 auto-save-timeout 设置为新值来更改这些文件。

#### 14.6.2 Location of auto-saved files
修改文件的自动保存可以在原始文件本身或缓存目录中原位执行（在这种情况下，原始文件将保持未保存状态）。默认情况下，Spacemacs 自动将文件保存在缓存目录中。

修改位置将变量 dotspacemacs-auto-save-file-location 设置为 original 或 cache。

本地文件将自动保存在缓存目录中的一个名为站点的子目录中，而远程文件（即通过 TRAMP 编辑的文件）将自动保存在名为 dist 的子目录中。

#### 14.6.3 Disable auto-save
禁用自动保存将变量 dotspacemacs-auto-save-file-location 设置为nil。

您可以通过调用命令 auto-save-mode 来切换自动保存在缓冲区中。

### 14.7 Searching
#### 14.7.1 With an external tool
Spacemacs 可以与不同的搜索工具连接，如：
- ack
- grep
- [ag](https://github.com/ggreer/the_silver_searcher)
- [pt](https://github.com/monochromegane/the_platinum_searcher)

Spacemacs 中的搜索命令在 SPC s 前缀下组织，下一个键是要使用的工具，最后一个键是范围。比如 SPC s a b 会使用 ag 在所有打开的缓冲区中搜索。

如果最后一个键（确定范围）是大写的，那么点下的当前区域或符号将被用作搜索的默认输入。例如 SPC s a B 将在符号下搜索符号（如果没有活动区域）。

如果省略了工具键，则会自动选择默认工具进行搜索。这个工具对应于在列表 dotspacemacs-search-tools 的系统上找到的第一个工具，默认顺序是 ag，pt，ack，然后是 grep 。例如，如果在系统中没有找 到 ag，spc 将使用 pt 在打开的缓冲区中搜索。

工具键是：

Tool | Key
---|---
ag|	a
grep|	g
ack|	k
pt|	t

可用的范围和相应的键是：

Scope | Key
---|---
打开缓冲区	|b
文件在给定的目录中	|f
当前的项目	|p

可以通过双击序列的第二个键在当前文件中进行搜索，例如 SPC s a a 将使用 ag 在当前文件中搜索。

**Notes:**
- ag 和 pt 被优化用于源代码控制库中，但是它们也可以在任意目录中使用。
- 也可以通过在 helm 缓冲区中标记它们来一次搜索多个目录。

当心如果你使用 pt，[TCL parser tools](https://core.tcl.tk/tcllib/doc/trunk/embedded/www/tcllib/files/apps/pt.html) 也会安装一个名为 pt 的命令行工具。

##### 14.7.1.1 Useful key bindings

Key Binding | Description
---|---
F3	|在 helm 或 ivy 缓冲区中，将结果保存到常规缓冲区
SPC r l	|恢复上一个完成缓冲区
SPC r s or SPC s l	|恢复搜索缓冲区（完成或转换的搜索缓冲区）
SPC s `	|回到以前用 helm-ag 达到的地方
Prefix argument	|将要求文件扩展名

当结果保存在 f3 的常规缓冲区中时，该缓冲区支持通过与 Spacemacs 的下一个错误和先前错误绑定（ SPC e n 和 SPC e p）以及错误瞬态（SPC e）进行浏览。

##### 14.7.1.2 Searching in current file

Key Binding	| Description
---|---
SPC s s	|用第一个找到的工具搜索
SPC s S	|用默认输入搜索第一个找到的工具
SPC s a a	|ag
SPC s a A	|ag with default input
SPC s g g	|grep
SPC s g G	|grep with default input
##### 14.7.1.3 Searching in all open buffers visiting files

Key Binding	| Description
---|---
SPC s b	|用第一个找到的工具搜索
SPC s B	|用默认输入搜索第一个找到的工具
SPC s a b	|ag
SPC s a B	|ag with default text
SPC s g b	|grep
SPC s g B	|grep with default text
SPC s k b	|ack
SPC s k B	|ack with default text
SPC s t b	|pt
SPC s t B	|pt with default text

##### 14.7.1.4 Searching in files in an arbitrary directory

Key Binding	| Description
---|---
SPC s f	|用第一个找到的工具搜索
SPC s F	|用默认输入搜索第一个找到的工具
SPC s a f	|ag
SPC s a F	|ag with default text
SPC s g f	|grep
SPC s g F	|grep with default text
SPC s k f	|ack
SPC s k F	|ack with default text
SPC s t f	|pt
SPC s t F	|pt with default text

##### 14.7.1.5 Searching in a project

Key Binding	| Description
---|---
SPC / or SPC s p	|用第一个找到的工具搜索
SPC * or SPC s P	|用默认输入搜索第一个找到的工具
SPC s a p	|ag
SPC s a P	|ag with default text
SPC s g p	|grep with default text
SPC s k p	|ack
SPC s k P	|ack with default text
SPC s t p	|pt
SPC s t P	|pt with default text

> 提示：也可以在项目中搜索，而无需事先打开文件。在一个给定的项目中使用 SPC p p 然后 C-s 来直接搜索它，就像使用 SPC s p 一样。

##### 14.7.1.6 Searching the web

Key Binding	| Description
---|---
SPC s w g	|在 emacs 中获得谷歌建议。在浏览器中打开google结果。
SPC s w w	|在 emacs 中获得维基百科建议。在浏览器中打开维基百科页面。

#### 14.7.2 Persistent highlighting
Spacemacs 使用 evil-search-highlight-persist 来保持搜索到的表达式直到下一次搜索。也可以通过按 SPC s c 或执行 ex 命令来清除突出显示：noh。

#### 14.7.3 Highlight current symbol
Spacemacs 支持按需高亮显示当前符号（由[ auto-highlight-symbol ](https://github.com/emacsmirror/auto-highlight-symbol) mode 提供），并添加瞬态以轻松导航并重命名此符号。

也可以将飞行中的导航范围更改为：
- buffer
- function
- visible area

在点按 SPC s h 下启动当前符号的突出显示。

高亮的符号之间的导航可以通过以下命令完成：


Key Binding	| Description
---|---
*	|在当前符号上启动导航暂态，并向前跳转
#	|在当前符号上启动导航暂态并向后跳转
SPC s e	|编辑所有出现的当前符号（/）
SPC s h	|高亮显示当前符号及其在当前范围内的所有出现
SPC s H	|转到上次搜索到的最后一个突出显示的符号
SPC t h a	|在 ahs-idle-interval 秒后切换点下的符号自动高亮

在'spacemacs'中高亮显示符号瞬态：

Key Binding	| Description
---|---
e	|edit occurrences (*)
n	|go to next occurrence
N	|go to previous occurrence
d	|go to next definition occurrence
D	|go to previous definition occurrence
r	|change range (function, display area, whole buffer)
R	|go to home occurrence (reset position to starting occurrence)
Any other key	|leave the navigation transient state

（*）使用 [iedit](https://github.com/tsdh/iedit) 或 auto-highlight-symbol 的默认实现

minibuffer 中的瞬态文本显示如下信息：

```
<M> [6/11]* press (n/N) to navigate, (e) to edit, (r) to change range or (R)
for reset
```

其中<M> [x/y] *是：
- M：当前的范围模式
- <B\>：整个缓冲区范围
- <D>：当前的显示范围
- <F>：当前的功能范围
- x：当前高亮显示的事件的索引
- y：发生的总次数
- *：如果至少有一个当前不可见的情况出现。

#### 14.7.4 Visual Star
用 [evil-visualstar](https://github.com/bling/evil-visualstar) 你可以搜索下一个出现的当前选择。

它与 [expand-region](http://spacemacs.org/doc/DOCUMENTATION.html#region-selection) 绑定相结合非常有用。

> 注意：如果当前状态不是 visual 状态，那么按 * 使用自动高亮符号及其瞬态状态。

#### 14.7.5按语义列出符号
使用 helm 的 helm-semantic-or-imenu 命令可以在缓冲区中的符号之间快速导航。 

列出一个缓冲区的所有符号按：SPC s j

#### 14.7.6 Helm-swoop
这与 moccur 非常相似，它显示了一个 helm 缓冲区，其中包含所有出现的单词。您可以实时更改搜索查询并轻松地在它们之间导航。

您甚至可以直接在 helm 缓冲区中编辑事件，并将修改应用到缓冲区。


Key Binding	| Description
---|---
SPC s s	|execute helm-swoop
SPC s S	|execute helm-multi-swoop
SPC s C-s	|execute helm-multi-swoop-all

### 14.8编辑
#### 14.8.1粘贴文本
##### 14.8.1.1粘贴瞬态
可以通过将变量 dotspacemacs-enable-paste-transient-state 设置为 t 来启用粘贴瞬变状态。默认情况下它被禁用。

当启用暂态时，再次按下 p 将会替换粘贴的文字与先前在 kill (ring) 上被 yanked（copied）的文字。

例如，如果复制 foo 和 bar，然后按 p 将粘贴文本栏，再次按 p 将用 foo 替换 bar。


Key Binding	| Description
---|---
p or P	|粘贴文本之前或之后的文本，并启动粘贴瞬态
p	|在瞬态：用先前复制的粘贴文本替换
P	|在瞬态中：用下一个复制的文本替换粘贴文本
.	|粘贴相同的文本，并离开瞬态
Any other key	|离开瞬态

##### 14.8.1.2自动缩进粘贴文本
默认情况下，任何粘贴的文本都将被自动缩进。粘贴文本不加缩进使用通用的参数。

可以通过在您的 dotspacemacs/user-config 函数的变量 spacemacs-indent-sensitive-modes 中添加 major-modes 来禁用特定   major-mode 的自动缩进。

#### 14.8.2文本操作命令
文本相关的命令（以x开头）：

Key Binding	| Description
---|---
SPC x a &	|align region at &
SPC x a (	|align region at (
SPC x a )	|align region at )
SPC x a ,	|align region at ,
SPC x a .	|align region at . (for numeric tables)
SPC x a :	|align region at :
SPC x a ;	|align region at ;
SPC x a =	|align region at =
SPC x a a	|align region (or guessed section) using default rules
SPC x a c	|align current intendation region using default rules
SPC x a r	|align region using user-specified regexp
SPC x a m	|align region at arithmetic operators (+-*/)
SPC x a ¦	|align region at ¦
SPC x c	|count the number of chars/words/lines in the selection region
SPC x d w	|delete trailing whitespaces
SPC x g l	|set languages used by translate commands
SPC x g t	|translate current word using Google Translate
SPC x g T	|reverse source and target languages
SPC x j c	|set the justification to center
SPC x j f	|set the justification to full
SPC x j l	|set the justification to left
SPC x j n	|set the justification to none
SPC x j r	|set the justification to right
SPC x J	|move down a line of text (enter transient state)
SPC x K	|move up a line of text (enter transient state)
SPC x l s	|sort lines
SPC x l u	|uniquify lines
SPC x o	|use avy to select a link in the frame and open it
SPC x O	|use avy to select multiple links in the frame and open them
SPC x t c	|swap (transpose) the current character with the previous one
SPC x t w	|swap (transpose) the current word with the previous one
SPC x t l	|swap (transpose) the current line with the previous one
SPC x u	|set the selected text to lower case
SPC x U	|set the selected text to upper case
SPC x w c	|count the number of occurrences per word in the select region
SPC x w d	|show dictionary entry of word from wordnik.com
SPC x TAB	|indent or dedent a region rigidly

#### 14.8.3文本插入命令
文本插入命令（从 i 开始）：

Key binding	| Description
---|---
SPC i l l	|insert lorem-ipsum list
SPC i l p	|insert lorem-ipsum paragraph
SPC i l s	|insert lorem-ipsum sentence
SPC i u	|Search for Unicode characters and insert them into the active buffer.
SPC i U 1	|insert UUIDv1 (use universal argument to insert with CID format)
SPC i U 4	|insert UUIDv4 (use universal argument to insert with CID format)
SPC i U U	|insert UUIDv4 (use universal argument to insert with CID format)

#### 14.8.4 Smartparens Strict mode
[Smartparens](https://github.com/Fuco1/smartparens)有一个严格的模式，如果结果不平衡，可以防止删除括号。

这种模式可能会让新手感到沮丧，这就是为什么它没有默认启用。

可以通过使用 〜/.spacemacs 的变量 dotspacemacs-smartparens-strict-mode 来轻松启用所有编程模式。

```lisp
(setq-default dotspacemacs-smartparens-strict-mode t)
```

#### 14.8.5 缩放(Zooming)
##### 14.8.5.1 文本
当前缓冲区的字体大小可以通过以下命令进行调整：

Key Binding	| Description
---|---
SPC z x +	|scale up the font and initiate the font scaling transient state
SPC z x =	|scale up the font and initiate the font scaling transient state
SPC z x -	|scale down the font and initiate the font scaling transient state
SPC z x 0	|reset the font size (no scaling) and initiate the font scaling transient state
+	|increase the font size
=	|increase the font size
-	|decrease the font size
0	|reset the font size
Any other key	|leave the font scaling transient state

请注意，只有当前缓冲区的文本被缩放，其他缓冲区，模式行和小缓冲区不受影响。使用缩放框架绑定缩放框架的全部内容（请参阅下一节）。

##### 14.8.5.2 框架(Frame)
您可以使用以下命令放大和缩小框架的全部内容：


Key Binding	| Description
---|---
SPC z f +	|放大框架内容并启动框架缩放瞬态
SPC z f =	|放大框架内容并启动框架缩放瞬态 scaling transient state
SPC z f -	|缩小框架内容并启动框架缩放瞬态
SPC z f 0	|重置框架内容大小并启动框架缩放瞬态
+	|放大
=	|放大
-	|缩小
0	|重置缩放
任何其他的键	|保持缩放框架的瞬态状态

#### 14.8.6增加/减少数字
Spacemacs 使用 [evil-number](https://github.com/cofi/evil-numbers) 来轻松地增加或减少数字。


Key Binding	| Description
---|---
SPC n +	|increase the number under point by one and initiate transient state
SPC n -	|decrease the number under point by one and initiate transient state

在瞬态中：

Key Binding | Description
---|---
+	|increase the number under point by one
-	|decrease the number under point by one
Any other key	|leave the transient state

> 提示：你可以通过使用前缀参数多次增加或减少一个值（即，10 SPC n + 将点数加10）。

#### 14.8.7 拼写检查
通过在你的 dotfile 中包含 spell checking layer 来启用拼写检查。

键绑定列在 layer 文档中。

#### 14.8.8区域选择
evil 支持 Vi 中所有的 Visual modes

##### 14.8.8.1 扩大区域(Expand-region)
Spacemacs 通过 [expand-regin](https://github.com/magnars/expand-region.el) mode 添加了另一种 Visual mode。

Key Binding	| Description
---|---
SPC v	| 启动 expand-regin 模式，然后...
v	| 用一个语义单位来扩展该区域
V	|通过一个语义单元来收缩区域
r	|将区域重置为初始选择
ESC	| 离开 expand-regin 模式

##### 14.8.8.2缩进文本对象(Indent text object)
[evil-indent-plus](https://github.com/TheBB/evil-indent-plus)  以下文本对象可用：
- ii  - 内部缩进：周围的文本块具有相同的缩进
- iI  - 上面和缩进：ii + 上面的行用不同的缩进
- iJ  - 上面，下面和缩进+：ii +下面的行用不同的缩进

还有一个包含空白的变体.例子（| 表示点）：

```lisp
(while (not done)
  (messa|ge "All work and no play makes Jack a dull boy."))
(1+ 41)
```
- vii 会选择带消息的行
- viI 会选择整个while循环
- viJ 将选择整个片段

#### 14.8.9 区域缩小(Region narrowing)
缓冲区的显示文本可以用命令缩小（从 n 开始）：

Key Binding	| Description
---|---
SPC n f	|将缓冲区缩小到当前的功能
SPC n p	|将缓冲区缩小到可见页面
SPC n r	|将缓冲区缩小到选定的文本
SPC n w	|扩大，即再次显示整个缓冲区

#### 14.8.10 用iedit替换文本(Replacing text with iedit)
Spacemacs 通过 [evil-iedit-state](https://github.com/syl20bnr/evil-iedit-state) 使用强大的 [iedit](https://github.com/tsdh/iedit) 模式来快速编辑多个符号或选项。

evil-iedit-state 定义了两个新的 evil stataes：
- iedit state
- iedit-insert state

这些状态的颜色代码是红色的。

evil-iedit-state 与 [expand-region](https://github.com/magnars/expand-region.el)  也有很好的集成，通过按 e 可快速编辑当前选定的文本。

##### 14.8.10.1 iedit states 键绑定( iedit states key bindings)
1. 状态转换
2. 
Key Binding	| From	| To
---|---|---
SPC s e	|normal or visual	|iedit
e	|expand-region	|iedit
ESC	|iedit	|normal
C-g	|iedit	|normal
fd	|iedit	|normal
ESC	|iedit-insert	|iedit
C-g	|iedit-insert	|normal
fd	|iedit-insert	|norma

总结，在 iedit-insert 状态，你必须按两次 ESC 回到 normal 状态。你也可以随时按 C-g 或 fd 回到 normal 状态。

> 注意：切换到 insert 状态的 evil 命令会切换到 iedit-insert 状态。

2. 在 iedi t状态
iedit 状态从 normal 状态继承，下面的键绑定是特定于 iedit 状态的。

Key Binding	| Description
---|---
ESC	|go back to normal state
TAB	|toggle current occurrence
0	|go to the beginning of the current occurrence
$	|go to the end of the current occurrence
#	|prefix all occurrences with an increasing number (SPC u to choose the starting number).
A	|go to the end of the current occurrence and switch to iedit-insert state
D	|delete the occurrences
F	|restrict the scope to the function
gg	|go to first occurrence
G	|go to last occurrence
I	|go to the beginning of the current occurrence and switch to iedit-insert state
J	|increase the editing scope by one line below
K	|increase the editing scope by one line above
L	|restrict the scope to the current line
n	|go to next occurrence
N	|go to previous occurrence
p	|replace occurrences with last yanked (copied) text
S	|(substitute) delete the occurrences and switch to iedit-insert state
V	|toggle visibility of lines with no occurrence
U	|Up-case the occurrences
C-U	|down-case the occurrences

> 注意：0，$，a和我有默认的 vim 行为在事件之外使用。

3. 在 iedit-insert 状态

Key Binding	| Description
---|---
ESC	go |back to iedit state
C-g	go | back to normal state

##### 14.8.10.2 例子
- 手动选择几个字然后替换：v w w SPC s e S "toto" ESC ESC
- 将文本附加到两行的单词上：v i w SPC s e J i "toto" ESC ESC
- 用 expand-region 替代符号：SPC v v e S "toto" ESC ESC
- 用扩展区域替换符号与被抽出（复制）的文本：SPC v e p ESC ESC

#### 14.8.11 替换几个文件中的文本
如果您安装了 ag ，pt 或 ack ，则可以通过 [helm-ag](https://github.com/syohex/emacs-helm-ag) 来替换多个文件中的文本。

假设你想在当前项目中用 bar 替换所有的 foo 事件：
- 用 SPC / 开始搜索
- 用 C-c C-e 编辑模式进入
- 用 SPC s e 去发生并进入 iedit state
- 编辑事件，然后离开 iedit state
- 按 C-c C-c

> 注意：在 Spacemacs 中，尽管 helm-ag 的名字与  ack 和 pt 一起工作（但不与 grep 一起）。

#### 14.8.12 重命名目录中的文件
可以使用 helm 会话中的 wdired 批量重命名目录中的文件：
- 使用 SPC f f 浏览目录
- 用 C-c C-e 进入 wdired
- 编辑文件名并使用 C-c C-c 确认更改
- 使用 C-c C-k 放弃所有更改
#### 14.8.13 评论
评论由 [evil-nerd-commenter](https://github.com/redguardtoo/evil-nerd-commenter) 处理，它被绑定到下面的键。

Key Binding	| Description
---|---
SPC ;	| comment operator
SPC c l	| comment lines
SPC c L	| invert comment lines
SPC c p	| comment paragraphs
SPC c P	| invert comment paragraphs
SPC c t	| comment to line
SPC c T	| invert comment to line
SPC c y	| comment and yank
SPC c Y	| invert comment and yank
> 提示：有效地评论一行使用组合 SPC ; SPC y

#### 14.8.14 正则表达式
Spacemacs 使用包 [pcre2el](https://github.com/joddie/pcre2el) 来操作正则表达式。在使用 Emacs Lisp 缓冲区时它很有用，因为它允许轻松地将 PCRE（ Perl 兼容 RegExp ）转换为 Emacs Regexp 或 rx。它也可以用来“解释”一个 PCRE RegExp   以 rx 形式表示的点。

键绑定以 SPC x r 开始并具有以下助记符结构：
- SPC x r <source> <target> 从源代码转换为目标代码
- spc x r 做我的意思

Key Binding	| Function
---|---
SPC x r /	|Explain the regexp around point with rx
SPC x r '	|Generate strings given by a regexp given this list is finite
SPC x r t	|Replace regexp around point by the rx form or vice versa
SPC x r x	|Convert regexp around point in rx form and display the result in the minibuffer
SPC x r c	|Convert regexp around point to the other form and display the result in the minibuffer
SPC x r e /	|Explain Emacs Lisp regexp
SPC x r e '	|Generate strings from Emacs Lisp regexp
SPC x r e p	|Convert Emacs Lisp regexp to PCRE
SPC x r e t	|Replace Emacs Lisp regexp by rx form or vice versa
SPC x r e x	|Convert Emacs Lisp regexp to rx form
SPC x r p /	|Explain PCRE regexp
SPC x r p '	|Generate strings from PCRE regexp
SPC x r p e	|Convert PCRE regexp to Emacs Lisp
SPC x r p x	|Convert PCRE to rx form

#### 14.8.15 删除文件
删除配置为将删除的文件发送到系统垃圾箱。

在 OS x 上需要垃圾程序。它可以通过 homebrew  以下命令与自制软件一起安装：

```
$ brew install trash
```
要禁用垃圾箱，您可以在 〜/.spacemacs 中将变量 delete-by-moving-to-trash 设置为 nil。

#### 14.8.16 编辑 lisp 代码
lisp 代码的编辑由 evil-lisp-state 提供。

命令会将当前状态设置为 lisp 状态，其中可以重复不同的命令组合，而无需按下 SPC k。

当处于 lisp 状态时，mode-line 的颜色变为粉红色。

例子：
- 在正常状态下啜饮三次：SPC k 3 s
- 在圆括号中包装一个符号，然后啜饮两次：SPC k w 2 s

> 注意：lisp 状态命令可以在任何模式下使用！试试看。

#### 14.8.16.1 lisp 键绑定
1. lisp状态键绑定
这些命令自动切换到  lisp 状态。

Key Binding	| Function
---|---
SPC k %	|evil jump item
SPC k :	|ex command
SPC k (	|insert expression before (same level as current one)
SPC k )	|insert expression after (same level as current one)
SPC k $	|go to the end of current sexp
SPC k ` k	|hybrid version of push sexp (can be used in non lisp dialects)
SPC k ` p	|hybrid version of push sexp (can be used in non lisp dialects)
SPC k ` s	|hybrid version of slurp sexp (can be used in non lisp dialects)
SPC k ` t	|hybrid version of transpose sexp (can be used in non lisp dialects)
SPC k 0	|go to the beginning of current sexp
SPC k a	|absorb expression
SPC k b	|forward barf expression
SPC k B	|backward barf expression
SPC k c	|convolute expression
SPC k ds	|delete symbol
SPC k Ds	|backward delete symbol
SPC k dw	|delete word
SPC k Dw	|backward delete word
SPC k dx	|delete expression
SPC k Dx	|backward delete expression
SPC k e	|unwrap current expression and kill all symbols after point
SPC k E	|unwrap current expression and kill all symbols before point
SPC k h	|previous symbol
SPC k H	|go to previous sexp
SPC k i	|switch to insert state
SPC k I	|go to beginning of current expression and switch to insert state
SPC k j	|next closing parenthesis
SPC k J	|join expression
SPC k k	|previous opening parenthesis
SPC k l	|next symbol
SPC k L	|go to next sexp
SPC k p	|paste after
SPC k P	|paste before
SPC k r	|raise expression (replace parent expression by current one)
SPC k s	|forward slurp expression
SPC k S	|backward slurp expression
SPC k t	|transpose expression
SPC k u	|undo
SPC k U	|got to parent sexp backward
SPC k C-r	|redo
SPC k v	|switch to visual state
SPC k V	|switch to visual line state
SPC k C-v	|switch to visual block state
SPC k w	|wrap expression with parenthesis
SPC k W	|unwrap expression
SPC k y	|copy expression

2. emacs lisp 特定的键绑定

Key Binding | Function
---|---
SPC m e $	|go to end of line and evaluate last sexp
SPC m e b	|evaluate buffer
SPC m e c	|evaluate current form (a def or a set)
SPC m e e	|evaluate last sexp
SPC m e f	|evaluate current defun
SPC m e l	|go to end of line and evaluate last sexp
SPC m e r	|evaluate region


Key Binding	| Function
---|---
SPC m g g	|go to definition
SPC m g G	|go to definition in another window
SPC m h h	|describe elisp thing at point (show documentation)
SPC m t b	|execute buffer tests
SPC m t q	|ask for test function to execute

#### 14.8.17 鼠标使用情况
有一些添加的鼠标功能为行号边距设置（如果显示）：
- 在行号边界中单击可直观地选择整个行
- 拖过行号边距可以直观地选择区域
- 双击行号边界，直观地选择当前的代码块

### 14.9管理项目
在 Spacemacs 中的项目是用 [projectile](https://github.com/bbatsov/projectile) 来管理的。在 projectile 项目中是隐式定义的，例如，当在文件树中遇到 .git 存储库或 .projectile 文件时找到项目的根。

只要有可能，就使用 Helm。

在项目中搜索查看 [project searching](http://spacemacs.org/doc/DOCUMENTATION.html#searching-in-a-project).

projectile 命令以 p 开头：

Key Binding	| Description
---|---
SPC p '	|open a shell in project's root (with the shell layer)
SPC p !	|run shell command in project's root
SPC p &	|run async shell command in project's root
SPC p %	|replace a regexp
SPC p a	|toggle between implementation and test
SPC p b	|switch to project buffer
SPC p c	|compile project using projectile
SPC p d	|find directory
SPC p D	|open project root in dired
SPC p f	|find file
SPC p F	|find file based on path around point
SPC p g	|find tags
SPC p C-g	|regenerate the project's etags / gtags
SPC p h	|find file using helm
SPC p I	|invalidate the projectile cache
SPC p k	|kill all project buffers
SPC p o	|run multi-occur
SPC p p	|switch project
SPC p r	|open a recent file
SPC p R	|replace a string
SPC p t	|open NeoTree in projectile root
SPC p T	|test project
SPC p v	|open project root in vc-dir or magit
SPC /	|search in project with the best search tool available
SPC s p	|see search in project
SPC s a p	|run ag
SPC s g p	|run grep
SPC s k p	|run ack
SPC s t p	|run pt

> 注意windows用户：启用快速索引 GNU find 或 Cygwin find 必须在你的 PATH 中。

### 14.10 寄存器(Registers)
对各个寄存器的访问命令以r开头:

Key Binding	| Description
---|---
SPC r e	|show evil yank and named registers
SPC r m	|show marks register
SPC r r	|show helm register
SPC r y	|show kill ring

### 14.11错误处理
Spacemacs 使用  [Flycheck](https://github.com/flycheck/flycheck) 实时提供错误反馈。检查仅在保存时间默认情况下执行。

错误管理命令（以e开头）：

Key Binding	|Description
---|---
SPC t s	|toggle flycheck
SPC e c	|clear all errors
SPC e h	|describe a flycheck checker
SPC e l	|toggle the display of the flycheck list of errors/warnings
SPC e n	|go to the next error
SPC e p	|go to the previous error
SPC e v	|verify flycheck setup (useful to debug 3rd party tools configuration)
SPC e .	|error transient state

下一个/上一个错误绑定和错误瞬态可用于浏览来自 flycheck 的错误以及来自编译缓冲区的错误，甚至可以用来支持 emacs 的下一个错误 API 的任何事情。这包括例如已经被保存到单独的缓冲区的搜索结果。

自定义边缘位图：

Symbol	|Description
---|---
![row 1 col 1](http://spacemacs.org/doc/img/dot-error.png) | Error
![row 2 col 1](http://spacemacs.org/doc/img/dot-warning.png) | warning
![image](http://spacemacs.org/doc/img/dot-info.png)| Info 

### 14.12 编译
Spacemacs 绑定了一些命令来支持编译项目。

Key Binding	| Description
---|---
SPC c c	|use helm-make via projectile
SPC c C	|compile
SPC c d	|close compilation window
SPC c k	|kill compilation
SPC c m	|helm-make
SPC c r	|recompile

### 14.13 模式(Modes)
#### 4.13.1 主模式 leader 键(Major Mode leader key)
特定于当前主要模式的键绑定以spc m开头。为方便起见，默认情况下会设置一个称为主模式 leader 键的快捷键，这可以节省一笔宝贵的击键。

可以通过在 〜/.spacemacs 中定义变量 dotspacemacs-major-mode-leader-key 来更改主模式的 leader 键。例如在列表中设置键：


```lisp
(setq-default dotspacemacs-major-mode-leader-key "<tab>")
```

#### 14.13.2 Helm
Spacemacs 将 hjkl 导航添加到 helm 缓冲区：

Key Binding	| Description
---|---
C-h	|go to next source
C-H	|describe key (replace C-h)
C-j	|go to previous candidate
C-k	|go to next candidate
C-l	|same as return

### 14.14 emacs服务器
Spacemacs 在启动时启动服务器。这个服务器在你关闭你的 emacs 窗口时会被终止。
#### 14.14.1 连接到 emacs 服务器
您可以使用 emacsclient 从终端在 emacs 中打开一个文件。使用 emacsclient -c 在 Emacs GUI 中打开文件。使用 emacsclient -t 在终端内的 Emacs 中打开文件。

如果您希望您的 Linux/OS X 系统默认使用 Emacs 作为任何提示，您需要将其设置为您的 shell 配置，例如，〜/.bashrc 或 〜/.zshrc：

```
export EDITOR="emacsclient -c"
```
请注意，如果您使用 OS X，则可能需要引用您的 GUI Emacs 附带的 emacsclient，例如：

```
export EDITOR="/Applications/Emacs.app/Contents/MacOS/bin/emacsclient -c"
```
> 提示：记得在 emacs 中编辑文件后使用：wq 或 C-x＃。

有关更多详细信息，请参阅官方 Emacs 手册中的 [Emacs 作为服务器](https://www.gnu.org/software/emacs/manual/html_node/emacs/Emacs-Server.html)。

### 14.15 保持服务器开着
通过在 〜/spacemacs 中将变量 dotspacemacs-persistent-server 设置为  t 关闭 Emacs，可以使服务器保持活动状态。


```lisp
(setq-default dotspacemacs-persistent-server t)
```

当此变量设置为 t 时，退出 Emacs 并终止服务器的唯一方法是使用以下绑定：

Keybinding	| Description
---|---
SPC q |Quit Emacs and kill the server, prompt for changed buffers to save
SPC q Q	|Quit Emacs and kill the server, lose all unsaved changes.
SPC q r	|Restart both Emacs and the server, prompting to save any changed buffers
SPC q s	|Save the buffers, quit Emacs and kill the server
SPC q z	|Kill the current frame

### 14.16 故障排除(Troubleshoot)
#### 14.16.1 Loading fails
如果在加载过程中发生错误，mode-line 将变为红色，并且错误应该在启动缓冲区中内联显示。Spacemacs 应该仍然可用;如果不是，那么用 emacs --debug-init 重新启动 Emacs，并用 backtrace 打开一个 [Github issue](https://github.com/syl20bnr/spacemacs/issues)。

#### 14.16.2 升级/降级 Emacs 版本
为了确保软件包能够针对您安装的新 Emacs 版本进行正确编译，请务必使用 SPC SPC spacemacs/recompile-elpa 运行交互式命令 spacemacs/recompile-elpa。

