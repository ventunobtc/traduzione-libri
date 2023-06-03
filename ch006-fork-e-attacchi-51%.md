
## Fork e Attacchi del 51%

In principio, Satoshi ha estratto i primi bitcoin utilizzando l'unità di elaborazione centrale (CPU) del proprio computer. Poiché la difficoltà iniziale del sistema di mining era bassa, per il suo computer era relativamente economico generare queste monete. 

Nel corso del tempo, le persone hanno iniziato a modificare il software per il mining in modo da renderlo sempre più efficiente. Ad un certo punto è stato scritto un software ottimizzato per sfruttare le schede grafiche specializzate (GPU), solitamente usate per i videogiochi. 

Con le GPU, il mining è diventato un ordine di grandezza più efficiente rispetto al mining su CPU. La difficoltà si è rapidamente adattata a tutto il nuovo tasso di hash che si è riversato nel sistema grazie alle GPU. A questo punto, chiunque svolgesse attività di mining tramite CPU era diventato poco produttivo ed ha dovuto spegnere il proprio miner.

Dopo l'avvento del mining su GPU, l'efficienza del mining è stata ulteriormente migliorata grazie alla produzione dei cosiddetti circuiti integrati specifici per le applicazioni, o *ASIC* (N.d.T.: dall'inglese Application Specific Integrated Circuits). Si tratta di microchip che svolgono una sola funzione: la funzione sha256 di Bitcoin e nient'altro. Essendo specializzati in questo particolare algoritmo, gli ASIC sono di un ordine di grandezza più efficienti rispetto alle GPU e, per tale ragione, la difficoltà si è ancora una volta adattata al rialzo, rendendo rapidamente le GPU non redditizie, proprio come le GPU avevano fatto in precedenza con le CPU. Ogni pochi anni, una nuova generazione di dispositivi ASIC mette fuori gioco le versioni precedenti grazie a grandi miglioramenti dell'efficienza.

I primi minatori della rete spendevano solo pochi centesimi di elettricità per produrre i loro bitcoin. Con l'aumento del prezzo di bitcoin e l'adesione di un numero sempre maggiore di minatori, la difficoltà è aumentata e la generazione di bitcoin è diventata sempre più costosa. Oggi il prezzo è vicino agli 8000 dollari per bitcoin (N.d.T.: 27000 dollari nel momento in cui sto traducendo) e si consumano migliaia di dollari di elettricità per ogni bitcoin emesso.

### Mining Pool

Un problema del mining di bitcoin è che non è deterministico come il lancio di un dado. Ciò significa che si potrebbe finire per spendere un sacco di soldi in elettricità senza mai trovare un blocco valido.

Nel 2010 è emersa un'innovazione chiamata *mining pool*, volta a risolvere il problema dei minatori che consumano elettricità senza ricevere ricompense. Una mining pool è un gruppo di rischio condiviso, che si ispira al funzionamento delle assicurazioni.

Tutti i minatori contribuiscono all'estrazione per il pool, prendendo così le sembianze di un unico grande minatore. Se qualcuno del pool trova un blocco valido, la ricompensa per il blocco viene suddivisa proporzionalmente tra tutti i minatori in base al tasso di hash che hanno fornito. In questo modo, anche le piccole attività di mining, come i singoli individui, possono ricevere una ricompensa per la piccola quantità di hash rate che hanno erogato. Per fornire questo servizio di coordinamento, il pool si prende una parte della ricompensa.

Le mining pool hanno causato un certo effetto di centralizzazione: gli utenti si sono riversati nei pool più grandi. Tuttavia è importante ricordare che gli utenti fanno mining per i pool e che i pool non possiedono il tasso di hash che rappresentano. Gli utenti possono cambiare mining pool e tendono a farlo, di tanto in tanto.

In effetti, ci sono precedenti storici di singoli minatori che abbandonano un pool diventato troppo potente. Nel 2014, Ghash.io aveva quasi la metà della potenza di mining totale. I minatori hanno visto che il mining stava diventando troppo centralizzato e hanno volontariamente optato per altri pool. 

Nonostante le mining pool relativamente centralizzate siano una realtà odierna, vengono apportati costanti miglioramenti alla tecnologia di mining, tra cui una proposta chiamata [BetterHash] (https://github.com/TheBlueMatt/bips/blob/betterhash/bip-XXXX.mediawiki), che consente ai singoli minatori di avere un maggiore controllo su ciò che estraggono e di ridurre la dipendenza dal coordinamento dei pool.

### Attacchi del 51%

La centralizzazione delle mining pool fa temere che alcune delle pool più importanti possano accordarsi per attaccare il 51% della rete. Oggi, i primi 5 pool identificabili detengono insieme più del 50% del tasso di hash mining totale. Esaminiamo come si svolge un attacco di questo tipo e quali pericoli comporta. 

Quando si possiede poco più del 50% dell'hash rate, si può controllare la scrittura nel libro mastro perché si può produrre una catena più pesante delle altre nel tempo. Ricordati che il Consenso di Nakamoto dice che i nodi devono accettare la catena di prove di lavoro cumulativa più pesante di cui vengono a conoscenza.

Ecco un esempio di come potresti eseguire un attacco del 51% molto semplice:

1.  Supponiamo che la rete nel suo complesso stia estraendo bitcoin a 1000 hash/secondo.
2.  Compri un mucchio di hardware per il mining e di elettricità per produrre 2000 hash/secondo. Ora possiedi il 66% del tasso di hash totale (2000 su 3000 hash al secondo).
3.  Inizi a minare una catena che contiene solo blocchi vuoti.
4.  Tra due settimane, inizi a diffondere la tua catena di blocchi vuoti. Poiché stai estraendo a una velocità circa doppia rispetto ai minatori onesti, la tua catena sarà due volte più pesante per prova di lavoro cumulativa. La trasmissione a tutti i nodi esistenti li porterà a riorganizzarsi e a perdere le ultime due settimane di storia.

Oltre all'estrazione di blocchi vuoti, cosa che rende la catena inutilizzabile, puoi eseguire un attacco a doppia spesa:

1.  Invii alcuni bitcoin ad un exchange.
2.  Li scambi in euro e prelevi.
3.  In un secondo momento, diffondi una catena minata segretamente che non contiene l'invio all'exchange.
4.  Hai riscritto la storia e ora possiedi sia i bitcoin originali che gli euro.

Il consumo energetico del tasso di hash di Bitcoin oggi è all'incirca equivalente a quello di un paese di discrete dimensioni. Acquisire hardware ed elettricità sufficienti per eseguire un attacco di questo tipo è estremamente costoso. Secondo le stime, oggi un attacco del 51% costerebbe all'incirca 700.000 dollari all'ora e il costo è in continuo aumento (N.d.T.: più di 1.100.000 dollari all'ora nel momento in cui sto traducendo). Questa stima non tiene conto della reazione a questo attacco da parte dei minatori onesti, che probabilmente lo renderebbe ancora più costoso. È possibile esaminare qual è il costo per attaccare Bitcoin e le criptovalute su [https://www.crypto51.app].

È inoltre molto difficile riuscire a portare a termine un attacco di queste proporzioni con una doppia spesa senza lasciare dietro di sé impronte che possano essere utilizzate per capire chi sei. Dopo tutto, per eseguire l'attacco si consuma l'energia di un Paese di medie dimensioni e si acquistano milioni di dollari in hardware, oltre ad effettuare con gli exchange transazioni per milioni di dollari.

Ma supponiamo che qualche entità malintenzionata con finanziamenti illimitati, come ad esempio un governo, decida di farlo e sia in grado di sostenere questo attacco superando queste difficoltà. In teoria, la rete potrebbe adattarsi passando a una funzione di prova di lavoro diversa (non sha256). Questo renderebbe inutilizzabile tutto l'hardware per il mining di Bitcoin utilizzato dall'attaccante, in quanto specializzato solo per l'hashing sha256. Tuttavia, cambiare la prova di lavoro è un'opzione da ultima spiaggia che metterebbe immediatamente fuori gioco anche tutti i minatori onesti. Ciononostante, la rete sopravvivrebbe e rinascerebbe dalle sue ceneri.

Oltre alla non fattibilità dell'attacco, avere la maggioranza dell'hash rate non dà diritto alle due cose più importanti:

1.  Non si possono creare monete dal nulla che violino il programma di emissione. Questo viola la regola del consenso sulla ricompensa dei blocchi e i tuoi blocchi verrebbero rifiutati, anche se avessero abbastanza prove di lavoro.
2.  Non potresti spendere monete che non sono tue. Non saresti in grado di fornire una firma digitale valida, il che viola le regole.

I nodi che accettano Bitcoin come pagamento manterrebbero la rete onesta anche di fronte a una maggioranza disonesta di minatori, semplicemente facendo rispettare le regole di Bitcoin. Pertanto, un attacco del 51% è più una seccatura che un problema di sicurezza. Molto probabilmente, lo scenario peggiore è quello di un attore statale con fondi ingenti che cerca di rendere inutilizzabile Bitcoin. Tuttavia, un attacco di questo tipo non può essere sostenuto per sempre. Quando Bitcoin si riprenderà da un eventuale attacco del genere, dimostrerà ulteriormente la sua resistenza e diventerà un problema ancora più grande per coloro che lo vogliono attaccare.

Sebbene ad oggi Bitcoin non abbia mai subito un attacco del 51% efficace, questo tipo di attacco è stato effettuato su reti caratterizzate da un tasso di hash molto basso. In questi casi, gli exchange sono stati vittime di attacchi a doppia spesa e hanno perso denaro su monete a basso tasso di hash che probabilmente non avrebbero dovuto mai quotare in primo luogo.
