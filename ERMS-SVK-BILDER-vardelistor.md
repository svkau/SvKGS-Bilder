# Värdelistor

Version 1.0

## ERMS-SVK-BILDER-värdelista 1 - Typ av identifikator

| **Giltiga värden**  | **Kommentar**                           | **Källa**        |
|---------------------|-----------------------------------------|------------------|
| aid                 | ArkivbildarID                           | ERMS-SVK         |
| arkivbildare        | Arkivbildarens namn                     | ERMS-SVK         |
| organisationsnummer | Tio siffror utan bindestreck            | ERMS-SVK         |
| ärendenummer        | Ärendets beteckning (t.ex. F 2020-0435) | ERMS-SVK         |
| uuid                | Ett genererat UUID                      | ERMS-SVK-BILDER  |

## ERMS-SVK-BILDER-värdelista 2 - Klassificeringsstruktur

| **Giltiga värden** | **Kommentar**                                  | **Källa** |
|--------------------|------------------------------------------------|-----------|
| KlaSL2016_1.0      | Klassificeringsstruktur för lokal nivå 1.0     | ERMS-SVK  |
| KlaSN2018_1.0      | Klassificeringsstruktur för nationell nivå 1.0 | ERMS-SVK  |
| KlaSS2016_1.0      | Klassificeringsstruktur för regional nivå 1.0  | ERMS-SVK  |

## ERMS-SVK-BILDER-värdelista 3 - XML-dokumentets status

| **Giltiga värden** | **Kommentar** | **Källa** |
|--------------------|---------------|-----------|
| cancelled          |               | ERMS      |
| created            |               | ERMS      |
| deleted            |               | ERMS      |
| derived            |               | ERMS      |
| new                |               | ERMS      |
| revised            |               | ERMS      |
| unknown            |               | ERMS      |
| updated            |               | ERMS      |

## ERMS-SVK-BILDER-värdelista 4 - Typ av ID

| **Giltiga värden**   | **Kommentar**                           | **Källa** |
|----------------------|-----------------------------------------|-----------|
| aid                  | ArkivbildarID                           | ERMS-SVK  |
| organisationsnummer  | Tio siffror utan bindestreck            | ERMS-SVK  |

## ERMS-SVK-BILDER-värdelista 5 - Typ av aktör, agentType

| **Giltiga värden** | **Kommentar**                               | **Källa**        |
|--------------------|---------------------------------------------|------------------|
| agent              | Används i betydelsen "Annan aktör".         | ERMS-            |
| photographer       | Fotograf.                                   | ERMS-SVK-BILDER  |

## ERMS-SVK-BILDER-värdelista 6 - Typ av idNumber

| **Giltiga värden**  | **Kommentar**                                              | **Källa** |
|---------------------|------------------------------------------------------------|-----------|
| username            | Personens användarnamn i kyrkans behörighetssystem.        | ERMS-SVK  |
| organisationsnummer | Tio siffror utan bindestreck.                              | ERMS-SVK  |
| personnummer        | Personens personnummer.<br/>Tolv siffror utan bindestreck. | ERMS-SVK  |

## ERMS-SVK-BILDER-värdelista 7 - Handlingstyp

| **Giltiga värden**   | **Kommentar** | **Källa** |
|----------------------|---------------|-----------|
| bild                 |               | ERMS-SVK  |

## ERMS-SVK-BILDER-värdelista 8 - Form

| **Giltiga värden**   | **Kommentar**      | **Källa** |
|----------------------|--------------------|-----------|
| physical             |                    | ERMS      |
| digitial             |                    | ERMS      |
| physical_and_digital | Stavfel i ERMS.xsd | ERMS      |

## ERMS-SVK-BILDER-värdelista 9 - Datum

| **Giltiga värden** | **Kommentar**                | **Källa** |
|--------------------|------------------------------|-----------|
| created            |                              | ERMS      |
| modified           | I betydelsen "senast ändrad" | ERMS      |
