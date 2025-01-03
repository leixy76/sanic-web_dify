# 大模型数据助手

🌟 **项目简介**

一个轻量级、支持全链路且易于二次开发的大模型应用项目

基于 Dify 、Ollama&Vllm、Sanic 和 Text2SQL 📊 等技术构建的一站式大模型应用开发项目，采用 Vue3、TypeScript 和 Vite 5 打造现代UI。它支持通过 ECharts 📈 实现基于大模型的数据图形化问答，具备处理 CSV 文件 📂 表格问答的能力。同时，能方便对接第三方开源 RAG 系统 检索系统 🌐等，以支持广泛的通用知识问答。

作为轻量级的大模型应用开发项目，Sanic-Web 🛠️ 支持快速迭代与扩展，助力大模型项目快速落地。🚀

🌈 **Live Demo**  
[在线体验即将上线，敬请期待！]()

## 架构方案
![image](./images/app-01.png)

## 🎉 **特性**
- **核心技术栈**：Dify + Ollama + RAG + LLM + Text2SQL
- **UI 框架**：Vue 3 + TypeScript + Vite 5
- **数据问答**：集成 ECharts大模型实现Text2SQL轻量级的图形化数据问答展示
- **表格问答**：支持 CSV格式文件的上传与基于大模型总结预处理和Text2SQL的表格数据问答
- **通用问答**：支持通用数据形式问答基于对接三方RAG系统+公网检索模式
- **应用架构**：作为一个轻量级全链路一站式大模型应用开发框架方便扩展落地
- **灵活部署**：支持大模型应用开发各依赖组件docker-compose一键拉起快速部署零配置

## 运行效果
![image](./images/chat-04.gif)
![image](./images/chat-05.jpg)
![image](./images/chat-01.png)
![image](./images/chat-03.png)

## 💡环境配置要求

在开始之前，请确保您的开发环境满足以下最低配置要求：

- **操作系统**：Windows 10/11, macOs M系列, Centos/Ubuntu
- **GPU**: 本地使用ollama部署，推荐使用Nvidia显卡或CPU模式。
- **内存**：8GB+

## 🔧 **前置条件**
* Python 3.8+
* Poetry 1.8.3+
* Dify 0.7.1+
* Mysql 8.0+
* Node.js 18.12.x+
* Pnpm 9.x


