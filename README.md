# Colophon

**Colophon** è una web app (PWA) gratuita per modificare i **metadati**, la **copertina**, lo **stile** e l'**indice** dei file EPUB, direttamente dal browser. Pensata come alternativa leggera alle funzioni di modifica di Calibre, utilizzabile da Chromebook, Android e PC.

**I tuoi libri non vengono mai caricati su nessun server**: i file sono letti, modificati e salvati sul tuo dispositivo.

- App online: `https://NOME-PROGETTO.pages.dev` *(sostituisci con il tuo indirizzo Cloudflare)*
- Copia di riserva: https://kevin-flynn89.github.io/epub-editor/

## Screenshot

<table>
  <tr>
    <td align="center"><img src="docs/screenshots/00-lingua.png" width="200" alt="Scelta della lingua"><br><sub>Scelta della lingua</sub></td>
    <td align="center"><img src="docs/screenshots/02-metadati.png" width="200" alt="Metadati e copertina"><br><sub>Metadati e copertina</sub></td>
    <td align="center"><img src="docs/screenshots/03-stile-anteprima.png" width="200" alt="Stile e anteprima"><br><sub>Stile e anteprima</sub></td>
    <td align="center"><img src="docs/screenshots/04-cerca-elimina.png" width="200" alt="Cerca ed elimina"><br><sub>Cerca, sostituisci ed elimina</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="docs/screenshots/05-ortografia.png" width="200" alt="Controllo ortografico"><br><sub>Controllo ortografico</sub></td>
    <td align="center"><img src="docs/screenshots/06-indice.png" width="200" alt="Indice del libro"><br><sub>Indice del libro</sub></td>
    <td align="center"><img src="docs/screenshots/07-controllo.png" width="200" alt="Controllo del libro"><br><sub>Controllo del libro</sub></td>
    <td></td>
  </tr>
</table>

*Gli screenshot usano un libro di prova creato per l'occasione.*

## Cosa puoi fare

**Metadati e copertina**
- Modifica titolo, autori, serie e numero, editore, lingua, data, tag e descrizione
- Sostituisci la copertina (JPG o PNG)
- **Cerca online** titolo, autore e copertina (Google Books, con Open Library come alternativa)
- Rinomina il file con un modello, per esempio `{serie} {numero} - {titolo}` (disponibili `{autore}`, `{titolo}`, `{serie}`, `{numero}`, `{anno}`)

**Stile e impaginazione** *(con anteprima del primo capitolo che si aggiorna mentre cambi le opzioni)*
- Margini laterali, interlinea, spazio tra paragrafi, rientro della prima riga, dimensione del testo
- Allineamento (a sinistra o giustificato), sillabazione, carattere (Serif o Sans serif)
- Capolettera dopo i titoli, titoli centrati o a sinistra

**Pulizia del testo**
- Virgolette caporali «…» o inglesi “…”, apostrofi tipografici
- Tre puntini che diventano …, spazi doppi, spazio prima della punteggiatura
- Dialoghi con il trattino lungo (—)
- **Cerca, sostituisci ed elimina** in tutto il libro (anche con espressioni regolari), con conteggio delle occorrenze

**Struttura del libro**
- **Controllo ortografico:** trova le parole non presenti nel dizionario, italiano o inglese (per esempio errori di scansione come "vImperatore"), mostra la frase in cui compaiono, propone una correzione e lascia scegliere a te quali applicare a tutto il libro. Funziona offline e può ignorare i nomi propri
- **Pulizia dello stile del libro:** togli colori, caratteri e dimensioni imposti dall'editore, oppure tutti gli stili
- **Indice:** rinomina, sposta, cambia livello o elimina le voci; rigenera l'indice dai capitoli
- **Controllo del libro:** segnala file mancanti o non dichiarati, collegamenti e immagini rotti, codice non valido, dati mancanti
- **Statistiche:** capitoli, parole e tempo di lettura stimato

**Comodità**
- **Italiano e inglese:** al primo avvio l'app propone la lingua rilevata dal dispositivo (italiano o inglese, altrimenti inglese) e chiede di confermarla; si può cambiare in qualsiasi momento con i pulsanti IT / EN in alto
- **Preset di stile:** salva le tue impostazioni e riapplicale ad altri libri
- Funziona anche offline dopo la prima apertura (tranne la ricerca online)

## Installarla come app

1. Apri l'indirizzo dell'app con **Chrome**.
2. Dal menu ⋮ scegli **Installa app** (o "Aggiungi a schermata Home").
3. Troverai l'icona tra le tue app, come una normale applicazione.

