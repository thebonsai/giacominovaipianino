# 🖥️ Giacominovaipianino — Guida al Deploy

## Struttura del progetto

```
giacominovaipianino/
└── index.html          ← tutto il sito in un solo file
└── README.md           ← questo file
```

---

## 🚀 OPZIONE A — Deploy su GitHub Pages (gratis, 5 minuti)

1. Vai su [github.com](https://github.com) → crea un account se non ce l'hai
2. Clicca **"New repository"**
3. Nome: `giacominovaipianino` · metti **Public** · clicca **Create**
4. Clicca **"uploading an existing file"** → trascina `index.html`
5. Clicca **Commit changes**
6. Vai in **Settings → Pages → Branch: main → Save**
7. Il sito sarà online in 1-2 minuti su:
   `https://TUOUSERNAME.github.io/giacominovaipianino`

---

## 🚀 OPZIONE B — Deploy su Netlify (gratis, 2 minuti)

1. Vai su [netlify.com](https://netlify.com) → Sign up gratis
2. Trascina la cartella `giacominovaipianino/` nel riquadro "Deploy manually"
3. Il sito è online subito su un URL tipo `random-name-123.netlify.app`
4. Puoi cambiare il nome in **Site settings → Change site name**

---

## 🚀 OPZIONE C — Deploy su Vercel (gratis, 2 minuti)

1. Vai su [vercel.com](https://vercel.com) → Sign up con GitHub
2. **"Add New Project"** → importa il repository GitHub
3. Clicca Deploy → pronto!

---

## 💬 CONFIGURARE LA CHAT (Firebase Realtime Database)

La chat funziona **già senza Firebase** in modalità automatica
(risponde con messaggi preimpostati). Se vuoi rispondere tu in tempo
reale, segui questi passi:

### Step 1 — Crea il progetto Firebase

1. Vai su [console.firebase.google.com](https://console.firebase.google.com)
2. Clicca **"Aggiungi progetto"** → nome: `giacominovaipianino`
3. Disabilita Google Analytics (non serve) → **Crea progetto**

### Step 2 — Abilita Realtime Database

1. Nel menu a sinistra: **Build → Realtime Database**
2. **Crea database** → seleziona **Europe West** → **Avvia in modalità test**
3. Copia l'URL del database (tipo `https://giovanninovaipianino-default-rtdb.europe-west1.firebasedatabase.app/`)

### Step 3 — Ottieni le credenziali

1. Clicca ⚙️ **Impostazioni progetto** (in alto a sinistra)
2. Scorri fino a **"Le tue app"** → clicca l'icona `</>`(Web)
3. Nome app: `giacominovaipianino-web` → **Registra app**
4. Copia il blocco `firebaseConfig` che appare

### Step 4 — Incolla in index.html

Apri `index.html` e trova questa sezione:

```javascript
const FIREBASE_CONFIG = {
  apiKey:            "INSERISCI_QUI_API_KEY",
  authDomain:        "INSERISCI_QUI.firebaseapp.com",
  databaseURL:       "https://INSERISCI_QUI-default-rtdb.europe-west1.firebasedatabase.app",
  ...
};
```

Sostituisci con i tuoi valori reali, poi cambia:

```javascript
let USE_FIREBASE = true;  // ← cambia da false a true
```

### Step 5 — Regole di sicurezza (importante!)

Nel Realtime Database → **Regole**, incolla questo:

```json
{
  "rules": {
    "chats": {
      ".read": true,
      ".write": true
    }
  }
}
```

*(Funziona per uso tra amici. Per produzione vera serve auth — ma qui siamo in modalità Giacomino.)*

---

## 🎮 COME RISPONDERE AI MESSAGGI IN TEMPO REALE

### Metodo 1 — Firebase Console (il più semplice)

1. Apri [console.firebase.google.com](https://console.firebase.google.com) → il tuo progetto
2. **Realtime Database** → espandi `chats`
3. Vedrai le conversazioni con i loro `session_XXXXXXX`
4. Per rispondere: clicca `+` accanto alla session → aggiungi un nodo con:
   - chiave: (lascia vuoto, Firebase lo genera)
   - valore (oggetto JSON):
   ```json
   {
     "sender": "giacomino",
     "text": "ciao! ho letto il tuo problemino, prova a fare...",
     "time": "16:42"
   }
   ```
5. Il messaggio appare **istantaneamente** nella chat dell'utente ✨

### Metodo 2 — App Firebase Console su mobile

Scarica l'app **Firebase** sul telefono → puoi rispondere da ovunque,
come se fosse WhatsApp Business ma in versione Giacomino.

---

## 🎨 PERSONALIZZARE IL SITO

Tutte le modifiche si fanno in `index.html`:

| Cosa cambiare | Dove trovarlo |
|---------------|---------------|
| Nome/logo | Cerca `Giacominovaipianino` nel testo |
| Testo hero | Cerca `ciao amico carino` |
| Statistiche | I `data-target="4982"` nella stats bar |
| Recensioni | Cerca `review-card` |
| Timeline | Cerca `tl-item` |
| Colori neon | Le variabili CSS all'inizio: `--neon-cyan`, `--neon-green`, ecc. |
| Orario chat | Cerca `fra le 16 e le 17` |

---

## 🐣 EASTER EGG

Sul sito c'è il **Konami Code** nascosto:
`↑ ↑ ↓ ↓ ← → ← → B A`

Provalo sulla tastiera — Giacomino avrà una risposta speciale 👾

---

## 💡 SUGGERIMENTI PER RENDERLO PIÙ CREDIBILE

1. **Aggiungi una vera favicon** — usa emoji 🖥️ come favicon SVG:
   ```html
   <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🖥️</text></svg>">
   ```
   (già inclusa nel file)

2. **Dominio personalizzato** — su Netlify puoi collegare un dominio
   tipo `giacomino.it` per pochi euro l'anno

3. **Condividi il link** — mandalo su WhatsApp come se fosse un vero
   servizio di assistenza e aspetta la reazione

4. **Messaggio preimpostato** — cambia il messaggio di benvenuto per
   rendere la trappola più convincente

---

## 📦 Tecnologie usate

- HTML5 / CSS3 vanilla (zero framework)
- JavaScript ES2022 vanilla
- Google Fonts (VT323, Courier Prime, Press Start 2P)
- Firebase Realtime Database (opzionale, per chat live)
- Deploy: GitHub Pages / Netlify / Vercel (tutto gratis)

**Nessun npm, nessun build step, nessun backend.** Funziona aprendo index.html nel browser.

---

*© 1987–2024 Giacominovaipianino · Tecnologia brevettata moralmente*
