## 6 Configuration layers
本部分是 layer 的概述。可以在这里找到更多关于编写配置 layers  的介绍（推荐阅读！）。
### 6.1 Purpose
layers 有助于收集相关的软件包以提供功能。例如，python 层为 python 文件提供自动完成，语法检查和 REPL 支持。这种方法有助于保持配置的组织性，并减少用户的开销，使他们不必考虑要安装哪些软件包。要安装所有的 python 功能，用户只需要将 python 图层添加到他们的 dotfile 文件中即可。

### 6.2 Structure
配置按层组织。每层都有以下结构：

```
[layer_name]
  |__ [local]
  | |__ [package 1]
  | |     ...
  | |__ [package n]
  |-- layers.el
  |__ packages.el
  |__ funcs.el
  |__ config.el
  |__ keybindings.el

[] = directory
```

Where:

文件 | 用法
---|---
layers.el | 声明额外图层的地方
packages.el | packages 列表及其配置函数（init，post-init等）
funcs.el | 在 layer 中定义的所有功能（例如在 package 配置中使用）
config.el | Layer 配置 （定义 layer 变量默认值并设置一些配置变量）
keybindings.el | 一般的 key 绑定不绑定到特定的 package 配置

Packages 可以是：
- 从符合 ELPA 的仓库安装的 ELPA packages
- 本地 packages 在一个 layer 的本地文件夹中
- 使用 [quelpa](https://github.com/quelpa/quelpa) 从在线来源安装。

### 6.3 Configure packages
#### With a layer
##### Declaration
Packages 在一个名为 <layer>-packages 的变量中声明，其中 <layer> 是 layer 的名称。

Example:

```lisp
(setq <layer>-packages '(package1 package2 ...)
```
来自所有 layers 的所有 packages 都按字母顺序处理，所以有时您必须使用一些加载后的黑魔法来正确配置它们。例如，如果包 a 取决于 b，那么你可以配置一个：

```lisp
(with-eval-after-load 'B ...)
```
有关使用 quelpa 或本地软件包安装软件包的详细信息，请参阅 [LAYERS](http://spacemacs.org/doc/LAYERS.html#orgheadline12).

##### 6.3.1.2 Initialization
要初始化一个包 xxx，用这个格式在 packages.el 中定义一个函数：

```lisp
(defun <layer>/init-xxx () ...body )
```
用 use-package 宏定义 body 是很常见的。

##### 6.3.1.3 Exclusion
有可能在每层的基础上从 spacemacs 中排除一些软件包。这在配置 layer 旨在替换 spacemacs layer 中声明的库存包时非常有用。

要这样做，请将要排除的软件包名称添加到变量 <layer>-excluded-packages 中

Example:

```
(setq <layer>-excluded-packages '(package1 package2 ...)
```
#### 6.3.2 Without a layer
有时一个 layer 可能是一个不必要的开销，如果你只想安装一个与其关联的配置很少的包，就是这种情况。一个很好的例子是一些你只对语法高亮感兴趣的小众语言。

您可以通过将它们添加到 dotfile 中的 dotspacemacs/layers 函数下的变量 dotspacemacs-additional-packages 来安装此类包。

例如，安装 llvm-mode 和 dts-mode：

```lisp
(defun dotspacemacs/layers ()
  "Configuration Layers declaration..."
  (setq-default
   ;; ...
   dotspacemacs-additional-packages '(llvm-mode dts-mode)
   ;; ...
   ))
```
如果您想为它们添加一些配置，请将配置放置在 dotspacemacs/user-config 函数中，或者考虑创建一个 layer。

### 6.4 Packages synchronization
spacemacs 将只安装用户明确使用的 packages 。如果使用该 layer（即，在 dotspacemacs-configuration-layers 中列出），则认为该 package 被使用。任何未使用的 package 都被认为是孤立的，并在下次启动 emacs 时被删除。

### 6.5 Types of configuration layers
有两种类型的配置 layers：
- 分布式 layers（在 layers 目录中，这些 layers 是社区共享的贡献，并在上游合并）
- 私人（在私人目录中，他们被git忽略）

### 6.6 Submitting a configuration layer upstream
如果您决定提供配置 layer，请首先查看[贡献指南](http://spacemacs.org/CONTRIBUTING.html) (现在404)）。

### 6.7 Example: Themes Megapack example
这是一个简单的配置 layer，列出了一些你可以在[这里](http://spacemacs.org/layers/themes-megapack/README.html)找到的主题。（这里也404）

要安装它，只需添加主题 megapack 到你的 〜/.spacemacs 就好：

```lisp
(setq-default dotspacemacs-configuration-layers '(themes-megapack))
```
添加这个 layer 将安装大约100个主题;卸载它们，从 dotspacemacs-configuration-layers 中删除该层，然后按 spc f e r。

### 6.8 Managing private configuration layers
spacemacs的配置系统足够灵活，让你以不同的方式管理你的私人 layers。

#### 6.8.1 Using the private directory
私人目录中的所有内容都被git忽略，所以它是存储私人 layers 的好地方。这种方法有一个巨大的缺点：你的 layers 不受源代码控制。

#### 6.8.2 Using an external Git repository
这是管理你的私人 layers 的推荐方式。

最好的方法是将你所有的私有 layers 存储到外部的 git 仓库中。如果有的话，将它们存储在 dotfiles 存储库中是一个很好的做法。还把你的 〜/.spacemacs文件放在里面。

那么你可以自由地将你的 layer 符号链接到 〜/emacs.d/private 或者让它们在你想要的任何地方，并且在 〜/.spacemacs 的变量 dotspacemacs-configuration-layer-path 中引用父目录。

请注意，您也可以为所有私有 layer 设置专用存储库，然后直接在 〜/.emacs.d/private 中克隆该存储库。

#### 6.8.3 Using a personal branch
管理你的私人 layers 的最后一个主要方法是把他们推到一个你跟上游 master 或者 devolop分支保持同步的个人分支。

### 6.9 Tips for writing layers
请参考这个介绍，了解一些关于写 layers 的技巧，以及如何最好地使它们符合 spacemacs 理念和加载策略。