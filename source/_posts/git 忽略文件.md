**.gitignore忽略已提交的文件**

描述 ：需要忽略的文件已经提交

解决方案

```
git  rm -r --cache .
git  add .
git  commit -m ".gitignore now work"
```

执行后 会发现.gitignore 文件起作用了。

