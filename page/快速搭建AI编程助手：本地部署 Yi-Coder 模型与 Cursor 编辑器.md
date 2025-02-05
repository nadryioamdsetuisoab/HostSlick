# 快速搭建AI编程助手：本地部署 Yi-Coder 模型与 Cursor 编辑器

Yi-Coder 是一款开源的**高性能代码语言大模型**，专为高效编程设计。它支持多达 52 种编程语言，擅长处理需要长上下文理解的任务，例如项目级代码理解和生成。该模型提供两种规模（15亿和90亿参数），并且分为基础版和聊天版两种类型。

在本教程中，您将学习如何：

- 在本地运行与 OpenAI 兼容的 API，驱动 Yi-Coder 模型
- 将 Yi-Coder 与 Cursor 编辑器集成，实现高效编程辅助

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)

## 本地运行 Yi-Coder 模型

首先，我们需要获取 Cursor 所需的本地 Yi-Coder-9B 模型的公共 HTTPS 端点。以下是详细步骤：

### 安装 Gaia 节点

Gaia 节点是一组轻量级、可移植的 LLM 推理工具。其技术栈基于 **WasmEdge**，这是一个专为无服务器计算和边缘应用优化的 WebAssembly 运行时。Gaia 节点的高效部署能力为 Yi-Coder 在不同环境中的运行提供了灵活性和可扩展性。

运行以下命令安装 Gaia 节点：

bash
curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' | bash


### 初始化并启动模型

下载并初始化模型：

bash
gaianet init --config https://raw.githubusercontent.com/GaiaNet-AI/node-configs/main/yi-coder-9b-chat/config.json


然后启动节点：

bash
gaianet start


启动成功后，您将获得一个 HTTPS URL，例如：`https://NODE-ID.us.gaianet.network`。同时，您可以在浏览器中访问 `http://localhost:8080`，向模型提问。

![Yi-Coder 运行界面](https://bbtdd.com/img/636488978628.webp@1192w)

> **提示**：默认情况下，Yi-Coder 以 8k 的上下文窗口启动。如果您的机器具备较大的 GPU 显存（例如 24GB），可以将上下文窗口扩展至 128k。更大的上下文窗口在编码任务中尤为有用，尤其是在需要将大量源代码文件导入 LLM 提示时。

## 将 Yi-Coder 与 Cursor 集成

接下来，我们将把 Yi-Coder-9B 集成到 Cursor 编辑器中。以下是具体步骤：

1. 用 Gaia 节点的 URL 替换 Cursor 默认的 OpenAI URL。
2. 正确设置模型名称和“API 密钥”。

完成上述配置后，您就可以在 Cursor 中使用 Yi-Coder 了。

![Cursor 集成测试](https://bbtdd.com/img/61685867283555.webp@1192w)

### 实际应用测试

让我们通过一个简单示例测试 Yi-Coder-9B 的能力。以下是生成一个搜索页面的过程：

1. 提示模型生成一个简单的搜索页面。
2. 要求模型修改按钮上的文字标签。

![搜索页面生成](https://bbtdd.com/img/95518035459.webp@1192w)

![按钮文字修改](https://bbtdd.com/img/9329709867.webp@1192w)

最终，网页按预期运行：

![网页运行结果](https://bbtdd.com/img/3759069464405.webp@1192w)

## 参考资料

- **Yi-Coder**: 了解模型的详细信息。
- **WasmEdge**: 查看 WasmEdge 的 GitHub 页面。
- **LlamaEdge 文档**: 获取更多技术细节。

## 关于 WasmEdge

WasmEdge 是一款轻量级、安全、高性能的软件容器与运行环境。它是 CNCF 的沙箱项目，广泛应用于 SaaS、云原生、边缘计算、LLM 推理等领域。