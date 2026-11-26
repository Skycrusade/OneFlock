Ecco una guida d'utilizzo approfondita per **** (`index.html`), pensata come un vero manuale operativo (`README.md`) da tenere nella repository o consultare quotidianamente.

---

# OneFlock — Manuale Completo d'Utilizzo

**OneFlock** è una web application (con supporto PWA e stampa/PDF) progettata per gestire in modo strutturato la quotidianità, la dieta, le scorte, il sonno, la salute, l'addestramento e la sicurezza dei pappagalli, con sincronizzazione tra dispositivi tramite **Family Sync**.

---

## 1. Architettura dei dati e avvio dell'applicazione

### Stato iniziale ("Vergine") e gestione multi-profilo

* Quando apri l'app senza profili attivi (o dopo aver eliminato tutti i profili esistenti), la schermata **Home** mostra al centro un pannello di benvenuto con i passaggi per creare il primo pappagallo e il pulsante **Aggiungi un pappagallo**.


* Ogni pappagallo ha un proprio profilo indipendente con storico pesi, sessioni di volo, attività 1-Tap personalizzate, diario alimentare, log del sonno, terapie farmacologiche, test infettivologici, referti PDF, diario feci, galleria fotografica comparativa, preferenze oggetti, giocattoli, esercizi di training e configurazione della gabbia.


* Puoi aggiungere più pappagalli e passare dall'uno all'altro tramite la barra di selezione nell'intestazione.



### Dove vengono salvati i dati

* **Dati dell'app (`localStorage`):** i profili, i log e le impostazioni vengono salvati in locale sotto la chiave `oneFlockState`.


* **File PDF (`IndexedDB`):** i PDF del **CITES** e i **referti veterinari** vengono archiviati nel database locale del browser (`OneFlockPdfStore`) per non appesantire il `localStorage` né il traffico di sincronizzazione. Ciò significa che i file PDF restano legati al dispositivo/browser in cui sono stati caricati e non vengono inclusi nel backup `.json`.


* **Immagini (avatar, galleria comparativa, giocattoli):** vengono compresse tramite `<canvas>` prima del salvataggio per ridurre l'occupazione di memoria.



---

## 2. Intestazione e strumenti globali

* **Logo e stato Sync:** a sinistra compare **OneFlock** insieme al badge di sincronizzazione (`Sync` / `Sync Attivo` / `Offline` / `Attiva Sync`), cliccabile per aprire rapidamente la sezione **Family Sync**.


* **Centro Sveglie e Notifiche (`🔔`):** il badge numerico indica quante sveglie/promemoria sono attivi. Toccandolo si apre il modale per gestire notifiche push, testare i suoni, creare nuovi promemoria giornalieri, collegarli all'orologio/calendario e gestire allarmi a schermo intero (con possibilità di **Spegnere** o **Posporre di 5 minuti**).


* **QR Code Gabbia (`QR`):** genera un QR Code legato all'ID del pappagallo attivo, visualizzabile e stampabile su tag da applicare alla gabbia; scansionandolo si apre l'app puntando direttamente a quel profilo.


* **Mini Scheda Profilo:** toccando la foto o l'iniziale di un pappagallo nella barra superiore si apre una scheda sintetica con specie, peso recente, anello/ID, veterinario, recapiti/social, finestra sonno di 12 ore, oggetti graditi/temuti, stato del PDF CITES, accesso rapido al PDF e pulsante **Modifica**.



---

## 3. Guida dettagliata alle 6 schede

### Tab 1: Home

1. **Banner di Stato Salute e Terapie:**
* Valuta automaticamente le variazioni di peso rispetto alla media recente (fino a 7 rilevamenti precedenti) e l'ultimo check feci: segnala cali moderati (`<= -5%`) o situazioni critiche (`<= -10%` o anomalie feci/urati segnalate).


* Mostra un avviso dedicato quando ci sono terapie farmacologiche attive con dosi non ancora segnate nella giornata.




2. **Peso Giornaliero:**
* Inserisci il peso in grammi (supporta decimali, es. `92.5`) e premi **Salva**. Se registri più volte nello stesso giorno, aggiorna il valore di quella data e riordina cronologicamente la serie.


* Visualizza l'ultimo peso, la media degli ultimi 7 log e un grafico a linee degli ultimi 14 rilevamenti (con colore adattato allo stato di salute).




3. **Tempo Fuori Gabbia (Volo):**
* **Avvia Timer / Ferma e Salva:** cronometra le uscite in tempo reale (anche se cambi tab o riapri la pagina, grazie al salvataggio dello stato del timer) e somma i minuti trascorsi al giorno attivo.


* **Registrazione manuale:** permette di aggiungere minuti manuali (es. `45`).


