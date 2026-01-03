# 🚀 GUIDA RAPIDA - Inizia Domani!

## 📋 Checklist Pre-Partenza (5 minuti)

- [ ] Hai Windows 11 Pro ✅
- [ ] Hai un iPhone per testare ✅
- [ ] Hai già Cloudflare Pages configurato ✅
- [ ] Devi installare Node.js
- [ ] Devi installare VS Code
- [ ] Devi configurare il progetto

---

## ⚡ Setup Rapido (20 minuti totali)

### PASSO 1: Installa Node.js (5 min)

Apri **PowerShell come Amministratore** e copia-incolla:

```powershell
# Scarica e installa Node.js LTS
winget install OpenJS.NodeJS.LTS
```

Chiudi e riapri PowerShell, poi verifica:

```powershell
node -v
npm -v
```

Dovresti vedere `v22.x.x` e `10.x.x`.

---

### PASSO 2: Installa VS Code (3 min)

```powershell
winget install Microsoft.VisualStudioCode
```

Dopo l'installazione, apri VS Code e installa le estensioni:

```powershell
code --install-extension ritwickdey.LiveServer
```

---

### PASSO 3: Prepara il Progetto (5 min)

1. **Crea una cartella per il progetto:**

```powershell
mkdir C:\progetti\preventivo-pro
cd C:\progetti\preventivo-pro
```

2. **Copia i file che ti ho preparato:**
   - Scarica il file `index.html` che ti ho creato
   - Copia anche i tuoi file esistenti: `manifest.webmanifest`, `sw.js`, `make-icons.html`
   - Crea la cartella `icons/` e copia le icone

3. **Struttura finale:**
```
C:\progetti\preventivo-pro\
├── index.html          (NUOVO - con foto integrate!)
├── manifest.webmanifest
├── sw.js
├── make-icons.html
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

---

### PASSO 4: Testa in Locale (5 min)

**Opzione A - Con VS Code (FACILE):**

1. Apri la cartella in VS Code:
```powershell
code C:\progetti\preventivo-pro
```

2. Clicca destro su `index.html` → "Open with Live Server"

3. Si apre automaticamente nel browser su `http://localhost:5500`

**Opzione B - Con npm (Manuale):**

```powershell
# Installa http-server globalmente
npm install -g http-server

# Avvia server
cd C:\progetti\preventivo-pro
http-server -p 8080 -c-1
```

Apri browser su `http://localhost:8080`

---

### PASSO 5: Testa su iPhone (7 min)

Per testare su iPhone hai **DUE opzioni**:

#### **OPZIONE A: Cloudflared (CONSIGLIATO - Gratuito e semplice)**

1. Installa Cloudflared:
```powershell
winget install Cloudflare.cloudflared
```

2. Avvia il tunnel (lascia Live Server attivo):
```powershell
cloudflared tunnel --url localhost:5500
```

3. Vedrai un URL tipo:
```
https://random-name-abc123.trycloudflare.com
```

4. **Su iPhone:** Apri Safari e vai a quell'URL!

#### **OPZIONE B: ngrok (Alternativa)**

```powershell
# Installa ngrok
winget install ngrok.ngrok

# Avvia tunnel
ngrok http 5500
```

Copia l'URL HTTPS mostrato e aprilo su iPhone Safari.

---

## 📱 Test su iPhone - Cosa Verificare

1. **Apri Safari** (DEVE essere Safari, non Chrome!)
2. Vai all'URL HTTPS dal tunnel
3. **Prova la fotocamera:**
   - Clicca "📷 Scatta Foto"
   - La fotocamera si dovrebbe aprire
   - Scatta una foto
   - Vedi l'anteprima compressa?

4. **Installa come PWA:**
   - Tap sull'icona **Condividi** (quadrato con freccia)
   - Scorri e tap **"Aggiungi a Home"**
   - Conferma
   - L'icona appare nella home!

5. **Apri la PWA installata:**
   - Deve aprirsi a schermo intero (no barra Safari)
   - Funziona anche offline!

---

## 🎯 Cosa Hai Ora di Nuovo

✅ **Funzionalità Foto Cantiere:**
- Scatta foto direttamente dall'app
- Galleria per scegliere foto esistenti
- Compressione automatica < 1MB
- Max 10 foto per preventivo
- Preview in griglia

✅ **Storage Avanzato:**
- IndexedDB invece di localStorage
- Supporta foto (blob)
- Preventivi + foto salvati insieme

✅ **Archivio Migliorato:**
- Carica preventivi con le foto
- Elimina preventivi con tutte le foto

---

## 🐛 Problemi Comuni e Soluzioni

### "Service Worker non si registra"
**Causa:** URL non è HTTPS  
**Soluzione:** Usa cloudflared o ngrok

### "Le foto non si comprimono"
**Causa:** Libreria non caricata  
**Soluzione:** Verifica connessione internet (usa CDN)

### "IndexedDB vuoto dopo riavvio iPhone"
**Causa:** iOS può cancellare dati dopo 7 giorni  
**Soluzione:** Normale, salva su cloud (prossimo step)

### "Fotocamera non si apre su iPhone"
**Causa:** Permessi o Safari non aggiornato  
**Soluzione:** Aggiorna iOS a versione recente (16.4+)

---

## 📋 Prossimi Passi (Dopo Domani)

Una volta che tutto funziona:

1. **Generazione PDF** con foto integrate
2. **Sincronizzazione Cloud** (Supabase)
3. **Multi-utente** con login
4. **Deploy pubblico** su Cloudflare Pages

---

## 💡 Comandi Rapidi da Ricordare

```powershell
# Avvia Live Server (VS Code)
# Clicca destro su index.html → Open with Live Server

# Oppure avvia http-server
http-server -p 5500 -c-1

# Tunnel HTTPS per iPhone
cloudflared tunnel --url localhost:5500

# Stop tutto: CTRL+C nei terminali
```

---

## 🆘 Help & Debug

Se qualcosa non funziona:

1. **Apri la Console:** F12 nel browser
2. **Cerca errori rossi** nella tab Console
3. **Verifica Network:** tab Network per vedere se carica le librerie
4. **iPhone Debug:** Aggiungi `?debug` all'URL per vedere la console Eruda

---

## ✅ Checklist Finale

Hai completato con successo quando:

- [ ] Vedi l'app in locale su Windows
- [ ] La fotocamera si apre su iPhone
- [ ] Le foto si comprimono e appaiono in griglia
- [ ] Puoi salvare un preventivo con foto
- [ ] Puoi riaprire il preventivo e vedi le foto
- [ ] La PWA si installa su iPhone home screen

---

**🎉 Sei pronto! Domani mattina inizia con il PASSO 1 e in 30 minuti avrai tutto funzionante!**
