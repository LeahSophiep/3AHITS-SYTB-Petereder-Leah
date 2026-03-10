# Arbeitsbericht

- **Name:** Leah Petereder
- **Klasse:** 3AHITS
- **Datum:** 10.3.2026
- **Fach:** SYTB
- **Thema:** Curl
- **Aufgabenstellung:** [cURL
Grundlagen UNIX shell](https://www.franzmatejka.at/htl/doc/ITSI_2_linux/13_curl.html)

---
## Inhaltsverzeichnis
```
1. curl example.com
2. Seite mit HTTP-Response-Header abrufen
3. Verbose Mode mittels curl
4. HTTP Status Code
5. Geschlechtsschätzung
6. Wetterinformationen in Braunau und Funchal
7. Mit Jq formatieren
8. Welche Stadt im Wetterbeispiel?
```


# Aufgaben

## 1. curl example.com

- **Rufe die Startseite von example.com mit curl ab. Du siehst den HTML Code der Seite im Terminal. Vergleiche dazu die Ansicht im Web-Browser.**

In Kali den command `curl https://example.com` eingeben und man bekommt in der Ausgabe dadurch einen HTML-Text:
```
<!doctype html><html lang="en"><head><title>Example Domain</title><meta name="viewport" content="width=device-width, initial-scale=1"><style>body{background:#eee;width:60vw;margin:15vh auto;font-family:system-ui,sans-serif}h1{font-size:1.5em}div{opacity:0.8}a:link,a:visited{color:#348}</style></head><body><div><h1>Example Domain</h1><p>This domain is for use in documentation examples without needing permission. Avoid use in operations.</p><p><a href="https://iana.org/domains/example">Learn more</a></p></div></body></html>
```

Danach geht man auf die Webseite `https://example.com` und vergleicht die Ansicht mit dem HTML Code:
```
Example Domain

This domain is for use in documentation examples without needing permission. Avoid use in operations.

Learn more
```

## 2. Seite mit HTTP-Response-Header abrufen

- **Rufe dieselbe Seite wie in Aufgabe 1 auf, aber gib zusätzlich den HTTP-Response-Header aus. Hinweis: Es gibt dafür eine eigene curl-Option.
Du siehst dann sogenannte Meta-Informationen, das sind Informationen über die Web-Site (z.B.date, content-type) und den Server – die aber vom Browser nicht angezeigt werden.**

Um den HTTP-Response Header mit auszugeben muss man im Terminal den Command:
`curl -i https://example.com`eingeben.

Die Ausgabe sieht dann so aus:

```
HTTP/2 200 
date: Tue, 10 Mar 2026 07:04:02 GMT
content-type: text/html
cf-ray: 9da0768748ad5b66-VIE
last-modified: Thu, 05 Mar 2026 11:54:13 GMT
allow: GET, HEAD
accept-ranges: bytes
age: 1614
cf-cache-status: HIT
server: cloudflare

<!doctype html><html lang="en"><head><title>Example Domain</title><meta name="viewport" content="width=device-width, initial-scale=1"><style>body{background:#eee;width:60vw;margin:15vh auto;font-family:system-ui,sans-serif}h1{font-size:1.5em}div{opacity:0.8}a:link,a:visited{color:#348}</style></head><body><div><h1>Example Domain</h1><p>This domain is for use in documentation examples without needing permission. Avoid use in operations.</p><p><a href="https://iana.org/domains/example">Learn more</a></p></div></body></html>
```

Hier kann man sehen, dass zuerst der Header und dann der HTML Code ausgegeben wird.

Im Header kann man sehen, ob die Anfrage erfolgreich war, wann der Server geantwortet hat. Die Art des Inhalts, die Größe der Antwort. Die Webserver-Software.

## 3. Verbose Mode mittels curl

- **Verbose Mode. Rufe eine beliebige URL auf und aktiviere den Verbose Mode, sodass Request, Response und Header sichtbar sind.**

Ich nehme als Beispiel **SHEIN** her.

Im Kali muss man jetzt den Command `curl -v https://shein.com` eingeben und bekommt daraus dann:
```
* Host shein.com:443 was resolved.
* IPv6: (none)
* IPv4: 52.39.206.44, 52.39.90.56
*   Trying 52.39.206.44:443...
* ALPN: curl offers h2,http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_128_GCM_SHA256 / x25519 / RSASSA-PSS
* ALPN: server did not agree on a protocol. Uses default.
* Server certificate:
*  subject: C=SG; L=Singapore; O=ROADGET BUSINESS PTE. LTD.; CN=*.shein.com
*  start date: Feb 25 00:00:00 2026 GMT
*  expire date: Aug 25 23:59:59 2026 GMT
*  subjectAltName: host "shein.com" matched cert's "shein.com"
*  issuer: C=US; O=DigiCert, Inc.; CN=DigiCert Secure Site OV G2 TLS CN RSA4096 SHA256 2022 CA1
*  SSL certificate verify ok.
*   Certificate level 0: Public key type RSA (2048/112 Bits/secBits), signed using sha256WithRSAEncryption
*   Certificate level 1: Public key type RSA (4096/152 Bits/secBits), signed using sha256WithRSAEncryption
*   Certificate level 2: Public key type RSA (2048/112 Bits/secBits), signed using sha256WithRSAEncryption
* Connected to shein.com (52.39.206.44) port 443
* using HTTP/1.x
> GET / HTTP/1.1
> Host: shein.com
> User-Agent: curl/8.13.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 301 Moved Permanently
< Server: openresty
< Date: Tue, 10 Mar 2026 07:12:15 GMT
< Content-Type: text/html
< Content-Length: 166
< Connection: keep-alive
< Location: https://www.shein.com/
< 
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
```

Die Ausgabe zeigt die Verbindungsinformationen, in diesem Fall sind das TLS-Verbindungen. Es zeigt auch die Request und die Response und wieder den HTML-Inhalt der Seite.

## 4. HTTP Status Code

- **curl auf mit der Option aus der vorangegangenen Aufgabenstellung. Recherchiere Was bedeutet dieser http Status Code? Was zeigt ein Web-Browser bei dieser URL an?**

Bei **SHEIN** ist es hier wie bei vielen größeren Webseiten, dass man weitergeleitet wird, da es länderübergreifende Webseiten sind. Dafür steht hier aus der Ausgabe `
```
* Request completely sent off
< HTTP/1.1 301 Moved Permanently
```
Also man wird hierbei auf eine neue URL geleitet.

## 5. Geschlechtsschätzung

- **Geschlechtsschätzung anhand von Namen. Lade https://api.genderize.io mit curl → du bekommst eine Fehlermeldung. Ein Parameter wird an die URL so angefügt: ?name=value. Ermittle das wahrscheinliche Geschlecht von: Noor, Ariel, Amina, Elowen, Levin. Hinweis: verwende Quotes ("<URL>") in der curl Kommandozeile, da ? in der shell eine spezielle Bedeutung hat.
Das Datenformat, das hier vom Server gesendet wird, ist JSON. Ganz viele Web-APIs verwenden JSON. Verwende die Option zum Anzeigen des Response-Headers und suche darin nach einem Hinweis auf dieses Datenformat.**

Hier muss man beisielsweise auf die Seite `"https://api.genderize.io"` und baut das in den Code ein und gibt jeweils jeden Namen einzelnd aus.
Bei Noor beispielsweise sieht die Ausgabe jetzt so aus:
```
HTTP/2 200 
server: nginx/1.16.1
date: Tue, 10 Mar 2026 07:24:58 GMT
content-type: application/json; charset=utf-8
content-length: 67
vary: accept-encoding
cache-control: max-age=0, private, must-revalidate
x-request-id: GJtqEKfOfxbkJOPjRQ3D
access-control-allow-credentials: true
access-control-allow-origin: *
access-control-expose-headers: x-rate-limit-limit,x-rate-limit-remaining,x-rate-limit-reset
x-rate-limit-limit: 100
x-rate-limit-remaining: 98
x-rate-limit-reset: 59702

{"count":167923,"name":"Noor","gender":"female","probability":0.61}   
```
Das bedeutet Noor ist **female**

Nun gibt man den Comman für alle ein und ändert nur den Namen.

**Ariel:** 
`{"count":74669,"name":"Ariel","gender":"male","probability":0.83} ` ist ein Mann

**Amina:** 
`{"count":198519,"name":"Amina","gender":"female","probability":0.96}` ist eine Frau.

**Elowen:** 
`{"count":23,"name":"Elowen","gender":"female","probability":0.87}` ist eine Frau.

**Levin:**`{"count":3186,"name":"Levin","gender":"male","probability":0.96}` ist ein Mann.

Das Datenformat ist dadurch erkennbar, dass oben im Header die Zeile `content-type: application/json; charset=utf-8`angezeigt wird.

## 6. Wetterinformationen in Braunau und Funchal

- **In einer URL sind auch mehrere Parameter möglich – diese sind mit einem & getrennt:
?para1=value1&para2=value2.
Aufgabe: Unter dem API Endpoint https://api.open-meteo.com/v1/forecast gibt es Wetter Informationen. Die notwendigen Parameter sind latitude, longitude, und current_weather (Wetter-Beispiel). Verwende diese API um die aktuelle Wetterinformation für Braunau und für Funchal abzurufen**

Zuerst sollte man die Latitude und Longitude von diesen zwei Städten herausfinden.

Hierfür kann man einfach auf Google suchen und bekommt dann diese Antworten:

**Braunau:**
- Latitude: 48.25628
- Longitude: 13.04343

**Funchal:**
- Latitude: 32.63333
- Longitude: -16.9

**Braunau**

Danach gibt man diesen Befehl als Command ein:
`curl "https://api.open-meteo.com/v1/forecast?latitude=48.25628&longitude=-13.04343&current_weather=true"`, indem man die latitude und longitude entsprechend einsetzt.
 und bekommt dann als Ausgabe:
 ```
{"latitude":48.249733,"longitude":-13.037582,"generationtime_ms":1.296401023864746,"utc_offset_seconds":0,"timezone":"GMT","timezone_abbreviation":"GMT","elevation":0.0,"current_weather_units":{"time":"iso8601","interval":"seconds","temperature":"°C","windspeed":"km/h","winddirection":"°","is_day":"","weathercode":"wmo code"},"current_weather":{"time":"2026-03-10T07:45","interval":900,"temperature":12.1,"windspeed":36.0,"winddirection":269,"is_day":1,"weathercode":51}}       
 ```

 **Funchal**

 Dasselbe jetzt für Funchal:
 `curl "https://api.open-meteo.com/v1/forecast?latitude=32.63333&longitude=-16.9&current_weather=true"`

 Die Ausgabe:
```
{"latitude":32.6875,"longitude":-16.8125,"generationtime_ms":0.07772445678710938,"utc_offset_seconds":0,"timezone":"GMT","timezone_abbreviation":"GMT","elevation":0.0,"current_weather_units":{"time":"iso8601","interval":"seconds","temperature":"°C","windspeed":"km/h","winddirection":"°","is_day":"","weathercode":"wmo code"},"current_weather":{"time":"2026-03-10T07:45","interval":900,"temperature":13.9,"windspeed":16.5,"winddirection":23,"is_day":1,"weathercode":2}} 
```

# 7. Mit Jq formatieren

- **JSON-Ausgaben sind kompakt und daher manchmal sehr schwer zu lesen. Pipe die Ausgabe von curl in das Tool jq, um zu formatieren.**

Dies erreicht man indem wir jetzt erstaml sudo jq installieren mit dem Command `sudo apt install jq`  und jetzt nehmen wir beispielsweise die Ausgabe von Funchal und setzen hinter den curl Command noch ein `|jq`, das sieht dann so aus:

`curl "https://api.open-meteo.com/v1/forecast?latitude=32.63333&longitude=-16.9&current_weather=true"|jq`

Die Ausgabe ist nun schön formatiert:
```
{
  "latitude": 32.6875,
  "longitude": -16.8125,
  "generationtime_ms": 0.06890296936035156,
  "utc_offset_seconds": 0,
  "timezone": "GMT",
  "timezone_abbreviation": "GMT",
  "elevation": 0.0,
  "current_weather_units": {
    "time": "iso8601",
    "interval": "seconds",
    "temperature": "°C",
    "windspeed": "km/h",
    "winddirection": "°",
    "is_day": "",
    "weathercode": "wmo code"
  },
  "current_weather": {
    "time": "2026-03-10T07:45",
    "interval": 900,
    "temperature": 13.9,
    "windspeed": 16.5,
    "winddirection": 23,
    "is_day": 1,
    "weathercode": 2
  }
```

## 8. Welche Stadt im Wetterbeispiel?

- **Um welche Stadt handelt es sich im Wetter-Beispiel? Verwende den API Endpoint https://api-bdc.io/data/reverse-geocode-client um das herauszufinden.**

Das Wetter-Beispiel in der Aufgabenstellung sieht so aus:
```
{"latitude":35.7,"longitude":139.6875,"generationtime_ms":479.18224334716797,"utc_offset_seconds":0,"timezone":"GMT","timezone_abbreviation":"GMT","elevation":40.0,"current_weather_units":{"time":"iso8601","interval":"seconds","temperature":"°C","windspeed":"km/h","winddirection":"°","is_day":"","weathercode":"wmo code"},"current_weather":{"time":"2026-03-10T08:00","interval":900,"temperature":6.6,"windspeed":5.4,"winddirection":42,"is_day":1,"weathercode":0}}
```
Hieraus nimmt man die latitude und longitude Zahlen.

- **latitude:** 35.7
- **longitude:** 139.6875

Man nimmt also den **reverse geocode client** her und setzt nur die latitude und longitude ein.

Der Command ist somit: `curl "https://api-bdc.io/data/reverse-geocode-client?latitude=35.7&longitude=139.6875"|jq`

Jq einfach nur damit es wieder schön formatiert ist.

Die Ausgabe sieht so aus:
```
{
  "latitude": 35.7,
  "lookupSource": "coordinates",
  "longitude": 139.6875,
  "localityLanguageRequested": "en",
  "continent": "Asia",
  "continentCode": "AS",
  "countryName": "Japan",
  "countryCode": "JP",
  "principalSubdivision": "Tokyo",
  "principalSubdivisionCode": "JP-13",
  "city": "Tokyo",
  "locality": "Nakano",
  "postcode": "",
  "plusCode": "8Q7XPM2Q+22",
  "localityInfo": {
    "administrative": [
      {
        "name": "Japan",
        "description": "island country in East Asia",
        "isoName": "Japan",
        "order": 3,
        "adminLevel": 2,
        "isoCode": "JP",
        "wikidataId": "Q17",
        "geonameId": 1861060
      },
      {
        "name": "Kanto region",
        "description": "one of 8 regions in Japan encompassing 8 prefectures",
        "order": 5,
        "adminLevel": 3,
        "wikidataId": "Q132480"
      },
      {
        "name": "Tokaido",
        "description": "Japanese geographical term",
        "order": 6,
        "adminLevel": 3,
        "wikidataId": "Q1196306"
      },
      {
        "name": "Tokyo",
        "description": "capital and largest city of Japan",
        "order": 7,
        "adminLevel": 4,
        "wikidataId": "Q1490",
        "geonameId": 1850147
      },
      {
        "name": "Tokyo",
        "description": "capital and largest city of Japan",
        "isoName": "Tokyo",
        "order": 8,
        "adminLevel": 4,
        "isoCode": "JP-13",
        "wikidataId": "Q1490",
        "geonameId": 1850144
      },
      {
        "name": "Musashi Province",
        "description": "former province of Japan",
        "order": 9,
        "adminLevel": 4,
        "wikidataId": "Q907398"
      },
      {
        "name": "Shinjuku",
        "description": "special ward in the Tokyo Metropolis, Japan",
        "order": 11,
        "adminLevel": 7,
        "wikidataId": "Q179645",
        "geonameId": 11790353
      },
      {
        "name": "Nakano",
        "description": "special ward in the Tokyo Metropolis in Japan",
        "order": 12,
        "adminLevel": 7,
        "wikidataId": "Q234087",
        "geonameId": 8715035
      }
    ],
    "informative": [
      {
        "name": "Asia",
        "description": "terrestrial continent, mainly in the northeastern quadrant",                                                                      
        "isoName": "Asia",
        "order": 1,
        "isoCode": "AS",
        "wikidataId": "Q48",
        "geonameId": 6255147
      },
      {
        "name": "Asia/Tokyo",
        "description": "time zone",
        "order": 2
      },
      {
        "name": "Honshu",
        "description": "largest island of Japan",
        "order": 4,
        "wikidataId": "Q13989",
        "geonameId": 1862185
      },
      {
        "name": "special ward of Japan",
        "description": "administrative division of Japan",
        "order": 10,
        "wikidataId": "Q5327704"
      }
    ]
  }
}
```

Also die Antwort zu der Aufgabe ist, die Stadt des Wetter-Beispiels ist: **Tokyo**