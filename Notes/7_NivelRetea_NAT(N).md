# NivelRetea - NAT, PAT, ARP, RARP, ICMP, DHCP, SNMP

## Epuizarea adreselor IPv4

- Spațiul de adrese IPv4 este limitat (~4 miliarde adrese).
- Introducerea adreselor private:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
- Dispozitivele cu adrese private au nevoie de translație pentru a accesa Internetul.

## NAT (Network Address Translation)

- Permite schimbarea adresei IP sursă sau destinație în pachete.
- Se aplică la traversarea unui router.

### Tipuri de NAT

- **NAT Static**: asociere fixă între o adresă internă și una publică.
- **NAT Dinamic**: folosirea unui pool de adrese publice.
- **PAT (Port Address Translation)**: multiple dispozitive interne partajează o adresă publică folosind porturi diferite.

### iptables și NAT

- **SNAT**: schimbarea adresei sursă (Postrouting).
- **DNAT**: schimbarea adresei destinație (Prerouting).
- **MASQUERADE**: pentru adrese dinamice (ex: DHCP).

## Problemele NAT/PAT

- Inițierea conexiunilor externe este dificilă.
- VPN-urile sunt mai complicat de configurat.
- Întârzie tranziția către IPv6.

---

## ARP (Address Resolution Protocol)

- Rezolvă adresa IP într-o adresă MAC.
- Folosește broadcast pentru a întreba toate dispozitivele.

## RARP (Reverse Address Resolution Protocol)

- Determină adresa IP pornind de la adresa MAC.
- Era folosit la dispozitive fără memorie proprie de configurare.

## NDP (Neighbor Discovery Protocol) în IPv6

- Echivalent ARP pentru IPv6.
- Descoperire automată a routerelor și adreselor vecine.

---

## ICMP (Internet Control Message Protocol)

- Protocol pentru semnalizarea erorilor IP.
- Exemple:
  - Destination Unreachable
  - Time Exceeded

### Utilitare ICMP

- **ping**: verificare conectivitate între două dispozitive.
- **traceroute**: identificarea traseului pachetelor prin rețea.

## ICMPv6

- Versiunea pentru IPv6, include și funcționalitățile de Neighbor Discovery.

---

## DHCP (Dynamic Host Configuration Protocol)

- Alocă adrese IP și alte informații de configurare automat.

### Proces DHCP

1. **Discovery**: clientul caută servere DHCP.
2. **Offer**: serverul propune o configurație.
3. **Request**: clientul cere alocarea adresei.
4. **Acknowledgment**: serverul confirmă alocarea.

### Lease

- Adresele IP sunt alocate temporar (lease time).

### DHCP Relay

- Permite trimiterea cererilor DHCP între rețele diferite.

---

## SNMP (Simple Network Management Protocol)

- Protocol de monitorizare și administrare a echipamentelor de rețea.

### Componente

- **Manager SNMP**: trimite cereri și colectează date.
- **Agent SNMP**: dispozitivul monitorizat.
- **MIB (Management Information Base)**: bază de date cu parametri administrați.

### Mesaje SNMP

- **Get**: cerere de citire a unei valori.
- **Set**: cerere de modificare a unei valori.
- **Trap**: notificare neașteptată de la agent către manager.

---

# Recapitulare rapidă

| Protocol | Rol Principal |
|:--------:|:--------------:|
| NAT/PAT | Traducerea adreselor IP |
| ARP     | Rezolvarea IP -> MAC |
| RARP    | Rezolvarea MAC -> IP |
| ICMP    | Semnalarea erorilor |
| DHCP    | Alocarea dinamică de IP |
| SNMP    | Monitorizare și administrare rețea |

