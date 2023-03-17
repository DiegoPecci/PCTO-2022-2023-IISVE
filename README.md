# PCTO-2022-2023-IISVE
**Movimento di un servo motore tramite Atom Motion e utilizzo di una camera AI per visualizzare ciò che viene ripreso**

Atom lite

![Image](https://user-images.githubusercontent.com/128048776/225636286-138b0cd3-e803-494c-bebf-4b496920355f.png)

Atom Motion

![Image](https://user-images.githubusercontent.com/128048776/225636501-ec7cad2a-80f6-4945-b004-ffbf9356d7b5.png)



Il progetto permette di comandare da uno a quattro servo motori sfruttando le possibilità fornite dall'Atom motion. L'idea era quella di comandare un servo motore in modo tale che simulasse a grandi linee il movimento della coda di un pesce robot. Inoltre si è pensato potesse essere utile l'implementazione di una camera AI, precisamente X, così da poter visualizzare la ripresa sullo schermo di uno smartphone e sfruttare tutte le funzioni garantite dalla camera. Per raggiungere lo scopo l'I2C è stato ottimale, vista la possibilità che offre di garantire la comunicazione tra un master ed uno slave, rappresentati in questo progetto dall'Atom lite e l'Atom Motion.

Atom lite, Atom Motion, Servo motore

![Image](https://user-images.githubusercontent.com/128048776/225637519-88b624ab-0a54-4c88-ab93-452b4875c3ac.jpeg)



Le difficoltà incontrate inizialmente sono state quelle di riuscire a mettere in comunicazione il master e lo slave attraverso l'ambiente di sviluppo online UIFlow, che permette di programmare in blocchi e in Phyton. Una seconda difficoltà annessa alla prima è stata comprendere le funzionalità dell'Atom Motion, dal momento che su Internet ci sono davvero poche informazioni disponibili per poterlo programmare.

Per poter svolgere il progetto è necessario inizializzare e connettere il microcontrollore, per farlo sono descritte tutte le operazioni da eseguire a questo link: https://docs.m5stack.com/en/quick_start/m5core/uiflow

Successivamente bisogna andare su UIFlow (scaricando il programma desktop o accedendo dal sito online) per scrivere il codice.
Link UIFlow: https://flow.m5stack.com/ 

Un codice utile a far funzionare il servo motore è il seguente -->


![Image](https://user-images.githubusercontent.com/128048776/225633404-158b16ea-14f5-4be0-a4dc-c7a32f8ca1bb.png)


In questo programma:
1. viene inizializzata la variabile utilizzata nell'If.
2.  vengono inizializzati i pin I2C dell'Atom Motion (SDL e SCL).
3. viene impostato l'indirizzo dei registri dello slave (0x38 --> Atom Motion address)
4. comincia il loop dove, attraverso una condizione If, il motore compie diversi movimenti.
5. Se il pulsante A viene premuto la condizione dell'If viene verificata.
