## Nivelul Rețea

### Funcțiile nivelului rețea

Nivelul rețea din modelul TCP/IP este responsabil pentru:

- **Fragmentarea segmentelor în pachete de rețea**  
  Segmentele venite de la nivelul transport pot fi prea mari pentru o transmisie directă. Nivelul rețea le fragmentează în pachete și asigură **reansamblarea acestora la destinație**.

- **Rutarea pachetelor de la sursă la destinație**  
  Nivelul rețea se ocupă cu determinarea traseului pe care un pachet trebuie să îl urmeze de la sursă până la destinație, chiar dacă cele două se află în rețele diferite.

---

### Tipuri de protocoale de nivel rețea

1. **Protocoale rutabile**  
   Acestea sunt protocoalele care transportă efectiv datele. Exemple:
   - IP (Internet Protocol)
   - ICMP

2. **Protocoale de rutare**  
   Acestea nu transportă date direct, ci ajută routerele să determine cea mai bună cale pentru rutare. Exemple:
   - RIP
   - OSPF
   - BGP

---

### Protocolul IP

- Este **protocolul esențial al Internetului**.
- Asigură **adresarea globală** a dispozitivelor și **rutarea pachetelor** între rețele.
- Adresele IP au **semnificație globală**, în timp ce adresele MAC (de nivel 2) au **semnificație locală** (într-o rețea locală, adresele MAC pot fi suficiente).
- IP-ul permite identificarea atât a **dispozitivului**, cât și a **rețelei** din care face parte.

---

### Versiuni ale protocolului IP

- **IPv4**:  
  - A fost versiunea inițială și este încă cea mai utilizată.  
  - Oferă aproximativ 4.3 miliarde de adrese (32 de biți).  
  - A devenit insuficient odată cu creșterea Internetului.

- **IPv6**:  
  - Oferă 128 de biți pentru adresare (2^128 adrese).  
  - A rezolvat problema spațiului limitat.  
  - Permite o conectivitate **end-to-end** reală (fără NAT).  
  - Aduce și alte optimizări, precum eliminarea checksum-ului.

---

### Comparație IPv4 vs IPv6

| Caracteristică           | IPv4                       | IPv6                               |
|--------------------------|----------------------------|-------------------------------------|
| Lungimea adresei         | 32 biți                    | 128 biți                            |
| Suport VLSM              | Da                         | Nu                                  |
| Verificare cu checksum   | Da                         | Nu                                  |
| Broadcasting             | Da                         | Nu, folosește multicast și anycast  |
| Mecanism anycast         | Nu                         | Da                                  |

---

### Formatele Pachetelor IPv4 și IPv6

---

#### Formatul pachetului IPv4

Pachetul IPv4 conține un header detaliat, care oferă multiple informații necesare pentru livrarea corectă a datelor:

