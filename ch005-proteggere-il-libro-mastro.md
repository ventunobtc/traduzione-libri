
## Proteggere il libro mastro

Finora abbiamo parlato di come riuscire a mantenere copie e a scrivere su un libro mastro distribuito senza consentire fenomeni di coercizione o corruzione, utilizzando un sistema basato su una lotteria e sulla verifica mediante consenso.

Ma cosa succede quando un vincitore della lotteria vuole agire con intenzioni malevole? Un minatore può modificare le vecchie voci registrate sul libro mastro? I nostri attori malevoli Eva, Davide e Francesca possono accordarsi per riscrivere la storia o modificare i saldi dei conti attribuendosi monete extra?

È il momento della *block chain*. Termine di marketing molto in voga nel settore FinTech, la block chain non è altro che il concetto secondo cui i *blocchi* di Bitcoin sono *concatenati* tra loro per stabilire dei collegamenti tra un insieme di transazioni ed il successivo. Questo crea una storia lineare del processo di emissione e di spesa delle monete a partire dal *blocco genesi* di Satoshi nel 2009 fino ad oggi.

Nel capitolo precedente abbiamo mentito un po' per semplificare le cose. Quando si effettua il mining giocando alla lotteria della prova di lavoro, le transazioni in fila per il blocco successivo e un nonce casuale non sono gli unici elementi ad essere sottoposti all'hashing. Infatti, per collegare ogni blocco a quello che lo ha preceduto, viene aggiunto anche l'hash del blocco antecedente.

È bene ricordare che l'output di una funzione hash è imprevedibile e si basa su tutti i dati immessi. Ora sappiamo che gli hash dei blocchi includono tre diversi input:

1.  Le transazioni che vogliamo registrare nel libro mastro.
2.  Un nonce casuale.
3.  L'hash del blocco precedente che utilizziamo come base della storia del nostro libro mastro.

![hashing](images/inputs-sha256-hash_svg.jpg)

*I tre input utilizzati per costruire il numero di hash per la lotteria ora includono il precedente hash vincente, creando un collegamento fra un blocco e l'altro*.

Questo ci consente di costruire un registro cronologico di ogni blocco partendo dal primissimo blocco genesi minato da Satoshi. Ogni volta che si scrive un nuovo blocco nella catena, bisogna verificare che questo blocco non contenga transazioni che spendono bitcoin già spesi nei blocchi precedenti. 

Se anche uno solo degli input dell'hash cambia, l'hash in uscita cambia in modo imprevedibile e radicale. Se si manomettono i dati di un blocco passato, si cambia l'hash. Ma dato che quell'hash è stato utilizzato come input per i blocchi successivi, così facendo si modificheranno anche gli hash di tali blocchi. L'hash dell'ultimo blocco della catena, essendo collegato a tutti gli hash precedenti, funge da impronta digitale dell'intera storia della catena fino a quel momento!

Non è possibile falsificare la prova di lavoro, poiché tutti sanno quanta energia deve essere consumata in ogni blocco in base al Numero Obiettivo richiesto per quel blocco. Se qualcuno cercasse di modificare un vecchio blocco presente nella catena, dovrebbe ricalcolare l'hash della prova di lavoro del blocco che sta manomettendo e di ogni singolo blocco successivo. Pertanto, la block chain non è soltanto a prova di manomissione, ma è anche *estremamente costosa* da manomettere.

Ogni nuovo blocco minato aumenta la sicurezza dei blocchi che lo hanno preceduto, poiché aumenta la quantità di elettricità necessaria per ricalcolare gli hash delle prove di lavoro della catena fino a quel punto. Una transazione contenuta in un blocco che è "sepolta" sotto 6 blocchi successivi è considerata definitiva dalla maggior parte dei commercianti. Ci vorrebbe un'enorme quantità di energia per ricalcolare l'hash degli ultimi sei blocchi al tasso di hash totale odierno. E una sepolta sotto 100 blocchi? Fuori discussione!

