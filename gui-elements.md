## 12 GUI Elements
spacemacs有一个简约和分布的免费的图形用户界面：
- 自定义 [powerline](https://github.com/milkypostman/powerline) mode-line 与[颜色反馈](http://spacemacs.org/doc/DOCUMENTATION.html#flycheck-integration)根据当前 [Flycheck](https://github.com/flycheck/flycheck) 状态
- Unicode 符号为了 minor mode 不兼容 出现在 mode-line
- [自定义 fringe bitmaps ](http://spacemacs.org/doc/DOCUMENTATION.html#errors-handling)和 Flycheck 的错误反馈

### 12.1 Color themes
官方的 spacemacs 主题是 spacemacs-dark，它是您首次启动 spacemacs 时安装的默认主题。有两个主题的变体，一个是黑色(dark)的，一个是轻(light)的。这些主题的一些方面可以在 〜/.spacemacs 的 dotspacemacs/user-init 函数中定制：
- 带有布尔值 spacemacs-theme-comment-bg 的注释背景
- org 部分标题的高度与 spacemacs-theme-org-height

可以使用变量 dotspacemacs-themes 在〜/.spacemacs 中定义默认主题。例如指定 spacemacs-light，leuven 和 zenburn：


```lisp
(setq-default dotspacemacs-themes '(spacemacs-light leuven zenburn))
```

Key Binding | Description
---|---
SPC T n	 | 切换到在 dotspacemacs-themes 中列出的下一个主题。
SPC T s | 从 helm buffer 选择一个主题。
您可以从 [Rob Merrell ](https://twitter.com/robmerrell)的[主题库](https://themegallery.robdor.com/)中看到所有包含主题的样本。

**注意：**
- 您不需要在 layers 中明确列出您在 dotspacemacs-themes 中定义的主题包，但是 spacemacs 非常聪明，可以从孤立列表中删除这些包。
- 由于 emacs 中主题的内部工作，在同一 session 中切换主题可能会有一些奇怪的副作用。虽然这些副作用应该是非常罕见的。
- 在 emacs 的终端版本中，颜色主题将无法正确呈现，因为终端呈现的是颜色，而不是由 emacs 呈现。你可能不得不改变你的终端调色板。更多的解释可以在 [emacs-color-theme-solarized](https://github.com/sellout/emacs-color-theme-solarized#important-note-for-terminal-users) 网页上找到。

提示：如果你是一名 Org 用户，[leuven-theme](https://github.com/fniessen/emacs-leuven-theme) 是你很好的选择。

### 12.2 Font
spacemacs 使用的默认字体是 [Source Code Pro](https://github.com/adobe-fonts/source-code-pro) 。如果你想使用它，建议将它安装在你的系统上。

更改默认字体在您的 .spacemacs 文件中设置变量 dotspacemacs-default-font。默认情况下它的值是：

```lisp
(setq-default dotspacemacs-default-font '("Source Code Pro"
                                          :size 13
                                          :weight normal
                                          :width normal
                                          :powerline-scale 1.1))
```

如果没有找到指定的字体，将使用回退之一（取决于您的系统）。还要注意，如果您在终端中运 行emacs，更改此值不起作用。

属性应该非常简单，可以设置 [font-spec ](http://www.gnu.org/software/emacs/manual/html_node/elisp/Low_002dLevel-Font.html)的任何有效属性：
- :family 字体族或 fontset（一个字符串）。
- :width 相对字符宽度。这应该是其中的一个符号：
    - ultra-condensed
    - extra-condensed
    - condensed
    - semi-condensed
    - normal
    - semi-expanded
    - expanded
    - extra-expanded
    - ultra-expanded
- :height 字体的高度。在最简单的情况下，这是以1/10点为单位的整数。
- :weight font weight - 符号之一（从最密集到最薄弱）：
    -   ultra-bold
    -   extra-bold
    -   bold
    -   semi-bold
    -   normal
    -   semi-light
    -   extra-light
    -   ultra-light
- :slant 字体倾斜 - 符号之一：
    - italic
    - oblique
    - normal
    - reverse-italic
    - reverse-oblique
- :size 字体大小 - 指定像素大小的非负整数或指定点大小的浮点数。
- :adstyle 字体的其他印刷风格信息，如“sans”。该值应该是一个字符串或一个符号。
- :registry charset注册表和字体的编码，如'iso8859-1'。该值应该是一个字符串或一个符号。
- :script 字体必须支持的脚本（一个符号）。

特殊属性：powerline-scale 是 spacemacs 特有的，用于快速调整模式行高度，以避免像下面截图（默认值为1.1）那样对分隔符进行糟糕的渲染。

![img](http://spacemacs.org/doc/img/crappy-powerline-separators.png)
Ugly separators

### 12.3 GUI Toggles
一些图形用户界面指标可以打开和关闭（切换从 t 和 T 开始）：

Key Binding | Description
---|---
SPC t 8 | 高亮显示第80列以后的任何字符
SPC t f | 显示填充列（默认填充列设置为80）
SPC t h h | 切换当前行的高亮显示
SPC t h i | 切换突出显示缩进级别
SPC t h c | 切换高亮显示缩进当前列
SPC t i | 在点处切换缩进指南
SPC t l | 切换截断线
SPC t L | 切换视线
SPC t n | 切换行号
SPC t v | 切换平滑滚动


Key Binding | Description
---|---
SPC T ~ | 在空行的边缘显示 ~ 
SPC T F | 全屏切换帧
SPC T f | 切换显示边缘
SPC T m | 切换菜单栏
SPC T M | 切换帧最大化
SPC T t | 切换工具栏
SPC T T | 切换帧透明度并进入透明度瞬态状态

> 注意：这些切换都可以通过 helm-spacemacs-help 界面获得（按 SPC h SPC 显示 helm-spacemacs-help 缓冲区）。

#### 12.3.1 Global line numbers
可以通过在 〜/.spacemacs 中将 dotspacemacs-line-numbers 变量设置为与 nil 不同的值来在所有编程模式和文本模式缓冲区中切换行号。

```lisp
(setq-default dotspacemacs-line-numbers t)
```
如果它被设置为 relative，行号以相对的方式显示：

```lisp
(setq-default dotspacemacs-line-numbers 'relative)
```
### 12.4 Mode-line

mode line 是一个高度定制的 [powerline](https://github.com/milkypostman/powerline)，具有以下功能：
- 显示窗口号码
- 当前状态的颜色代码
- 通过 anzu 显示搜索次数
- 切换 flycheck 信息
- 切换电池信息
- 切换 minor mode lighters

提醒各状态的颜色代码：

Evil State | Color
---|---
Normal | Orange
Insert | Green
Visual | Grey
Emacs | Blue
Motion | Purple
Replace | Chocolate
Lisp | Pink
Iedit/Iedit-Insert | Red

一些元素可以动态切换：

Key Binding | Description
---|---
SPC t m b | 切换电池状态
SPC t m c | 切换 org 任务时钟（在 org layer 中可用）
SPC t m m | 切换 minor mode lighters
SPC t m M | 切换 major mode
SPC t m n | 切换 cat！（如果在 dotfile 中声明了 colors layer）
SPC t m p | 切换点字符位置
SPC t m t| 切换 mode line 本身
SPC t m v | 切换版本控制信息
SPC t m V | 切换新版本更轻

#### 12.4.0.1 Powerline font installation for terminal-mode users
在终端模式下运行 emacs的 用户可能需要安装 [powerline 补丁字体](https://github.com/powerline/fonts)并配置其终端客户端使用它们使 powerline 分隔符正确呈现。
#### 12.4.0.2 Flycheck integration
当启用 Flycheck次要模式时，会显示一个新元素，显示错误，警告和信息的数量。

![flycheck](http://spacemacs.org/doc/img/powerline-wave.png)
*Flycheck integration in mode-line*

#### 12.4.0.3 Anzu integration
[Anzu](https://github.com/syohex/emacs-anzu) 显示执行搜索时发生的次数。当 n 或  N 被按下时，spacemacs 通过暂时显示 Anzu 状态来很好地集成 Anzu 状态。请参阅以下屏幕截图中的 5/6 细分。
![Anzu](http://spacemacs.org/doc/img/powerline-anzu.png)
*Anzu integration in mode-line*

#### 12.4.0.4 Battery status integration
[fancy-battery](https://github.com/lunaryorn/fancy-battery.el) 显示电池总电量的百分比，以及电池完全充电或放电的剩余时间。

颜色码用于电池状态：

Battery State | Color
---|---
Charging| Green
Discharging | Orange
Critical | Red
请注意，这些颜色可能因您的主题而异。

#### 12.4.0.5 Powerline separators
可以通过在 〜/spacemacs 中设置 powerline-default-separator 变量，然后重新编译模式行来轻松定制 powerline 分隔符。例如，如果您想将分隔符设置回已知的箭头分隔符，请将以下代码段添加到您的配置文件中：

```lisp
(defun dotspacemacs/user-config ()
  "This is were you can ultimately override default Spacemacs configuration.
This function is called at the very end of Spacemacs initialization."
  (setq powerline-default-separator 'arrow))
```

为了节省时间来尝试所有可能的 powerline，下面是一组详尽的截图：

Separator | Screenshot
---|---
alternate | ![alternate](http://spacemacs.org/doc/img/powerline-alternate.png)
arrow | ![arrow](http://spacemacs.org/doc/img/powerline-arrow.png)
arrow-fade | ![arrow](http://spacemacs.org/doc/img/powerline-arrow-fade.png)
bar | ![arrow](http://spacemacs.org/doc/img/powerline-bar.png)
box | ![arrow](http://spacemacs.org/doc/img/powerline-box.png)
brace | ![arrow](http://spacemacs.org/doc/img/powerline-brace.png)
butt | ![arrow](http://spacemacs.org/doc/img/powerline-butt.png)
hamfer | ![arrow](http://spacemacs.org/doc/img/powerline-chamfer.png)
contour | ![arrow](http://spacemacs.org/doc/img/powerline-contour.png)
curve | ![arrow](http://spacemacs.org/doc/img/powerline-curve.png)
rounded | ![arrow](http://spacemacs.org/doc/img/powerline-rounded.png)
roundstub | ![arrow](http://spacemacs.org/doc/img/powerline-roundstub.png)
slant | ![arrow](http://spacemacs.org/doc/img/powerline-slant.png)
wave | ![arrow](http://spacemacs.org/doc/img/powerline-wave.png)
zigzag | ![arrow](http://spacemacs.org/doc/img/powerline-zigzag.png)
nil | ![arrow](http://spacemacs.org/doc/img/powerline-nil.png)

#### 12.4.0.6 Minor Modes
spacemacs 使用 [diminish mode](http://www.emacswiki.org/emacs/DiminishedModes) 来减小 minor mode 指示器的大小：

minor mode 区域可以用 spc t m m 来打开和关闭

unicode 符号默认显示。在 〜/.spacemacs 中将变量 dotspacemacs-mode-line-unicode-symbols 设置为 nil 将会显示 ascii 字符（如果你不能设置合适的字体，可能会在终端中使用）。

显示在 mode-line 中的字母与用于切换它们的键绑定相对应。

一些切换有两种风格：local 和 global。可以使用 control 键来达到切换的全局版本。

Key Binding | Unicode | ASCll | Mode
---|--- | --- | ---
SPC t -	|⊝ |	-	| centered-cursor mode
SPC t 8	|⑧	|8	|toggle highlight of characters for long lines
SPC t C-8|	⑧	|8	|global toggle highlight of characters for long lines
SPC t C--|	⊝|	-|	global centered cursor
SPC t a	|ⓐ	|a	|auto-completion
SPC t c|	ⓒ|	c|	camel case motion with subword mode
none|	ⓔ|	e|	evil-org mode
SPC t E e|	Ⓔe|	Ee	|emacs editing style (holy mode)
SPC t E h|	Ⓔh	|Eh	|hybrid editing style (hybrid mode)
SPC t f|	ⓕ|	f|	fill-column-indicator mode
SPC t F	|Ⓕ	|F	a|uto-fill mode
SPC t g	|ⓖ	|g	|golden-ratio mode
SPC t h i|	ⓗi|	hi	|toggle highlight indentation levels
SPC t h c|	ⓗc	|hc	|toggle highlight indentation current column
SPC t i	|ⓘ|	i|	indentation guide
SPC t C-i|	ⓘ|	i	|global indentation guide
SPC t I|	Ⓘ|	I	|aggressive indent mode
SPC t K	|Ⓚ	|K	|which-key mode
SPC t p	|ⓟ	|p	|smartparens mode
SPC t C-p|	ⓟ|	p|	global smartparens
SPC t s	|ⓢ	|s	|syntax checking (flycheck)
SPC t S|	Ⓢ	|S	|enabled in spell checking layer (flyspell)|	W|	automatic whitespace cleanup (see dotspacemacs-whitespace-cleanup)
SPC t C-W|	Ⓦ	|W	|automatic whitespace cleanup globally
SPC t y	|ⓨ	|y|	yasnippet mode

#### 12.4.0.7 Customizing the mode-line
spacemacs 使用 [Spaceline](https://github.com/TheBB/spaceline) 来提供其 mode-line。它由左右两侧的若干段组成。这些在变量 spaceline-left 和 spaceline-right 中定义。可以使用 spaceline-define-segment 定义段，并将其添加到左侧或右侧变量的相应位置。

请参阅 Spaceline 文件以获取更多信息。