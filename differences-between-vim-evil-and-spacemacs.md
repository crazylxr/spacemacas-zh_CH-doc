## 9 Differences between Vim, Evil and Spacemacs
. 键，“在 vim 中反向重复上一个 f，t，F 或 T 命令，但是在 spacemacs 中，默认情况下它是主要模式特定的 leader 键（可以在 dotfile 中的另一个键绑定上设置）

发送一个 PR 来添加您在本节中找到的差异。

### 9.1 The vim-surround case

有一个明显的可见区别。它不是在 Evil 和 vim 之间，而是在 spacemacs 和 vim-surround 之间：在 visual 模式下，surround 命令在 vim-surround 中，而在 spacemacs 中则在 S 上。

这是一些可以让一些 vim 用户感到惊讶的东西，所以这里有一些动机背后的变化：
- s 和 c 在 visual state 下做同样的事情，
- s 仅用于删除一个字符并添加一个非常狭窄的用例的多个字符
- c 可以移动，可以做一切 normal 状态下的事情（注意这对于 r 也是如此，但是 r 更有用，因为它保持 normal state）
- surround 命令只是一个比 s 更强大的命令。

如果你不相信，那么这里是恢复到默认的 vim + vim-surround 设置（将它添加到你的 dotspacemacs/user-config 函数或你的 〜/.spacemacs）的片段：


```lisp
(evil-define-key 'visual evil-surround-mode-map "s" 'evil-substitute)
(evil-define-key 'visual evil-surround-mode-map "S" 'evil-surround-region)


```
