# KipuBank 🏦

**KipuBank** es un contrato inteligente desarrollado en Solidity como parte del proyecto **Ethereum Developer** del curso dictado por **ETH-Kipu**. Su objetivo es simular un banco descentralizado donde los usuarios pueden depositar y retirar Ether respetando límites definidos por el contrato.

---

## 📜 Descripción

Este contrato permite:
- Depositar Ether en el contrato.
- Retirar Ether con límites de seguridad.
- Consultar el balance personal y del contrato.
- Control de límites por transacción y límite total de almacenamiento del banco.

### Autor
- **Matías Grando**, estudiante de EthKipu

---

## ⚙️ Detalles Técnicos

- **Versión de Solidity:** `>0.8.28`
---

## 🔐 Variables clave

- `MAX_WITHDRAFT_PER_TRANSACTION`: Límite máximo de retiro por transacción.
- `MAX_CAP_BANK`: Límite máximo de fondos totales que puede tener el contrato.
- `userBalance`: Mapea direcciones de usuarios con sus saldos en Ether.
- `totalDeposits`, `totalWithdraft`: Contadores de depósitos y retiros.

---

## 📥 Funciones principales

### `deposit()`, `receive()`, `fallback()`
Permiten enviar Ether al contrato. Todas actualizan el saldo del usuario y verifican que el depósito no supere el `MAX_CAP_BANK`.

### `withdraf(uint256 amount)`
Permite al usuario retirar Ether de su saldo bajo las siguientes condiciones:
- No exceder `MAX_WITHDRAFT_PER_TRANSACTION`.
- Tener suficiente saldo disponible.

### `getBalance()`
Devuelve el saldo del llamador.

### `getContractBalance()`
Devuelve el balance total en Ether del contrato.

---

## 🚨 Manejador de Errores

El contrato implementa errores personalizados para mejorar la legibilidad y gas eficiencia:
- `MaxCapBank`: Si el depósito supera el límite del contrato.
- `MaxWithdraftPerTransaction`: Si el retiro supera el límite permitido.
- `WithdraftFail`: Si la operación de retiro falla.
- `WithoutSufficientBalance`: Si el usuario intenta retirar más de lo disponible.

---

## 🛠 Constructor
constructor(uint256 _maxWithdraftPerTransaction, uint256 _maxCapBank)


Al desplegar el contrato, se deben pasar:

Límite de retiro por transacción (_maxWithdraftPerTransaction)

Límite de fondos del banco (_maxCapBank)

---
## 🛡️ Seguridad


- Evita depósitos que excedan el límite total del banco.

- Impide retiros por encima del límite por transacción.

- Solo el propietario del saldo puede retirar sus fondos.

- Validación estricta de errores con revert.


