# Agent-Practice-Demo
👉 本仓库为个人脱敏复现Demo，**不含任何任职企业真实业务源码与数据**，对应简历中两个企业Agent项目核心逻辑。

## 项目简介
复现两类业务Agent核心能力：
1. **客服故障排障Agent**：基于LangGraph + Milvus RAG，实现设备实体提取、指代消解、多轮会话持久化、SSE流式输出，模拟厨电售后问答。
2. **对话式BI NL2SQL Agent**：基于LangGraph实现Human-in-the-Loop人机审批，SQL AST语法安全拦截，指标知识库RAG优化SQL生成，自然语言查询模拟经营数据。

## 技术栈
Python3.10｜FastAPI｜LangGraph｜Milvus｜Redis｜sqlparse｜BGE-Rerank｜Docker-Compose

## 架构图
- 客服Agent架构图：`./docs/customer_agent_arch.png`
- BI-NL2SQL Agent架构图：`./docs/bi_agent_arch.png`

## 功能特性
### 客服排障Agent
- ✅ LangGraph状态机编排多轮故障排查流程
- ✅ Milvus向量检索 + Rerank重排优化召回
- ✅ 实体归一、查询重写，解决多轮指代歧义
- ✅ RedisSaver 会话状态持久化
- ✅ FastAPI SSE流式接口、模型调用异常重试封装

### NL2SQL对话BI Agent
- ✅ LangGraph Interrupt 实现Human-in-the-Loop人工审批节点
- ✅ sqlparse AST语法树校验，拦截DROP/ALTER等高危SQL
- ✅ 业务指标口径知识库RAG注入Prompt，提升SQL准确率
- ✅ 多轮对话上下文继承

## 快速启动
```bash
# 1. 复制环境配置模板，填入自己的密钥
cp .env.example .env

# 2. 启动Milvus、Redis依赖
docker-compose up -d

# 3. 安装依赖
pip install -r requirements.txt

# 4. 启动服务
python service/main_api.py
