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
    -> CeWL?\
    -> Crunch?\
    -> ODER ABER VIELLEICHT MAL DIE AUFGABENSTELLUNG ORDENTLICH LESEN!!! -> WORDLISTS
- Response-Length ist nicht zu vernachlässigen!

## Lab: Username enumeration via subtly different responses

_To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page._

### Durchführung

- Ähnlich wie in der Aufgabe zuvor
    -> BurpSuite\
    -> falschen Username und falsches Passwort und das mit BurpSuite abfangen\
    -> Wordlist Usernames und ein grep-Match setzen 'Invalid username and password.'
    

### Ergebnis

- Username: agent
- Passwort: amanda
 
### Folgerung

- der kleinste Unterschied in der Zeichenkette, die bei unterschiedlichen Responses ausgegeben wird, kann entscheidend sein\
    -> Hier war es der Punkt\
    -> BurpSuite grep-Match sehr stark!

## Lab: Username enumeration via response timing

_This lab is vulnerable to username enumeration using its response times. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page._

### Durchführung

- Login-Versuch mit der Username-Liste
    - IP-Adresse wird gesperrt
    - Hinweis auf zu setzenden Header ('X-Forwarded-For')
        - _If an application trusts an HTTP request header like X-Forwarded-For to accurately specify the remote IP address of the connecting client, then malicious clients can spoof their IP address. This behavior does not necessarily constitute a security vulnerability, however some applications use client IP addresses to enforce access controls and rate limits._
        - Header einfach per Rammbock-Attacke gleich wie Username setzen
    - Response-Time ist trotzdem nichtsaussagend
    - Kurz drüber nachdenken:
        - Die Response-Time wird länger, je nachdem wie viel geprüft wird\
        - Ist der Username richtig, geht es mit dem Passwort weiter\
            - Passwort sehr lang setzen -> lange Response-Time\
- Ähnlich bei Passwort
    - auf den Status-Code achten -> muss ein 302 Redirect sein

### Ergebnisse

- Username: Info (_hat die längste Response-Time_)
    -> Beim nächsten mal vielleicht einen bekannten User mit in die Wordlist setzen, um zu sehen, ob sich die Response-Times ähneln\
- 

### Folgerung