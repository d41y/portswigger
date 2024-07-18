# Meine wichtigsten Lessons learned

### Response Length

Eine unterschiedliche Response Length (_wenn alle anderen ~gleich sind_) kann ein Hinweis über eine andere Response geben.\
-> Blick draufwerfen

### BurpSuite grep-Match

Vorher anschauen, was die ausgegebene Antwort auf falsche Credentials ist.\
Im besten Fall wurde beim Programmieren der Website ein kleiner Fehler in der Zeichenkette für die Ausgabe TEILS falscher Eingaben ist.

Bsp.:\
bei invalid username AND invalid password -> Invalid username or password.\
bei valid username AND invalid password -> Invalid username or password [ohne Punkt]

### Header

| Header | Effekt | Beispiel |
| ------ | ------ | -------- |
| X-Forwarded-For | Kann zum Spoofen von IP-Adressen genutzt werden | X-Forwarded-For: 'abc123'/'[WORDLIST]' |