* **Pulsante `(i)`:** spiega che non c'è un limite massimo purché siano garantiti sicurezza ambientale e 10–12 ore di sonno, indicando i minimi giornalieri consigliati per specie piccole, medie e grandi.


* **Sottomenu Impostazioni (icona ingranaggio):** espande i campi per impostare il **Minimo giornaliero (min)** e l'orario di **Reset timer giornaliero** (utile se la giornata di volo segue un orario diverso dalla mezzanotte).


* **Storico e Statistiche:** espandibile, con filtri **Giorno**, **Settimana** e **Mese**, medie giornaliere, totali, giorni a target e possibilità di eliminare singole registrazioni giornaliere.




4. **Routine e Igiene (1-Tap):**
* Organizza le attività in sezioni (es. *Cibo e Acqua*, *Igiene e Gabbia*, *Benessere e Ambiente*) e cambia colore in base ai giorni passati dall'ultima esecuzione rispetto alla scadenza (`warnDays`) impostata per quel pappagallo.


* Toccare una card segna l'attività come svolta **adesso**.


* Con **Personalizza** puoi aggiungere nuove attività 1-Tap (scegliendo nome, sezione, scadenza in giorni e icona) oppure modificare/eliminare quelle esistenti per il pappagallo selezionato.




5. **Scheda Profilo e Anagrafica:**
* Card collassabile con riepilogo anagrafico, recapiti, veterinario e pulsanti **Modifica info** ed **Elimina** (se elimini l'ultimo profilo, l'app torna allo stato iniziale senza profili).





---

### Tab 2: Dieta

1. **Registra Pasto e Consumo:**
* Mostra i badge/box con la media giornaliera di pellet (`Estrusi`) e la media totale mangiata (`g/giorno`) calcolate sui giorni registrati.


* Scegli il **Tipo di Alimento**, indica **Grammi dati (g)** e **Grammi mangiati (g)** (i grammi mangiati non possono superare quelli offerti) e aggiungi eventuali note.


* **Collegamento alla Dispensa:** quando **Scala automaticamente i grammi dalla dispensa** è attivo, compare il menu per scegliere esattamente quale prodotto in dispensa scalare (utile se hai più confezioni o due tipi di pellet).




2. **Dispensa e Scadenze:**
* Permette di aggiungere prodotti specificando nome, categoria, quantità totale iniziale in grammi e data di scadenza.


* Calcola la percentuale residua rispetto ai grammi iniziali: evidenzia in **Giallo** sotto il **30%** (o entro 14 giorni dalla scadenza) e in **Rosso** sotto il **10%** (o se scaduto), mostrando un avviso riepilogativo anche in Home quando necessario.




3. **Scorta "Chop" in Freezer:**
* Gestisce il numero di porzioni congelate (`+` / `-`), calcola i grammi complessivi in base al peso della singola porzione e mostra un avviso quando le porzioni scendono sotto la soglia impostata.




4. **Conversione Dieta:**
* Cursore da `0%` a `100%` (a passi di 5) per tracciare la percentuale di dieta sana rispetto ai semi, accompagnato dalla regola pratica di non ridurre la quota di semi in caso di calo di peso oltre il 5% rispetto alla media.




5. **Storico Pasti:**
* Elenca i pasti registrati con grammi dati, avanzo, grammi mangiati, prodotto di dispensa associato e note.


* **Cancellazione con riaccredito:** eliminando una voce dallo storico pasti, i grammi scalati vengono riaggiunti automaticamente al prodotto collegato in Dispensa.




6. **Allerta Pericoli Letali in Cucina e Cibi:**
* Riquadro sempre visibile con i principali pericoli domestici e alimentari da evitare (es. fumi di PTFE/Teflon, avocado, cioccolato, caffè/alcol, cipolla/aglio, semi/noccioli, xilitolo, sale, funghi, rabarbaro, arachidi con guscio).





---

### Tab 3: Salute

1. **Esporta Scheda Clinica (Vet+):**
* Apre un modale per impostare **Dal giorno** e **Al giorno** (con pulsanti rapidi per 7, 30, 90 o 365 giorni) e genera la scheda di stampa/PDF con paziente, test infettivologici, preferenze oggetti, terapie e medicinali rilevanti nel periodo, pesate, log del sonno, diario feci e alimentazione.




2. **Orario Sonno:**
* Permette di impostare l'orario abituale di inizio sonno (mostrando la finestra indicativa di 12 ore).


* **Registra Sonno Effettivo del Giorno:** consente di salvare per una data specifica l'ora di inizio sonno, l'ora di sveglia, l'eventuale risveglio durante il periodo di riposo con i **minuti trascorsi sveglio** e le note. Calcola automaticamente i minuti/ore di sonno netto.


