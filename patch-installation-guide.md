# Installazione della patch per i TTML locali

Questa patch permette a **Spicy Lyrics** di interpretare localmente i file TTML caricati per i brani locali di Spotify.

La patch supporta:

* TTML sincronizzati riga per riga;
* TTML sincronizzati parola per parola;
* righe di sottofondo compatibili;
* formati temporali come `00:01:23.456` e `1:23.456`.

> La patch non modifica Spotify direttamente: sostituisce il file di avvio dell’estensione Spicy Lyrics con una versione che include il parser TTML locale.

---

## Requisiti

Prima di continuare, assicurati di avere installato:

* Spotify Desktop;
* Spicetify;
* Spicy Lyrics.

Chiudi completamente Spotify prima di modificare i file.

---

## 1. Scarica la patch

Scarica il file:

```text
spicy-lyrics_local_ttml_patched.mjs
```

dalla cartella `patch` di questa repository.

Rinominalo in:

```text
spicy-lyrics.mjs
```

---

## 2. Apri la cartella Extensions di Spicetify

Su Windows, premi `Win + R` e inserisci:

```text
%appdata%\spicetify\Extensions
```

Premi Invio.

All’interno della cartella dovrebbe essere presente il file:

```text
spicy-lyrics.mjs
```

Se la cartella o il file non sono presenti, controlla che Spicy Lyrics sia stato installato correttamente.

---

## 3. Crea un backup

Prima di sostituire il file originale, rinominalo in:

```text
spicy-lyrics.original.mjs
```

In questo modo potrai ripristinare facilmente la versione normale di Spicy Lyrics, oppure puoi reinstallarlo normalmente.

---

## 4. Installa la patch

Copia il file patch rinominato `spicy-lyrics.mjs` dentro:

```text
%appdata%\spicetify\Extensions
```

Quando richiesto, conferma la sostituzione del file esistente.

Alla fine la cartella dovrebbe contenere almeno:

```text
spicy-lyrics.mjs
spicy-lyrics.original.mjs
```

---

## 5. Applica Spicetify

Apri PowerShell e avvia:

```powershell
spicetify apply
```

Al termine del comando, apri Spotify.

Se Spotify era ancora aperto durante l’installazione, chiudilo completamente e riaprilo.

---

## 6. Verifica l’installazione

Apri Spicy Lyrics e riproduci un brano locale al quale è stato associato un file TTML.

Se la patch è stata caricata correttamente, Spicy Lyrics dovrebbe mostrare il testo senza restituire errori durante l’elaborazione del TTML.

Per una verifica più tecnica:

1. apri gli strumenti per sviluppatori di Spotify;
2. apri la scheda `Console`;
3. cerca il seguente messaggio:

```text
[Spicy Local TTML Patch] installed
```

Quando viene elaborato un TTML dovrebbe inoltre apparire:

```text
[Spicy Local TTML Patch] handled parseTTML locally
```

---

## Aggiornamenti di Spicy Lyrics

Un aggiornamento di Spicy Lyrics può sovrascrivere automaticamente il file modificato e rimuovere la patch.

Se i TTML smettono improvvisamente di funzionare:

1. controlla se Spicy Lyrics è stato aggiornato;
2. verifica se `spicy-lyrics.mjs` è ancora il file patchato;
3. scarica nuovamente la patch dalla repository;
4. sostituisci il file;
5. esegui nuovamente:

```powershell
spicetify apply
```

La patch carica una versione remota di Spicy Lyrics. Modifiche future alla struttura dell’estensione potrebbero quindi causare incompatibilità.

---

## Disinstallazione

Chiudi completamente Spotify.

Apri:

```text
%appdata%\spicetify\Extensions
```

Elimina il file patchato:

```text
spicy-lyrics.mjs
```

Rinomina quindi:

```text
spicy-lyrics.original.mjs
```

in:

```text
spicy-lyrics.mjs
```

Infine apri PowerShell ed esegui:

```powershell
spicetify apply
```

Spicy Lyrics tornerà a utilizzare il file originale.

---

## Reinstallazione completa

Se non hai conservato il backup:

1. elimina `spicy-lyrics.mjs` dalla cartella Extensions;
2. rimuovi Spicy Lyrics da Spicetify Marketplace;
3. installa nuovamente Spicy Lyrics;
4. esegui:

```powershell
spicetify apply
```



---

## Risoluzione dei problemi

### La cartella Extensions non esiste

Apri PowerShell ed esegui:

```powershell
spicetify path
```

Controlla il percorso mostrato da Spicetify e cerca al suo interno la cartella `Extensions`.

Puoi anche crearla manualmente se necessario.

---

### Spicy Lyrics non appare più

Controlla che il file si chiami esattamente:

```text
spicy-lyrics.mjs
```

e non, per esempio:

```text
spicy-lyrics.mjs.txt
```

Su Windows può essere necessario attivare la visualizzazione delle estensioni dei file da Esplora file.

Esegui poi:

```powershell
spicetify config extensions spicy-lyrics.mjs
spicetify apply
```

---

### Spotify si apre, ma il TTML non viene caricato

Controlla che:

* il file TTML sia valido;
* il TTML sia associato al brano corretto;
* la patch non sia stata sostituita da un aggiornamento;
* il brano riprodotto sia realmente un file locale;
* Spicy Lyrics funzioni normalmente con altri brani.

Controlla inoltre la console per eventuali errori contenenti:

```text
[Spicy Local TTML Patch]
```

---

### Il testo appare, ma è fuori tempo

La patch non modifica automaticamente la sincronizzazione.

Il file audio utilizzato deve corrispondere alla stessa versione sulla quale è stato creato il TTML. Differenze nella durata, silenzi iniziali, intro o versioni alternative possono causare uno sfasamento.

---

### Le parole sono unite o gli spazi non sono corretti

Questo può dipendere dalla struttura interna del TTML.

Controlla che ogni parola o gruppo di parole sia racchiuso correttamente negli elementi `<span>` e che il testo contenga gli spazi necessari.

---

## Compatibilità

La patch è stata progettata per la versione di Spicy Lyrics basata sul file:

```text
spicy-lyrics.mjs
```

Non è garantita la compatibilità con:

* versioni future di Spicy Lyrics;
* installazioni modificate dell’estensione;
* sistemi operativi diversi da Windows;
* formati TTML non standard;
* file TTML con strutture non supportate.

In caso di problemi, apri una Issue indicando:

* versione di Spotify;
* versione di Spicetify;
* versione di Spicy Lyrics;
* file TTML utilizzato;
* messaggi presenti nella console.
