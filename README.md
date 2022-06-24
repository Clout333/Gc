



</div>

简中

**请注意:** 欢迎成为本项目的贡献者。在提交 PR 之前, 请仔细阅读[代码规范](https://github.com/Clout333/Gc/blob/stable/CONTRIBUTING.md)。

## 当前功能

* 登录
* 战斗
* 好友列表
* 传送系统
* 祈愿系统
* 从控制台生成魔物
* 多人游戏 *部分* 可用
* 物品栏相关 (接收物品/角色, 升级角色/武器等)

## 快速设置指南

**注意:** 如需帮助请加入 [QQ频道](https://qun.qq.com/qqweb/qunpro/share?_wv=3&_wwv=128&appChannel=share&inviteCode=1W5m76A&appChannel=share&businessType=9&from=246610&biz=ka)

### 环境需求

* Java SE - 17 ([链接](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html))

  **注意:** 如果仅想**运行服务端**, 使用 **jre** 即可

* [MongoDB](https://www.mongodb.com/try/download/community) (推荐 4.0+)

* 代理: mitmproxy (推荐 mitmdump), Fiddler Classic 等

### 运行

**注意:** 从旧版本升级到新版本, 需要删除 `config.json` 文件

1. 获取 `grasscutter.jar`
   - [自行编译](#编译)
2. 在 JAR 文件根目录中创建 `resources` 文件夹并复制 `BinOutput` 和 `ExcelBinOutput`
3. 命令行 `java -jar grasscutter.jar` 运行 Grasscutter。**在此之前请确认 MongoDB 服务运行正常**

### 客户端连接

½. 在服务器控制台创建账户

1. 重定向流量: (选择其中一个)
    - mitmdump: `mitmdump -s proxy.py -k`
    
      信任 CA 证书:
    
      ​	**注意:** mitmproxy 的 CA 证书通常存放在 `%USERPROFILE%\ .mitmproxy`, 或者在 `http://mitm.it` 下载证书
    
      ​ 双击[安装根证书](https://docs.microsoft.com/en-us/skype-sdk/sdn/articles/installing-the-trusted-root-certificate#installing-a-trusted-root-certificate)或者...
    
      - 使用命令行
    
        ```shell
        certutil -addstore root %USERPROFILE%\.mitmproxy\mitmproxy-ca-cert.cer
        ```
    
    - Fiddler Classic: 运行 Fiddler Classic, 在设置中开启 `解密 https 通信` 并将端口设为除 `8888` 以外的任意端口 (工具 -> 选项 -> 连接) 并加载[此脚本](https://github.lunatic.moe/fiddlerscript)
      
    
2. 设置代理为 `127.0.0.1:8899` 或你设置的端口

**也可直接运行 `start.cmd` 一键启动服务端并设置代理, 但必须设置 `JAVA_HOME` 环境变量**

### 编译

Grasscutter 使用 Gradle 来处理依赖及编译。

**依赖:**

- Java SE Development Kits - 17
- Git

##### Windows

```shell
git clone https://github.com/Clout333/Gc.git
cd Grasscutter
.\gradlew.bat # 建立开发环境
./gradlew jar # 编译
```

##### Linux

```bash
git clone https://github.com/Clout333/Gc.git
cd Grasscutter
chmod +x gradlew
./gradlew jar # 编译
```

编译后的 JAR 文件存放在根目录


# 快速排除问题

* 如果编译失败, 请检查 JDK 安装是否正确 (要求 JDK 17 并确认 JDK 处于环境变量 `PATH` 中)
* 客户端无法登录/连接, 4206, 其他问题... - 大部分情况是因为代理设置本身就是*问题*。
  如果使用 Fiddler 请确认 Fiddler 监听端口不是 `8888`
* 启动顺序: MongoDB > Grasscutter > 代理程序 (mitmdump, fiddler 等) > 客户端
