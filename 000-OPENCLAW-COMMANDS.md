# OpenClaw 常用命令速查

## 0) 进入目录
```bash
cd /home/homura/openclaw
```

## 1) 查看服务状态
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml ps
```

## 2) 启动/重启网关
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml up -d openclaw-gateway
```

## 3) 停止网关
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml stop openclaw-gateway
```

## 4) 查看实时日志
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml logs -f openclaw-gateway
```

## 5) 本机直接问 Agent（不走 Telegram）
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml run --rm openclaw-cli \
  agent --agent main --message "你好，做个自我介绍"
```

## 6) 指定项目路径让 Agent 分析代码/文档
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml run --rm openclaw-cli \
  agent --agent main --message "请先查看 /home/node/workspace/project，然后总结项目结构和进度。"
```

## 7) 打开本机控制台地址（Control UI）
```text
http://127.0.0.1:18789/#token=你的gateway_token
```

## 8) 检查模型配置状态
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml run -T --rm openclaw-cli models status
```

## 9) 读取配置项
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml run -T --rm openclaw-cli \
  config get agents.defaults.model.primary
```

## 10) 设置默认模型（示例）
```bash
docker compose -f docker-compose.yml -f docker-compose.extra.yml run --rm openclaw-cli \
  config set agents.defaults.model.primary "packycode/gpt-5.2"
```

## 11) 网关健康检查
```bash
curl -fsS http://127.0.0.1:18789/healthz
curl -fsS http://127.0.0.1:18789/readyz
```

## 12) 常见排障
```bash
# 看端口占用
ss -ltnp | rg '18789|18790'

# 查看容器详情
docker ps -a | rg openclaw

# 查看网关容器主进程
docker top openclaw-openclaw-gateway-1
```

## 13) 你当前关键文件
```text
/home/homura/openclaw/.env
/home/homura/openclaw/docker-compose.yml
/home/homura/openclaw/docker-compose.extra.yml
```
