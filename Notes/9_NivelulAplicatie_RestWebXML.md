# Nivelul Aplicatie: Resurse REST si Servicii Web XML

- REST = Represetational State Transfer

- Este un stil arhitectural, protocol de comunicare client - server

## Principiile REST

- REST are la baza comportamentul browserului care isi schimba starea dupa incarcarea unei pagini, solicitand la indicatiile paginii resursele incluse de aceasta

- API-urile REST au un punct de intrare care instruieste consumatorul ce sa faca mai departe pentru a descoperi si consuma prin apel de operatii resursele expuse de API

## Nivelurile REST (Richardson Maturity Model)

| Nivel   | Descriere                                                                                                                                                   | Utilizare HTTP                | Exemplu simplificat                                    |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|--------------------------------------------------------|
| **0**   | Apeluri la distanță peste HTTP – HTTP sunt folosite doar ca transport. Acțiunile sunt transmise în payload (ex: RPC).                                       | Doar ca transport             | `POST /api` cu corp: `{ "action": "getEmployee" }`     |
| **1**   | Resurse adresabile – Se folosesc URL-uri pentru a identifica entități, dar acțiunile nu sunt mapate pe verbe HTTP.                                          | URL-uri, dar fără verb HTTP   | `POST /employee/123` pentru citire, ștergere etc.      |
| **2**   | Resurse + Verbe HTTP – Se folosesc corect `GET`, `POST`, `PUT`, `DELETE`, iar resursele sunt clare și adresabile.                                           | Corect – verb + resursă       | `GET /employee/123`, `DELETE /employee/123`            |
| **3**   | HATEOAS – Resursele conțin link-uri către operații permise și subresurse. Clientul descoperă navigarea prin API din răspunsuri.                            | HTTP complet + Hypermedia     | `GET /employee/123` returnează și link-uri cu next-uri |

---

## 📦 Ce trebuie adresat într-o aplicație REST

| Aspect esențial                            | Detalii                                                                                 |
|-------------------------------------------|-----------------------------------------------------------------------------------------|
| **Identificarea resurselor**              | Fiecare resursă trebuie să aibă cel puțin o adresă URL unică                           |
| **Exemplu adresă URL**                    | `http://www.example.com/hr/employees/1234567`                                           |
| **Structură resurse**                     | Pot conține subresurse (ex: `/employees/123/salary`)                                   |
| **Formate de reprezentare**               | XML, JSON, YAML etc. – adică *proiecția stării resursei*                               |
| **Acțiuni HTTP suportate**                | `GET`, `POST`, `PUT`, `PATCH`, `DELETE` în funcție de resursă                          |
| **Status code-uri așteptate**             | `200 OK`, `201 Created`, `204 No Content`, `400 Bad Request`, `404 Not Found`, etc.    |
| **Descoperirea resurselor (nivel 3)**     | Se poate face prin `OPTIONS` sau prin link-uri HATEOAS în corpul răspunsului           |

---

> Dacă aplicația  REST nu folosește verbe HTTP corecte, e sub nivelul 2.  
> Dacă vrei **REST complet**, mergi până la nivelul 3 cu link-uri și descoperire automată (HATEOAS).

## Principiile Arhitecturii Orientate pe Resurse

- Adresabilitate: Orice resursa trebuie sa fie disponibila la un URL

- Fara Stare:
  - Nu se pastreaza starea intre mai multe apeluri REST
  - Simplifica proiectarea si dezvoltarea arhitecturilor scalabile

- Conectivitate: Resursele trebuie sa fie conectate intre ele pentru a fi usor de descoperit

- Manipularea uniforma: Acelasi set de operatii aplicatibile tuturor resurserselor dintr-o categorie

## Servicii Web XML

