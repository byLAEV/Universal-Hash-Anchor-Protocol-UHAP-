# Anchored in Bitcoin

Official repository of the global project “Anchored in Bitcoin”

"If your data can’t be verified outside your system, it’s not truth. It’s a narrative."

## Overview

Anchored in Bitcoin is a universal API and toolkit designed to anchor the state of any database or digital content directly into the Bitcoin blockchain.  
Its mission is to provide a decentralized, transparent, and incorruptible root of trust.

It allows anyone on Earth (organizations, DAOs, individuals, servers, governments, artists) to cryptographically sign their data and verify its integrity, detecting any tampering or manipulation through public Bitcoin-based proof.

## Core Function

- Seal the state of databases or files using cryptographic hashes  
- Anchor those hashes on the Bitcoin blockchain via OP_RETURN transactions  
- Enable anyone to externally verify whether data has been altered  
- Ensure data integrity, transparency, and sovereignty

## How It Works (Step-by-Step)

1. Select the content  
   Choose what part of your system you want to anchor: entire database, key tables, documents, texts, contracts, evidence, etc.

2. Deterministic serialization  
   Convert the data into a stable format like sorted JSON or flat CSV.

3. Hash computation  
   Generate a cryptographic hash (e.g. SHA256) of the serialized content.

4. Submit to the API  
   Send that hash to the Anchored in Bitcoin API to be signed and broadcasted to the Bitcoin network using the OP_RETURN field.

5. Blockchain confirmation  
   You receive a TXID that proves the anchoring. This becomes a public and immutable record, timestamped and accessible worldwide.

6. Public verification  
   Anyone can re-compute the hash from the data and compare it to the one stored on Bitcoin.  
   If it doesn’t match — the content was altered.

## Repository Contents

- /api/: REST API source code for anchoring and verifying hashes on Bitcoin  
- /clients/: Usage examples in Python, Node.js, Bash  
- /utils/: Scripts for deterministic serialization and hashing  
- /examples/: Real-world implementation cases  
- whitepaper.md: Technical and philosophical manifesto  
- /docs/: Integration guides for PostgreSQL, MongoDB, Redis, etc.

## Use Cases

| Sector        | Use Case |
|---------------|----------|
| Education     | Verifiable, immutable academic records  
| Justice       | Digital evidence and official declarations sealing  
| Journalism    | Anchor investigations and whistleblower material  
| DAOs / NGOs   | Transparent voting and governance anchoring  
| Digital Art   | Authenticated works without reliance on NFTs  
| Governments   | Anchored statistics and public policy data  
| Enterprises   | Auditable financials and data integrity systems  

## Project Philosophy

Any truth that matters must be able to be anchored in Bitcoin.  
If it can’t — it’s not truth. It’s narrative.

We reject:  
- Shitcoins  
- Institutional censorship  
- Third-party dependency  
- Centralized narratives

We promote:  
- Radical transparency  
- Individual sovereignty  
- Verifiable integrity  
- Corruption-resistant design

## Target Audience

- Developers of critical systems  
- Information architects  
- Artists, writers, journalists  
- Privacy and truth activists  
- Ethical governments and DAOs  
- Web3 projects with real decentralization goals

## License

MIT — full freedom to use, modify, and implement.  
Any attempt to co-opt or corrupt this tool for centralized purposes will be publicly exposed.

## Contact / Integration

Want to integrate Anchored in Bitcoin into your system?  
Want to contribute or propose improvements?

Direct contact:  
laev.lab@proton.me  
https://github.com/lerryalexanderelizondo

Anchored in Bitcoin is for those who refuse to have their truth erased.

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
