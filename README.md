Questo é un mio progetto realizzato con il software TiaPortal in particolare la versione 13 durante i miei studi universitari.

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Per chi non conoscesse il software TiaPortal:TIA Portal (Totally Integrated Automation Portal) è un software di ingegneria sviluppato da Siemens per la programmazione e la configurazione di dispositivi di automazione, come PLC (Programmable Logic Controllers), HMI (Human-Machine Interface) e sistemi di azionamento. TIA Portal è una piattaforma unificata che consente di integrare vari dispositivi e sistemi di automazione in un unico ambiente di sviluppo.Per il download del software e eventuale simulatore annesso consultare il sito https://www.siemens.com/it/it.html.

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Track Project:
Il codice di questo progetto simula sul PLC un sistema di produzione costituito da una macchina che lavora tre tipi di parti.
I pezzi attendono di essere lavorati in tre buffer distinti, i quali hanno una capacità massima limitata (gli arrivi vengono ignorati se il contenuto del buffer ha raggiunto il suo valore massimo).
La dinamica degli arrivi è modellata con un temporizzatore che fa arrivare un pezzo ogni tot secondi. 
Le lavorazioni dei tre tipi di pezzi vengono invece effettuate quando gli interruttori collegati agli ingressi I0.0, I0.1 e I0.2 rispettivamente per le parti di tipo 1, 2 e 3, passano da 0 a 1.
Un pannello HMI permette di visualizzare in tempo reale l'evoluzione dinamica del contenuto dei tre buffer. Modificare il progetto tenendo conto delle seguenti specifiche:
Modifiche da applicare al codice esposto pocanzi:
Il sistema presenta sempre tre buffer con tre tipi di pezzi, ma i pezzi dei primi due buffer vengono assemblati in un prodotto finale formato da due pezzi di tipo 1 e un pezzo di tipo 2. 
L'operazione di assemblaggio richiede un tempo pari a τ12.
I pezzi nel terzo buffer effettuano invece una normale lavorazione di durata pari a τ3.
Le lavorazioni non devono più essere effettuate manualmente, pigiando gli interruttori come nel progetto originario, ma implementando una politica CLB che, vuotato un buffer, sceglie quello successivo come quello con maggior numero di pezzi, e li comincia a lavorare dopo un certo tempo necessario per il setup.
I pezzi 1 e 2 vengono scelti dalla CLB (che preleva due pezzi dal buffer 1 e uno dal buffer 2) quando il minimo tra x1/2 (arrotondato all'intero inferiore) e x2 è maggiore o uguale a x3, altrimenti viene scelto il buffer 3.
Questo perché tale minimo rappresenta il numero di assemblaggi effettuabili con i pezzi 1 e 2 al momento disponibili nei due buffer.
Il colore della macchina deve variare in base al suo stato: 
a) colorata del colore del buffer che sta lavorando durante le lavorazioni (del colore quindi del buffer 3 nel caso stia lavorando questo buffer e di un colore misto nel caso stia assemblando i pezzi 1 e 2);
b) colorata di un altro colore se sta facendo un setup; 
c) nera se inattiva.
Inserire nel pannello grafico tre interruttori, uno per ogni buffer, per disattivare gli arrivi in quel buffer. Inserire anche dei campi di I/O per leggere e/o modificare il valore del contenuto dei tre buffer.
Organizzare il codice in modo che, se la macchina dopo aver vuotato un buffer deve riprendere a lavorare lo stesso buffer (per esempio perché gli arrivi degli altri buffer sono disattivati), il setup non va effettuato: il setup va fatto solo all'inizio e ogni qualvolta si cambia lavorazione.
Scegliere un sistema con i seguenti parametri: tempo di setup pari a 2 secondi; capacità dei 3 buffer pari a 20; tempi di interarrivo dei pezzi nei tre buffer pari rispettivamente a 2, 4 e 2.5 secondi (questo corrisponde a tassi di domanda rispettivamente pari a 30, 15 e 24 pezzi al minuto per le parti di tipo 1, 2 e 3); tempi di lavorazione τ12 = 2 secondi per l'assemblaggio e τ3 = 1 secondo per la lavorazione dei pezzi di tipo 3.
