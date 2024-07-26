# Git 忽略文件夹使用 .gitignore
在开发过程中，经常会遇到一些不需要纳入版本控制的文件夹，例如缓存文件夹、日志文件夹等。为了解决此类问题，git 引入了 `.gitignore` 文件，使用该文件来选择性的上传文件。
## 创建.gitignore 文件
要在 Git 中忽略文件夹，我们首先需要创建一个名为 `.gitignore` 的文件。这个文件可以在代码仓库的根目录下或者特定的子目录下创建。
```bash
vim .gitignore
```
## 规则
### 注释
注释使用 `#` 开头，后面跟注释内容:
```gitignore
# this is .gitignore file.
out
*.exe
```
### 忽略文件和目录
忽略同名的文件与目录:
```gitignore
file_and_directory
```
例如本地仓库的目录结构:
```bash
>>> tree
.
├── folder
│   └── file1
└── src
    ├── folder
    └── utils
        └── folder

3 directories, 3 files
```
`.gitignore` 内容如下：
```gitignore
# this is .gitignore file.
folder
```
在本地仓库中，同名的 `folder/` 目录、`src/folder` 文件、`src/utils/folder` 文件都会被忽略。

### 仅忽略文件
仅忽略文件，不忽略同名目录:
```gitignore
file_and_directory
!file_and_directory/
```
仅忽略 `file_and_directory` 文件，而不忽略 `file_and_directory` 目录，其中，感叹号 `!` 表示反向操作。

例如 `.gitignore` 内容如下：
```gitignore
# this is .gitignore file.
folder
!folder/
```
在本地仓库中，`src/folder` 文件、`src/utils/folder` 文件会被忽略，而同名的 `folder/` 目录不会被忽略。

### 忽略目录
仅忽略目录，不忽略同名文件:
```gitignore
directory/
```
忽略 `directory` 目录，包括：
* 当前目录下的 `directory`，例如：`directory/`
* 多级目录下的 `directory`，例如：`*/*/directory/`

例如 `.gitignore` 内容如下：
```gitignore
# this is .gitignore file.
folder/
```
在本地仓库中，`folder/` 目录会被忽略，而同名的 `src/folder` 文件和 `src/utils/folder` 文件不会被忽略。

### 通配符
常用的通配符有：
* 星号 `*` ：匹配多个字符；
* 问号 `?`：匹配除 `/`外的任意一个字符；
* 方括号 `[...]`：匹配多个列表中的字符；如果 `[` 之后的第一个字符是感叹号 `!`，则该模式匹配除指定集合中的字符以外的任何字符。

例如本地仓库的目录结构如下所示:
```bash
>>> tree
.
├── src
│   ├── add.c
│   ├── add.i
│   └── add.o
├── test.c
├── test.i
└── test.o

1 directory, 6 files
```
`.gitignore` 内容如下：
```gitignore
# this is .gitignore file.
*.[io]
```
在本地仓库中，`test.i` 文件、`test.o` 文件、`src/add.o` 文件、`src/add.i` 文件会被忽略，而 `test.c` 文件和 `add.c` 文件不会被忽略。

再例如 `.gitignore` 内容如下：
```gitignore
# this is .gitignore file.
*.[!o]
```
在本地仓库中，`test.i` 文件、`src/add.i`、 `test.c` 文件和 `add.c` 文件不会被忽略, `test.o` 文件、`src/add.o` 文件会被忽略。

### 反模式
否定先前模式, 模式如下所示:
```gitignore
!匹配模式
```
表示之前忽略的匹配模式再次包含在跟踪内容里。

例如在仅忽略文件时提到的模式：
```gitignore
folderName
!folderName/
```
表示仅忽略 `folderName` 文件，而不忽略 `folderName` 目录。

### 双星号
斜杠后紧跟两个连续的星号 `**`，表示多级目录。

例如 `.gitignore` 文件的内容如下所示：
```gitignore
# this is .gitignore file.
src/**/file
```
可以表示忽略 `src/folder1/file` 、`src/folder1/folder2/***/foldern/file` 等。

# 参考
https://blog.csdn.net/nyist_zxp/article/details/119887324