---
title: 'django.core.exceptions.ImproperlyConfigured: SQLite 3.9.0 or later is required (found 3.7.17). 解决'
date: 2022-02-16 17:21:26
tags: [Python,shell]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Python'
id: 'django-sqlite-version-error-solution'
---

sqlite3版本太低导致，升级sqlite3

脚本：

```shell
#!/bin/bash
sqlite3 --version
wget https://www.sqlite.org/2022/sqlite-autoconf-3370200.tar.gz
tar -xaf sqlite-autoconf-3370200.tar.gz
cd sqlite-autoconf-3370200/
./configure --prefix=/usr/local/
make && make install
mv /usr/bin/sqlite3 /usr/bin/sqlite3.bak
ln -s /usr/local/bin/sqlite3 /usr/bin/sqlite3
echo export LD_LIBRARY_PATH="/usr/local/lib">> ~/.bashrc
source ~/.bashrc
sqlite3 --version
```

<!-- more -->

