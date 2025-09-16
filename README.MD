# @elrayyxml/baileys

### 📦 Installation

```bash
npm install @elrayyxml/baileys
# or
yarn add @elrayyxml/baileys
```

### 🚀 Quick Example

```ts
import makeWASocket from '@elrayyxml/baileys'
import { getSenderLid, toJid } from '@elrayyxml/baileys'

const sock = makeWASocket({ printQRInTerminal: true })

sock.ev.on('messages.upsert', ({ messages }) => {
    const msg = messages[0]
    const info = getSenderLid(msg) // logs the sender LID
    const jid = toJid(info.lid)
    console.log('normalized jid:', jid)
})
```

### 🧪 Advanced Usage (Multi-file Auth)

```ts
import makeWASocket, { useMultiFileAuthState } from "@elrayyxml/baileys"

async function start() {
    const { state, saveCreds } = await useMultiFileAuthState("auth_info")
    const sock = makeWASocket({ auth: state, printQRInTerminal: true })

    sock.ev.on("creds.update", saveCreds)
    sock.ev.on("messages.upsert", ({ messages }) => {
        for (const m of messages) {
            console.log(m.key.remoteJid, m.message?.conversation)
        }
    })
}

start()
```

### ⚠️ Disclaimer
This project is not affiliated with WhatsApp Inc. Use it responsibly. Avoid spam, abuse, or any illegal activities.

---

### 📄 License
MIT © 2024 elrayyxml Network
