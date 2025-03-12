# 🚀 Cursor中集成MCP Servers指南

本文档提供了如何在Cursor中集成Model Context Protocol (MCP) Servers的详细指南，支持三种集成方式（NPX、Node和Docker）以及不同操作系统（MacOS/Linux和Windows）的配置说明。

## 📋 目录

- [什么是MCP Servers](#什么是mcp-servers)
- [准备工作](#准备工作)
- [配置方式](#配置方式)
  - [使用NPX](#使用npx)
  - [使用Node](#使用node)
  - [使用Docker](#使用docker)
- [验证集成](#验证集成)
- [常见问题解答](#常见问题解答)

## 🔍 什么是MCP Servers

> Model Context Protocol (MCP) Servers是用于扩展大语言模型能力的工具，允许模型与各种外部服务和APIs交互，例如文件系统、数据库、云服务等。通过集成MCP Servers，Cursor可以实现更强大的功能，如文件操作、数据查询、API交互等。

## 🛠️ 准备工作

在开始集成之前，请确保您已经完成以下准备工作：

| 步骤 | 描述 |
|------|------|
| **📥 安装最新版本的Cursor** | 访问[Cursor官网](https://cursor.sh/)下载最新版本，确保Cursor版本支持MCP功能。 |
| **⚙️ 安装Node.js和npm** | 访问[Node.js官网](https://nodejs.org/)下载LTS版本，建议使用Node.js 14.x或更高版本。安装完成后验证： |
| **🐳 安装Docker** | 访问[Docker官网](https://www.docker.com/products/docker-desktop/)下载Docker Desktop，安装并启动Docker Desktop。验证安装： |
| **📁 准备项目目录** | 确保您有项目目录的读写权限，创建`.cursor`目录和配置文件： |

> ⚠️ **注意**：确保您拥有操作系统的管理员权限，以便安装所需的软件和进行配置。

### 安装Node.js和npm

安装完成后验证：  
```bash
node --version
npm --version
```

### 安装Docker

验证安装：  
```bash
docker --version
docker run hello-world
```

### 准备项目目录

确保您有项目目录的读写权限，创建`.cursor`目录和配置文件：  
```bash
mkdir .cursor
touch .cursor/mcp.json
```

## ⚙️ 配置方式

在Cursor中集成MCP Servers需要在项目目录下创建`.cursor/mcp.json`文件进行配置。以下是三种不同方式的具体配置说明：

### 🔄 使用NPX

> 📌 **提示**：这是最简单的集成方式，适合快速部署和测试。

1. **编辑`.cursor/mcp.json`文件**，添加MCP服务器配置：

   - **对于MacOS/Linux**：  
   ```json
   {
     "mcpServers": {
       "服务器名称": {
         "command": "npx",
         "args": [
           "-y",
           "@modelcontextprotocol/server-名称",
           "其他参数1",
           "其他参数2"
         ]
       }
     }
   }
   ```

   - **对于Windows**：  
   ```json
   {
     "mcpServers": {
       "服务器名称": {
         "command": "cmd",
         "args": [
           "/c",
           "npx",
           "-y",
           "@modelcontextprotocol/server-名称",
           "其他参数1",
           "其他参数2"
         ]
       }
     }
   }
   ```

2. **例如，配置Sequential Thinking服务器**（用于动态和反思性问题解决的工具）：

   - **对于MacOS/Linux**：  
   ```json
   {
     "mcpServers": {
       "sequential-thinking": {
         "command": "npx",
         "args": [
           "-y",
           "@modelcontextprotocol/server-sequential-thinking"
         ]
       }
     }
   }
   ```

   - **对于Windows**：  
   ```json
   {
     "mcpServers": {
       "sequential-thinking": {
         "command": "cmd",
         "args": [
           "/c",
           "npx",
           "-y",
           "@modelcontextprotocol/server-sequential-thinking"
         ]
       }
     }
   }
   ```

   此服务器提供以下功能：
   - 🧩 将复杂问题分解为可管理的步骤
   - 🔄 随着理解的深入修改和完善思路
   - 🌳 在不同的推理路径中进行分支
   - ⚖️ 动态调整思考步骤的总数
   - 💡 生成和验证解决方案假设

3. **另一个例子，配置filesystem服务器**：

   - **对于MacOS/Linux**：  
   ```json
   {
     "mcpServers": {
       "filesystem": {
         "command": "npx",
         "args": [
           "-y",
           "@modelcontextprotocol/server-filesystem",
           "./",  // 允许访问当前项目目录
           "--workspace-root",
           "./"
         ]
       }
     }
   }
   ```

   - **对于Windows**：  
   ```json
   {
     "mcpServers": {
       "filesystem": {
         "command": "cmd",
         "args": [
           "/c",
           "npx",
           "-y",
           "@modelcontextprotocol/server-filesystem",
           "./",  // 允许访问当前项目目录
           "--workspace-root",
           "./"
         ]
       }
     }
   }
   ```

### 📦 使用Node

> 📌 **提示**：这种方式适合需要定制化或优化性能的场景，但需要额外的构建步骤。

使用Node方式需要先下载MCP服务器的源代码，然后在本地构建。以下以Sequential Thinking服务器为例说明配置步骤：

1. **克隆服务器源码并构建**：
   ```bash
   # 克隆仓库
   git clone https://github.com/Zengwenliang0416/mcp-server-sequential-thinking.git
   cd mcp-server-sequential-thinking

   # 安装依赖并构建
   npm install
   npm run build
   ```

2. **在`.cursor/mcp.json`中配置**，使用构建后的文件路径：
   ```json
   {
     "mcpServers": {
       "sequential-thinking": {
         "command": "node",
         "args": [
           "/absolute/path/to/mcp-server-sequential-thinking/dist/index.js"
         ]
       }
     }
   }
   ```

   > ⚠️ **注意**：
   > - 必须使用绝对路径指向构建后的文件
   > - Windows系统使用反斜杠，如：`C:\path\to\mcp-server-sequential-thinking\dist\index.js`
   > - 确保路径指向的是构建后的JavaScript文件

3. **验证文件权限**：
   ```bash
   # MacOS/Linux系统需要确保文件有执行权限
   chmod +x dist/index.js
   ```

例如，如果您的项目结构如下：
```
your-project/
├── .cursor/
│   └── mcp.json
└── mcp-servers/
    └── sequential-thinking/
        ├── node_modules/
        ├── src/
        └── dist/
            └── index.js
```

则配置文件可能如下：

- **MacOS/Linux**：
```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "node",
      "args": [
        "/Users/username/your-project/mcp-servers/sequential-thinking/dist/index.js"
      ]
    }
  }
}
```

- **Windows**：
```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "node",
      "args": [
        "C:\Users\username\your-project\mcp-servers\sequential-thinking\dist\index.js"
      ]
    }
  }
}
```

> 💡 **小贴士**：如果遇到构建问题，检查以下几点：
> - 确保Node.js版本符合要求
> - 检查是否有所有必要的依赖
> - 查看项目的README文件获取特定的构建说明
> - 确保构建命令成功执行且生成dist目录

### 🐳 使用Docker

> 📌 **提示**：Docker方式提供了最好的隔离性和可移植性，适合团队协作和生产环境。

1. **在`.cursor/mcp.json`中配置**：
   ```json
   {
     "mcpServers": {
       "服务器名称": {
         "command": "docker",
         "args": [
           "run",
           "--rm",
           "-v",
           "${workspaceRoot}:${workspaceRoot}",
           "-w",
           "${workspaceRoot}",
           "mcp-server-名称",
           "其他参数1",
           "其他参数2"
         ]
       }
     }
   }
   ```

## ✅ 验证集成

完成配置后，按以下步骤验证MCP服务器集成是否成功：

1. 确保`.cursor/mcp.json`文件格式正确
2. 重启Cursor
3. 在项目中尝试使用MCP服务器提供的功能
4. 检查Cursor的日志输出，确认服务器是否正常启动和运行

> 💡 **小贴士**：如果验证失败，请检查配置文件和日志输出，确认错误原因。

## ❓ 常见问题解答

### 1. 配置文件位置问题
Q: 为什么找不到配置文件？
A: 确保`.cursor`文件夹和`mcp.json`文件都在项目根目录下，并且文件名和路径完全匹配。

### 2. 权限问题
Q: 遇到权限相关错误怎么办？
A: 检查以下几点：
- 🔑 确保`.cursor`文件夹和`mcp.json`文件有正确的读写权限
- 🔓 对于filesystem服务器，确保配置的目录路径有正确的访问权限
- 👤 使用Docker方式时，确保当前用户有权限执行Docker命令

### 3. 服务器启动失败
Q: 服务器无法正常启动怎么办？
A: 
- 🔍 检查配置文件格式是否正确
- 📦 确认所需依赖是否已安装
- 📋 查看Cursor的日志输出，了解具体错误信息
- ⚙️ 确保指定的命令和参数路径正确

### 4. 路径配置
Q: 如何正确配置路径？
A:
- 📂 使用相对路径时，以项目根目录为基准
- 🔄 使用`${workspaceRoot}`变量表示项目根目录
- 💻 Windows系统注意使用正确的路径分隔符

> 📣 **记住**：正确的路径配置是MCP服务器成功运行的关键！

### 5. 多服务器配置
Q: 如何配置多个服务器？
A: 在`mcpServers`对象中添加多个服务器配置：
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "./",
        "--workspace-root",
        "./"
      ]
    },
    "postgres": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-v",
        "${workspaceRoot}:${workspaceRoot}",
        "-w",
        "${workspaceRoot}",
        "mcp-server-postgres",
        "--connection-string",
        "postgresql://user:password@localhost:5432/dbname"
      ]
    }
  }
}
```