| Tehnologie        | Descriere                                                                                   | Platformă            | Alte detalii importante                                 |
|-------------------|----------------------------------------------------------------------------------------------|----------------------|----------------------------------------------------------|
| **CORBA**         | Common Object Request Broker Architecture – bazată pe IDL pentru definirea contractelor      | C++, Java (cross)    | Folosește ORB (Object Request Broker) pentru interoperabilitate binară |
|                   |                                                                                              |                      | Permite comunicarea între aplicații scrise în C++ și Java |
| **DCOM**          | Distributed Component Object Model – tehnologie proprietară Microsoft                       | Windows (C++)        | Permite consumul de componente COM între mașini diferite |
|                   |                                                                                              |                      | Nu este portabil între platforme                        |
| **RMI**           | Remote Method Invocation – apel de metode la distanță în Java                               | Java                 | Serviciile sunt înregistrate într-un registru RMI       |
|                   |                                                                                              |                      | Fiecare serviciu ascultă pe un port dedicat             |
| **.NET Remoting** | Apel la distanță în .NET – bazat pe un format binar derivat din DCOM                        | .NET (Windows)       | Folosește activatori și interceptori de canal           |
|                   |                                                                                              |                      | Considerată tehnologie legacy, înlocuită de WCF și gRPC |

## Tehnologii și standarde în arhitectura XML Web Services (SOA)

| Tehnologie | Descriere                                                                                                     | Format principal | Rol în ecosistemul SOA                                     |
|------------|--------------------------------------------------------------------------------------------------------------|------------------|-------------------------------------------------------------|
| **SOAP**   | Simple Object Access Protocol – protocol de apel la distanță bazat pe mesaje XML                             | XML              | Permite comunicații cerere-răspuns sau document-based RPC  |
|            |                                                                                                              |                  | Poate rula peste HTTP, SMTP etc.                           |
| **WSDL**   | Web Service Description Language – document XML ce descrie interfața, protocolul și locația unui serviciu    | XML + XSD        | Definește contractul complet al serviciului (metode, tipuri de date, endpoint-uri) |
|            |                                                                                                              |                  | Este legat direct de invocările SOAP                       |
| **UDDI**   | Universal Description, Discovery and Integration – registru de servicii (directory)                          | XML-based        | Permite publicarea și descoperirea serviciilor web         |
|            |                                                                                                              |                  | Popularitatea sa a scăzut, dar se mai folosește în enterprise |

## SOAP

**SOAP (Simple Object Access Protocol)** este un protocol de comunicație bazat pe **mesaje XML** utilizat pentru apeluri la distanță între aplicații, în special în arhitecturi orientate pe servicii (SOA).

### Scopul SOAP

SOAP a fost conceput pentru a permite **schimbul structurat și standardizat de date** între aplicații care rulează pe sisteme diferite, în rețele eterogene (ex: .NET ↔ Java, Windows ↔ Linux), indiferent de limbajul de programare sau platforma folosită.

### Cum funcționează

- Aplicația client trimite o **cerere SOAP** (un mesaj XML standardizat).
- Serverul procesează cererea și returnează un **răspuns SOAP**, tot în format XML.
- Mesajele SOAP sunt transportate, de obicei, peste **HTTP**, dar pot fi livrate și prin **SMTP**, **FTP**, etc.

### Structura unui mesaj SOAP

Un mesaj SOAP conține următoarele componente, toate în format XML:

1. **Envelope** – delimitează mesajul SOAP.
2. **Header** *(opțional)* – pentru informații adiționale (ex: autentificare, tracking).
3. **Body** – conține efectiv cererea sau răspunsul (ex: numele metodei și parametrii).
4. **Fault** *(opțional)* – detalii despre eventuale erori.

### 📌 Exemplu simplificat

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <getUser xmlns="http://example.com/userService">
      <userId>123</userId>
    </getUser>
  </soap:Body>
</soap:Envelope>
```

### Beneficii

- Este standardizat și extensibil.
- Suportă securitate (WS-Security), transacții și routing.
- Este ideal pentru sisteme enterprise.

### Limitări

- Este verbal (XML) și greu, deci mai lent decât alternative moderne (ex: REST/JSON).
- Necesită instrumente de generare automată (ex: WSDL) pentru consumare facilă.
