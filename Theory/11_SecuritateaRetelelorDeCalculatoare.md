# Securitatea retelelor de calculatoare

- Tipuri de atac:
  - Ping Sweep (statile din retea)
  - Sniffing (ascultarea traficului)
  - Port Scan (ce porturi sunt deschise)
  - Dos / DDoS (inunda serverul cu request-uri)
  - Atacarea unei parole (dictionar / brute-force)
  - Buffer Overflow (daca avem acces la binarele aplicatiei - oferim o dimensiune mai mare pentru o variabila si avem acces la alta parte din memorie)

## Scop

- Recoltarea de informatii despre o retea
  - IP-uri
  - Servicii care ruleaza
  - Locatia serviciilor folosite

### Ping-Sweep

- Ce adrese IP dintr-un range sunt active
- Face ping pentru mai multe IP-uri si vedem ce hosturi raspund

### NMAP

- Pentru scanarea statiilor din retea si ce sistem de operare foloseste
- Functioneaza si pe interval de porturi

## DOS

- Scopul este sa crestem cererile de procesare pentru server pentru a nu mai putea procesa cererile valide
- Pentru server concurent TCP NU este recomandat sa facem un thread pentru fiecare request pentru ca intra in DDOS
- Avem infectate mai multe calculatoare care executa un atac DOS
- Trafic cu rezultate DOS: Slashdot Effect - un site are o crestere mare de trafic pentru ca este referit de alt site mare

## Smurf Attach

- Ping catre o adresa de broadcast si primeste raspunsuri de la toate statiile din acea retea
- Victima este cea care lanseaza requestul pentru ca intra in DOS la primirea raspunsurilor

## TCP SYN FLOOD

- Deschid multe conexiuni dar nu inchid handshake-ul
- Serverul ajunge sa nu mai poata inchide conexiunile care nu sunt inchise

## CAM Overflow

- Atacam tabela care mapeaza MAC - PORT (la nivelul switch-ului)
- Tabela CAM este plina si switchul va lucra in regim de hub
- Se evita prin limitarea numarul de adrese care se memoreaza pentru un anumit port

## Rainbow Tables

- Foloseste hash-uri precalculate
- Necesita foarte mult spatiu

## Salting

- Adaugi un segment suplimentar la parola
- Stocarea se face cu un segment suplimentar de tip salt

## Man-in-the-Middle

- Traficul este interceptat de catre un atacator
- Se poate optine accesul prind:
  - ARP Poisoning: ARP nu face auth si o statie poate sa minta legat de nivelul de retea.

## Specter & Metdown

- Vulnerabilitate la nivel hardware (procesare Intel)
- Acces la memoria protejata a altor procese
