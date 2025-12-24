# AI医疗助手项目文档

## 项目简介
AI医疗助手是一个结合前沿人工智能技术的医疗问答系统，采用现代化前后端分离架构，集成了智能问答、知识检索和多模态交互功能。

## 技术架构

### 前端技术栈
- 开发框架：React 19+TypeScript
- 状态管理：React Hooks
- 样式设计：CSS Modules
- 网络通信：Fetch API（具备流式响应能力）
- 功能组件：自定义聊天界面、Markdown内容渲染、通知提示组件

### 后端技术栈
- API框架：FastAPI
- AI开发框架：LangChain 0.3.0
- 大模型服务：通义千问系列模型
- 向量存储：Chroma数据库
- 文本处理：DashScope嵌入模型
- 实时通信：SSE技术方案
- 文档解析：LangChain文本分割器

## 系统架构图

```
用户界面层 → API服务层 → AI能力层 → 知识存储层
   (React)     (FastAPI)   (LangChain)    (Chroma)
      ↓           ↓           ↓              ↓
   展示交互  ←  业务逻辑  ←  智能处理  ←  知识检索
```

## 安装部署指南

### 运行环境要求
- Python运行环境 3.10以上版本
- Node.js运行环境 16以上版本
- 有效的通义千问API访问凭证

### 后端服务配置步骤

#### 环境准备
```bash
cd backend
python -m venv venv_env
# Windows系统执行：
venv_env\Scripts\activate
# Linux/Mac系统执行：
source venv_env/bin/activate
```

#### 依赖安装
```bash
pip install -r requirements.txt
```

#### 环境变量设置
创建环境配置文件 `.env`：

```ini
API_KEY=your_actual_api_key
SERVER_PORT=8000
SERVER_HOST=0.0.0.0
ALLOWED_ORIGINS=http://localhost:3000
```

#### 服务启动
```bash
python app_main.py
# 或使用以下命令：
uvicorn app_main:application --host 0.0.0.0 --port 8000 --reload
```

### 前端界面配置步骤

#### 进入项目目录
```bash
cd frontend
```

#### 安装依赖包
```bash
npm install
```

#### 启动开发服务器
```bash
npm run dev
```

#### 访问地址
浏览器中打开：http://localhost:3000

## 功能特性

### 核心功能
- 医疗健康问题智能解答
- 实时对话流式输出效果
- 多轮对话上下文保持
- 专业知识库检索增强
- 图片上传与医学图像分析
- 文本到图像生成功能
- 对话历史记录管理

### 特色功能
- Markdown格式响应内容
- 医疗术语专业解释
- 健康建议结构化输出
- 重要信息突出强调
- 会话状态持久保存

## API接口文档

服务启动后访问 http://localhost:8000/docs 查看完整接口文档

### 主要接口端点

#### 聊天相关接口
- `POST /api/conversation` - 标准聊天接口
- `POST /api/conversation/stream` - 流式聊天接口
- `GET /api/conversation/stream` - 流式连接接口

#### 多媒体接口
- `POST /api/multimodal/upload` - 文件上传聊天
- `POST /api/multimodal/json` - JSON格式聊天
- `POST /api/image/generate` - 图像生成接口

#### 数据管理接口
- `GET /api/conversations/{id}/history` - 历史记录查询
- `GET /api/health` - 服务健康检查

### 请求示例

```python
# Python请求示例
import requests

# 标准聊天请求
response = requests.post(
    "http://localhost:8000/api/conversation",
    json={
        "query": "高血压日常注意事项",
        "history": []
    }
)

# 流式聊天请求
import aiohttp
import asyncio

async def stream_chat():
    async with aiohttp.ClientSession() as session:
        async with session.post(
            "http://localhost:8000/api/conversation/stream",
            json={"query": "糖尿病饮食建议"}
        ) as response:
            async for data_chunk in response.content:
                print(data_chunk.decode(), end="")
```

## 项目结构说明

```
项目根目录/
├── 后端代码/
│   ├── app_main.py          # 主程序入口
│   ├── 依赖列表.txt         # Python包依赖
│   ├── 环境配置.env         # 环境变量文件
│   └── 上传文件/            # 用户文件存储
└── 前端代码/
    ├── 公共资源/            # 静态资源文件
    ├── 源代码/
    │   ├── 应用主组件.tsx   # 根组件
    │   ├── 程序入口.tsx     # 应用入口
    │   └── 组件模块/        # 功能组件目录
    │       └── 聊天界面.tsx # 核心聊天组件
    └── 包管理.json          # 前端依赖配置
```

## 配置参数说明

### 环境变量配置

```ini
# 必需配置项
API_KEY=your_api_key_here

# 可选配置项
SERVER_PORT=8000                    # 服务端口号
SERVER_HOST=0.0.0.0                 # 服务监听地址
ALLOWED_ORIGINS=http://localhost:3000 # 跨域允许来源
KNOWLEDGE_BASE_FILE=medical_kb.md   # 知识库文件路径
UPLOAD_DIR=user_uploads             # 上传文件目录
```

### 知识库配置
1. 在backend目录创建医疗知识文件
2. 使用Markdown格式组织内容
3. 系统自动构建向量索引

## 系统特性详解

### 智能问答机制
- 检索增强生成技术应用
- 上下文对话历史管理
- 智能回答策略选择
- 异常情况后备处理

### 实时通信机制
- Server-Sent Events协议
- 实时数据流式传输
- 自动连接维护
- 网络异常处理

### 多模态支持
- 图像文件格式兼容
- Base64数据编码
- 多媒体模型调用
- 生成图像功能

## 重要注意事项

### 医疗信息声明
⚠️ **医疗免责说明**：本系统提供的信息仅供教育和参考用途，不能替代专业医疗建议。如有健康问题，请咨询合格医疗专业人员。

### 使用限制说明
1. **API调用限制** - 遵循服务商调用频率限制
2. **知识范围限制** - 依赖于配置的知识库内容
3. **数据持久性** - 当前版本使用内存存储，重启后数据清空
4. **性能考量** - 响应时间受网络和API服务影响

## 扩展开发计划

### 近期规划
- 支持更多大语言模型接口
- 用户身份验证系统
- 数据库持久化存储
- 医疗报告生成功能

### 远期规划
- 语音交互功能支持
- 医疗预约集成
- 数据分析可视化
- 移动端应用适配

## 鸣谢名单
- LangChain开发团队 - AI应用框架
- FastAPI项目组 - Web框架
- React社区 - 前端框架
- 通义千问团队 - AI模型服务

## 问题反馈
- **问题报告**：通过项目Issue功能提交
- **功能建议**：使用Discussion功能讨论
- **技术交流**：开发者社区沟通

---
**AI医疗助手** - 智能医疗咨询服务系统 🏥💡
