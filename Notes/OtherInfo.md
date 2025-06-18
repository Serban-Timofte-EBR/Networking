# Other Information

## Router vs Switch vs Hub

## Comparație Hub vs Switch vs Router

| Caracteristică          | **Hub**                             | **Switch**                            | **Router**                                 |
|-------------------------|-------------------------------------|----------------------------------------|--------------------------------------------|
| **Nivel OSI**           | 1 – Fizic                           | 2 – Data Link                          | 3 – Network                                |
| **Adresare**            | Nu folosește adrese                 | Adrese MAC                             | Adrese IP                                  |
| **Mod transmitere**     | Retransmite la toate porturile      | Trimite doar către portul destinatar   | Direcționează între rețele                 |
| **Inteligent?**         | ❌ Nu                               | ✅ Da (învață adrese MAC)              | ✅ Da (routing, NAT, firewall etc.)        |
| **Coliziuni**           | Da, multe                           | Rar sau deloc                          | Nu, izolează rețele                         |
| **Scop**                | Conectare simplă în LAN-uri vechi   | Comunicare eficientă în LAN            | Conectarea între rețele (LAN ↔ Internet)   |
| **Funcții avansate**    | Nu                                  | VLAN (opțional)                        | NAT, DHCP, VPN, Firewall, QoS etc.         |
| **Exemplu uzual**       | Laborator vechi sau testare         | Birou, casă, switch-uri de rack        | Router casnic sau enterprise, ISP gateways |

## Calcul de subretele

- Calcul adresa de retea

- Calcul adresa broadcast

- Calcul subretele

### Adresa Retea + Broadcast

O stație care are adresa 172.15.27.59/25 scanează subrețeaua pentru a afla ce stații sunt pornite.

```txt
10101100.10101100.10101100.00111011
11111111.11111111.11111111.10000000
----------------------------------------------------- AND
10101100.10101100.10101100.00000000
```

Adresa de retea: 172.15.27.0

Numarul de adrese: 2 ^ (32-25) = 2^7 = 128

172.15.27.0 + 128 adrese - 1 = 172.15.27.127 (Adresa Broadcast)

### Adresa Retea + Broadcast - 2

Stația cu adresa 69.35.7.120/19 direște să trimit o datagramă UDP care să ajungă la toate stațiile din aceeați subrețea.

```txt
128 64 32 16 8 4 2 1
0 1 0 0 0 1 0 1. 0 0 1 0 0 0 1 1. 0 0 0 0 0 1 1 1. 0 1 1 0 1 1 1 0
1 1 1 1 1 1 1 1.1 1 1 1 1 1 1 1. 1 1 1 0  0 0 0 0. 0 0 0 0 0 0 0 0
----------------------------------------------------------------------- AND
0 1 0 0 0 1 0 1.0 0 1 0 0 0 1 1. 0 0 0 0 0 0 0 0. 0 0 0 0 0 0 0 0
```

69.25.0.0 (Adresa de retea)

Numaru de adresse in subretea 2 ^ (32 – 19) = 2 ^ 13 = 8192 adrese

8192 / 256 = 32 de blocuri de cate 256 de adresse

Adresa de broadcast: 69.25.0.0 + 8192 adrese - 1= 69.25.31.255

### Calcul subretele egale

Să se împartă optim spațiul de adrese 172.18.240.0/23 astfel încât să fie satisfăcute cerințele:

- O rețea cu 200 de host-uri; => Minim 202 adrese => 2^8 = 256 => 32 - 8 = 24 => Masca /24
- O rețea cu 90 de host-uri; => Minim 92 adrese => 2^7 = 128 => 32 - 7 = 25 => Masca /25
- Două rețele cu 20 de host-uri; => Minim 22 adrese => 2^5 => Masca /27
- O rețea cu 6 host-uri; => Minim 8 adrese => Masca /29
- Trei rețele cu 4 host-uri. => Minim 6 adrese => Masca /29 

```txt
10101100.00010010.11110000.00000000
11111111.11111111.11111110.00000000
----------------------------------- AND
10101100.00010010.11110000.0000000
````

Adresa de retea: 172.18.240.0
Avem 32 - 23 = 9 biti pentru host => 2^9 = 512 adrese disponibile
Confom impartirii noastre ne trebuie 202 + 92 + 22 + 8 + 6 = 330

```txt
1. Reteaua A: 200 de host-uri => Masca /24
    172.18.240.0 -> 172.18.240.255 /24

2. Reteaua B: 90 host-uri => Masca /25
    172.18.241.0 -> 172.18.241.127

3. Reteaua C: 20 hosturi => Masca /27
    172.18.241.128 -> 172.18.241.159

4. Reteaua D: 20 hosturi => Masca /27
    172.18.241.160 -> 172.18.241.191

5. Reteaua E: 6 hosturi => Masca /29
    172.18.241.192 -> 172.18.241.199

6. Reteaua F: 3 hosturi => Masca /29
    172.18.241.200 -> 172.18.241.207

7. Reteaua G: 3 hosturi => Masca /29
    172.18.241.208 -> 172.18.241.215

8. Reteaua H: 3 hosturi => Masca /29
    172.18.241.216 -> 172.18.241.223
```
