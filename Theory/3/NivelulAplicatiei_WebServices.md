# Nivelul Aplicatiei - Web Services

## Comunicarea cu mesaje SOAP

- Protocolul de comunicare este format dintr-o serie de tab-uri XML

- Mesajele SOAP sunt transmite cu HTTP, SMTP sau cozi de mesaje

### Anvelopa SOAP

1. SOAP Part

2. Attachement Part

3. Attachement Part

### Protocoale WS-*

- Adreseaza anumite nevoi practice

- Ex: UDDI, WS-Discovery (transparenta localizarii), WS-Management (Protocoale de management), WS-Eveting, ES-Notification (de publicare), WS-Addressing: rutarea raspunsurilor sau a erorii

### Localizarea serviciilor cu ajutorul UDDI

- Sunt postate Singleton

- Instanta aloca un port pentru acel serviciu

- Cand publicam un serviciu, avem un registru prin care eu localizez elemente in IntraNet (inclusiv servicii)

- Functioneaza asemanator cu un proxy

- Acest registru poate accesa serviciul

- Clinetul pentru a accesa serviciul trebuie sa stie intefata contract. Astfel, daca modific in serviciu ceva pot sa trimit on the fly.

### WS-Addressing

- Protocol de rutare a raspunsului in mod asincron

- Se bazeaza pe headere

- Aceste servicii sunt fatada pentru accesarea unei platforme

- Adica raspunsurile nu sunt accesate sincron

- Se bazeaza pe HTTPS (TLS) pentru nivelul transport + standard WS-Securing (criptarea payload-urilor transmise). Partile trasnmise pe un canal HTTP nu pot sa fie citite perse pentru ca sunt criptate. WS-RealiableMessaging stocheaza mesajele transmise intr-un store local pentru a nu fi pierdute

- Trimit o cerere -> Inregistrez un npoint -> Fiecare mesaj are un ID -> In headere pun adrese de rutare (pentru cazul de complete sau cazuri pentru eroare)

- Nu astept raspunsul in acelasi canal, ci redirectionez prin headere

- **Important:** Prin wsdl se comunica XML Contract to Contract. Aceste contracte functioneaza ca proxy si ca reverse proxy, comunicand de la contractul clientului catre cel al serverului.

- *De citit:* Canal Duplex (Microsoft WCF Duplex Channel). Expun o singura componenta, nu si pe client si pe server: <https://learn.microsoft.com/en-us/dotnet/framework/wcf/feature-details/duplex-services>

### SOAP cu atasament MTOM

- Datele binare brute sunt transportate cu SOAP ca base64

- Definesc un set minim de informatii de transmis si extensii

- Este utilizat pentru transmiterea de documente

- RPC este practic un set determinat de informatii ce se trimit. Type-ul Document permite utilizatorului sa mai ataseze headere cu informatii
