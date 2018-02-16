## 11 Binding keys
键序列绑定到各个键盘映射中的 emacs 中的命令。最基本的 map 是 global-map。使用 global-set-key 函数来实现 global-map 中的键绑定。示例将键绑定到命令 forward-char：

```lisp
(global-set-key (kbd "C-]") 'forward-char)
```
kbd 宏接受描述键序列的字符串。global-map 经常被其他地图遮蔽。例如，evil 模式定义了目标状态的键盘映射（或 vim 术语中的模式）。这里是一个创建与上面相同的绑定的例子，但只有在插入状态下（define-key是一个内置函数，evil-mode有自己定义键的函数）。


```lisp
(define-key evil-insert-state-map (kbd "C-]") 'forward-char)
```
也许对于 spacemacs 来说最重要的是使用 bind-map 包来绑定 leader 键后的键。这是大多数 spacemacs 绑定的地方。绑定在 leader 键后的键是通过函数 spacemacs/set-leader-keys 和 spacemacs/set-leader-keys-for-major-mode 来实现的，例如：

```lisp
(spacemacs/set-leader-keys "C-]" 'forward-char)
(spacemacs/set-leader-keys-for-major-mode 'emacs-lisp-mode "C-]" 'forward-char)
```

最后，应该知道前缀键。实质上，所有键映射都可以嵌套。嵌套的键映射广泛用于 spacemacs，在 vanilla emacs 的这个问题。例如，SPC 指向“applications”的键绑定，例如用于 calc-dispatch 的 SPC a c。嵌套绑定很容易。

```
(spacemacs/declare-prefix "]" "bracket-prefix")
(spacemacs/set-leader-keys "]]" 'double-bracket-command)
```
第一行声明 SPC ] 为前缀，第二行将键序列 SPC ]] 绑定到相应的命令。第一行实际上并不需要创建前缀，但它会为您的新前缀提供 key-discovery 工具可以使用的名称 (e.g., which-key).

有很多关于绑定键的说法，但这些都是基础知识。键可以绑定在你的 〜/.spacemacs 文件或者单独的 layers 中。