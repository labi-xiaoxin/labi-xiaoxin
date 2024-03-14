# python多版本管理工具安装教程

## 下载

[下载安装地址](https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md)

有多种安装步骤可供选择，这里我选择使用`Pyenv-win zip`方式，通过下载压缩包，配置系统环境

## 解压

- 下载完的文件为`ZIP`文件，将文件解压至任意目录下

> 该目录不允许存在中文

## 配置系统环境变量

- `此电脑`——`高级系统设置`——`环境变量`
- 上面是用户变量，下面是系统变量。选择`系统变量`
- `新建`
  - 变量名： `PYENV`
  - 变量值: `C:\pyenv\pyenv-win` （这里变量根据你解压的目录修改）
- 将刚刚添加的`PYENV`加入Path中
  - 在`系统变量`中，找到`Path`变量，点击`编辑`
  - 在`编辑`页面，点击`新建`
  - 添加如下两个参数
    - `%PYENV%\bin`
    - `%PYENV%\shims`

至此，系统环境变量配置完成

## 测试是否配置正确

`cmd`终端执行`pyenv`，出现如下文字则配置正确：

> 如果出现其他问题，确保配置流程正确，重启下cmd终端

![pyenv配置正常测试](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403131214419.png)