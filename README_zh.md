
# QuecPython Project Manager 使用文档

中文 | [English](./readme.md)

## 概述

- 该包管理以 git 仓库为基础，可以访问 QuecPython 组织或其它指定组织下的 github 仓库。

- 在用户指定的是包的名称而非 URL 时，默认访问 github 的 QuecPython 组织，即对 QuecPython 发布的包进行管理。

- 允许用户通过 config 命令重新指定 github 的组织，进而管理自己组织下的包。

- 包管理器不为项目做本地提交，用户需要提交什么内容，可通过 `git commit` 命令自行决定。但是包管理器可为用户将包发布到服务器，同时指定发布的版本。

## 命令

`qpm` 是一个用于管理 QuecPython 项目的命令行工具。它提供了创建、初始化、导入、添加、移除、发布、列出、显示版本、部署和配置项目的功能。

### 版本信息

```bash
qpm -v,--version
```

显示工具的版本信息。

### 帮助信息

```bash
qpm [help|-h,--help]
```

显示帮助信息。

### 创建新项目

```bash
qpm new [-h] [-u URL] proj_name
```

**-h, --help**: 显示 `new` 命令的帮助信息。  
**-u, --upstream URL**: 添加远程仓库的 URL（可选）。  
**proj_name**: 项目名称。  

### 初始化当前目录为 QuecPython 项目

```bash
qpm init [-h] [-u URL]
```

**-h, --help**: 显示 `init` 命令的帮助信息。  
**-u, --upstream URL**: 添加远程仓库的 URL（可选）。  

### 导入项目

```bash
qpm import [-h] [-v version] proj_name_or_url
```

**-h, --help**: 显示 `import` 命令的帮助信息。  
**-v, --version version**: 项目版本（可选）。  
**proj_name_or_url**: 项目名称或 URL。  

### 添加依赖包

```bash
qpm add [-h] [-v version] pkg_name_or_url path
```

**-h, --help**: 显示 `add` 命令的帮助信息。  
**-v, --version version**: 包版本（可选）。  
**pkg_name_or_url**: 包名称或 URL。  
**path**: 包路径。  

### 移除依赖包

```bash
qpm remove [-h] [pkg_path]
```

**-h, --help**: 显示 `remove` 命令的帮助信息。  
**pkg_path**: 包路径（可选）。  

### 发布当前包

```bash
qpm publish [-h] [-v version] [-m message] [-d version]
```

**-h, --help**: 显示 `publish` 命令的帮助信息。  
**-v, --version version**: 发布的版本。  
**-m, --message message**: 发布版本的消息（可选）。  
**-d, --delete version**: 删除已发布的版本。  

### 列出本地或远程包信息

```bash
qpm ls [-h] [-l] [-r] [-p remote_pkg_name] [-v version]
```

**-h, --help**: 显示 `ls` 命令的帮助信息。  
**-l, --local**: 列出本地包信息。  
**-r, --remote**: 列出远程包。  
**-p, --package remote_pkg_name**: 列出远程包的依赖项。  
**-v, --version version**: 要列出的远程包的版本（可选）。  

### 显示本地或远程包发布的所有版本

```bash
qpm release [-h] [pkg_name_or_url]
```

**-h, --help**: 显示 `release` 命令的帮助信息。  
**pkg_name_or_url**: 包名称或 URL（可选）。  

### 部署项目或包

```bash
qpm deploy [-h] [-v version]
```

**-h, --help**: 显示 `deploy` 命令的帮助信息。  
**-v, --version version**: 项目或包版本（可选）。  

### 查看包版本

```bash
qpm version [-h]
```

**-h, --help**: 显示 `version` 命令的帮助信息。  

### 配置项目

```bash
qpm config [-h] [-g] key [value]
```

**-h, --help**: 显示 `config` 命令的帮助信息。  
**-g, --global-config**: 全局配置（可选）。  
**key**: 配置项的键。  
**value**: 配置项的值（可选）。  

> - 项目配置的优先级，从高到低分别为：本地配置 > 全局配置 > 默认配置。
> - 用户的本地或全局配置将会覆盖默认配置。
> - 包管理默认配置了QuecPython 作为 github 组织，并配置了对应的访问 token。

---

## 示例

### 创建新项目

```bash
# 不关联远程仓库的 URL
qpm new project

# 关联远程仓库的 URL
qpm new project -u https://github.com/user/repo.git
```

### 初始化当前目录为 QuecPython 项目

```bash
# 不关联远程仓库的 URL
qpm init

# 关联远程仓库的 URL
qpm init -u https://github.com/user/repo.git
```

### 导入项目

```bash
# 根据包名称导入项目，不指定项目的版本
qpm import project

# 根据包名称导入项目，并指定项目的版本
qpm import project -v 1.0.0

# 根据 URL 导入项目，不指定项目的版本
qpm import https://github.com/user/repo.git

# 根据 URL 导入项目，并指定项目的版本
qpm import https://github.com/user/repo.git -v 1.0.0
```

### 添加依赖包

```bash
# 根据包名称添加依赖包，不指定依赖包的版本
qpm add package /path/to/package

# 根据包名称添加依赖包，并指定依赖包的版本
qpm add package /path/to/package -v 2.25.1

# 根据 URL 添加依赖包，不指定依赖包的版本
qpm add https://github.com/user/repo.git /path/to/package

# 根据 URL 添加依赖包，并指定依赖包的版本
qpm add https://github.com/user/repo.git /path/to/package -v 2.25.1
```

### 移除依赖包

```bash
# 移除指定的依赖包
qpm remove /path/to/package

# 移除所有依赖包
qpm remove
```

### 发布当前包

```bash
# 发布当前包，不指定版本说明信息
qpm publish -v 1.0.0

# 发布当前包，并指定版本说明信息
qpm publish -v 1.0.0 -m "Initial release"

# 删除已发布的版本
qpm publish -d v1.0.0
```

### 列出本地或远程包信息

```bash
# 列出本地包的依赖关系树
qpm ls
qpm ls -l

# 列出 github 组织下所有的包
qpm ls -r

# 列出 github 组织下指定的包的依赖关系，不指定包的版本
qpm ls -p package

# 列出 github 组织下指定的包的依赖关系，并指定包的版本
qpm ls -p package -v v1.2.0
```

### 显示本地或远程包发布的所有版本

```bash
# 查看本地当前包发布的所有版本
qpm release

# 根据包名称查看 github 组织下指定的包发布的所有版本
qpm release package

# 根据 URL 查看包发布的所有版本
qpm release https://github.com/user/repo.git
```

### 部署项目或包

```bash
# 不指定版本
qpm deploy

# 指定版本
qpm deploy -v 1.0.0
```

### 查看包版本

```bash
qpm version
```

### 配置项目

```bash
# 设置本地配置
qpm config key value

# 查询本地配置
qpm config key

# 设置全局配置
qpm config -g key value

# 查询全局配置
qpm config -g key

# 配置本地 github 组织
qpm config github_organization your_github_organization

# 配置本地 github 访问 token
qpm config github_access_token your_github_access_token

# 配置全局 github 组织
qpm config -g github_organization your_github_organization

# 配置全局 github 访问 token
qpm config -g github_access_token your_github_access_token
```

## 注意事项

- 在执行某些命令时，工具会检查当前目录是否在 QuecPython 项目内，如果不符合条件，工具会打印错误信息并出。
