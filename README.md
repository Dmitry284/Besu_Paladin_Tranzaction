# Hyperledger Besu + Paladin: Private Transaction Demo

Демонстрация работы приватных транзакций в корпоративной блокчейн-сети с использованием Hyperledger Besu и менеджера приватности Paladin (протокол Noto).

## Цель проекта

Показать, как участники сети могут обмениваться токенами так, что детали транзакции (сумма, отправитель, получатель) видны только вовлеченным сторонам, а в публичный реестр записывается только зашифрованный маркер (Privacy Marker Transaction).

## 🛠 Стек технологий

- **Blockchain:** Hyperledger Besu 26.2.0 (QBFT consensus)
- **Privacy Manager:** Paladin (Noto protocol)
- **Smart Contracts / Scripts:** TypeScript, Hardhat, Paladin SDK
- **Infrastructure:** Docker, Docker Compose
- **Block Explorer:** Chainlens

##  Архитектура сети

Сеть состоит из ~20 контейнеров Docker, разделенных на три слоя:

### Слой блокчейна (Hyperledger Besu)
- `rpcnode` — точка входа для внешних запросов (порт 8545)
- `validator1-4` — ноды-валидаторы консенсуса QBFT
- `member1-3` — ноды участников сети

### Слой приватности (Paladin)
- `paladin1-3` — сервисы шифрования и маршрутизации приватных данных

### Слой наблюдаемости (Chainlens)
- `chainlensingestion` — сервис чтения блоков из Besu
- `chainlensmongodb`, `chainlensredis` — база данных и кэш
- `chainlensapi`, `chainlensweb`, `chainlensnginx` — веб-интерфейс (порт 8081)

## Как запустить

### Предварительные требования
- Ubuntu 20.04+ (Linux)
- Docker и Docker Compose v2.0+
- Node.js 18+
- Минимум 8 ГБ RAM (рекомендуется 16 ГБ)

### Шаг 1: Развертывание сети

```bash
npx @consensys-software/besu-dev-quickstart \
    --networkType private \
    --privacy true \
    --chainlens true \
    --otel false \
    --outputPath ./besu-test-network

cd besu-test-network
./run.sh
