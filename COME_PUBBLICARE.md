# Come pubblicare archiconsulting.it

Guida operativa, ~30 minuti totali. Tutto già pronto: copy, foto, immagini AI, font, prezzi, CF, P.IVA, mail. Devi solo caricare e collegare il dominio.

---

## TL;DR — i 6 step

1. Crea account GitHub + carichi questa cartella (10 min)
2. Crea account Vercel + colleghi GitHub (3 min)
3. Sul pannello Vercel aggiungi `archiconsulting.it` (3 min)
4. Su Aruba modifichi 2 record DNS (10 min)
5. Aspetti 1-2 ore che il DNS si propaghi
6. HTTPS si attiva da solo, sito online

**Costo: zero.** Hosting gratis, dominio già tuo.

---

## STEP 1 — GitHub (10 min)

GitHub è il "magazzino online" del codice. Vercel lo legge per pubblicare il sito.

### a) Account GitHub
1. Vai su https://github.com/signup
2. Registrati (email + password). Username consigliato: `giacomobonci`.
3. Conferma l'email.

### b) Nuovo repository
1. In alto a destra clicca il "+" → **"New repository"**
2. Nome: `archiconsulting`
3. Lascia **Public**
4. **NON** spuntare nulla sotto
5. Clicca **"Create repository"**

### c) Carica i file
Nella pagina del repo vuoto vedi un link *"uploading an existing file"*. Cliccalo.

**Trascina solo questi file** (NON la cartella `_dev/` che contiene file di sviluppo da non pubblicare):

```
archiconsulting/
  ├── index.html
  ├── COME_PUBBLICARE.md   (opzionale, se non vuoi pubblicarla salta)
  ├── .gitignore
  ├── fonts/
  │   ├── Futura-Bold.ttf
  │   └── Futura-Medium.ttf
  └── images/
      ├── giacomo-portrait.jpg
      ├── giacomo-casual.jpg
      ├── hero-architecture.png
      ├── workspace-architect.png
      ├── blueprint-pattern.png
      ├── feedback-9000.jpg
      ├── feedback-5800.jpg
      ├── feedback-leadig.jpg
      ├── feedback-affiancamento.jpg
      ├── feedback-fattibilita.jpg
      └── feedback-storia.jpg
```

> **IMPORTANTE — privacy**: NON caricare la cartella `_dev/feedback-originali/`. Contiene gli screenshot WhatsApp con i nomi visibili. Se finiscono online sono raggiungibili da chiunque e violi il GDPR.

In fondo alla pagina, scrivi un breve messaggio (es. "primo upload") e clicca **"Commit changes"**.

---

## STEP 2 — Vercel (3 min)

1. Vai su https://vercel.com/signup
2. Clicca **"Continue with GitHub"** → autorizza Vercel
3. Una volta dentro, clicca **"Add New..." → "Project"**
4. Trovi `archiconsulting` nell'elenco → clicca **"Import"**
5. Vercel rileva che è un sito statico. **Non toccare nulla**, clicca **"Deploy"**
6. Aspetta 30-60 secondi. Sito online a un URL temporaneo tipo `https://archiconsulting-xyz.vercel.app`
7. Apri quell'URL e verifica:
   - L'hero si vede con la villa al tramonto?
   - Le foto di Giacomo caricano?
   - Gli screenshot WhatsApp sono visibili nella sezione "Trasformazioni reali"?
   - Il bottone "Scrivici" apre il client mail?

✅ Se tutto ok, sito è già online. Manca solo il dominio personalizzato.

---

## STEP 3 — Dominio su Vercel (3 min)

1. Dalla dashboard del progetto Vercel → **"Settings"** in alto
2. Menu laterale → **"Domains"**
3. Nel campo "Add" scrivi: `archiconsulting.it` → clicca **"Add"**
4. Vercel ti mostra una schermata con i record DNS da impostare. Lasciala aperta in una scheda.

I valori che ti servono (li vedi nel pannello, indicativamente):
- **Record A** per `archiconsulting.it` → IP `76.76.21.21`
- **Record CNAME** per `www` → `cname.vercel-dns.com`

> Prendi i valori esatti dalla schermata Vercel, non da questa guida.

---

## STEP 4 — DNS su Aruba (10 min)

1. https://admin.aruba.it → login
2. **"I miei prodotti e servizi"** → **"Domini"** → clicca su `archiconsulting.it`
3. Cerca **"Gestione DNS"** o **"Pannello DNS Avanzato"**
4. Clicca **"Modifica DNS"**

### Cancella se ci sono:
- Record A esistenti per `@`
- Record CNAME per `www`

### Aggiungi:

| Tipo  | Host (Nome) | Valore                          | TTL  |
|-------|-------------|----------------------------------|------|
| A     | @           | 76.76.21.21  *(verifica con Vercel)*  | Auto |
| CNAME | www         | cname.vercel-dns.com  *(verifica)*    | Auto |

**Salva.** Aruba potrebbe chiedere conferma via SMS/email.

