---
tags:
  - Git
url: https://www.30secondsofcode.org/git/s/find-commit-with-bug/
source: 30 seconds of code
---
Git 的 **bisect** 命令是一个功能强大但未被充分利用的工具，可以帮助您找到代码库中错误的根源。它使用二进制搜索算法来查找引入错误的提交，并且您可以手动或自动将提交标记为“好”或“坏”以帮助缩小搜索范围。
# 手动查找有 bug 的 commit
为了启动该过程，需要使用 [`git bisect start` ](https://git-scm.com/docs/git-bisect#_basic_bisect_commands_start_bad_good)。你需要将一个提交标记为“good”，表明它已知没有错误，将另一个提交标记为“bad”，表明它有错误。你可以使用 [`git bisect good <commit>`](https://git-scm.com/docs/git-bisect#_basic_bisect_commands_start_bad_good) 和 [`git bisect bad <commit>`](https://git-scm.com/docs/git-bisect#_basic_bisect_commands_start_bad_good)

执行这些步骤后，二分搜索算法将在**每次 commit 时停止**，你必须使用`git bisect (good | bad)` 将每个提交标记为“好”或“坏”，具体取决于它是否有错误。

运行完提交后，算法将打印引入错误的提交。最后，您可以使用 `git bisect reset` 重置到原始分支。您可以选择指定要重置到的提交。
```shell
# Syntax:
#  git bisect start
#  git bisect good <commit>
#  git bisect bad <commit>
#  git bisect (good | bad)
#  git bisect reset [<commit>]

git bisect start

git bisect good 3050fc0de
git bisect bad c191f90c7

git bisect good  # Current commit is good
git bisect bad   # Current commit is buggy

# ... some time later the bad commit will be printed
git bisect reset # Goes to the original branch
```
# 自动查找有 bug 的 commit
如果所有这些看起来工作量太大，幸运的是您可以使用 `git bisect run` 自动化该过程。此命令将在每个后续提交上运行给定脚本，以查找哪个提交引入了错误。

除此之外，进程的启动是相同的，您需要使用 [`git bisect start`](https://git-scm.com/docs/git-bisect#_basic_bisect_commands_start_bad_good) 并将提交标记为“好”，将另一个标记为“坏”。之后，您可以使用 [`git bisect run <command>`](https://git-scm.com/docs/git-bisect#_bisect_run) 在每个后续提交上运行给定的命令，并等待打印错误的提交。
```shell
# Syntax:
#  git bisect start
#  git bisect good <commit>
#  git bisect bad <commit>
#  git bisect run <command>
#  git bisect reset [<commit>]

git bisect start

git bisect good 3050fc0de
git bisect bad c191f90c7

git bisect run npm test # Run `npm test` for each commit

# ... some time later the bad commit will be printed
git bisect reset # Goes to the original branch
```