Quando si scarica una copia della block chain, tutte le transazioni in ogni blocco sono completamente trasparenti e si possono verificare gli hash delle prove di lavoro per controllare che nulla sia stato alterato dalla persona che ti ha inviato il libro mastro.

### Quando i blocchi sono in conflitto

C'è ancora un tassello mancante nel sistema di consenso: come possiamo fare in modo che tutti seguano necessariamente la stessa cronologia lineare delle transazioni nel caso in cui i minatori abbiano estratto simultaneamente due blocchi e li abbiano inviati a tutti?

Immaginiamo di gestire una rete mondiale. Persone in tutto il mondo, dagli Stati Uniti alla Cina, sono collegate a questa rete globale e giocano tutti alla lotteria del mining di prove di lavoro.

Qualcuno a Chicago trova un blocco valido. Lo annuncia alla rete e tutti i computer in America iniziano a raccoglierlo. Nel frattempo, anche qualcuno a Shanghai trova un blocco a pochi secondi da quello di Chicago. I loro vicini non hanno ancora saputo del blocco americano, quindi ricevono prima il blocco cinese.

Entrambi i blocchi contengono una transazione di 1 bitcoin da Alice a Bob. Ma subito dopo aver ricevuto quel bitcoin, Bob lo invia a Carlo. A causa delle differenze temporali, il blocco americano riflette questa transazione e Bob ha un saldo finale pari a zero. Tuttavia, i cinesi hanno estratto il loro blocco prima di vedere la spesa di Bob verso Carlo. Il blocco cinese mostra il saldo di Bob a 1 bitcoin.

La rete è divisa su quale block chain costituisca la copia corretta del libro mastro, poiché entrambe contengono transazioni valide che sono collegate alla cronologia di tutti i blocchi che le hanno precedute. Entrambe contengono una quantità valida di prove di lavoro. Questo fenomeno è chiamato *scissione della catena*. Non potendo contare su una autorità centrale, non si può stabilire quale dei due blocchi vinca. E allora cosa si fa?

Bitcoin offre una soluzione semplice: aspettare e vedere. I minatori sono liberi di scegliere quale blocco utilizzare come base per le successive estrazioni. Gli americani effettueranno il mining per collegarsi al blocco di cui hanno sentito parlare per la prima volta, mentre i cinesi effettueranno il mining sulla base del loro blocco.

Nei successivi dieci minuti circa, verrà estratto un altro blocco. Nel codice Bitcoin esiste una regola che dice che vince chi ha speso più energia totale per tutti i blocchi della sua catena. Questa regola chiave di Bitcoin, che ci chiede di sommare il lavoro totale in una catena e di favorire la catena con la prova di lavoro cumulativa più pesante, viene talvolta chiamata Consenso di Nakamoto, in onore di Satoshi. 