> Se Aruba non accetta `@` come host, prova a lasciarlo vuoto, oppure scrivi `archiconsulting.it`.

---

## STEP 5 — Configura la mail info@archiconsulting.it

**Critico**: il sito invia tutti i contatti a `info@archiconsulting.it`. Se la casella non esiste o non viene letta, perdi i lead.

Su Aruba (stesso pannello del dominio):
1. Vai in **"Caselle email"** o **"Email del dominio"**
2. Hai due strade:
   - **Crea casella vera** `info@archiconsulting.it` con password (consigliato a regime)
   - **Imposta forwarder/alias**: `info@archiconsulting.it` → inoltra a `email@giacomobonci.com` (più rapido per partire)

Per la prima fase, l'**alias** è sufficiente: ricevi le mail nella tua casella personale, rispondi da lì.

> **Da mentore**: imposta anche un autoresponder per le prime 2-3 settimane: *"Ciao, ti rispondo entro 24h. Nel frattempo ecco 3 storie del nostro Instagram che ti spiegano come lavoriamo: [link]."*

---

## STEP 6 — HTTPS (automatico)

Il DNS impiega 10 minuti - 24 ore per propagarsi (di solito 1-2 ore con Aruba).

Verifica propagazione: https://dnschecker.org → digita `archiconsulting.it`. Quando vedi il record A che risponde con l'IP Vercel ovunque, sei pronto.

Vercel attiva HTTPS **da solo** non appena rileva il DNS. Vedrai sul pannello Domains:
- ✓ `archiconsulting.it` con stato **"Valid Configuration"**
- 🔒 lucchetto verde HTTPS

Vercel fa anche da solo:
- Redirect www → senza www
- Redirect http → https

---

## TEST FINALI (10 min)

Apri questi URL in finestra in incognito:

- ✅ https://archiconsulting.it → sito carica
- ✅ https://www.archiconsulting.it → redirect su archiconsulting.it
- ✅ http://archiconsulting.it → redirect su https
- ✅ Mobile: apri sul cellulare. Sticky CTA in basso visibile?

Click test:
- Bottone hero "Scrivici per la call gratuita" → scrolla al CTA finale
- Bottone CTA finale "Scrivici a info@archiconsulting.it" → apre client mail con oggetto preimpostato
- Link Instagram nel footer → porta a @giacomo_bonci_archiconsulting

---

## MODIFICARE IL SITO IN FUTURO

Per cambiare prezzo, copy, foto, ecc:

1. Vai su github.com/{tuo-username}/archiconsulting
2. Clicca il file da modificare (es. `index.html`) → icona matita ✏️
3. Modifica → "Commit changes"
4. Vercel rideploya **da solo** in 30 secondi

Niente più drag & drop manuali.

---

## CHE COSA C'È NELLA CARTELLA

```
archiconsulting/
├── index.html              ← il sito (single page)
├── COME_PUBBLICARE.md      ← questa guida
├── .gitignore              ← evita di caricare file dev su Git
├── fonts/                  ← Futura Bold + Medium
├── images/                 ← tutte le immagini del sito
└── _dev/                   ← FILE DI SVILUPPO. NON pubblicare.
    ├── generate_images.py      (script che ha generato immagini AI)
    ├── redact_feedback.py      (script che ha oscurato i nomi)
    ├── screenshot.py           (script che ha fatto le anteprime)
    ├── screenshots/            (anteprime desktop+mobile)
    └── feedback-originali/     (screenshot WhatsApp originali, NON pubblicare)
```

---

## SE QUALCOSA VA STORTO

| Problema | Causa | Fix |
|---|---|---|
| Sito non carica le foto | File non caricati su GitHub | Verifica che `images/` e `fonts/` siano nel repo |
| `archiconsulting.it` non risponde dopo 24h | DNS sbagliati su Aruba | Confronta i valori su dnschecker.org con quelli Vercel |
| Vercel: "Invalid Configuration" | DNS non ancora propagato | Aspetta 24h e riprova |
| Bottone "Scrivici" non apre la mail | Browser strano / link mailto bloccato | Lo dice già il sito sotto: "copia info@archiconsulting.it" |
| Mail `info@` non arrivano | Casella non creata su Aruba | Step 5 sopra |

In caso di blocco scrivimi e mandami screenshot.

---

## CHECKLIST FINALE

- [ ] Account GitHub creato
- [ ] File caricati su GitHub (escluso `_dev/` e `feedback-originali/`)
- [ ] Account Vercel creato e connesso a GitHub
- [ ] Sito deployato, URL temporaneo Vercel funziona
- [ ] Dominio `archiconsulting.it` aggiunto su Vercel
- [ ] Record A e CNAME aggiornati su Aruba
- [ ] Casella `info@archiconsulting.it` configurata (vera o alias)
- [ ] DNS propagato (verifica su dnschecker.org)
- [ ] HTTPS attivo, lucchetto verde
- [ ] Test su mobile passato
- [ ] Bottone "Scrivici" testato → apre il client mail correttamente
- [ ] Test mail: ti sei mandato una mail di prova a info@archiconsulting.it?
