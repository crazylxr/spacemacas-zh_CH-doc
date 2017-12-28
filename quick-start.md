# Quick start
## 1 Configuration layers
spacemacs将其配置分为独立的单元（称为***configuration layers***(配置层)）。这些层堆叠在一起，实现自定义配置。

默认情况下，spacemacs 使用称为 〜/ .spacemacs 的点文件来控制要加载的层。在这个文件中你也可以配置某些功能。

配置层是一个至少包含一个 packages.el 文件的目录，该文件使用 emacs 的 package.el 内置特性来定义和配置要从 emacs 包存储库下载的包。

如果您已经拥有自己的 emacs 配置，则可以将其移至自己的 layer。

以下命令在专用目录中创建一个图层：

```
SPC : configuration-layer/create-layer RET
```

你创建的任何配置层必须显式加载到 〜/ .spacemacs 中。

注意：为了您的隐私，私人目录的内容不受源代码管理。请参阅[文档](http://spacemacs.org/doc/DOCUMENTATION.html)中有关专用配置管理的部分。

## 2 Dotfile (.spacemacs)
如上所述 .spacemacs 控制要加载的配置层，也是自定义 spacemacs 的一种手段

以下命令将在您的主目录中创建一个 .spacemacs 文件：


```
SPC : dotspacemacs/install RET
```
打开已安装的 dotfile 文件：

```
SPC f e d
```
使用变量 dotspacemacs-configuration-layers 加载一些配置层


```lisp
;; List of configuration layers to load.
dotspacemacs-configuration-layers '(auto-completion smex)
```
一些配置层支持配置变量来暴露对层特定功能的粒度控制，git层就是这样一个例子。变量可以直接在 dotspacemacs-configuration-layers 中设置，如下所示：

```lisp
;; List of configuration layers to load.
dotspacemacs-configuration-layers '(auto-completion
                                    (git :variables
                                         git-magit-status-fullscreen t)
                                    smex)
```
在任何时候，您都可以通过按 spc f e r 来应用对点文件或图层所作的更改，而无需重新启动 spacemacs。

dotfile 模板包含有关如何自定义 spacemacs 的更多信息。有关更多详细信息，请参阅文档的 dotfile 配置部分。

## 3 Dotdirectory (~/.spacemacs.d)
像emacs一样，spacemacs 的初始化也可以被包含在特殊目录 〜/ .spacemacs.d 中的 init.el 文件中。dotfile 的内容应该被复制到 init.el 文件中。

emacs dotfile 或 dotdirectory 不会被替换，而是被 spacemacs dotfile 或  dotdirectory 所补充。在启动过程中，emacs 仍然使用 〜/.emacs.d/init.el（或〜/ .emacs）进行初始化，而 user-emacs-directory 仍然会指向 〜/ .emacs.d /，即使 〜/.spacemacs.d 或 〜/.spacemacs 存在。只有现在〜/.emacs.d/init.el 是由 spacemacs 提供的（例如在将 spacemacs git repo 克隆到一个空的 〜/.emacs.d/ 之后），并且你自己的个人配置进入 〜/ .spacemacs.d/init.el（或 〜/.spacemacs）。

有一个简单的解决方法，以维护（您的以前）原生 emacs 和（你的新的）spacemacs 配置并排，而不需要重命名和备份〜/.emacs.d/。

## 4 Learning Spacemacs
### 4.1 Editing Styles
spacemacs 可以被 vim 用户或 emacs 用户使用，方法是在 dotfile〜/.spacemacs 中将 dotspacemacs-editing-style 变量设置为 vim，emacs 甚至是 hybrid。
### 4.2 The leader keys
spacemacs 键绑定使用默认绑定到 vim 的 spc（空格键）或混合编辑样式的绑定键和 emacs 样式的 M-m。

如果使用 vim 风格或者使用 emacs 风格（这些变量必须在文件〜/ .spacemacs中设置），则可以通过设置变量 dotspacemacs-leader-key 来更改它。

为了简单起见，文档始终将 leader 称为 spc 。

在默认情况下设置 , 为辅助的leader key被称为 major-mode 的leader key。此键是所有主模式特定命令都绑定的 spc m 的快捷方式。

### 4.3 Evil-tutor
如果你愿意学习 vim 的键绑定（强烈推荐，因为你可以从 emacs 风格中获益），按 spc h t 开始一个 Evil-adapted vimtutor。

### 4.4 Universal argument
在vim编辑风格中，通用参数默认为 spc u 而不是 c-u，因为后者用于在vim中向上滚动。

### 4.5 Configuration layers and Package discovery
通过使用helm-spacemacs-help与spc h spc，您可以快速搜索包并获取使用它的图层的名称。你也可以轻松地去一个图层的readme.org或去一个包的初始化函数。

### 4.6 Key bindings discovery
由于[which-key](https://github.com/justbur/emacs-which-key), 每当一个前缀命令被按下（如SPC）一秒钟后出现一个缓冲区列出了这个前缀可能的键。

也可以通过按下来搜索特定的键绑定：

```
SPC ?
```

要将绑定列表缩小到以spc为前缀的那些列表，请键入如下正则表达式的模式：


```
SPC\ b
```

这将列出所有缓冲区相关的绑定。注意：你在helm-descbind提示符下，模式由6个字母组成：大写的spc，反斜线，实际的空格和小写的b。

### 4.7 Describe functions
Describe functions 是强大的 emacs introspection 命令来获取有关函数，变量，模式等信息，因此这些命令是绑定的：

Key Binding | Description
---|---
SPC h d f | describe-function
SPC h d k | describe-key
SPC h d m | describe-mode
SPC h d v | describe-variable

### 5 How-To's
一些快速的方法是编写在[FAQ.org](http://spacemacs.org/doc/FAQ.html#MissingReference)文件中。