## 📚 **大模型部署**
- [参考Ollama部署](https://qwen.readthedocs.io/zh-cn/latest/run_locally/ollama.html)
- 模型: Qwen2.5

## ⚙️ **Dify环境配置**
1. **使用项目脚本默认安装Dify**
   - 为了兼顾第一次接触大模型应用的同学，本项目提供了一键拉起Dify服务零配置，同时启动服务方式，方便大家快速体验。
   - Dify本机访问地址：http://localhost 账号:admin@123.com 密码:admin123 
   ```bash
   # 拉起内置的dify服务
   cd docker/dify/docker
   docker-compose up -d
   
2. **如果已安装过Dify环境**
   - **如果你已经有Dify环境,这种情况只能本地修改源码启动服务 !!!**
   - 第一步直接导入项目根目录下的**docker/dify/数据问答.yml画布**至Dify
   - 第二步修改源码DiFyAppEnum枚举里的DATABASE_QA密钥Key(**key从dify流程画布中获取**)
   - 第三步修改项目根目录下的.env文件，根据环境修改实际的Dify Rest服务接口地址即可
   - 第四步修改Dify画布里HttpRequest配置，修改url地址为具体sanic-web服务地址

3. **安装最新版本Dify**
   - 如果需要安装最新版Dify的同学,可以参考官方文档[Dify官方文档](https://docs.dify.ai/zh-hans)。
   
## 🚀 **快速体验**
   - 具体步骤如下：
   - 第一步克隆代码到本地
   - 第二步参考上面**大模型部署**先安装Ollama部署Qwen2.5模型
   - 第三步Dify环境配置直接参考上面**Dify环境配置**里的,**第1种情况[使用项目脚本默认安装Dify]** **这步很重要!!!!**
   - 第四步启动服务具体步骤如下:

1. **克隆仓库**
   ```bash
   git clone https://github.com/apconw/sanic-web.git

2. **启动服务**
   ```bash
   # 拉起前后端服务和中间件
   cd docker
   docker compose up -d

3. **数据初始化**
   ```bash
   cd docker
   ./init.sh
   
   或执行
   
   cd docker
   python3 ../common/initialize_mysql.py
   
4. **访问服务**
 - 前端服务：http://localhost:8081


## 🛠️ **本地开发**
- 第一步克隆代码到本地
- 第二步参考上面**大模型部署**先安装Ollama部署Qwen2.5模型
- 第三步本地开发环境Dify配置，参考上面**Dify环境配置**里的,**第1或2种两种情况自行选择即可**
- 第四步编辑项目根目录下的.env文件，**修改ENV=dev**，以及数据库配置信息
- 第五步安装前后端项目依赖并启动前后端服务具体步骤如下:

1. **后端依赖安装**  
   - poetry安装 [参考poetry官方文档](https://python-poetry.org/docs/)
   ```bash
   # 安装poetry
   pip install poetry
   
   # 安装依赖根目录执行
   # 设置国内仓库
   poetry source add --priority=default mirrors https://pypi.tuna.tsinghua.edu.cn/simple/
   poetry install

2. **安装数据库**
   ```bash
   docker run --name mysql-local \
   -p 13006:3306 \
   -v /Users/lihuan/docker-mount/mysql:/var/lib/mysql \
   -e MYSQL_ROOT_PASSWORD=1 \
   -d mysql:latest
   
3. **初始化数据库**
- 如果使用本地环境mysql,初始化数据时需修改源码initialize_mysql，修改数据库连接信息即可
   ```bash
  cd docker
  ./init.sh
   
  或执行
   
  cd docker
  python3 ../common/initialize_mysql.py

4. **前端依赖安装**  
   - 前端是基于开源项目[可参考chatgpt-vue3-light-mvp安装](https://github.com/pdsuwwz/chatgpt-vue3-light-mvp)二开
   ```bash
   # 安装前端依赖&启动服务
   cd web
   
   #安装依赖
   npm install -g pnpm

   pnpm i
   
   #启动服务
   pnpm dev
   
5. **启动后端服务**
   ```bash
   #启动后端服务
   python serv.py
   ```

6. **访问服务**
 - 前端服务：http://localhost:2048

## 🐳 构建镜像
- 编辑项目根目录下的.env文件，***修改ENV=test***，并保存。
- 执行构建命令：
   ```bash
   # 构建前端镜像 
   make web-build
  
   # 构建后端镜像
   make server-build


## 🌹 支持

如果你喜欢这个项目或发现有用，可以点右上角 [`Star`](https://github.com/apconw/sanic-web) 支持一下，你的支持是我们不断改进的动力，感谢！ ^_^ 

如果你觉得这个项目对你有帮助，或者你喜欢我们所做的事情，欢迎点击右上角的 [⭐️ Star] 按钮来支持我们！你的每一个星标都是对我们莫大的鼓励，也是我们不断改进和发展的动力。感谢你的支持！ ^_^

[![GitHub stars](https://img.shields.io/github/stars/yourusername/yourproject?style=social)](https://github.com/apconw/sanic-web)

此外，如果你有任何建议或想参与项目的发展，也非常欢迎你通过以下方式联系我们：

- **提交Issue** - 如果你发现了任何问题或有改进建议，可以在 [Issues](https://github.com/apconw/sanic-web/issues) 中提交。
- **加入讨论** - 可以添加加入我们讨论群，进行交流讨论。 参与讨论。
- **贡献代码** - 如果你有兴趣贡献代码，可以参考 [贡献指南](#如何开始)。

再次感谢你的支持！ 🙏

## QA交流群
- 大模型应用交流群欢迎大家, 欢迎加进群讨论分享经验
- 关注下面的公众号点击·**微信群**菜单添加微信拉你入群

|                 微信群                 |
|:-----------------------------------:|
| ![image](./images/wchat-search.png) | 

## License

[MIT](./LICENSE) License | Copyright © 2024-PRESENT [AiAdventurer](https://github.com/apconw)