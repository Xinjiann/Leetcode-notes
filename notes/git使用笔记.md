## rebase合并多个commit

```
$ git rebase -i HEAD~[number_of_commits]
or
$ git rebase -i d2bf14b495fe57583371be8d0a48c927a2da7eb9 7fc6da429881c5bca2705f61aac0e3a1a3c0b1c7
```

要覆盖的pick改成s

保留一条commit信息

## git冲突的解决

push本地的commit，发现无法push。 vim编辑CONFLICT后面的文件。
其中<<<<<<< HEAD 到 ======= 中间的内容是local提交的。
======= 到 >>>>>>> commit-id 是远程仓库中的内容。




