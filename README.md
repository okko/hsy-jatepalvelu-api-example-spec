# Jätepalvelun rajapintatunnus

Kiinteistön jätepalvelutunnuksella ja postinumerolla voi tehdä jätepalveluihin muutoksia, joten jätepalvelutunnus on luottamuksellinen tieto. Sen vuoksi rajapinnasta ei voi suoraan kysellä tietoja jätepalvelutunnuksella ja postinumerolla, vaan avaimena käytetään erillistä jätepalvelun rajapintatunnusta. Jätepalvelun rajapintatunnus on noudettavissa HSY:n verkkopalvelusta sisäänkirjautumisen jälkeen, eikä ulkopuolinen voi päätellä siitä kiinteistön jätepalvelutunnusta tai postinumeroa.

### Miten HSY voisi muodostaa jätepalvelun rajapintatunnuksen
HSY voisi muodostaa jätepalvelun rajapintatunnuksen esim.
```
echo 'BB11-012345-6:00100' | openssl enc -aes-256-cbc -a -salt
U2FsdGVkX1+rozkAyHFzbNjASdX0uamvwU84aMouTgfyy5itMcxF+QvQoTwD5GUL
```
ja purkaa sen takaisin esim.
```
echo 'U2FsdGVkX1+rozkAyHFzbNjASdX0uamvwU84aMouTgfyy5itMcxF+QvQoTwD5GUL' | openssl enc -d -aes-256-cbc -a
BB11-012345-6:00100
```
Salausavainta tai avaimen purkulogiikkaa ei saa antaa HSY:n ulkopuolelle. Rajapinnan käyttäjän ei tarvitse tietää miten rajapintatunnus on laskettu.

# Esimerkkikysely

`GET https://api.hsy.fi/jatepalvelu/v1/schedule?idVersion=1&id=U2FsdGVkX1%2BrozkAyHFzbNjASdX0uamvwU84aMouTgfyy5itMcxF%2BQvQoTwD5GUL&locale=fi_FI`

# Esimerkkivastaus
```
{  
  id: "Sijaintipaikka 1",
  types: [
    {
      type: "Kartonki",
      weekdays: ["maanantai", "torstai"],
      next: "2020-05-21",
      previous: "2020-05-18"
    },
    {
      type: "Sekajäte",
      weekdays: ["tiistai", "perjantai"],
      next: "2020-05-19",
      previous: "2020-05-17"
    },
    {
      type: "Lasi",
      weekdays: ["keskiviikko"],
      next: "2020-06-10",
      previous: "2020-05-10"
    },
    {
      type: "Metalli",
      weekdays: ["keskiviikko"],
      next: "2020-06-10",
      previous: "2020-05-10"
    },
    {
      type: "Muovi",
      weekdays: ["torstai"],
      next: "2020-05-25",
      previous: "2020-05-15"
    },
    {
      type: "Biojäte",
      weekdays: ["tiistai"],
      next: "2020-05-19",
      previous: "2020-05-15"
    }
  ]
}
```
