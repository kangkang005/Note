# 本地 git 操作
## 链接远程仓库
```bash
git clone [-b first] /home/project/ET-003/module/bst
```

## 复制要上传文件
```bash
cp [code] ./bst
```

## 建立分支
```bash
git checkout -b first
```

## 添加文件并提交
```bash
git add .
git commit -m 'first version'
git push origin first
```

## 克隆 develp 分支的远程仓库
```bash
git clone -b develop /home/project/ET-004/module/tppc
```