# 🚀 Deploy su Cloudflare Pages

## Opzione 1: Upload Diretto (VELOCE - 5 minuti)

Questa è l'opzione più rapida se non vuoi usare Git.

### Passo 1: Prepara i File

Assicurati di avere tutti i file nella cartella:
```
preventivo-pro/
├── index.html
├── manifest.webmanifest
├── sw.js
├── make-icons.html
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

### Passo 2: Crea le Icone

1. Apri `make-icons.html` nel browser
2. Clicca "Scarica 192" → salva in `icons/icon-192.png`
3. Clicca "Scarica 512" → salva in `icons/icon-512.png`

### Passo 3: Deploy su Cloudflare

1. Vai su https://dash.cloudflare.com
2. **Workers & Pages** → **Create**
3. Seleziona **Pages** → **Upload assets**
4. Dai un nome al progetto: `preventivo-pro`
5. **Seleziona tutta la cartella** e trascinala
6. Clicca **Deploy**

🎉 **Fatto!** L'URL sarà: `https://preventivo-pro.pages.dev`

---

## Opzione 2: Deploy con Git (CONSIGLIATO per aggiornamenti continui)

### Passo 1: Installa Git

```powershell
winget install Git.Git
```

Chiudi e riapri PowerShell.

### Passo 2: Configura Git (una volta sola)

```powershell
git config --global user.name "Tuo Nome"
git config --global user.email "tua@email.com"
```

### Passo 3: Inizializza Repository Locale

```powershell
cd C:\progetti\preventivo-pro

# Inizializza repo
git init

# Crea .gitignore
echo "node_modules/" > .gitignore
echo ".DS_Store" >> .gitignore

# Aggiungi tutti i file
git add .

# Primo commit
git commit -m "Prima versione con foto integrate"
```

### Passo 4: Crea Repository su GitHub

1. Vai su https://github.com/new
2. Nome repository: `preventivo-pro`
3. **Lascia tutto vuoto** (no README, no .gitignore)
4. Clicca **Create repository**

### Passo 5: Collega Locale a GitHub

```powershell
# Sostituisci TUO_USERNAME con il tuo username GitHub
git remote add origin https://github.com/TUO_USERNAME/preventivo-pro.git
git branch -M main
git push -u origin main
```

**Ti chiederà username e password GitHub:**
- Username: tuo username GitHub
- Password: usa un **Personal Access Token** (vedi sotto)

#### Come Creare Personal Access Token

1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. **Generate new token**
3. Nome: `preventivo-pro-deploy`
4. Scadenza: No expiration (oppure 1 anno)
5. Scope: seleziona **`repo`** (tutto)
6. Clicca **Generate token**
7. **COPIA IL TOKEN** (non lo vedrai più!)
8. Usalo come password quando Git te la chiede

### Passo 6: Collega Cloudflare Pages a GitHub

1. Cloudflare Dashboard → **Workers & Pages** → **Create**
2. **Pages** → **Connect to Git**
3. **Autorizza GitHub** (la prima volta)
4. Seleziona repository: `preventivo-pro`
5. Configurazione build:
   - **Project name:** `preventivo-pro`
   - **Production branch:** `main`
   - **Framework preset:** None
   - **Build command:** (lascia vuoto)
   - **Build output directory:** `/`
6. Clicca **Save and Deploy**

🎉 **Fatto!** Cloudflare builderà e deployerà automaticamente.

---

## 🔄 Aggiornamenti Futuri

### Con Upload Diretto
Ogni volta che modifichi:
1. Vai su Cloudflare Pages → tuo progetto
2. **Create new deployment**
3. Trascina i file aggiornati

### Con Git (CONSIGLIATO)
Ogni volta che modifichi:

```powershell
cd C:\progetti\preventivo-pro

# Vedi cosa hai modificato
git status

# Aggiungi tutte le modifiche
git add .

# Commit con messaggio descrittivo
git commit -m "Aggiunte funzionalità XYZ"

# Push su GitHub
git push
```

Cloudflare **deploy automaticamente** ogni push! 🚀

---

## 🌐 Dominio Personalizzato (Opzionale)

### Se hai già un dominio (es. `preventivi.tuosito.it`)

1. Cloudflare Pages → tuo progetto → **Custom domains**
2. Clicca **Set up a custom domain**
3. Inserisci: `preventivi.tuosito.it`
4. Cloudflare configura DNS automaticamente
5. Aspetta 5-10 minuti per propagazione

