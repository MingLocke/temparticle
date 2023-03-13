# Python3中的os、shutil 模块使用

Python的os和shutil模块封装了常见的文件和目录操作如copy，cd，mv，rm以及解压等等操作。无需在无脑使用os.system()了(抠脚代码的小尴尬)。做此笔记备用，轻拍。

以下是我总结的一些使用方法，首先import..

### shutil 模块

shutil可以简单地理解为`sh + util`，shell工具的意思。shutil模块是对os模块的补充，主要针对文件的拷贝、删除、移动、压缩和解压操作。

拷贝文件, shutil会自动识别拷贝的到底是文件还是文件夹, 如果存在同名的文件将会自动进行覆盖。

```
shutil.copy($file_path, $dir_path)
```

移动或重命名文件，但如果路径下已有重名的文件，将报错！

```
shutil.move($file_path, $dir_path) # 移动到另外一个文件夹中
shutil.move($file_path, $new_file_path) # 重命名为新的绝对路径
```

拷贝文件夹/删除文件夹

```
shutil.copytree($file_path, $dir_path) # 拷贝所有文件到新的文件夹下，保持原有的文件结构。
shutil.rmtree($dir_path) # 删除此路径的文件夹
```

生成压缩文件:

```
shutil.make_archive(base_name, 'gztar', root_dir, [base_dir)
```

-   base\_name : 创建的目标文件名，包括路径，减去任何特定格式的扩展。
-   format : 压缩包格式。”zip”, “tar”, “bztar”或”gztar”中的一个。
-   root\_dir : 需要打包的文件夹路径。打包完成时存储在上一级目录。
-   base\_dir : 使用后会将base\_dir作为路径，解压后有个有层级的文件夹，而仅非只有单独的打包内容。

解压文件:

```
shutil.unpack_archive(filename[, extract_dir[, format]])
```

-   filename是压缩文档的完整路径
-   extract\_dir是解压缩路径，默认为当前目录。
-   format是压缩格式。默认使用文件后缀名代码的压缩格式。”zip”, “tar”, “bztar”或”gztar”中的一个。

### os模块

Python的os模块封装了常见的文件和目录操作

判断使用的平台:字符串指示你正在使用的平台。比如对于Windows，它是'nt'，而对于Linux/Unix用户，它是 'posix'。有时候给出的信息不够细。

```
# 获取平台名称
os.name

# 获取系统的核心数
os.cpu_count()

# 改变权限
os.chmod(path, mode)
```

工作目录与路径相关的操作

```
# 获取路径和文件名等
os.getcwd()    函数得到当前工作目录，即当前Python脚本工作的目录路径
os.path.abspath($name)  当前目录下文件或文件夹的绝对路径
os.path.basename(path)   返回文件名
os.path.dirname(path)    返回文件的上级路径
os.path.split()          分离文件名和上级路径
os.path.join()           合并文件名和指定路径
os.path.splitext()      分离文件名与扩展名，返回的扩展名包括了'.'符号，默认只返回第一个'.后缀'和前缀。

# 改变工作目录到dirname
os.chdir($dirname)

# 列出路径中的文件
os.listdir($path)  返回指定目录下的所有文件和目录名

# 创建、重命名文件夹
os.mkdir($path)    创建一个目录
os.rmdir($path)    删除一个目录
os.rename(src, dst)  记得不能有同名文件存在

# 获取文件大小信息
os.path.getsize(name)    获得文件大小，如果name是目录返回0L
```

判断文件是否存在？

```
os.path.isfile()   函数分别检验给出的路径是一个文件?
os.path.isdir()    函数分别检验给出的路径是一个目录?
os.path.exists()   函数用来检验给出的路径是否真地存在
```

执行外部shell命令

```
os.system('')      执行外部shell命令。
```
