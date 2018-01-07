## 7 Dotfile Configuration

用户配置可以存储在你的 〜/ .spacemacs 文件中。

### 7.1 Dotfile Installation
spacemacs 第一次启动，它会问你几个问题，然后在 *HOME* 中安装 .spacemacs。
### 7.2 Alternative dotdirectory
一个 dotdirectory 〜/ .spacemacs.d /可以用来代替 dotfile。如果你想使用这个选项，把  〜/.spacemacs 移动到〜/.spacemacs.d/init.el。

也可以使用环境变量 SPACEMACSDIR 来覆盖 〜/.spacemacs.d/ 的位置。当然你也可以使用符号链接来改变这个目录的位置。

> 注意：〜/.spacemacs将总是优先于  〜/.spacemacs.d/init.el，所以 〜/.spacemacs 不能存在于 〜/.spacemacs.d/init.el 以供 spacemacs 使用

### 7.3 Synchronization of dotfile changes

要应用在 〜/.spacemacs 中进行的修改，请按 spc f e r。它将重新执行spacemacs初始化过程。
> 注意：同步将重新执行函数 dotspacemacs/init，dotspacemacs/user-init 和 dotspacemacs/user-config, 根据这个功能的内容，你可能会遇到一些不需要的副作用。例如，如果在 dotspacemac/user-config 中使用切换来启用某些行为，则只要 dotfile 重新同步，就会关闭此行为。为了避免这些副作用，建议使用setq表达式而不是切换功能，或者使用 on 或 off 版本来代替 (spacemacs/toggle-<thing>，使用 spacemacs/toggle-<thing> 或者 spacemacs/toggle-<thing>-off）。

可以使用通用参数（spc u spc f e r）跳过执行 dotspacemacs/user-config。

### 7.4 Testing the dotfile
你可以使用命令 SPC SPC dotspacemacs/test-dotfile 来检查你的 〜/.spacemacs 是否正确。除此之外，这将检查是否可以找到已声明的 layers，以及变量是否具有合理的值。这些测试也会在与 SPC f e r 同步时自动运行。

### 7.5 Dotfile Contents
#### 7.5.1 Configuration functions
〜/.spacemacs 文件中的三个特殊函数可用于在 spacemacs 加载过程的开始和结束时执行配置：

- dotspacemacs/layers 在 spacemacs 初始化的启动时被调用，这是您设置 spacemacs 分配和声明 layers 以在您的配置中使用的位置。你也可以添加或排除你选择的包，并调整一些spacemacs加载行为。
- dotspacemacs/init 在层配置之前的 spacemacs 初始化启动时被调用。除了修改前缀为 spacespacemacs- 的 spacemacs 变量值之外，不应该在其中放置任何用户代码。
- 在进行 layers 配置之前，在 spacespacemacs/init 之后立即调用 dotspacemacs/user-init。此函数对于在加载包之前需要设置的变量非常有用。
- dotspacemacs/user-config 在层配置后的 spacemacs 初始化的最后被调用。这是大部分配置应该完成的地方。除非明确指定应在加载包之前设置变量，否则应将代码放在此处。
#### 7.5.2自定义变量
自定义变量配置从 M-x 自定义组内置的 emacs 功能会被 emacs 自动保存在 〜/.spacemacs 文件的末尾。

### 7.6 Declaring Configuration layers
要使用配置层，通过将它添加到 〜/.spacemacs 的 dotspacemacs-configuration-layers 变量中，将它声明在 dotfile 中。
> 注意：在这个文档中，一个 used layer 相当于一个 declared layer。

例如，[RMS](http://spacemacs.org/doc/DOCUMENTATION.html#thank-you) 可以像这样添加他的私有配置 layer：

```lisp
(setq-default dotspacemacs-configuration-layers
  '(
    ;; other layers
    ;; rms layer added at the end of the list
    rms
  ))
```
带有 spacemacs 的官方layers 存储在 〜/.emacs.d/layers 中.目录〜/.emacs.d/private 是你的私人 layers 的一个插入位置。如果您告诉 spacemacs 在哪里查找它们，可以将 layers 放在您选择的位置。这是通过在 〜/.spacemacs 中设置列表 dotspacemacs-configuration-layer-path 完成的。例如在 〜/.myconfig 中添加一些 layers，像这样设置变量：

```lisp
(setq-default dotspacemacs-configuration-layer-path '("~/.myconfig/"))
```
#### 7.6.1 Setting configuration layers variables
一些配置 laysers 具有配置变量来启用特定功能。比如 git layer 有几个配置变量，可以像这样直接在 dotspacemacs-configuration-layers 中设置：

```lisp
(defun dotspacemacs/layers ()
  ;; List of configuration layers to load.
  (setq-default dotspacemacs-configuration-layers
    '(auto-completion
      (git :variables
           git-magit-status-fullscreen t
           git-variable-example nil)
      smex)))
```
:variables 关键字可以方便地保持 layer 配置接近他们的声明。在 dotfile 的 dotspacemacs/user-init 函数中设置 layer 变量也是配置 layer 的完美方法。
#### 7.6.2 Disabling layer services in other layers
通常 layers 可以启用其他 layers 可以使用的服务。例如，如果使用 layers auto-completion ，则每个支持 auto-completion 的其他 layers 都将启用此功能。

有时你可能想要禁用某些特定 layers 中的某个 layers 添加的服务。假设你想在 org 和 git  layers 中禁用 auto-completion，你可以用下面的 layer 声明来完成。

```lisp
(defun dotspacemacs/layers ()
  ;; List of configuration layers to load.
  (setq-default dotspacemacs-configuration-layers
    '(org git
      (auto-completion :disabled-for org git))))
```
您还可以使用 :enabled-for 构造对除显式标识的那些层以外的所有 layers 禁用它。

```lisp
(defun dotspacemacs/layers ()
  ;; List of configuration layers to load.
  (setq-default dotspacemacs-configuration-layers
    '(java python c-c++
      (auto-completion :enabled-for java python))))
```
注意 :enabled-for 可能是一个空的列表。


```lisp
(defun dotspacemacs/layers ()
  ;; List of configuration layers to load.
  (setq-default dotspacemacs-configuration-layers
    '(java python c-c++
      (auto-completion :enabled-for))))
```
如果两者都存在， :enabled-for 优先于 :disabled-for 。
#### 7.6.3 Selecting/Ignoring packages of a layer
默认情况下，声明的 layer 将安装/配置所有关联的包。你可能只想选择其中的一部分或忽略其中的一部分。这可以通过：packages关键字来实现。

例如忽略来自 spacemacs-ui-visual layer 的 neotree 和 fancy-battery 包：

```lisp
(defun dotspacemacs/layers ()
  ;; List of configuration layers to load.
  (setq-default dotspacemacs-configuration-layers
    '(auto-completion
      (spacemacs-ui-visual :packages (not neotree fancy-battery))))

```
相反的是忽略除neotree和fancy-battery之外的所有软件包：

```lisp
(defun dotspacemacs/layers ()
  ;; List of configuration layers to load.
  (setq-default dotspacemacs-configuration-layers
    '(auto-completion
      (spacemacs-ui-visual :packages neotree fancy-battery)))
```
> 注意：忽略 layer 中的包不同于排除包。排除的包将从您的配置中完全删除，而被忽略的包仅在给定 layers 中被忽略，但可以保留在您的系统上。如果给定的 layers 是包的所有者，那么忽略这个包与排除它是一样的（因为包成为孤立的，所以它被认为是 spacemacs 未使用的）。

#### 7.6.4 Excluding packages
您可以通过变量 dotspacemacs-excluded-packages 排除您不想安装的软件包（有关软件包的更多信息，请参阅[配置 layers](http://spacemacs.org/doc/DOCUMENTATION.html#configuration-layers)）。

例如，禁用 rainbow-delimiters 包：

```lisp
(setq-default dotspacemacs-excluded-packages '(rainbow-delimiters))
```
当您排除软件包时，下次启动 emacs 或下次点文件同步时，spacemacs 会自动删除它。所有的孤立依赖也被自动删除。不包括一个软件包有效地删除 spacemacs 的所有引用，而不会破坏其余的配置，这是一个强大的功能，它允许你快速删除 spacemacs 的任何功能。

> 注意：一些软件包对于 spacemacs 正确运行是必不可少的，这些软件包是受保护的，即使它们成为孤立的或被排除在外，也不能被排除或不被拆除。use-package 是一个不能从 spacemacs 中删除的受保护软件包的例子。