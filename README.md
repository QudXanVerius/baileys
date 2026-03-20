# WhatsApp Baileys

WhatsApp Baileys adalah library open-source berbasis WebSocket untuk membangun solusi otomatisasi WhatsApp tanpa memerlukan browser. Library ini mendukung pengelolaan pesan, chat, administrasi grup, serta pesan interaktif secara efisien.

### Fitur Utama
* Mendukung proses pairing otomatis dan kustom.
* Peningkatan stabilitas koneksi dan autentikasi.
* Mendukung pesan interaktif: tombol, menu dinamis, dan polling.
* Manajemen sesi otomatis untuk operasional yang reliabel.
* Kompatibel dengan fitur multi-device WhatsApp terbaru.

---

## Instalasi

Tambahkan dependensi berikut pada file \`package.json\`:

```json
"dependencies": {
  "@whiskeysockets/baileys": "github:QudXanVerius/baileys"
}
```

## Koneksi

### Menggunakan QR Code
\`\`\`javascript
const { default: makeWASocket } = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.0.0'],
  printQRInTerminal: true
});
\`\`\`

### Menggunakan Pairing Code
\`\`\`javascript
const { default: makeWASocket, fetchLatestWAWebVersion } = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: ['Ubuntu', 'Chrome', '20.0.0'],
  printQRInTerminal: false,
  version: (await fetchLatestWAWebVersion()).version
});

const number = "628XXXXX";
const code = await client.requestPairingCode(number);
console.log("Pairing Code: " + code);
\`\`\`

---

## Pengiriman Pesan

### Order Message
\`\`\`javascript
const fs = require('fs');

await client.sendMessage(jid, {
  thumbnail: fs.readFileSync('./image.jpg'),
  message: "Order Description",
  orderTitle: "Item Title",
  totalAmount1000: 1000000,
  totalCurrencyCode: "IDR"
}, { quoted: m });
\`\`\`

### Poll Message
\`\`\`javascript
await client.sendMessage(jid, {
  pollResultMessage: {
    name: "Poll Name",
    options: [
      { optionName: "Option 1" },
      { optionName: "Option 2" }
    ],
    newsletter: {
      newsletterName: "Channel Name",
      newsletterJid: "1@newsletter"
    }
  }
});
\`\`\`

---