- **Version** (4 biți): indică versiunea protocolului IP (valoarea este 4).
- **IHL** (Internet Header Length - 4 biți): specifică lungimea header-ului în unități de 32 de biți.
- **DSCP** (Differentiated Service Code Point - 6 biți): identifică tipul de serviciu și permite prioritizarea traficului.
- **ECN** (Explicit Congestion Notification - 2 biți): indică congestia din rețea.
- **Total Length** (16 biți): lungimea totală a pachetului (header + date).
- **Identification** (16 biți): identificator unic pentru pachetele care fac parte din același segment.
- **Flags** (3 biți):
  - Bit 0: rezervat (0)
  - Bit 1: DF (Don't Fragment)
  - Bit 2: MF (More Fragments)
- **Fragment Offset** (14 biți): poziția fragmentului în cadrul datelor inițiale.
- **Time To Live (TTL)** (8 biți): numărul maxim de routere prin care poate trece pachetul (previne loop-urile).
- **Protocol** (8 biți): identifică protocolul de transport (ex: TCP, UDP).
- **Header Checksum** (16 biți): sumă de control pentru validarea header-ului. Dacă suma este incorectă, pachetul este eliminat.
- **Source Address** (32 biți): adresa IP a expeditorului.
- **Destination Address** (32 biți): adresa IP a destinatarului.
- **Options** (variabil, până la 40 de octeți): folosite rar, pentru funcționalități avansate.
- **Data**: partea efectivă cu informații utile către aplicație.

Dimensiunea maximă a unui pachet IPv4 este de 65.535 bytes.

#### Formatul pachetului IPv6

IPv6 aduce un format de header simplificat și mai eficient față de IPv4. Are dimensiune fixă de 40 bytes și elimină câmpuri considerate inutile:

- **Version** (4 biți): valoarea este 6.
- **Traffic Class** (8 biți): similar cu DSCP + ECN din IPv4, indică tipul traficului și congestia.
- **Flow Label** (20 biți): permite identificarea rapidă a fluxurilor de date continue.
- **Payload Length** (16 biți): dimensiunea datelor utile (fără header).
- **Next Header** (8 biți): identifică tipul următorului header (ex: TCP, UDP, extensii IPv6).
- **Hop Limit** (8 biți): similar cu TTL din IPv4.
- **Source Address** (128 biți): adresa IPv6 a expeditorului.
- **Destination Address** (128 biți): adresa IPv6 a destinatarului.

IPv6 nu conține checksum în header și folosește extensii separate pentru fragmentare, ceea ce simplifică prelucrarea pachetelor de către routere.

#### Comparativ IPv4 vs IPv6

| Caracteristică     | IPv4                | IPv6                     |
|--------------------|---------------------|--------------------------|
| Lungime adresă     | 32 biți             | 128 biți                 |
| Verificare checksum| Da                  | Nu                       |
| Fragmentare        | Inclusă în header   | Delegată extensiilor     |
| Broadcasting       | Da                  | Nu (folosește multicast) |
| Suport anycast     | Nu                  | Da                       |
| Suport VLSM        | Da                  | Nu                       |

IPv6 a fost proiectat pentru a rezolva limitările IPv4, oferind mai multe adrese disponibile, securitate îmbunătățită și performanță mai mare în procesare.

### Masca de rețea (Subnet Mask)

Masca de rețea este un concept fundamental în definirea rețelelor IP. Ea determină ce parte dintr-o adresă IP reprezintă rețeaua și ce parte reprezintă hostul (dispozitivul).

---

#### Cum funcționează?

Masca de rețea este un număr binar de 32 de biți (în IPv4) care se aplică printr-o operație binară AND peste o adresă IP.

Scopul este de a separa adresa IP în două componente:

- Partea de rețea (network address)

- Partea de host (host address)

---

#### Exemplu de calcul

Să presupunem o adresă IP și o mască:

- Adresă IP: 192.168.1.10

- Masca de rețea: 255.255.255.0

În binar:

```plain-text
192.168.1.10     = 11000000.10101000.00000001.00001010  
255.255.255.0    = 11111111.11111111.11111111.00000000
-----------------------------------------------------
REȚEA (AND)      = 11000000.10101000.00000001.00000000
                 = 192.168.1.0
```

- Deci adresa de rețea este 192.168.1.0.

- Partea de host este ce rămâne (ultimii biți, aici 00001010 adică 10).

---

#### Notații importante

- Masca definește dimensiunea rețelei și câți hosturi sunt posibile.
- Este strâns legată de conceptul de CIDR (Classless Inter-Domain Routing), unde masca e reprezentată ca /n, de ex: 192.168.1.0/24.

---

#### Exemple de măști frecvente

| Masca zecimală | Scurtătură CIDR | Nr. hosturi posibili |
|----------------|-----------------|----------------------|
| 255.0.0.0      | /8              | 16.777.214           |
| 255.255.0.0    | /16             | 65.534               |
| 255.255.255.0  | /24             | 254                  |
| 255.255.255.192| /26             | 62                   |

Notă: numărul maxim de hosturi = 2^(număr biți de host) - 2 (se scad rețeaua și broadcast-ul)

#### Concluzie

Masca de rețea este cheia pentru a înțelege structura internă a unei rețele IP. Aplicarea unei măști printr-un AND binar cu adresa IP îți arată la ce rețea aparține un host. Aceasta este baza oricărui mecanism de rutare, segmentare de rețele, și planificare IP.

### Clasele de adrese IP

Adresele IP pot fi clasificate în mai multe clase, în funcție de valoarea primului octet, ceea ce determină masca de rețea și dimensiunea rețelei.

| Clasa | Primul octet | Masca de rețea |
|-------|--------------|----------------|
| A     | 1 - 126      | 255.0.0.0      |
| B     | 128 - 191    | 255.255.0.0    |
| C     | 193 - 223    | 255.255.255.0  |
| D     | 224 - 239    | (Multicast)    |
| E     | 240 - 254    | (Experimental) |

- Clasele A, B și C sunt utilizate pentru alocarea adreselor către rețele și hosturi.
- Clasa D este utilizată pentru multicast (transmisie către grupuri).
- Clasa E este rezervată pentru experimente și nu este folosită în mod curent.

---

### Tipuri de transmisie IPv4

- **Unicast** – Transmiterea unui pachet de la un singur emitent către un singur destinatar.
- **Multicast** – Transmiterea către un grup specific de dispozitive. Se folosesc adrese speciale din clasa D (224.0.0.0 – 239.255.255.255).
- **Broadcast** – Transmiterea către toate dispozitivele dintr-o rețea locală. Se folosește adresa de broadcast, completând toți biții de host cu 1 (ex: 192.168.1.255).

---

### Adrese speciale IPv4

- **Adrese multicast**: utilizate pentru trimiterea pachetelor către mai mulți destinatari (grupuri).
- **Adresa 0.0.0.0** ("orice rețea"): utilizată de obicei în procesele de boot sau pentru ascultarea pe toate interfețele.
- **Adrese de loopback** (ex: 127.0.0.1): utilizate pentru testarea conexiunilor locale pe dispozitiv.
- **169.254.0.0/16**: alocare automată (APIPA) atunci când DHCP nu funcționează.
- **Adrese private**:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

    Acestea nu sunt rutabile în Internet și sunt folosite pentru rețele interne.

---

### Exemplu de calcul pentru o rețea

- Adresă IP: 153.112.34.22
- Clasa: B ⇒ Masca: 255.255.0.0
- Adresa rețelei: 153.112.0.0 (rezultatul unui AND binar între adresa IP și masca de rețea)
- Adresa de broadcast: 153.112.255.255 (toți biții host setați pe 1)
- Intervalul adreselor de host: 153.112.0.1 – 153.112.255.254

---

### Masca de rețea – rol și utilizare

Masca de rețea este un număr binar care permite separarea părții de rețea de partea de host dintr-o adresă IP.

Se aplică un AND binar între adresa IP și masca de rețea pentru a obține adresa rețelei.

**Exemplu:**

- Adresă IP: 192.168.1.130
- Masca: 255.255.255.0 ⇒ partea de rețea este 192.168.1.0

Masca este esențială pentru determinarea corectă a topologiei rețelei și pentru rutare.

### CIDR și Subnetting

CIDR (Classless Inter-Domain Routing) este un sistem de alocare a adreselor IP care nu mai ține cont de clasele tradiționale (A, B, C). CIDR a fost introdus pentru a îmbunătăți utilizarea spațiului de adrese și pentru a simplifica rutarea.

#### Caracteristici CIDR:

- Alocare a adreselor de IP fără clase.
- Masca de rețea nu se mai deduce din primii biți ai adresei IP, ci trebuie specificată explicit.
- Se folosește o notație nouă: de exemplu, 255.255.0.0 este echivalent cu /16, ceea ce înseamnă că primii 16 biți reprezintă partea de rețea.

---

### Subnetting

Subnetting-ul presupune împărțirea unei rețele IP într-o serie de subrețele mai mici. Acest proces este util pentru organizarea și gestionarea eficientă a adreselor IP în rețele mari.

#### Motivații pentru subnetting:

- Separarea traficului intern.
- Alocare eficientă a spațiului de adresare.
- Posibilitatea de a crea subrețele independente în cadrul unei rețele mai mari.

#### Tipuri de subnetting:

- **Cu mască fixă** – toate subrețelele au aceeași dimensiune.
- **Cu mască variabilă (VLSM)** – dimensiunea subrețelelor poate varia în funcție de nevoi.

#### Întrebări utile înainte de subnetting:

- Este blocul de adrese suficient pentru nevoi?
- Este necesară o mască variabilă?
- Putem acoperi extinderi viitoare?
- Putem optimiza tabelele de rutare?

---

### Exemplu de subnetting:

Să presupunem că avem rețeaua 192.168.23.0/24 și dorim să o împărțim în 4 subrețele egale, fiecare cu câte 30 de hosturi utilizabile. Vom extinde masca de rețea de la /24 la /26 (2 biți suplimentari pentru rețea).

Masca binară devine: 11111111.11111111.11111111.11000000 → echivalent cu 255.255.255.192

### Ce înseamnă `/24`?

Notația `/24` este o formă prescurtată de a scrie **masca de rețea** în format CIDR (Classless Inter-Domain Routing).

- `/24` înseamnă că **primii 24 de biți** ai adresei IP sunt rezervați pentru identificarea rețelei.
- În binar: `11111111.11111111.11111111.00000000`
- În zecimal: `255.255.255.0`

Astfel, în rețeaua `192.168.23.0/24`:

- Toate adresele IP care încep cu `192.168.23.` fac parte din această rețea.
- Ultimul octet (8 biți) este disponibil pentru identificarea **hosturilor** (calculatoare, imprimante etc.).

---

### De ce trecem la `/26`?

Vrem să împărțim rețeaua `/24` în **4 subrețele egale**. Pentru asta avem nevoie de **2 biți** suplimentari pentru a diferenția între 4 subrețele:

- 2 biți → 2² = **4 subrețele**
- Noul prefix CIDR: **/26** (24 + 2 biți pentru subrețele)

Noua mască de rețea:

- Binar: `11111111.11111111.11111111.11000000`
- Zecimal: `255.255.255.192`

---

### Câte adrese avem per subrețea?

Cu o mască /26 avem 6 biți rămași pentru hosturi (32 biți - 26 biți = 6 biți):

- 2⁶ = 64 adrese
- 64 - 2 = **62 hosturi utilizabile** (una e adresa de rețea, alta e adresa de broadcast)

---

### Calculul subrețelelor

#### Subrețeaua A

- Adresă de rețea: `192.168.23.0` (toți biții host = 0)
- Broadcast: `192.168.23.63` (toți biții host = 1) - mai avem 6 biti disponibili pe /26
- Hosturi: `192.168.23.1` – `192.168.23.62`

#### Subrețeaua B

- Adresă de rețea: `192.168.23.64` (următoarea după 63)
- Broadcast: `192.168.23.127`
- Hosturi: `192.168.23.65` – `192.168.23.126`

#### Subrețeaua C

- Adresă de rețea: `192.168.23.128`
- Broadcast: `192.168.23.191`
- Hosturi: `192.168.23.129` – `192.168.23.190`

#### Subrețeaua D

- Adresă de rețea: `192.168.23.192`
- Broadcast: `192.168.23.255`
- Hosturi: `192.168.23.193` – `192.168.23.254`

---

### Observații finale

- Ultima adresă din fiecare subrețea este adresa de broadcast.
- Prima adresă este adresa de rețea (nereutilizabilă).
- Primele 2 subrețele folosesc biții adăugați (din cei 2 extinși) ca 00 și 01, iar următoarele 10 și 11 (binare).
- Subnettingul eficient reduce irosirea spațiului de adrese și optimizează tabelele de rutare în rețele mari sau distribuite.

### VLSM (Variable Length Subnet Masking)

VLSM permite alocarea de adrese IP în mod flexibil, folosind măști de subrețea de lungime variabilă. Această tehnică este extrem de utilă în rețelele unde subrețelele nu au dimensiuni egale, oferind o utilizare mai eficientă a spațiului de adresare disponibil.

#### Avantaje VLSM

- Permite alocarea progresivă a biților de subrețea.
- Permite optimizarea resurselor atunci când subrețelele au dimensiuni diferite.
- Fără VLSM, ar trebui să folosim o mască fixă pentru toate subrețelele, ceea ce duce la risipă.

#### Exercițiu VLSM

**Rețeaua: 193.226.3.0/24**

Avem nevoie să împărțim această rețea în 6 subrețele cu următoarele cerințe:

- Subrețeaua A: 50 hosts
- Subrețeaua B: 24 hosts
- Subrețeaua C: 8 hosts
- Subrețelele D, E, F: câte 2 hosts

Vom aloca mai întâi subrețeaua cu cele mai multe hosturi (A), apoi în ordine descrescătoare.

##### Subrețeaua A (50 hosts)

- Avem nevoie de 6 biți pentru partea de host: 2^6 = 64 (din care 62 utilizabili)
- Masca: /26 (255.255.255.192)
- Rețea: 193.226.3.0/26
- Broadcast: 193.226.3.63
- Hosts: 193.226.3.1 la 193.226.3.62

##### Subrețeaua B (24 hosts)

- 5 biți pentru partea de host: 2^5 = 32 (30 utilizabili)
- Masca: /27 (255.255.255.224)
- Rețea: 193.226.3.64/27
- Broadcast: 193.226.3.95
- Hosts: 193.226.3.65 la 193.226.3.94

##### Subrețeaua C (8 hosts)

- 4 biți pentru partea de host: 2^4 = 16 (14 utilizabili)
- Masca: /28 (255.255.255.240)
- Rețea: 193.226.3.96/28
- Broadcast: 193.226.3.111
- Hosts: 193.226.3.97 la 193.226.3.110

##### Subrețeaua D (2 hosts)

- 2 biți pentru partea de host: 2^2 = 4 (2 utilizabili)
- Masca: /30 (255.255.255.252)
- Rețea: 193.226.3.112/30
- Broadcast: 193.226.3.115
- Hosts: 193.226.3.113 la 193.226.3.114

##### Subrețeaua E (2 hosts)

- Masca: /30
- Rețea: 193.226.3.116/30
- Broadcast: 193.226.3.119
- Hosts: 193.226.3.117 la 193.226.3.118

##### Subrețeaua F (2 hosts)

- Masca: /30
- Rețea: 193.226.3.120/30
- Broadcast: 193.226.3.123
- Hosts: 193.226.3.121 la 193.226.3.122

#### Concluzii

- VLSM permite să folosim doar atâția biți cât avem nevoie pentru fiecare subrețea.
- În loc să rezervăm un spațiu de 64 de adrese pentru toate subrețelele (dacă am folosi mască fixă /26), folosim măști variate: /26, /27, /28, /30.
- Prin utilizarea VLSM se optimizează utilizarea spațiului de adresare, evitând risipa de adrese IP.

## Calcul de subrețele

### Identificare host rețelei, broadcastului și a hosturilor

- Adresa IP: 192.168.1.130

- Masca de rețea: /26

1. Identificăm masca în format binar

/26 => Primii 26 de biți sunt 1

```text
11111111.11111111.11111111.11000000
```

2. Transformăm masca în format decimal

Din punctul 1, rezulta masca

```text
255.255.255.192
```

3. Identificăm incrementul blocului

- Ultimul octet din mască este 192 => 256 - 192 = 64.

4. Stabilim intervalele pentru subrețele

- Avem următoarele intervale disponibile

```text
192.168.1.0 - 192.168.1.63
192.168.1.64 - 192.168.1.127
192.168.1.128 – 192.168.1.191  
192.168.1.192 – 192.168.1.255
```

5. În ce bloc se află adresa IP 192.168.1.130?

- 192.168.1.130 este între 192.168.1.128 – 192.168.1.191

6. Rezultate

- Adresă de rețea: 192.168.1.128

- Adresă de broadcast: 192.168.1.191

- Primul host valid: 192.168.1.129

- Ultimul host valid: 192.168.1.190

- Număr total de hosturi valide: 2^(32 - 26) - 2 = 64 - 2 = 62 hosturi
