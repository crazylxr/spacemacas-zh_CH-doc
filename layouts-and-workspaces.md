布局是具有缓冲区隔离的窗口配置，每个布局可以定义几个工作空间（将它们视为子布局）共享与其父布局相同的缓冲区列表。

### 13.1 Layouts
布局是与缓冲区列表关联的窗口配置。缓冲区列表可以是任意选择的一组缓冲区。spacemacs 提供了一些设施来创建有意义的缓冲区集，例如与一个抛射项目相关的缓冲区。

当前布局的名称出现在最左边的模式行中（模式行的第一个元素）。

要创建一个新的布局键入一个尚不存在的布局编号。例如，如果当前有两个布局，则键入 SPC l 3 以创建第三个布局。
### 13.1.1 The default layout
默认布局（在 emacs 启动时创建的布局）不会显示在 mode-line 中，但可以通过将变量 dotspacemacs-display-default-layout 设置为 t 来显示它。

它的名字默认是“default”，但是可以通过设置变量 dotspacemacs-default-layout-name 来改变。

默认布局是特殊的，因为它具有全局范围，意味着所有打开的缓冲区都属于它。所以只使用默认布局感觉就像根本不使用布局。
### 13.1.2 Project layouts
一个项目布局是绑定到一个抛射项目。使用 SPC p l 创建项目布局。

布局的名称是项目根目录的名称。
### 13.1.3 Custom Layouts
可以使用宏 spacemacs | define-custom-layout 定义自定义布局，可以通过 SPC l o 访问它们。

按照惯例，自定义布局的名称应该以 @ 开头。

ERC 缓冲区的自定义布局定义示例：

```lisp
(spacemacs|define-custom-layout "@ERC"
  :binding "E"
  :body
  (progn
    ;; hook to add all ERC buffers to the layout
    (defun spacemacs-layouts/add-erc-buffer-to-persp ()
      (persp-add-buffer (current-buffer)
                        (persp-get-by-name
                         erc-spacemacs-layout-name)))
    (add-hook 'erc-mode-hook #'spacemacs-layouts/add-erc-buffer-to-persp)
    ;; Start ERC
    (call-interactively 'erc)))
```
然后用 SPC l o E 来启动它自己的布局中的 ERC。任何新的 ERC 缓冲区将成为自定义布局的一部分。

一些与 spacemacs 一起提供的自定义布局：

Name | Key Binding | Description
---|---|--
@Spacemacs|	e|	Custom perspective containing all buffers of ~/.emacs.d
@ERC|	E|	Custom perspective containing all ERC buffers (needs the erc layer enabled)
@RCIRC|	i|	Custom perspective containing all RCIRC buffers (needs the rcirc layer enabled)
@Org|	o|	Custom perspective containing all the org-agenda buffers

#### 13.1.4 Save/Load layouts into a file
使用 SPC l s 和 SPC l L 可以保存并从一个文件加载布局。

> 注意：默认情况下，spacemacs 将自动保存名称为 persp-auto-save 的布局

将变量 dotspacemacs-auto-resume-layouts 设置为 t 将自动恢复上次保存的布局。

#### 13.1.5 Layout key bindings
快捷键绑定被注册为临时态。临时状态的文档字符串显示现有的布局，当前活动的布局有方括号。按布局编号将激活它（或创建一个新的）并退出瞬态。可以用 Ctrl-<number> 预览一个布局。按下 TAB 将激活之前选择的布局。

按 ？切换完整的帮助。


Key Binding | Description
---|---
SPC l|	activate the transient- state
?|	toggle the documentation
[1..9, 0]|	switch to nth layout
[C-1..C-9, C-0]|	switch to nth layout and keep the transient state active
<tab>|	switch to the latest layout
a|	add a buffer to the current layout
A|	add all the buffers from another layout in the current one
b|	select a buffer in the current layout
d|	delete the current layout and keep its buffers
D|	delete the other layouts and keep their buffers
h|	go to default layout
C-h	|previous layout in list
l|	select/create a layout with helm
L|	load layouts from file
C-l	|next layout in list
n|	next layout in list
N|	previous layout in list
o|	open a custom layout
p|	previous layout in list
r|	remove current buffer from layout
R|	rename current layout
s|	save layouts
t|	display a buffer without adding it to the current layout
w|	workspaces transient state (needs eyebrowse layer enabled)
x|	kill current layout with its buffers
X|	kill other layouts with their buffers
### 13.2 Workspaces
工作空间是子布局，他们允许定义多个布局到一个给定的布局，这些布局共享与父布局相同的缓冲区。

在窗口编号之前显示当前激活的工作空间编号，例如“➊|➍”或“1 | 4”表示第一个工作空间的第四个窗口。

任何新的布局都带有一个默认的工作区，它是工作区1。

切换到当前布局中不存在的工作空间将创建一个新的工作空间。例如在启动时，您可以按 SPC l w 2 以默认布局创建工作区2。

当创建一个工作空间是匿名的，你可以给他们一个名字与 SPC lw R.

#### Workspace key bindings

快捷键绑定被注册为临时态。临时状态的文档字符串显示现有的工作区，当前活动的工作区有方括号。按下工作区号码将激活它（或创建一个新的）并退出瞬态状态。可以用 Ctrl-<number> 预览一个工作区。按 TAB 将激活之前选择的工作区。

按 ？切换完整的帮助。

Key Binding | Description
---|---
SPC l w|	activate the transient state
?|	toggle the documentation
[1..9, 0]|	switch to nth workspace
[C-1..C-9, C-0]	|switch to nth workspace and keep the transient state active
TAB	|switch to last active workspace
d|	close current workspace
n or l|	switch to next workspace
N or p or h	|switch to previous workspace
R|	set a tag to the current workspace
w|	switched to tagged workspace

还有一些方便的全局可用的与工作区相关的键绑定：

Key Binding | Description
---|---
gt|	go to next workspace
gT|	got to previous workspace
SPC b W|	go to workspace and window by buffer