* **Storico e Statistiche Ore Sonno:** sezione espandibile filtrabile per date (**Dal giorno / Al giorno** o scorciatoie rapide) con media sonno netto, conteggio notti con risvegli, media minuti di veglia notturna e lista eliminabile delle singole notti.




3. **Piano Terapeutico e Calcolo Dosi:**
* Calcola automaticamente i `ml` da somministrare usando l'ultimo peso registrato del pappagallo, la dose (`mg/kg`) e la concentrazione (`mg/ml`), indicando anche le unità su siringa da 1 ml.


* Permette di impostare frequenza (1 o 2 volte al giorno), durata in giorni e sveglia/notifica collegata (con scelta del suono).


* Consente di spuntare le dosi del giorno (Mattina / Sera), attivare o disattivare le sveglie e **eliminare** singole terapie (rimuovendo anche l'eventuale sveglia associata).




4. **Test Infettivologici, Check-up e PDF Esami:**
* Toccando i riquadri dei test (PBFD, Polyomavirus, Clamidia, Bornavirus, Sessaggio DNA, Esame Coprologico) si cicla tra gli stati disponibili.


* Permette di impostare la data dell'ultimo check-up annuale (con conto alla rovescia o avviso di scadenza) e di caricare/visualizzare/eliminare referti in **PDF**.




5. **Check Feci e Diario Feci:**
* Il form registra stato feci, colore urati e note.


* Subito sotto, il pannello espandibile **Diario Feci** mostra il contatore delle voci e l'elenco cronologico con pulsante **Elimina** per ciascuna registrazione.




6. **Galleria Comparativa:**
* Permette di caricare foto etichettate per zona/data e nota, confrontare due scatti affiancati (**Prima / Dopo**), aprirli a schermo intero o eliminarli.




7. **Verifica Sicurezza Gabbia e Posatoi:**
* Valuta taglia specie, distanza tra le sbarre (mm), dimensioni (larghezza, profondità, altezza) e presenza di posatoi in legno naturale, segnalando eventuali criticità.





---

### Tab 4: Training

1. **Training e Trick:** gestisce esercizi e premi collegati, facendo avanzare il livello (`Da iniziare` -> `In corso` -> `Acquisito`) o aggiungendone di nuovi.


2. **Oggetti: Cosa Piace / Cosa Spaventa:** archivia oggetti graditi o che spaventano il pappagallo, rendendoli visibili anche nella Mini Scheda, nella Scheda Clinica e nella guida Pet Sitter.


3. **Giocattoli:** registra i giochi presenti nella gabbia con nome, gradimento (`Piace moltissimo`, `Gradito`, `Non interessa` — modificabile con un tocco), link d'acquisto, foto opzionale e note.



---

### Tab 5: Guida/SOS

* **Volantino SOS:** genera una scheda stampabile per lo smarrimento con foto, nome, specie, anello/microchip, suoni a cui risponde, indicazioni per chi lo avvista e contatti del proprietario.


* **Pet Sitter Mode:** apre un modale in cui puoi spuntare quali **giocattoli** lasciare per l'affidamento e aggiungere note generali. La stampa risultante include regole di sicurezza, note generali e, per ogni pappagallo, orario sonno (12h), alimentazione abituale (media in grammi per ciascun alimento/prodotto senza doppioni), terapie mediche in corso con relative dosi e frequenze/orari, premi di rientro, oggetti graditi/temuti, giochi selezionati con note e veterinario.


* **Checklist Primo Soccorso, Emergenze e Pericoli in Casa:** spunta gli elementi del kit di primo soccorso (con contatore `X/6`), consulta il promemoria sulle emergenze (che invita sempre a rivolgersi tempestivamente a un veterinario aviario) e rivedi i principali pericoli domestici.



---

### Tab 6: Family Sync

* **Sincronizzazione tra dispositivi:** consente di creare un nuovo codice famiglia (con apertura del **QR Invito** e condivisione link) oppure di collegarsi inserendo un codice esistente, con aggiornamento periodico e pulsante per forzare il pull o scollegare il dispositivo. *(Nota: perché la sincronizzazione cloud funzioni, devono essere configurati URL e chiave del backend e predisposta la relativa tabella sul database).*


* **Backup File Locale (JSON):** permette di scaricare una copia di sicurezza in formato `.json` o di ripristinare i dati da un file `.json` precedente.



---

## 4. Suggerimenti pratici d'uso

* **Esportare in PDF:** le funzioni di stampa (**Scheda Clinica Vet+**, **Volantino SOS**, **Pet Sitter Mode**, **Stampa Tag QR**) preparano una vista dedicata per la stampa o il salvataggio come **PDF** tramite la finestra di stampa del sistema operativo/browser.


* **Backup periodici:** se usi l'app solo in locale o carichi molti dati, scarica regolarmente un file **JSON** dalla scheda **Family Sync** come copia di sicurezza aggiuntiva.
