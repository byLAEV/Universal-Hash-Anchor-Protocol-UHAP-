Universal Hash Anchor Protocol (UHAP)

Desarrollado por

LAEV & El Cartel de Bitcoiners


---

📌 Descripción

UHAP es un protocolo abierto, minimalista y universal que permite a cualquier sistema externo (blockchains, DAOs, contratos, Dapps, etc.) registrar su estado o evento en la red Bitcoin utilizando una transacción con OP_RETURN.
Si no está en el hash de Bitcoin, no pasó.


---

🧠 Filosofía

Bitcoin es el único notario descentralizado, global e incorruptible.

Las blockchains externas son herramientas, no raíz de verdad.

Descentralizar sin anclar es ficción útil, pero peligrosa.

Un registro anclado a Bitcoin vale más que mil logos.



---

❓¿Por qué?

Porque los sistemas descentralizados necesitan un testigo imparcial y permanente. Bitcoin, con su seguridad de proof-of-work y su inmutabilidad, es el único candidato serio para cumplir ese rol.
Usar UHAP es usar Bitcoin como el testigo supremo.


---

⚙️ Cómo funciona

1. Definí el estado que querés registrar desde una blockchain externa (por ejemplo: bloque, snapshot, contrato, NFT).


2. Convertilo a string JSON y calculá su hash (SHA-256).


3. Creá una transacción en Bitcoin con una salida OP_RETURN que contenga ese hash.


4. Transmití la transacción. ¡Listo! Ya está anclado públicamente.




---

💻 Ejemplo de código en Python

import hashlib
from bitcoinlib.transactions import Transaction, Output
from bitcoinlib.wallets import Wallet

# Datos del estado externo
estado_xchain = {
    "project_id": "XCHAIN-2025",
    "block_height": 18400,
    "merkle_root": "c3d4e1a84f7e8f9b1c93e2dd44b71a5a"
}

# Hash del estado
estado_str = str(estado_xchain).encode('utf-8')
hash_estado = hashlib.sha256(estado_str).hexdigest()
print("Hash para anclar en Bitcoin:", hash_estado)

# Crear transacción con OP_RETURN
wallet = Wallet('mi_wallet_bitcoin')
tx = Transaction()
tx.add_output('bc1qdireccionsalida...', 1000)  # Enviar sats
op_return_script = '6a20' + hash_estado
tx.outputs.append(Output(0, 'OP_RETURN', data=bytes.fromhex(op_return_script)))
wallet.get_key().sign_transaction(tx)
txid = tx.send()
print("TXID:", txid)


---

📦 Requisitos

Python 3.7+

bitcoinlib o bit como librería de Bitcoin

Una wallet con acceso a UTXOs y claves privadas (Electrum o Bitcoin Core RPC también sirven)



---

🔍 Auditoría del registro

Podés verificar cualquier TXID con OP_RETURN desde:

blockstream.info

mempool.space

o desde tu propio nodo Bitcoin



---

⚖️ Licencia

Este protocolo es de uso libre bajo la MIT License
o bajo una licencia custom LAEV Public License para adopción institucional extrema.


---

🛠 Contacto y comunidad

GitHub: lerryalexanderelizondo


---

> Cartel de Bitcoiners:
No hay descentralización sin ancla. No hay verdad sin hash.
