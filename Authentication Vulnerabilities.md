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
    - Rammbock-Attacke
    - auf den Status-Code achten -> muss ein 302 Redirect sein

### Ergebnis

- Username: Info (_hat die längste Response-Time_)
    - Beim nächsten mal vielleicht einen bekannten User mit in die Wordlist setzen, um zu sehen, ob sich die Response-Times ähneln
- Passwort: jordan

### Folgerung

- Status-Code ist wichtig (und logisch)
- künstliche Verlängerung der Response-Time durch langen String, der beim Verarbeiten deutlich länger braucht
- IP-Spoofing kann wichtig sein

## Lab: Broken brute-force protection, IP block

_This lab is vulnerable due to a logic flaw in its password brute-force protection. To solve the lab, brute-force the victim's password, then log in and access their account page._

### Durchführung

- Nutzen der beiden Wordlists
- Nach jedem erfolglosen Versuch muss einmal ein erfolgreicher Versuch stattfinden
    - durch Benutzen der eigenen validen Credentials
- neue Wordlists
    - Usernames: Meiner, dann Carlos, meiner, dann Carlos, ...
    - Passwords: Meins, eins aus der Liste, meins, eins aus der Liste ...

### Ergebnis

- Passwort: aaaaaa

### Folgerung

- IP-Blocking _kann_ resettet werden, indem ein erfolgreicher Login stattgefunden hat
    - Angriffe so bauen, dass nach jedem Versuch ein erfolgreicher Login mit vorher erstellten Zugangsdaten stattfindet

## Lab: Username enumeration via account lock

_This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page._

### Durchführung:

- Benutzen der Username-Wordlist
- Setzen einer Payload von 5 für das Passwortparameter
- Idee:
    - Nicht vorhandene Usernames werden mit einer anderen Response ausgegeben als valide Usernames
    - Invalid username or password vs. too many login attempts
    - too many login attempts -> User existiert
- Beim Passwort kann dann wieder auf Sniper-Attack gewechselt werden
    - In Kombination mit Grep-Extract, da ich nach einem bestimmten String suche bzw. nach seiner Abwesenheit
    - Username ist fix gesetzt, Passwort anhand der Liste

### Ergebnis:

- Username: atlanta
- Passwort: 159753

### Folgerung:

- BurpSuite Community dauert länger als der Time Out gültig ist -> kleinere Häppchen bei den Usernamen ausprobieren
- Grep Extract -> _Response extraction rules are used in various locations within Burp, to define the location within a response of a varying item that needs to be extracted._
- Mitteilung direkt im Webservice können ziemlich wichtig sein
- Herausfinden, wann der Login-Timeout einsetzt

## Lab: 2FA simple bypass

### Durchführung

- Beobachten, was passiert, wenn ich mich mit validen Credentials anmelde -> /login2 -> /my-account
- Victim-Credentials nehmen
    - in der URL das Verzeichnis wechseln

### Ergebnis

- Lab solved

### Folgerung

- 2FA durch Verzeichnisangabe umgehen
    - Logik der Website verstehen!!!

## Lab: 2FA broken logic

_This lab's two-factor authentication is vulnerable due to its flawed logic. To solve the lab, access Carlos's account page._

### Durchführung

- Zunächst Logik der Seite verstehen
- nach Login mit validen Credentials verify= Cookie auf Victim setzen
- 4 digit Code bruteforcen 

### Ergebnis

- Erstmal übersprungen, weil ohne BurpSuite Pro kaum lösbar in unter 10 Jahren

### Folgerung

- Cookies wieder mal sehr wichtig
- Cookies, wenn vulnerabel, händisch ändern und bei der Request mitgeben


TESTETSTETSTETSTETSTE