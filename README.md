# pdf-reader

Dockerを用いたPython実行環境です。

## 環境の起動
```bash
docker compose -f docker/docker-compose.yml up -d --build
```

## Pythonバージョン確認
```bash
docker compose -f docker/docker-compose.yml exec pdf-reader-dev python --version
```

## コンテナに入る
```bash
docker compose -f docker/docker-compose.yml exec pdf-reader-dev sh
```

## 環境の停止
```bash
docker compose -f docker/docker-compose.yml down
```
