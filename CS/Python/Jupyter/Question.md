# 一、在安装nbextensions会报ModuleNotFoundError: No module named ‘notebook.base‘错误
## 1.描述
安装 jupyter_contrib_nbextensions，提示报错 No module named 'notebook.base'。
```
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
pip install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
```
**配置**：(加上--user 代表只对当前用户有效，如果是 root 则可以去掉后对所有用户有效)

执行第二步的时候，提示报错: `No module named 'notebook.base'`
经过一番查询，是版本问题，将 notebook 更改为 6.1.0 版本后问题解决。
```
pip install jupyter notebook==6.1.0
```
期间也曾找到降低版本的解决方式，其版本降低到 5.0 以下，尝试后连 nbextensions 标签也没有了。
基于变更版本的思路，尝试了继续变更 notebook 的版本。最后确定 notebook==6.1.0。
## 2.参考
https://blog.csdn.net/jingmenghai/article/details/131870625