**Certificato SSL gratuito** incluso automaticamente! 🔒

---

## ✅ Verifica Deploy Riuscito

Dopo il deploy, verifica:

1. **Apri l'URL** su desktop
2. **Apri DevTools** (F12) → Lighthouse
3. **Genera report PWA** → Deve essere 90+
4. **Apri su iPhone Safari**
5. **Condividi → Aggiungi a Home**
6. **Apri PWA** → Deve funzionare offline
7. **Scatta una foto** → Deve comprimersi e salvarsi

---

## 🐛 Problemi Comuni

### "Service Worker non si registra"
**Causa:** Cloudflare non serve i file correttamente  
**Soluzione:** Verifica che `sw.js` sia nella root

### "Icone non appaiono"
**Causa:** Path errato nel manifest  
**Soluzione:** Verifica `manifest.webmanifest` ha `./icons/icon-192.png`

### "Push su GitHub fallisce"
**Causa:** Token scaduto o permessi insufficienti  
**Soluzione:** Genera nuovo token con scope `repo`

### "Build fallisce su Cloudflare"
**Causa:** File mancanti  
**Soluzione:** Verifica che tutti i file siano committati

---

## 📊 Statistiche Cloudflare

Dopo il deploy, puoi vedere:

- **Richieste totali**
- **Bandwidth usato**
- **Paesi visitatori**
- **Performance** (Web Vitals)

Dashboard → Analytics

---

## 🔐 Sicurezza

### Cosa Cloudflare Fornisce GRATIS

- ✅ SSL/TLS certificato automatico
- ✅ DDoS protection
- ✅ CDN globale
- ✅ HTTP/3 e QUIC
- ✅ Minification automatica
- ✅ Brotli compression

### Best Practices

1. **HTTPS Only** - Sempre (Cloudflare forza automaticamente)
2. **CSP Headers** - Configurabili in `_headers` file
3. **Rate Limiting** - Disponibile nei piani a pagamento

---

## 💰 Costi

### Piano Free (Quello che usi)

- **Banda:** Illimitata ✅
- **Build:** 500/mese
- **Richieste:** Illimitate
- **Storage:** 25 MB per build
- **Collaboratori:** 1

**Perfetto per il tuo caso d'uso!** Non pagherai nulla.

### Se in Futuro Serve di Più

**Plan Pro ($20/mese):**
- 5000 builds/mese
- 100 collaboratori
- Deploy preview illimitati

---

## 🚀 Comandi Git Rapidi

```powershell
# Vedere modifiche non committate
git status

# Vedere differenze
git diff

# Aggiungere file specifico
git add index.html

# Commit + Push in un comando
git add . && git commit -m "Messaggio" && git push

# Vedere storico commit
git log --oneline

# Tornare indietro a commit precedente (ATTENZIONE!)
git reset --hard HEAD~1
```

---

## 📱 Test Pre-Deploy Checklist

Prima di fare deploy, verifica:

- [ ] Service Worker funziona in locale
- [ ] Manifest.json accessibile
- [ ] Icone esistono e sono corrette
- [ ] Foto si comprimono correttamente
- [ ] IndexedDB salva preventivi
- [ ] Archivio carica preventivi con foto
- [ ] WhatsApp funziona con numero corretto

---

## 🎯 Deploy Production-Ready

### File Aggiuntivi Consigliati

**_headers** (ottimizzazione cache):
```
/*
  Cache-Control: public, max-age=3600
  X-Content-Type-Options: nosniff
  X-Frame-Options: DENY

/sw.js
  Cache-Control: public, max-age=0, must-revalidate

/icons/*
  Cache-Control: public, max-age=31536000, immutable
```

**robots.txt** (se vuoi renderlo pubblico):
```
User-agent: *
Allow: /
Sitemap: https://preventivo-pro.pages.dev/sitemap.xml
```

---

## ✨ Extra: Auto-Deploy con GitHub Actions

Se vuoi deploy automatici ultra-rapidi:

1. Crea `.github/workflows/deploy.yml`
2. Incolla:

```yaml
name: Deploy to Cloudflare Pages

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy
        uses: cloudflare/pages-action@v1
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          projectName: preventivo-pro
          directory: .
```

3. Aggiungi secrets in GitHub → Settings → Secrets

**Ora ogni push deployerà automaticamente in < 30 secondi!**

---

**Buon deploy! 🚀**
