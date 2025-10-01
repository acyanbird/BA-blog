---
title: "Bash Intro"
date: 2025-09-30T11:14:08+01:00
draft: false
author: "acyanbird"
summary: "Bash Intro"
# tags: [""]
---

### 创建.sh文件

```
mkdir TestWild
cd TestWild
touch File1.txt
touch File2.txt
touch File3.txt
touch File4.txt
touch File1.csv
touch File2.csv
touch File3.csv
touch File4.csv
touch Anotherfile.csv
touch Anotherfile.txt
ls 
ls | wc -l
```

这个本来相用 for，不过有更好的办法 `touch File{1..4}.txt`  