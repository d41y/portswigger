# Meine wichtigsten Lessons learned

### Response Length

Eine unterschiedliche Response Length (wenn alle anderen ~gleich sind) kann ein Hinweis über eine andere Response geben.
-> Blick draufwerfen

### BurpSuite grep-Match

Vorher anschauen, was die ausgegebene Antwort auf falsche Credentials ist.
Im besten Fall wurde beim Programmieren der Website ein kleiner Fehler in der Zeichenkette für die Ausgabe TEILS falscher Eingaben ist.

Bsp.:\n
bei invalid username AND invalid password -> Invalid username or password.\n
bei valid username AND invalid password -> Invalid username or password [ohne Punkt]