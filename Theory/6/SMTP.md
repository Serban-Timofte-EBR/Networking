# SMTP

- Zona de accesare de email (Simple Mail Transport Trotocol)

- Protocol text care foloseste TCP la baza

- Nu necesita autentificare, dar permite si autentificare

- Acum se foloseste DNS communication

## Posibile Intarzieri

- Exista un Spool care stocheaza datele pana ajung la MTA (Mail Transfer Agent) pentru a astepta rutarea mai departe

- Serverul stocheaza mesajul inainte de a fi livrat pe masina client (comun in caz de email alias pentru un grup. sau alias care trimite la mai multe conturi.)

## Pasi

- Comanda MAIL cu destinatie

- MAIL -> Utilitar la nivel de OS

## Descarcare de mesaje

1. POP

- Descarca toate emailurile pe client si le trimit cand sunt conectat la server

- Port 110

- Asteapta raspuns la fiecare pas

- Necesita autentificare

- Se ocupa doar de un client la un moment dat (decom)

2. IMAP

- Internet Message Access Protocol -> Folosit astazi

- Ne conectam cu mai multi clienti simultan la o casuta de email (accesez un cont de pe mai multe device uri)

- Organizare pe foldere

- Pot atasa taburi - system tags