## Come si usa

1. Tocca **Scegli un file EPUB** e seleziona il libro (anche da Google Drive, tramite il selettore file del dispositivo).
2. Modifica i campi e le opzioni che ti servono. Le sezioni vuote non cambiano nulla.
3. Premi **Salva EPUB**: scarichi un nuovo file, l'originale non viene toccato.

> Consiglio: provala sempre su una copia del libro prima di sovrascrivere l'originale.

## Struttura del progetto

Non serve nessuna compilazione: è una semplice pagina statica.

| File | A cosa serve |
|---|---|
| `index.html` | L'app completa (HTML, CSS e JavaScript in un unico file) |
| `manifest.webmanifest` | Nome e icone per l'installazione come app |
| `sw.js` | Service worker: uso offline e cache |
| `icon-192.png`, `icon-512.png` | Icone dell'app |
| `hunspell.bundle.js` | Motore del correttore ortografico (Hunspell compilato in WebAssembly) |
| `dict/` | Dizionari italiano e inglese (`it.*`, `en.*`) con le relative licenze |
| `README.md`, `docs/` | Questa documentazione e gli screenshot (non servono per pubblicare l'app) |

Librerie: [JSZip](https://stuk.github.io/jszip/), caricata da CDN, per leggere e scrivere i file EPUB (che sono archivi ZIP); [hunspell-asm](https://github.com/kwonoj/hunspell-asm) (licenza MIT) e i dizionari [dictionary-it](https://github.com/wooorm/dictionaries) (italiano, licenza GPL-3.0) e dictionary-en (inglese, licenza MIT e BSD), con i testi delle licenze in `dict/`, inclusi nel progetto.

## Pubblicazione e aggiornamenti

**Cloudflare Pages (versione principale)**
1. Dalla dashboard di Cloudflare: **Workers & Pages → Create application → Pages → Drag and drop your files**.
2. Carica **tutti i file dell'app** (`index.html`, `manifest.webmanifest`, `sw.js`, le due icone, `hunspell.bundle.js` e la cartella `dict/` completa), come cartella o come file zip. Non caricare `README.md` e `docs/`.
3. Per aggiornare: nel progetto, scheda **Deployments**, crea una nuova distribuzione e carica i file nuovi.

**GitHub (copia di sicurezza)**
Tieni i file nel repository come archivio. Con GitHub Pages attivo (Settings → Pages → `main` / root) la stessa app è raggiungibile anche dall'indirizzo `github.io`.

**Importante a ogni modifica:** cambia il numero di versione della cache in `sw.js`, per esempio da `colophon-v1` a `colophon-v2`. Senza questo cambio i telefoni continuano a mostrare la versione vecchia.

## Limiti noti

- La ricerca e la sostituzione agiscono dentro un singolo blocco di testo: una frase interrotta da un grassetto o da un corsivo non viene trovata.
- Alcune app di lettura (per esempio Kindle o Apple Books) ignorano margini e carattere se l'utente ha impostato i propri.
- La ricerca online richiede connessione e dipende da servizi esterni, che possono rifiutare temporaneamente le richieste. A volte la copertina non si riesce a scaricare: in quel caso puoi scegliere tu l'immagine.
- Il controllo del libro segnala i problemi ma non li corregge.
- Il controllo ortografico usa un dizionario, non un'intelligenza artificiale: i suggerimenti sono quelli del dizionario. Non conosce i nomi propri e i termini inventati (vanno ignorati) e per impostazione predefinita salta le parole con l'iniziale maiuscola, quindi un errore a inizio frase può sfuggire. Non verifica la grammatica.
- Le traduzioni sono due (italiano e inglese). Per aggiungere una lingua basta un nuovo elenco di traduzioni in `index.html` (oggetto `EN`) e, per il correttore, un dizionario Hunspell in `dict/`.
- Testata su Chrome (Chromebook): su altri browser alcune funzioni potrebbero comportarsi diversamente.

---

## English summary

**Colophon** is a free, offline-capable PWA to edit EPUB **metadata, cover, style and table of contents** in the browser, with online metadata lookup, text cleanup, find/replace and a **spell checker** (Italian and English dictionaries, you choose which corrections to apply). The interface is available in **Italian and English**: on first launch it proposes the language of your device and you can switch at any time with the IT / EN buttons. Your books never leave your device.

To publish: upload all the app files (including `hunspell.bundle.js` and the whole `dict/` folder) to any static hosting such as Cloudflare Pages or GitHub Pages. Bump the cache name in `sw.js` after every change so installed copies update.
