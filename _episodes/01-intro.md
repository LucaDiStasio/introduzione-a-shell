---
title: "Presentazione della conchiglia"
Durata: 5
Esercizi: 0
Domande:
- "Cos'è una shell dei comandi e perché dovrei usarne una?"
Obiettivi formativi:
- "Spiega come la shell si relaziona con la tastiera, lo schermo, il sistema operativo e i programmi degli utenti."
- "Spiega quando e perché le interfacce della riga di comando dovrebbero essere utilizzate al posto delle interfacce grafiche."
punti chiave:
- "Una shell è un programma il cui scopo principale è leggere comandi ed eseguire altri programmi."
- "Questa lezione usa Bash, la shell predefinita in molte implementazioni di Unix."
- "I programmi possono essere eseguiti in Bash immettendo i comandi al prompt della riga di comando."
- "I principali vantaggi della shell sono il suo elevato rapporto azione-battitura, il suo supporto per
automatizzando le attività ripetitive e la sua capacità di accedere alle macchine in rete."
- "I principali svantaggi della shell sono la sua natura principalmente testuale e come
i suoi comandi e il suo funzionamento possono essere criptici."
---
### Perchè imparare la Shell Unix?

Gli esseri umani e i computer interagiscono comunemente in molti modi diversi, ad esempio attraverso una tastiera e un mouse,
interfacce touch screen o utilizzando sistemi di riconoscimento vocale.
Il modo più utilizzato per interagire con i personal computer è chiamato a
**interfaccia utente grafica** (GUI).
Con una GUI, diamo istruzioni facendo clic con il mouse e utilizzando interazioni guidate da menu.

Mentre l'aiuto visivo di una GUI rende intuitivo l'apprendimento,
questo modo di fornire istruzioni a un computer è molto poco bilanciato.
Immagina il seguente compito:
per una ricerca bibliografica, devi copiare la terza riga di mille file di testo in mille
directory diverse e incollarlo in un unico file.
Usando una GUI, non solo faresti clic sulla tua scrivania per diverse ore,
ma potresti anche commettere un errore nel processo di completamento di questa attività ripetitiva.
È qui che sfruttiamo la shell Unix.
La shell Unix è sia una **interfaccia a riga di comando** (CLI) che un linguaggio di scripting,
consentendo di eseguire tali attività ripetitive in modo automatico e veloce.
Con i comandi appropriati, la shell può ripetere le attività con o senza alcune modifiche
tutte le volte che vogliamo.
Utilizzando la shell, l'attività nell'esempio della letteratura può essere eseguita in pochi secondi.


### La Shell


La shell è un programma in cui gli utenti possono digitare comandi.
Con la shell è possibile invocare programmi complicati come i software di modellazione climatica
o semplici comandi che creano una directory vuota con una sola riga di codice.
La shell Unix più popolare è Bash (la Bourne Again SHell ---
così chiamato perché derivato da una shell scritta da Stephen Bourne).
Bash è la shell predefinita sulla maggior parte delle moderne implementazioni di Unix e nella maggior parte dei pacchetti che forniscono
Strumenti simili a Unix per Windows.

L'uso della shell richiederà uno sforzo e del tempo per imparare.
Mentre una GUI ti presenta le scelte da selezionare, le scelte CLI non ti vengono presentate automaticamente,
quindi devi imparare alcuni comandi come un nuovo vocabolario in una lingua che stai studiando.
Tuttavia, a differenza di una lingua parlata, un piccolo numero di "parole" (cioè comandi) ti porta lontano,
e oggi tratteremo quei pochi essenziali.

La grammatica di una shell consente di combinare strumenti esistenti in potenti
pipeline e gestire automaticamente grandi volumi di dati. Sequenze di
i comandi possono essere scritti in uno *script*, migliorando la riproducibilità di
flussi di lavoro.