Supponiamo che i cinesi estraggano il blocco successivo. La loro catena è ora un blocco avanti rispetto a quella americana e contiene più prove di lavoro totali. Quando trasmetteranno questa scoperta, i nodi americani riconosceranno che i nodi cinesi hanno prodotto una catena di Proof of Work cumulativa più pesante e si riorganizzeranno (o *reorg*, N.d.T.: abbreviato dall'inglese). Ciò significa che scarteranno il blocco che hanno estratto a favore dei due blocchi cinesi.

![Chain split](images/longest-chain_svg.jpg)

*La scissione della catena è un processo naturale che si verifica quando due minatori trovano un blocco nello stesso momento. La catena che risulta più pesante in base alla totale prova di lavoro è valida, e l'altro blocco diventa orfano.*

Il blocco americano è ora chiamato "orfano". Poiché è stato rifiutato, il minatore che l'ha estratto non ha ricevuto la sua ricompensa e nessuna delle transazioni in quel blocco è stata inserita nel libro mastro. Tuttavia, le transazioni rifiutate non sono andate perse. Alcune potrebbero essere state inserite nel blocco cinese concorrente, mentre le altre saranno scritte in un blocco futuro.

I minatori memorizzano tutte le transazioni di cui vengono a conoscenza in un luogo speciale del loro computer chiamato *mempool*. Tutte le transazioni di un blocco rifiutato vengono rimesse nella mempool. In futuro saranno estratte da qualcuno, a condizione che non siano in conflitto con la nuova cronologia del libro mastro prodotta dall'ultimo blocco.

Si tenga presente che, anche se ci siamo riferiti ad essi come americani e cinesi, in realtà i nodi non sanno nulla dell'identità o della posizione geografica degli altri partecipanti. L'unica prova di validità di cui hanno bisogno è che qualcuno abbia la catena di prove di lavoro più pesante e che le transazioni nella catena siano tutte valide (senza doppi pagamenti, ecc.).

Questo genere di rotture della catena sono normali e si verificano di tanto in tanto in Bitcoin. Di solito vengono risolte nel blocco successivo. I miglioramenti nella tecnologia di propagazione dei blocchi e nella connettività di rete tra i minatori rendono questo problema meno grave. Oggi, e probabilmente per il prossimo futuro, Bitcoin ha un limite fisso alla quantità di dati ammessi in un blocco. Il motivo per cui Bitcoin produce blocchi relativamente piccoli, a distanza di circa dieci minuti l'uno dall'altro, è proprio quello di garantire che gli orfani siano estremamente rari.

Il mining è probabilistico. A volte i blocchi sono distanti dieci minuti l'uno dall'altro, altre volte solo pochi secondi. Se producessimo blocchi ogni secondo o se avessimo blocchi molto grandi, avremmo un'alta probabilità che i blocchi americani e cinesi entrino in conflitto perché sono geograficamente molto distanti e impiegano più tempo per raggiungersi. Se gli orfani si verificassero troppo spesso, la block chain si sgretolerebbe. Ci sarebbero orfani su orfani e i nodi non avrebbero il tempo di accordarsi sull'ultimo blocco prima che venga estratto quello successivo.

È importante mantenere i blocchi piccoli per aumentare la possibilità che l'intera rete possa ricevere l'ultimo blocco prima di estrarre il successivo. L'altra ragione, forse più importante, è quella di mantenere relativamente bassi i requisiti hardware per il funzionamento di un nodo, in modo da incoraggiare nel tempo un maggior numero di nodi ed un'attività di mining decentralizzata. Blocchi di grandi dimensioni incoraggerebbero i minatori a dislocarsi in data center e in alcune regioni geografiche per prevenire i blocchi orfani, che hanno un impatto negativo sulla loro redditività.

### L'unica vera catena

Torniamo all'esempio del Capitolo 3, in cui Enrico si unisce per la prima volta alla rete Bitcoin.

Il nodo di Enrico si connetterà ad altri nodi della rete e chiederà loro informazioni sui nodi che conoscono, per poi connettersi anch'esso ad alcuni di questi nodi. Questa operazione si chiama "scoperta dei nodi".

Alcuni di questi nodi saranno assolutamente malevoli e gli forniranno una copia falsa del libro mastro, con firme errate per le transazioni, o bitcoin falsificati e coniati in modo improprio e senza hash validi della prova di lavoro. Tali copie saranno rifiutate immediatamente ed i nodi in questione saranno istantaneamente banditi dal connettersi ulteriormente al nodo di Enrico[^1].

Gli altri nodi a cui si connette saranno onesti, ma avranno versioni contrastanti della verità. Ad esempio, alcuni di essi potrebbero essere stati messi offline e risultare indietro di un blocco o due. Se scarica più copie della block chain, tutte ugualmente valide, il software del suo nodo utilizzerà il Consenso di Nakamoto. Misurando la prova di lavoro cumulativa totale, la catena più pesante sarà ritenuta l'unica vera catena.

I nodi comunicano costantemente tra loro per assicurarsi di avere i blocchi più recenti. Poiché tutti i nodi seguono la regola della catena più pesante, si trova un consenso su quale sia il vero stato del libro mastro. Enrico non deve affidarsi al voto di maggioranza, che sarebbe facile da raggirare rendendo la maggioranza dei nodi malvagia.

Anche se Enrico si connette a decine di nodi non aggiornati o maligni e ad un solo nodo corretto, il suo software Bitcoin riconoscerà l'unica copia corretta perché è quella che contiene la maggior quantità di prove di lavoro e consisterà in transazioni valide risalenti al blocco genesi. L'importanza di questo aspetto non può essere sottovalutata. Enrico non deve fidarsi di nessuno; il suo nodo eseguirà tutte le convalide per garantire che la block chain che sta guardando sia l'unica vera catena.

È quindi estremamente difficile per gli hacker malintenzionati fornire ad un nodo una copia falsa della block chain. Per farlo, occorrerebbe interrompere la connessione di quel nodo con tutti gli altri nodi onesti e collegarlo solo ai nodi controllati dagli attaccanti.

### Reversibilità delle transazioni

Due catene concorrenti sono di solito prodotte per puro caso e vengono rapidamente risolte. Tuttavia, chi vuole attaccare la rete può sfruttare il Consenso di Nakamoto controllando più del 50% del tasso di hash totale. Può quindi produrre la catena di prove di lavoro cumulativa più pesante contenente transazioni di sua scelta, purché sia disposto a consumare abbastanza energia per farlo. Quando trasmette questa catena, gli altri nodi la accettano come l'unica vera catena. Questo è chiamato *attacco del 51%* perché richiede il controllo di più della metà del tasso di hash.

È importante capire che in Bitcoin non esiste una vera e propria finalità della transazione, poiché gli attacchi al 51% o persino l'orfanizzazione casuale dei blocchi, sono sempre teoricamente possibili. Per questo motivo, i destinatari delle transazioni attendono in genere che vengano estratti diversi blocchi sopra una transazione prima di poterla considerare definitiva. A quel punto, la quantità di energia necessaria per invertire la transazione diventa così costosa che è improbabile che ciò accada.

I blocchi estratti sopra un blocco contenente una transazione di interesse per l'utente sono spesso chiamati *conferme*. Pertanto, quando si sente dire che una transazione Bitcoin ha sei conferme, significa che sono stati estratti sei blocchi sopra di essa. Se stai vendendo un libro digitale che ha un costo marginale per te come commerciante, potresti volere solo una conferma, o addirittura zero conferme, consegnando all'acquirente il link per il download non appena vedi la transazione trasmessa sulla rete. Se invece stai vendendo una casa, forse vorrai aspettare dodici conferme, ovvero circa due ore di mining. Più è lunga l'attesa, più prove di lavoro si accumulano sul blocco che contiene la transazione e più diventa costoso, nel mondo reale, invertire la transazione. Oggi la maggior parte delle persone accetta 6 conferme come prova definitiva di pagamento.

Se il tasso di hash di Bitcoin dovesse diminuire in modo significativo, implicando che viene impiegata meno energia per garantire ogni blocco, si potrebbe sempre aumentare il numero di conferme necessarie per il regolamento conclusivo. Anche se la non-finalità delle transazioni può sembrare sconcertante all'inizio, è importante tenere presente che le transazioni con carta di credito possono essere stornate anche 120 giorni dopo essere state effettuate.

D'altra parte, le transazioni Bitcoin sono quasi irreversibili solo dopo pochi blocchi. Da questo punto di vista, la reversibilità e la definitività delle transazioni Bitcoin rappresentano un notevole miglioramento rispetto alla maggior parte delle reti di pagamento tradizionali, almeno dal punto di vista del commerciante.

Le stime odierne mostrano che se avessi a disposizione l'energia dell'intera rete Bitcoin - una quantità davvero elevata, poiché dovresti avere accesso ad una quantità di energia pari a quella di una nazione e a tutti i componenti hardware specializzati di Bitcoin disponibili - ti ci vorrebbe comunque più di un anno per riscrivere l'intera storia della catena. È possibile esplorare questi dati su [<http://bitcoin.sipa.be>].

***
[^1]: Questo eccellente saggio approfondisce il modo in cui Bitcoin gestisce i blocchi non validi: <https://hackernoon.com/bitcoin-miners-beware-invalid-blocks-need-not-apply-51c293ee278b>

