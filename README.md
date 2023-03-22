# PCTO-2022-2023-IISVE
**Movimento di un servo motore tramite Atom Motion e utilizzo di una camera AI per visualizzare ciò che viene ripreso**

Atom lite

![image](https://user-images.githubusercontent.com/128048776/226885422-69b86aee-fa04-4359-909b-d32c75cee99b.png)

Atom Motion

![image](https://user-images.githubusercontent.com/128048776/226885926-e2ddae4a-1584-4de5-901e-fd91ecf2cbef.png)

Il progetto permette di comandare da uno a quattro servo motori sfruttando le possibilità fornite dall'Atom motion. L'idea era quella di comandare un servo motore in modo tale che simulasse a grandi linee il movimento della coda di un pesce robot. Inoltre si è pensato potesse essere utile l'implementazione di una camera AI, precisamente la UnitV2, così da poter visualizzare la ripresa sullo schermo di uno smartphone e sfruttare tutte le funzioni garantite dalla camera. Per raggiungere lo scopo l'I2C è stato ottimale, vista la possibilità che offre di garantire la comunicazione tra un master ed uno slave, rappresentati in questo progetto dall'Atom lite e l'Atom Motion.

Atom lite, Atom Motion, Servo motore

![image](https://user-images.githubusercontent.com/128048776/226886227-22032518-a3a0-4714-901c-e53cc99081ae.png)



Le difficoltà incontrate inizialmente sono state quelle di riuscire a mettere in comunicazione il master e lo slave attraverso l'ambiente di sviluppo online UIFlow, che permette di programmare in blocchi e in Phyton. Una seconda difficoltà annessa alla prima è stata comprendere le funzionalità dell'Atom Motion, dal momento che su Internet ci sono davvero poche informazioni disponibili per poterlo programmare.

Per poter svolgere il progetto è necessario inizializzare e connettere il microcontrollore, per farlo sono descritte tutte le operazioni da eseguire a questo link: https://docs.m5stack.com/en/quick_start/m5core/uiflow

Successivamente bisogna andare su UIFlow (scaricando il programma desktop o accedendo dal sito online) per scrivere il codice.
Link UIFlow: https://flow.m5stack.com/ 

Un codice utile a far funzionare il servo motore è il seguente -->


![image](https://user-images.githubusercontent.com/128048776/226888429-a98a95a6-a1b8-4487-bf91-7f1177193e67.png)


In questo programma:
1. viene inizializzata la variabile utilizzata nell'If.
2.  vengono inizializzati i pin I2C dell'Atom Motion (SDL e SCL).
3. viene impostato l'indirizzo dei registri dello slave (0x38 --> Atom Motion address)
4. comincia il loop dove, attraverso una condizione If, il motore compie diversi movimenti.
5. Se il pulsante A viene premuto la condizione dell'If viene verificata.


La seconda parte del progetto era quella di aggiungere quindi la camera UnitV2. Questa camera AI permette di visualizzare ciò che riprende su un sito apposito, raggiungibile al seguente indirizzo IP: 10.254.239.1. 

UnitV2:
![image](https://user-images.githubusercontent.com/128048776/226589561-de440cc1-217a-4f5c-89dd-277c8aeb8138.png)

Schermata del sito:

![image](https://user-images.githubusercontent.com/128048776/226888625-a369f9e3-b07e-47a2-83ce-70216738f63d.png)

Per utilizzare la camera è necessario accedere alla sua pagina delle documentazioni sul sito di M5Stack, e seguire i passaggi indicati sulla pagina al seguente link: https://docs.m5stack.com/en/unit/unitv2?id=uiflow. 

Approciando la seconda parte del progetto è emerso un problema che ha fatto sì che il progetto prendesse un'altra strada rispetto a quella che si credeva. Inizialmente si credeva di poter visualizzare facilmente la ripresa della camera attraverso la funzione "Remote+" di UIflow. Questa funzione permette di visualizzare sullo schermo del dispositivo da cui si sta programmando un'interfaccia interattiva simile a quella di un possibile schermo di un cellulare. Permette inoltre di posizionare su questa interfaccia dei pulsanti, delle barre di incremento, dei joystick, delle immagini e poco altro. Dopo aver scelto quel che si vuole utilizzare basta cliccare su un tasto per generare un codice QR. Il codice generato potrà essere scansionato con qualsiasi dispositivo ne sia in grado, e aprirà sullo stesso una pagina dalla quale sarà possibile visualizzare ciò che vi è stato inserito dall'ambiente di programmazione.

![image](https://user-images.githubusercontent.com/128048776/226888840-ef72ab1d-54b4-4d4a-a3d4-a5c0b0ca5377.png)

Tuttavia la funzione non permette di inserire anche l'elemento video, e questo ha ostecolato il lavoro. La soluzione proposta è stata quella di dover creare un blocco custom su UIflow per poter inserire anche l'elemento video nell'interfaccia interattiva. La creazione di blocchi su UIflow è possibile effettuarla tramite l'uso del Python, quindi sono servite conoscenze a riguardo. Cercando altre info a riguardo si è rivelato non possibile creare un blocco custom di questo tipo e altre idee sono state quella di creare una funzione loop che all'interno contenesse sempre il frame aggiornato della ripresa della cam ogni 3 sec (tempo minimo accettato da UIflow). i problemi di questa idea sono stati che l'url dell'immagine generato dall'app della UnitV2 cambiava con il cambiare del frame stesso, questo comportava la necessità di un continuo reinserimento manuale di un nuovo url nell'interfaccia di remote+. Nel caso in cui non ci fosse stato questo problema il video sarebbe risultato comunque ad una velocità di 0.3 fps. 

