# fix git push error: shallow update not allowed


> git推送rustlings 5.4.1分支到自己仓库的时候，提示了错误：shallow update not allowed

手动执行强推：`git push -u origin rustlings_5.4.1`，没有效果。

根据提示，提示的问题应该是浅拷贝，就是在git fetch [rust-lang/rustlings](https://github.com/rust-lang/rustlings) 仓库的时候，depth设置的太浅或者默认是浅拷贝，没有全部的历史记录。

所以方案应该是：

1. 添加源库到本地github分支： `git remote add rustlings_raw git@github.com:rust-lang/rustlings.git`
2. 重新获取源库的数据: `git fetch --unshallow rustlings_raw`
3. 推送git代码到自己的git服务器: `git push -u origin rustlings_5.4.1`

推送成功，问题解决。

### 注意：

* 上述地址 `git@github.com:rust-lang/rustlings.git` 为对应的rustlings的仓库地址
* 上述 `rustlings_5.4.1`分支为自定义的对应rustlings仓库的最新`tag 5.4.1`
