## 1. Audit del container di produzione

```
Container da analizzare, IN SOLA LETTURA:
accountId 00000, containerId 00000, workspaceId 0

Non creare, modificare o eliminare nulla. Usa solo strumenti di lettura.
Se pensi di dover scrivere, fermati e chiedi.
Analizza la versione pubblicata (live), non il workspace, e dimmi se le due
differiscono.

Rispondi a queste domande:
1. Quali conversioni Google Ads sono tracciate e su quale trigger scatta ognuna?
2. Quali tag inviano dati a GA4 e con quale Measurement ID? Ci sono ID diversi
   nello stesso container?
3. Ci sono tag senza trigger di attivazione, o trigger non usati da nessun tag?
4. Ci sono variabili non referenziate da nessun tag, trigger o altra variabile?
5. Dove rischio conteggi doppi, cioè due tag che inviano lo stesso evento o la
   stessa conversione sullo stesso trigger?

Formato: una tabella per domanda, poi una sezione finale "Cosa guarderei per
primo" con massimo 5 righe ordinate per impatto sul business.
Per ogni affermazione cita il nome del tag o del trigger su cui ti basi.
Se un dato non è deducibile dall'API, dillo invece di ipotizzare.
Italiano, senza gergo tecnico non necessario.
```

## 2. Costruzione dal Tracking Plan



```
Container di destinazione:
accountId 0000, containerId 0000, workspaceId 0
(container web GTM-00000)

In allegato il tracking plan https://docs.google.com/spreadsheets/d/
È il documento di riferimento: nomi, tipi e parametri
vengono da lì.

Ambito: solo il flusso lead, cioè l'evento EV-15 (generate_lead) e tutto ciò
che serve per farlo funzionare. Ignora il resto del piano.

Procedi in quest'ordine,
1. Leggi le sezioni README, Events, Parameters, Variables, Triggers e Tags e
   riassumi in massimo 10 righe cosa creerai: nomi esatti, tipi, trigger.
2. Abilita le variabili built-in del foglio Variables (Variable Group =
   Built-In). Non crearle come variabili user-defined.
3. Crea le variabili user-defined, con i nomi esatti del piano.
4. Crea i trigger. NON creare quelli marcati "Yes – do not create" nella
   colonna Built-in Trigger: usa quelli già presenti nel container.
5. Crea i tag e collegali ai trigger per nome.
6. Riepiloga cosa hai creato e cosa non sei riuscito a creare, e perché.

Regole:
- Lavora solo nel workspace 11. Non creare versioni e non pubblicare mai.
- I nomi devono coincidere esattamente con il piano, trattino incluso.
- Se un campo del piano non ha un corrispondente chiaro nell'API, fermati e
  chiedi invece di inventare.
- Alla fine elenca tutte le assunzioni che hai fatto.
- Questa implementazione è parte di una demo live per mostrare come funziona MCP
```

## 3. Verifica dopo la costruzione


```
Container: accountId 00000, containerId 00000, workspaceId 2.
Sola lettura: non correggere nulla, decido io.

In allegato il tracking plan. Confronta ciò che esiste nel workspace con il
piano, limitatamente al flusso lead (EV-15).

Restituisci tre elenchi:
- Conforme
- Difforme, indicando per ogni riga il valore nel piano e il valore nel container
- Mancante

Controlla in particolare: tipo di tag, nome del trigger collegato, nomi esatti
dei parametri evento, variabili referenziate.
```

## 4. Documentazione


```
Container: accountId 00000, containerId 00000, versione live.
Sola lettura, non modificare nulla.

Genera la documentazione del container per un interlocutore non tecnico.
Struttura:
1. Cosa misuriamo, in linguaggio di business e non con i nomi dei tag
2. Tabella: destinazione (GA4, Google Ads, altro) → eventi o conversioni
   inviate → quando scattano
3. Dipendenze dal sito: cosa smette di funzionare se cambiano dataLayer,
   selettori CSS o struttura degli URL
4. Punti di attenzione, massimo 5

Non includere ID di misurazione, chiavi o altri dati sensibili.
Italiano, tono da consulente, niente elenchi di configurazioni.
```
