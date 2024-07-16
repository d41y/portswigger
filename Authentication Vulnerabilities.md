# Authentication Vulnerabilities

## Lab: Username enumeration via different responses

_To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page._

### Durchführung

- Anschauen der Posts
    -> einige Usernamen
- Login-Versuch mit Username:Username
    -> händisch wird's nichts; deswegen BurpSuite
- Abfangen der Request mit BurpSuite
- ~~Erstellen einer Liste mit potentiellen Usernamen~~
- Benutzen der Wordlists von PortSwigger gegeben
- BurpSuite zunächst Usernames -> Length
    -> dann Passwords -> Length
- die Response-Length verändert sich in Abhängigkeit zu dem, was ausgegeben wird (logisch)
- invalid username AND invalid password hat eine andere Länge als username AND invalid password
    -> gleiches gilt für invalid password und password

### Ergebnis

- Username: adkit
- Passwort: 131313


### Folgerung

- Wordlists von Websites erstellen -> automatisieren!
    -> CeWL?
    -> Crunch?
    -> ODER ABER VIELLEICHT MAL DIE AUFGABENSTELLUNG ORDENTLICH LESEN!!! -> WORDLISTS
- Response-Length ist nicht zu vernachlässigen!
