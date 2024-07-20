# Meine wichtigsten Lessons learned

### Response Length

Eine unterschiedliche Response Length (_wenn alle anderen ~gleich sind_) kann ein Hinweis über eine andere Response geben.\
-> Blick draufwerfen

### Response Time

Kann durch das Hinzufügen von langen Strings künstlich vergrößert werden. Das kann zu einer besseren Unterscheidung in der Art und Weise, wie Anfragen bearbeitet werden, führen.

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

### IP-Blocking

#### Möglichkeiten zum umgehen

- Header setzen
- Reset durch erfolgreichen Login
    - Ein Login mit validen Credentials _kann_ dazu führen, dass der Timeout resettet wird
        - Logik: Username: valide, victim, valide, victim; Passwort: valide, PasswortBruteForce

### 2FA

- Logik der Seite ansehen und verstehen
    - manchmal reicht es, das Verzeichnis in der URL zu ändern
