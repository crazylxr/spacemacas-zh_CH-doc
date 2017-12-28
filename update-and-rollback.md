## 5 Update and Rollback
### 5.1 Update Spacemacs repository
有几种方法可以更新 spacemacs 的核心文件和 layer 信息。建议先更新软件包;看下一节。
#### 5.1.1 Automatic Updates
每次启动时，spacemacs将自动检查新版本。当它检测到新版本可用时，模式行中将出现一个箭头。点击它来更新spacemacs。更新后必须重新启动emacs。
![image](http://spacemacs.org/doc/img/powerline-update.png)
Update Button

注意：如果你使用spacemacs的develop分支，自动更新被禁用 - 你必须使用git手动更新。

#### 5.1.2 Updating from the Spacemacs Buffer
使用 spacemacs buffer 中标记为“更新 spacemacs ”的按钮。系统会提示您输入要使用的版本。

> 注意：如果你使用 spacemacs 的 develop 分支，你不能使用这个方法。

#### 5.1.3 Updating Manually with git
手动更新关闭emacs并更新git存储库：

```bash
$ git pull origin master
```
> 注意：主分支被认为是不可变的，因为你不能通过添加你自己的提交来修改它。如果你这样做，你会打破主分支上的spacemacs的自动更新。要fork spacemacs代码，您必须使用您手动管理的自定义分支。

### 5.2 Update packages
更新 spacemacs 使用的 emacs 软件包按回车键（回车）或点击横幅下的启动页面中的链接 [Update Packages]，然后重新启动 emacs。如果你愿意，你可以使用命令 configuration-layer / update-packages 而不是按钮。

如果出现任何问题，您应该能够通过按下 RET 或单击启动页面中的 [rollback package update] 链接并选择一个回滚槽（按日期排序）来回滚更新。这个按钮使用命令 configuration-layer/rollback