# wbh

## Login

```bash
docker login --username=<USER> <REG>
```

## Build & Push Docker

发布新版本时同时打 `:<版本号>` 和 `:latest` 两个 tag，保证 `latest` 永远指向最新一次发布的版本。

```bash
REPO=<REG>/uaigc/sub2api
TAG=0.0.2            # 每次发布改成新版本号
docker build -t "$REPO:$TAG" -t "$REPO":latest .
docker push "$REPO:$TAG"
docker push "$REPO":latest
```

> 注意：`latest` 的含义是「最近一次发布的 tag」，不是 git 历史上数值最大的版本。
> 如果后打的 tag 版本号反而更小、或发布后需要回滚重发旧版本，`latest` 会跟着指向它——这通常是期望行为。
> 服务器/容器编排拉镜像时去掉 tag（或写 `:latest`）即可始终拿到最新发布的镜像。