Inoltre, la riga di comando è spesso il modo più semplice per interagire con macchine remote
e supercomputer.
La familiarità con la shell è quasi essenziale per eseguire una varietà di strumenti e risorse specializzati
compresi i sistemi di calcolo ad alte prestazioni.
Man mano che i cluster e i sistemi di cloud computing diventano più popolari per il crunching di dati scientifici,
saper interagire con la shell sta diventando un'abilità necessaria.
Possiamo basarci sulle abilità della riga di comando trattate qui
per affrontare una vasta gamma di questioni scientifiche e sfide computazionali.

Iniziamo.

Quando la shell viene aperta per la prima volta, ti viene presentato un **prompt**,
indicando che la shell è in attesa di input.

~~~
$
~~~
{: .language-bash}

La shell usa tipicamente `$ ` come prompt, ma può usare un simbolo diverso.
Negli esempi di questa lezione, mostreremo il prompt come `$ `.
Più importante:
quando si digitano comandi, da queste lezioni o da altre fonti,
*non digitare il prompt*, solo i comandi che lo seguono.
Nota anche che dopo aver digitato un comando, devi premere il tasto <kbd>Invio</kbd> per eseguirlo.

Il prompt è seguito da un **cursore di testo**, un carattere che indica la posizione in cui il tuo
apparirà la digitazione.
Il cursore è solitamente un blocco lampeggiante o pieno, ma può anche essere un trattino basso o una barra verticale.
Potresti averlo visto in un programma di editor di testo, ad esempio.

Quindi proviamo il nostro primo comando, `ls` che è l'abbreviazione di elenco.
Questo comando elencherà il contenuto della directory corrente:

~~~
$ l
~~~
{: .language-bash}

~~~
Desktop Scarica Film Immagini
Documenti Biblioteca Musica Pubblico
~~~
{: .output}

> ## Comando non trovato
> Se la shell non riesce a trovare un programma il cui nome è il comando che hai digitato, esso
> stamperà un messaggio di errore come:
>
> ~~~
> $ ks
> ~~~
> {: .language-bash}
> ~~~
> ks: comando non trovato
> ~~~
> {: .output}
>
> Ciò potrebbe accadere se il comando è stato digitato in modo errato o se il programma corrispondente a quel comando
> non è installato.
{: .callout}

## Pipeline di Nelle: un problema tipico

Nelle Nemo, biologo marino,
è appena tornato da un'indagine semestrale del
[Gyre del Pacifico settentrionale](http://en.wikipedia.org/wiki/North_Pacific_Gyre),
dove ha campionato la vita marina gelatinosa nel
[Great Pacific Garbage Patch](http://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
Ha 1520 campioni che ha fatto passare attraverso una macchina di analisi per misurare l'abbondanza relativa
di 300 proteine.
Ha bisogno di eseguire questi 1520 file attraverso un programma immaginario chiamato `goostats.sh` che ha ereditato.
Oltre a questo enorme compito, deve scrivere i risultati entro la fine del mese, quindi il suo articolo
può apparire in un numero speciale di *Aquatic Goo Letters*.

La cattiva notizia è che se deve eseguire manualmente `goostats.sh` usando una GUI,
dovrà selezionare e aprire un file 1520 volte.
Se `goostats.sh` impiega 30 secondi per eseguire ciascun file, l'intero processo richiederà più di 12 ore
dell'attenzione di Nelle.
Con la shell, Nelle può invece assegnare al suo computer questo compito banale mentre si concentra
la sua attenzione nello scrivere il suo giornale.

Le prossime lezioni esploreranno i modi in cui Nelle può raggiungere questo obiettivo.
Più specificamente,
spiegano come può usare una shell dei comandi per eseguire il programma `goostats.sh`,
utilizzando i loop per automatizzare i passaggi ripetitivi di immissione dei nomi dei file,
in modo che il suo computer possa funzionare mentre scrive la sua carta.

Come bonus,
una volta che ha messo insieme una pipeline di elaborazione,
potrà riutilizzarlo ogni volta che raccoglierà più dati.

Per portare a termine il suo compito, Nelle deve sapere come:
- navigare in un file/directory
- creare un file/directory
- controlla la lunghezza di un file
- concatenare i comandi insieme
- recuperare una serie di file
- scorrere i file
- eseguire uno script di shell contenente la sua pipeline

{% include links.md %}
