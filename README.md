# ☕ Home Connect Morgenkaffe

**Våkne opp til nybrygget kaffe fra din Home Connect-maskin.**

Denne automasjonen (Blueprinten) skal håndtere hele "Nattmodus"-syklusen for kaffemaskiner fra Siemens, Bosch, Neff og Gaggenau. Den omgår maskinens auto-av-timer, holder maskinen våken gjennom natten (ved hjelp av en smart "trippel-dans" keep-alive logikk), og brygger favorittkaffen din nøyaktig når du ønsker det.
Jeg har laget Blueprinten for at kanskje andre også kan ha glede av en kopp ferdig om morgenen.


**✨ Ettersom jeg kun har en Bosch Kaffemaskin CTL836EC6, er det kun denne maskinen jeg får testet det på**


---

## 📥 Importer Blueprints

Klikk på knappen for å importere versjonen som passer ditt behov direkte inn i Home Assistant.

### Norsk Versjon

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/stiglinga/ha-home-connect-morgenkaffe-norsk/blob/main/home_connect_morgenkaffe_norsk.yaml)

---

## ⚙️ Forutsetninger (Påkrevde Hjelpere)

Før du importerer, **MÅ** du opprette disse 4 hjelperne i Home Assistant (`Innstillinger` -> `Enheter og tjenester` -> `Hjelpere`).
I tilleg må du ha satt opp integrasjon mot Home Connect i Home Assistant (https://www.home-assistant.io/integrations/home_connect/).

**⚠️ Viktig:** ID-en på hjelperne (Entity ID) må være **NØYAKTIG** som vist under for at den norske versjonen skal fungere.

| Navn på Hjelper (Eksempel) | Type | **Entity ID (Påkrevd for Norsk versjon)** |
| :--- | :--- | :--- |
| **Kaffe Start** | Knapp (Button) | `input_button.kaffe_start` |
| **Kaffe Nattmodus** | Veksle (Boolean) | `input_boolean.kaffe_nattmodus` |
| **Kaffe Start Tid** | Dato og/eller tid | `input_datetime.kaffe_start_tid` |
| **Kaffe Favoritt** | Tekst (Text) | `input_text.kaffe_favoritt` |


---

## 🚀 Hvordan bruke den

### Enkel Modus (Tidsstyrt)
1.  Legg til **Start-knappen** (`input_button.kaffe_start`) på Dashboardet ditt.
2.  Trykk på knappen når du gjør maskinen klar for kvelden (sjekk at kopp står klar og vanntank er full).*
3.  Maskinen skyller og slår seg av (dersom på), og slår seg på og skyller igjen (dersom av).
4.  Du vil motta et varsel på mobilen.
5.  Velg ønsket drikke og tidspunkt (f.eks. 07:00).
6.  Sov godt! 😴

*Årsaken til av og på sekvens, er for å sikre at maskinen får skylt gjennom systemet minst en gang i løpet av døgnet.

### Avansert Modus (Sensorstyrt)
Du kan konfigurere blueprinten til å aktivere **Alternative Triggere**.
1.  I Blueprint-innstillingene, huk av for "Aktiver Alternative Triggere".
2.  Velg dine sensor-entiteter (f.eks. `sensor.iphone_neste_alarm`, `binary_sensor.bevegelse_kjokken`, `input_button.morgen_scene`).
3.  Når du armerer systemet på kvelden, vil du få et ekstra spørsmål: *"Hvordan skal kaffen starte?"*.
4.  Hvis du velger en trigger (f.eks. "Bevegelse"), venter systemet på den spesifikke hendelsen i stedet for et klokkeslett.

---

## 🔧 Tekniske Detaljer
* **Keep-Alive:** Automasjonen veksler maskinen mellom Kaffe- og Espresso-modus hver 2. time for å hindre at maskinens egen auto-av funksjon slår den av.
* **Sikkerhet:** Hvis maskinen slås av manuelt eller går tom for vann (status blir unavailable/off), deaktiveres automasjonen umiddelbart for å hindre uhell.
* **Skjult Logikk:** All logikk og mellomlagring håndteres via den skjulte `input_text`-hjelperen, noe som holder dashboardet ditt ryddig.

---

## 🤝 Utvikling

* **Konsept & Testing:** Utviklet og testet på grunnlag av tidligere lagde automasjoner av meg.
* **Blueprint Logikk & Arkitektur:** har jeg benyttet stor grad av AI og da særlig **Gemini (Google DeepMind)**. 🤖✨

---
*Ansvarsfraskrivelse: Bruk på eget ansvar. Sørg for at koppen din er stor nok!*
