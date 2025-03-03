# TCP/IP

## Niveluri

1. Acces Retea

&emsp;&emsp; - Accesul

2. Internet

&emsp;&emsp; - Livrarea Pachetelor

&emsp;&emsp; - Gestiunea starii statiilor

3. Transport

&emsp;&emsp; - Transferul de date intre statiile unei retea

&emsp;&emsp; - TCP garanteaza receptia si ordinea primirii pachetelor

&emsp;&emsp; - UDP nu garanteaza receptia totala, dar este mai rapid (Fire & Forget)

4. Aplicatie

&emsp;&emsp; - Ofera servicii

- Fiecare step down pe schema TCP/IP presupune adaugarea unor informatii noi. In cazul HTTP, la fiecare nivel se adauga noi headere

### Exemplu

1. Application Layer

- Message

2. Transport Layer

- Message + Source Port + Destination Port

3. Network Layer

- Transport Layer + Source IP Addr + Dest IP Addr

4. Data Link Layer

- Network Layer + MAC Addr + Dest MAC Addr
