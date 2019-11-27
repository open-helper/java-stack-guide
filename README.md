# java-stack-guide
Java based technology stack guide
Java开源代码**统一托管**，**落地实践**心路历程


## 特性
- 批量管理源码(**pull**, **sync**)
- 源码、修改分离
- 开源代码，一键落地，快速部署
- 开源代码按标签分组，指标评估(reserved)

## 受众
- 源码学习、调研

## 前置约定
**源码统一管理 URL -> URI标准化**

|Key|Value|Memo|
|:--|--|--|
|URL|https://github.com/open-helper/java-stack-guide||
|URI|**open-helper/java-stack-guide**|topic.lst|
|local_uri|**open-helper-java-stack-guide**||

> 转换规则: "/."转为"-", 大写转小写
> `fname=$(echo $x | tr '/.' '-' | tr A-Z a-z);`

**中控操作**
- 除非删除目录文件等极其危险操作，尽量不要在当前目录下执行，保证更强适应性
- 建立在/tmp或项目根目录 下执行
- 无特别说明，本项目所有操作，均以**项目根目录**下(同该README.md)为例


## Quick Started
**场景1** local_uri存在 快速运行起来，看看效果
```bash
# 基于docker 启动/停止/状态/启动并查看状态
make -C apps/local_uri/docker-compose start
make -C apps/local_uri/docker-compose stop
make -C apps/local_uri/docker-compose status
make -C apps/local_uri/docker-compose start status

# 基于k8s 启动/停止/状态/启动并查看状态
make -C apps/local_uri/k8s start
make -C apps/local_uri/k8s stop
make -C apps/local_uri/k8s status
make -C apps/local_uri/k8s start status
```

**场景1.2** 运行数据目录在哪里
- **data**: apps/local_uri/{docker-compose,k8s}/data
- **conf**: apps/local_uri/{docker-compose,k8s}/data
- **log**: log/local_uri


**场景2** local_uri不存在，面向开发人员或自己定制
```bash
# step1. 添加代码URI(很简单，参考其它即可)
# 写入 conf/git.repos.d/gitee.d/custom.d/misc.lst

# step2. 拉取源码，初始化环境
make sync
```

**场景2.2**　修改扩展源码
```bash
# 基于Linux的rsync命令，同步src/buddy到repo目录下对应文件
make merge
```

## 扩展
```bash
# 同上，不再哆嗦啦...
# conf/git.repos.d/*.d/custom.d/*.lst
```


## 依赖
- docker(**必备**)
- k8s(可选)

## 开发环境
- 类Unix系统, 支持**make,git,bash**命令行工具集; 目录**符号链接**
- Win10系统: 建议安装Linux子系统**WSL**
- Win7等: 建议安装**cygwin,msys2,命令行git**等**posix层**模拟环境

---
# 目录结构
```bash
.
├── apps      # apps 净数据data,conf等目录
│   ├── docker-compose      # 基于docker-compose
│   └── k8s                 # 基于k8s
├── bin           
│   ├── make                # linux下make可执行文件，方便祼机操作
│   └── Makefile            # reserved
├── conf
│   ├── env.d
│   │   ├── docker-dev.env  # docker 相关的环境变量(生产环境: docker-prod.env)
│   │   └── mk-dev.env      # makefile 用到的环境变量(生产环境: mk-prod.env)
│   └── git.repos.d         # 源码uri列表文件
│       ├── gitee.d
│       │   ├── *.lst       # 按标签分文件的列表
│       │   └── custom.d     
│       │       └── *.lst   # 用户自定义扩展(gitignore)
│       ├── github.d
│       └── gitlab.d
├── docs                    # 实战记录(踩坑)
├── log                     # log 集中存储
│   ├── nameM-projectX      # apps/{docker-compose,k8s}/log 符号链接 源
│   └── nameN-projectY
│
├── scripts
│   ├── ansible
│   ├── deps                # git,subtree管理等
│   ├── docker-ctl.mk
│   └── git-repo-mgr        # git源码批量管理
│
├── src
│   ├── repo                # 源码仓库列表
│   ├── topics              # 按标签分目录 符号链接 到 repo目录
│   └── buddy               # 与repo子目录对应，如需要微改源代码，请在这里修改
│       └── .open-helper/   # 非侵入式修改，存储Makefile等中控进一步封装脚本
│
├── templates
│   ├── ide                 # IDE 相关一些脚手架模板(reserved)
│   └── java                # java 相关一些模板之类的(reserved)
│
└── Makefile                # 中控脚本

```
