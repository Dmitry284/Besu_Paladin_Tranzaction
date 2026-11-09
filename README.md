# Hyperledger Besu + Paladin: Private Transaction Demo

Этот проект демонстрирует работу приватных транзакций в корпоративной блокчейн-сети с использованием Hyperledger Besu и менеджера приватности Paladin (протокол Noto).

## Цель проекта
Показать, как участники сети могут обмениваться токенами так, что детали транзакции (сумма, отправитель, получатель) видны только вовлеченным сторонам, в то время как публичный реестр содержит только зашифрованный маркер (Privacy Marker Transaction).

## Стек технологий
- **Blockchain:** Hyperledger Besu (QBFT consensus)
- **Privacy Manager:** Paladin (Noto protocol)
- **Smart Contracts / Scripts:** TypeScript, Hardhat, Paladin SDK
- **Infrastructure:** Docker, Docker Compose

## Как это работает 
Скрипт `scripts/privacy/noto_tx.ts` выполняет следующую последовательность:
1. **Deploy:** Развертывание приватного токена Noto, где `member1` выступает в роли нотариуса (notary).
2. **Mint:** Выпуск 2000 токенов для `member1`.
3. **Private Transfer 1:** Приватный перевод 1000 токенов от `member1` к `member2`.
4. **Private Transfer 2:** Приватный перевод 800 токенов от `member2` к `member3`.
5. **Verification:** Проверка финальных балансов, подтверждающая корректность приватных вычислений.

## Как запустить локально

1. Запустите тестовую сеть Besu + Paladin через Docker:
   ```bash
   npx @consensys-software/besu-dev-quickstart --networkType private --privacy true
   cd besu-test-network && ./run.sh