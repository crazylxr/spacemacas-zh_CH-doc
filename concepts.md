## 8 Concepts
### 8.1 Editing Styles
spacemacs 带有几种可动态切换的编辑风格，提供了一种更简单的方式来进行配对编程，例如 vim 用户和 emacs 用户之间。

有三种风格可供选择：
- Vim
- Emacs
- Hybrid(a mix between Vim and Emacs)

#### Vim
spacemacs 的行为就像在 vim 中使用 Evil mode 包模拟 vim 快捷键绑定。这是 spacemacs 的默认样式;可以通过在 dotfile 中将 dotspacemacs-editing-style 变量设置为 vim 来明确设置。

在 vim 编辑风格（插入状态）中绑定键值：

```lisp
(define-key evil-insert-state-map (kbd "C-]") 'forward-char)

```
#### 8.1.2 Emacas
spacemacs 的行为就像在原始 emacs 中使用 Holy mode 配置 Evil，使 emacs 处于默认状态。在 dotfile 中将 dotspacemacs-editing-style变量设置为 emacs。

在 emacs 风格 leader 是可用的 M-m。当关闭 vim 风格时，可以使用 SPC t E e 和 M-m t E e 来打开和关闭。

在 emacs 编辑风格（emacs state）中绑定键值：

```lisp
(define-key evil-emacs-state-map (kbd "C-]") 'forward-char)
```
#### 8.1.3 Hybrid
Hybrid 编辑风格就像 vim 风格，只不过插入状态被称为混合状态的新状态所取代。在混合状态下，所有 emacs 键绑定都可用;这就像用 emacs 状态替换插入状态，但提供了一个孤立的键映射 evil-hybrid-state-map。

以 Hybrid 编辑风格（hybrid state）绑定键：


```lisp
(define-key evil-hybrid-state-map (kbd "C-]") 'forward-char)
```
这种风格可以调整为更像 Emacs 或更像 Vim 取决于用户的喜好。以下变量可用于更改样式配置：

- hybrid-mode-default-state 打开新缓冲区时的默认状态，默认是 normal。将其设置为 emacs 以获得更多的流畅风格。
- hybrid-mode-enable-hjkl-bindings 如果不是空，那么软件包将配置 h j k l 导航的键绑定。
- hybrid-mode-enable-evilified-state，如果非 nil 缓冲区在被支持的情况是 evilified，如果 nil 则在这些缓冲区中启用 emacs 状态。

默认配置是：

```lisp
(setq-default dotspacemacs-editing-style '(hybrid :variables
                                           hybrid-mode-enable-evilified-state t
                                           hybrid-mode-enable-hjkl-bindings nil
                                           hybrid-mode-default-state 'normal)
```
使用 SPC t E h 和 M-m t E h 来切换混合风格。当关闭vim样式启用。

### 8.2 States
spacemacs有10种状态:

State | Default Color | Descripton
---|--- | ---
normal | orange | 像 vim 的 normal mode，用来执行和组合命令
insert | green | 像 vim 的 insert mode，用于实际插入文本
visual | gray | 像 vim 的 visual mode，用来进行文本选择
motion | purple | Evil 专属，用于导航只读缓冲区
emacs | blue | Evil 专属，使用这种状态就像使用没有 vim 的普通 emacs 一样
replace | chocolate | Evil专属，覆盖点下的字符而不是插入新字符
hybrid | blue | Spacemacs 专属，这就像插入状态，除了所有的 emacs 键绑定是可用的
evilified | light brown | Spacemacs 专属，这是一个 emacs 状态修改，以带来 vim 导航，选择和搜索。
lisp | pink | Spacemacs 专属，用于导航 lisp 代码并修改它（[更多信息](http://spacemacs.org/doc/DOCUMENTATION.html#editing-lisp-code)）
iedit | red | Spacemacs 专属，用于使用 iedit 在多个文本区域之间导航（[更多信息](http://spacemacs.org/doc/DOCUMENTATION.html#replacing-text-with-iedit)）
iedit-insert | red | Spacemacs 专属，用于使用 iedit 替换多个文本区域（[更多信息](http://spacemacs.org/doc/DOCUMENTATION.html#replacing-text-with-iedit)）

> 注意：从技术上讲还有 operator 的 evil 状态。

### 8.3 Evilified modes
一些缓冲区不用于编辑文本，并为某些操作提供自己的键绑定。这些经常与vim绑定冲突。为了使这样的缓冲区更像 vim 一致的方式，他们使用一个称为 evilified 状态的特殊状态。在 evilified 状态中，一些键工作在Evil中，有 /, :, h, j, k, l, n, N, v, V, gg, G, C-f, C-b, C-d, C-e, C-u, C-y 和 C-z，所有其他的按键按照底层模式的意图工作。

Shadowed keys 将按照以下模式移动：a → A → C-a → C-A。

例如，如果模式将函数绑定到n，在 evilified 状态下在 C-n 下被发现，因为 n 和 N 都是保留的，但 C-n 不是。另一方面，任何最初绑定到 k 的东西都会在 K 上找到，因为 k 是保留的，但 K 不是。如果在 K 上有绑定，那将被移到 C-k。

除此之外，C-g（作为 emacs 中的一个重要的转义键）被跳过。所以任何绑定到 g 的东西都会在 C-g 上找到，因为 g，G和 C-g 都是保留的。

### 8.4 Evil leader
spacemacs 使用 leader 键来绑定几乎所有的键绑定。

这个 leader 键 通常被 vim 用户设置在 spacemacs 中， leader 键 被设置在 SPC（空格键，因此命名为 spacemacs）上。这个键是键盘上最容易访问的键，用拇指按下这个键是降低 rsi 风险的好选择。它可以使用变量 dotspacemacs-leader-key 和 dotspacemacs-emacs-leader-key 来定制到任何其他键。

使用 spacemacs 不需要重新映射你的键盘修改器来试图减少 RSI 的风险，当你在正常模式下按下 SPC leader 键时，每个命令都可以很容易地执行，这里有几个例子：
- 保存一个buffer： SPC f s
- 保存所有打开的buffer： SPC f S
- 打开（切换）到一个缓冲区用 helm: SPC b b

### 8.5 Universal argument
通用参数 C-u 是 emacs 中的一个重要命令，但它也是一个非常方便的 vim 键绑定向上滚动。

spacemacs 绑定 C-u 以向上滚动并将通用参数绑定更改为 spc u。

> 注意：SPC u 在 helm-M-x（SPC SPC）之前不工作。相反，首先调用 helm-M-x，选择要运行的命令，然后在按下 return 之前按 C-u。例如：SPC SPC org-reload C-u RET

### 8.6 Transient-states
spacemacs 定义了各种各样的 transient states（临时覆盖图）。这可以防止在 SPC 键上进行重复和繁琐的按压。

当 transient state 处于活动状态时，文档将显示在小型 buffer 中。附加信息也可以显示在小 buffer 中。

自动高亮符号 transient state：
![image](http://spacemacs.org/doc/img/spacemacs-ahs-transient-state.png)

[文本缩放 transient state：](http://spacemacs.org/doc/DOCUMENTATION.html#text)
![image](http://spacemacs.org/doc/img/spacemacs-scale-transient-state.png)