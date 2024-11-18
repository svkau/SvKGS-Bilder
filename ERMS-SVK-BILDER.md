# SvKGS-Bilder

***Version 0.1***

# Innehåll

- 1 [Inledning](#1-inledning)
  - 1.1 [Arkivpaket](#11-arkivpaket)
- 2 [Specifikationer för ärendehandlingar](#2-specifikationer-för-ärendehandlingar)
  - 2.2 [XML-dokumentet](#22-xml-dokumentet)
  - 2.3 [Värdelistor](#23-värdelistor)
  - 2.4 [Scheman](#24-scheman)
  - 2.5 [Datatyper](#25-datatyper)
  - 2.6 [Råd om användandet av *SvKGS Ärendehandlingar*](#26-råd-om-användandet-av-svkgs-ärendehandlingar)
- 3 [Dataelement med exempel](#3-dataelement-med-exempel)
  - 3.1 [Övergripande information om XML-dokumentet](#31-övergripande-information-om-xml-dokumentet)
  - 3.2 [Element som används för information om både ärendeakter och handlingar](#32-element-som-används-för-information-om-både-ärendeakter-och-handlingar)
  - 3.3 [Information om ärendeakter](#33-information-om-ärendeakter)
  - 3.4 [Information om ärendehandlingar](#34-information-om-ärendehandlingar)
  - 3.5 [Information om bifogade filer](#35-information-om-bifogade-filer)

# 1. Inledning

*Svenska kyrkans gemensamma specifikationer för elektronisk arkivering* beskriver vilken information som ska
ingå vid leverans till Svenska kyrkans gemensamma e-arkiv och hur denna information ska struktureras.

Leveranser till e-arkivet delas in i informationstyper. Exempel på sådana kan vara ärendeakter med handlingar,
ekonomisk redovisning, löneredovisning, personalakter, information om gravrätter, projekthandlingar, bilder
och så vidare. Varje informationstyp kan behöva sin egen specifikation.

Beteckningen gemensamma specifikationer anger att specifikationerna gäller alla leveranser till e-arkivet oavsett
vem det är som levererar informationen och oavsett vilket IT-system som leveranser kommer ifrån.
Genom att informationen arkiveras på detta standardiserade sätt underlättas det långsiktiga bevarande
och möjligheten att återsöka den arkiverade informationen. Standardformatet kan utöver e-arkivering
även användas vid migrering av information mellan andra IT-system.

Svenska kyrkans gemensamma specifikationer är i första hand anpassningar av de specifikationer som
förvaltas av *the Digital Information LifeCycle Interoperability Standards Board* (DILCIS Board).
De kan också vara anpassningar av de förvaltningsgemensamma specifikationer (FGS) som har upprättats av Riksarkivet.
Specifikationerna kan också utgå ifrån andra standarder, om det finns några som är särskilt lämpliga
för informationstypen i fråga.

- [Dilcis Board](https://dilcis.eu)
- [Riksarkivet FGS](https://riksarkivet.se/fgs-earkiv)

## 1.1. Arkivpaket

Leverans av information till e-arkivet sker i form av leveranspaket. Ett paket är en mappstruktur med filer som samlas i en arkivfil, t.ex. ZIP och TAR. Paketet innehåller den levererade informationen, arkivobjektet, men också metadata som beskriver informationen och den levererande arkivbildaren.

Svenska kyrkans utformning av leveranspaket (SIP) utgår från Riksarkivets specifikation [FGS Paketstruktur 1.2](https://riksarkivet.se/Media/pdf-filer/doi-t/FGS_Paketstruktur_RAFGS1V1_2.pdf) men är anpassad efter egna behov. Efter mottagande i e-arkivet omformas paketet till ett arkivpaket (AIP) som är helt i enlighet med FGS Paketstruktur 1.2. Det finns en plan att övergå till version 2.0 av Riksarkivets FGS så snart det är möjligt.

Specifikationerna i det här dokumentet beskriver arkivobjektet, det vill säga den information som
ska arkiveras. Det utgör endast en del av hela arkivpaketet. För mer information om leveranspaket,, se [SvKGS-Leveransbeskrivning](https://github.com/svkau/SvKGS-Leveransbeskrivning/blob/main/SvKGS-Leveransbeskrivning.md#svkgs-leveransbeskrivning)

# 2. Specifikationer för bilder

*SvKGS Bilder* avser arkivering av digitala bilder.
Specifikationerna är främst avsedda för amatörfotografier som har tagits i församlingsverksamheten för att dokumentera händelser av olika slag.
Bilder som har tagits fram i ett mer specialiserat syfte, t.ex. ritningar, kartor och bilder för inventarieförteckningar kräver troligen en
annan uppsättning av metadata än den *SvKGS Bilder* kan erbjuda.

Registrerad information om en bild bevaras i ett XML-dokument som
regleras av specifikationerna genom användandet av scheman (XSD och Schematron).

*SvKGS Bilder* kräver också att viss metadata sparas inbäddade i bildfilen i formatet [XMP](https://www.adobe.com/devnet/xmp.html).
Se avsnittet [Metadata i XMP-format](#26-metadata-i-xmp-format) nedan.

*SvKGS Bilder* följer helt och hållet *Specification for the E-ARK Content Information Type
Specification for Electronic Records Management Systems* (ERMS) version 2.1.0.
Detta innebär att specifikationen också följer [FGS Ärendehantering 2.0](https://www.riksarkivet.se/faststallda-kommande-fgser)
och [Riksarkivets tillämpning av CITS ERMS (för överlämnande till Riksarkivet)](https://www.riksarkivet.se/Media/pdf-filer/doi-t/Riksarkivets_tillampning_CITS_ERMS_overlamnande_V1.0.pdf). 

ERMS tillåter att man gör anpassningar för den egna organisationens behov.
För användning i Svenska kyrkan har ett antal anpassningar gjorts.
Dessa redovisas nedan i detta dokument.

## 2.2. XML-dokumentet

Det XML-dokument som innehåller information bilder definieras i ett XML-schema.
Se avsnittet [Scheman](#24-scheman) nedan. Detta är XML-dokumentets grundläggande uppbyggnad:


- erms (1...1)
    - control (1...1)
    - records (1...1)
      - record (1...n)
      	- appendix (1...1)


Notera att elementet `aggragation` inte används i specifikationen. Varje enskild bild betraktas som ett `record`, och bilderna leveras löpande
utan någon form av aggregering.

Elementet `erms` är dokumentets rot-element. Elementet `control` innehåller underelement med information om
själva XML-dokumentet (se avsnitt [3.1. Övergripande information om XML-dokumentet](#31-övergripande-information-om-xml-dokumentet)).

Elementet `records` rymmer underelement av typen `record`, vilket i det här fallet betyder bild.
(se avsnitt [3.3. Information om ärendeakter](#33-information-om-ärendeakter)).

Varje `record` kan innehålla flera elementet av typen `appendix` som är en bifogad bildfil till den registrerade bilden.
(se avsnitt [3.5. Information om bifogade filer](#35-information-om-bifogade-filer)).

Observera att det tillagda elementet `svkAppendix` används i *SvKGS Bilder* i stället för ERMS-elementet `appendix`.

Till varje `record` får endast *en* fil kopplas (det är en anpassning av ERMS-standrad).

I elementlistorna nedan finns de element som bör eller måste finnas i ett XML-dokument enligt *SvKGS Ärendehandlingar*.

- [Elementlista 1. Kontroll](#elementlista-1-kontroll)
- [Elementlista 2. ERMS-element för både ärendeakter och handlingar](#elementlista-2-erms-standardelement)
- [Elementlista 3. Tillagda element för både ärendeakter och handlingar](#elementlista-3-tillagda-element)
- [Elementlista 4. ERMS-element för ärendeakter](#elementlista-4-ärendeakter)
- [Elementlista 5. Tillagda element för ärendeakter](#elementlista-5-svenska-kyrkans-tilläggsinformation-om-ärendeakter)
- [Elementlista 6. ERMS-element för handlingar](#elementlista-6-ärendehandlingar)
- [Elementlista 7. Tillagda element för handlingar](#elementlista-7-svenska-kyrkans-tilläggsinformation-om-ärendehandlingar)
- [Elementlista 8. Element för bifogade filer](#elementlista-8-bifogad-fil)

## 2.3. Värdelistor

I många fall är det värde som får anges i ett dataelement begränsat till värden som finns i en specificerad värdelista.
De värdelistor som ingår i *SvKGS Ärendehandlingar* finns i ett eget dokument, [ERMS-SVK-ARENDE-vardelistor.md](ERMS-SVK-ARENDE-vardelistor.md).
Värdelistorna kan innehålla värden från ERMS eller vara tillagda värden och är därför också en del av
Svenska kyrkans anpassning av ERMS. Utgångspunkten har varit att så långt som möjligt använda värden från ERMS.

## 2.4. Scheman

XML-scheman och Schematron används i ERMS för att på ett mer tekniskt sätt definiera hur dataelementen
ska utformas. Scheman kan också användas för att validera ett XML-dokument så att man kan avgöra om det
följer specifikationen.

I ERMS ingår schemana [ERMS_v3.xsd](https://citserms.dilcis.eu/schema/ERMS_v3.xsd) och [ERMS.sch](https://citserms.dilcis.eu/schema/erms_v3.sch).

I *SvKGS Ärendehandlingar* används schemana

**ERMS_v3.xsd**<br/>
Schemat används för att validera de delat av XML-dokumentet som följer ERMS-standard.

**ERMS-SVK-element.xsd**<br/>
I detta schema definieras alla element som är Svenska kyrkans tillägg till ERMS. Schemat är alltså inte
specifikt för *SvKGS Ärendehandlingar* utan används i andra anpassningar av ERMS.
Schemat är publikt tillgängligt på [Github](https://github.com/svkau/ERMS-SVK-element).

**ERMS-SVK-ARENDE.xsd**<br/>
Schemat reglerar själva strukturen på den del av XML-dokumentet som utgörs av Svenska kyrkans tillägg
och vilka tillagda element som får användas i enlighet med SvKGS Ärendehandlingar.
Denna del av XML-dokumentet ingår i ERMS-elementet `additionalXMLData`.

**ERMS-SVK-ARENDEN.sch**<br/>
Schemat innehåller Svenska kyrkans regler som
de beskrivs i *SvKGS Ärendehandlingar*. De två sistnämnda schemana är specifika för
*SvKGS Ärendehandlingar* och är publikt tillgängliga på [Github](https://github.com/svkau/SvKGS-Arendehandlingar).

En särskild anmärkning om elementet `appendix` i behöver göras. Eftersom det har funnits behov av att
utöka detta element med flera underelement, och då det inte finns något element `additionalXMLData` här,
används inte `appendix` utan i stället ett eget element `svkAppendix` som definieras i ERMS-SVK-element.xsd.

Användandet av elementet appendix förbjuds genom en regel i ERMS-SVK-ARENDEN.sch.

För att validera ett XML-dokument och avgöra om det följer specifikationerna i *SvKGS Ärendehandlingar*, måste man
alltså använda både **ERMS_v3.xsd** och **ERMS-SVK-ARENDE.xsd** (som i sin tur importerar och använder **ERMS-SVK-element.xsd**).
Därtill måste dokumentet valideras mot **ERMS-SVK-ARENDE.sch**.

## 2.5. Datatyper

Värden som anges i dataelementen måste vara av de datatyper som definieras i XML-schemana.
Datatyper som kan förekomma är:

- [string](https://www.w3.org/TR/xmlschema-2/#string)
- [token](https://www.w3.org/TR/xmlschema-2/#token)
- [integer](https://www.w3.org/TR/xmlschema-2/#integer)
- [decimal](https://www.w3.org/TR/xmlschema-2/#decimal)
- [dateTime](https://www.w3.org/TR/xmlschema-2/#dateTime)
- [boolean](https://www.w3.org/TR/xmlschema-2/#boolean)

För att ange datum används alltid datatypen dateTime, vilket betyder att både datum och klocklag ned till
sekundnivå ska anges i [UTC-format](https://sv.wikipedia.org/wiki/Koordinerad_universell_tid)
enligt [ISO 8601](https://sv.wikipedia.org/wiki/ISO_8601) (med bindestreck och kolon). Om klockslag saknas används
noll-tecken. Tidszon anges i regel inte och förutsätts då vara Europe/Stockholm.

Exempel på datum och tid: `2018-03-04T15:15:22`. Enbart datum: `2020-09-17T00:00:00`.

Vid angivande av tal (integer och decimal) används inte tusentalsavgränsare.

Vid angivande av decimal används punkt som decimalavgränsare.

## 2.6. Metadata i XMP-format
Information om bilderna (metadata) ska dokumenteras både i XML-dokumentet (ERMS) och inbäddat i respektive bildfil i XMP-format.
Utöver den obligatoriska informationen är det möjligt att i XMP-strukturen spara vilken metadata man själv önskar.

Den XMP-information som finns inbäddad i bildfilen ska också ingå i ERMS-dokumentet. Se exemplet XMP-data nedan.

Dessutom måste den information som finns i ERMS-fälten vara identisk med den information som finns i motsvarande fält i XMP-strukturen enligt nedanstående tabell

| ERMS                           | XMP                    |
|--------------------------------|------------------------|
| ERMS-SVK:86 - *Identifikator*  |  xmpMM:DocumentID      |
| ERMS-SVK:89 - *ObjektID*       |  xmpMM:DocumentID      |
| ERMS-SVK:95 - *Nyckelord*      |  dc:subject            |
| ERMS-SVK:97 - *Titel*          |  dc:title              |
| ERMS-SVK:104 - *Skapare*       |  dc:creator            |
| ERMS-SVK:109 - *Beskrivning*   |  dc:description        |
| ERMS-SVK:111 - *Skapat*        |  exif:DateTimeOriginal |
| ERMS-SVK:164 - *Skapad*        |  xmp:CreateDate        |
| ERMS-SVK:165 - *Senast ändrad* |  xmp:ModifyDate        |


- **XMP namespace** (xmp): `http://ns.adobe.com/xap/1.0/`
- **XMP Media Management namespace** (xmpMM): `http://ns.adobe.com/xap/1.0/mm/`
- **Exif** (exif): `http://ns.adobe.com/exif/1.0/`
- **Dublin Core** (dc): `http://purl.org/dc/elements/1.1/`


## 2.7. Råd om användandet av *SvKGS Bilder*

I tabellerna med dataelement nedan har varje element en identifieringskod (t.ex. ERMS-SVK:1).
Även elementets motsvarande kod i ERMS anges, om det inte är ett tillagt element.

Om ett element är obligatoriskt, anges detta särskilt. I annat fall är det frivilligt att använda elementet.

Element kan få förekomma en enda gång eller upprepade gånger i ett XML-dokument.
Om ett element får upprepas, anges detta särskilt. I annat fall får elementet endast förekomma en gång.

I tabellerna anges också motsvarande XML-elements namn och vilken datatyp som ska användas.

Innan en leverans till e-arkivet görs, måste den levererande parten och e-arkivets förvaltningsorganisation
tillsammans upprätta en leveransöverenskommelse där villkor och förutsättningar för leveransen specificeras.
Se mer om leveransförfarandet i Arkivhandboken, kapitel 8.

# 3. Dataelement med exempel

## 3.1. Övergripande information om XML-dokumentet

Kontroll är ett obligatoriskt element som beskriver själva XML-filen och vad den innehåller.
Den underlättare förståelsen av informationen, om XML-filen skulle separeras från arkivpaketet.

### Elementlista 1. Kontroll

---

#### ERMS-SVK:1 - *Identifikator*

(ERMS1)

> Identifierar ERMS-dokumentet

> Obligatoriskt. Elementet får upprepas.

> Tre identifikatorer måste användas: arkivbildarens namn och id samt ärendets nummer. Se exempel nedan.

> **XML-element:**	`identification`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:2 - *Typ av identifikator*

(ERMS2)

> Beskrivning av identifikatorn.

> Obligatoriskt. Värdet väljs från [Värdelista 1](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-1---typ-av-identifikator).

> **XML-element:**	`identification/@identificationType`<br/>
> **Datatyp:**	string

---

#### Exempel 1 – Identifikator

```xml
<control>
    <identification identificationType="arkivbildare">Sunne pastorat</identification>
    <identification identificationType="organisationsnummer">1234567890</identification>
    <identification identificationType="aid">5610</identification>
    <identification identificationType="ärendenummer">P 2019-0254</identification>
</control>
```

---

#### ERMS-SVK:3 - *Informationsklassning*

(ERMS3)

> Informationsklass som baseras på säkerhetsklassificering.

> **XML-element:**	`informationClass`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:4 - *Klassificeringsstruktur*

(ERMS4-6)

> Den klassificeringsstruktur som har använts vid klassificering av det aktuella ärendet.

> Obligatoriskt. Värdet välj från [Värdelista 2](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-2---klassificeringsstruktur).

> **XML-element:**	`classificationSchema/textualDescriptionOfClassificationSchema/p` <br/>
> **Datatyp:**	string

---

#### Exempel 2 – Klassificeringsstruktur

```xml
<control>
	<classificationSchema>
		<textualDescriptionOfClassificationSchema>
			<p>KlaSL2016_1.0</p>
		</textualDescriptionOfClassificationSchema>
	</classificationSchema>
</control>
```
---

#### ERMS-SVK:5 - *Säkerhetsklassning*

(ERMS8)

> Säkerhetsklass.

> **XML-element:**	`securityClass` <br/>
> **Datatyp:**	string

---

#### ERMS-SVK:6 - *Underhåll*

(ERMS10)

> Samlingselement för underhållsinformation som används för att beskriva XML-dokumentets tillkomst och eventuella ändringar.

> Obligatoriskt.

> **XML-element:**	`maintenanceInformation`

---

#### ERMS-SVK:7 - *Status*

(ERMS11)

> XML-dokumentets status.

> Obligatoriskt. Värdet välj från [Värdelista 3](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-3---xml-dokumentets-status).
>
> För ett nyskapat dokument är värdet alltid `new`.

> **XML-element:**	`maintenanceStatus/@value` <br/>
> **Datatyp:**	string

---

#### ERMS-SVK:8 - *Skapare*

(ERMS12)

> Samlingselement med beskrivning av den instans som har skapat XML-dokumentet.

> Obligatoriskt.

> **XML-element:**	`maintenanceAgency`

---

#### ERMS-SVK:9 - *Skapare ID*

(ERMS13)

> Identifierande kod för den instans som har skapat XML-dokumentet.

> Obligatoriskt.

> **XML-element:**	`agencyCode`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:10 - *Typ av ID*

(ERMS14)

> Beskriver vilken typ av kod som har använts för att identifiera skaparen av XML-dokumentet.

> Obligatoriskt. Värdet väljs från [Värdelista 4](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-4---typ-av-id).

> **XML-element:**	`agencyCode/@type`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:11 - *Alternativt ID*

(ERMS15)

> Ytterligare en identifierande kod som kan användas vid behov.

> **XML-element:**	`otherAgencyCode<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:12 - *Typ av alternativt ID*

(ERMS16)

> Samma som ovan (ERMS-SVK:10)

> Obligatoriskt om Alternativt ID används.

> **XML-element:**	`otherAgencyCode/@type`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:13 - *Skapare Namn*

(ERMS17)

> Namn på den instans som har skapat XML-dokumentet.

> Obligatoriskt.

> **XML-element:**	`agencyName`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:14 - *Underhållshistoria*

(ERMS19)

>Samlingselement för dokumentets underhållshistoria.

> Obligatoriskt.

> **XML-element:**	`maintenanceHistory`

---

#### ERMS-SVK:15 - *Underhållshändelse*

(ERMS20)

> En händelse i dokumentets underhållshistoria.

> Obligatoriskt. Elementet kan upprepas.
> 
> När XML-dokumentet skapas, får det en *Underhållshändelse* av typen "created".

> **XML-element:**	`maintenanceEvent`

---

#### ERMS-SVK:16 - *Typ av händelse*

(ERMS21)

> Typ av underhållshändelse.

> Obligatoriskt. Värdet väljs från [Värdelista 5](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-5---typ-av-underh%C3%A5llsh%C3%A4ndelse).

> **XML-element:**	`eventType/@value`<br/>
> **Datatyp:**	token

---

#### ERMS-SVK:17 - *Datum för händelse*

(ERMS22)

> Datum då underhållshändelsen inträffade.

> Obligatoriskt.

> **XML-element:**	`eventDateTime`<br/>
> **Datatyp:**	dateTime

---

#### ERMS-SVK:18 - *Utförare*

(ERMS23)

> Den agent som har utfört handlingen.

> Obligatoriskt.

> **XML-element:**	`agent`

---

#### ERMS-SVK:19 - *Typ av utförare*

(ERMS93)

> Anger vilken egenskap utföraren har i förhållande till den utförda handlingen.

> Obligatoriskt. Värdet väljs från [Värdelista 6](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-6---typ-av-akt%C3%B6r-agenttype).

> **XML-element:**	`agent/@agentType`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:20 - *Namn*

(ERMS95)

> Namn på den person eller organisation som har utfört handlingen.

> Obligatoriskt.

> **XML-element:**	`agent/name`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:21 - *Organisation*

(ERMS99)

> Organisationstillhörighet.

> Obligatoriskt om det är en person som är agent.

> **XML-element:**	`agent/organisation`<br/>
> **Datatyp:**	string

---

#### Exempel 3 – Underhåll

```xml
<control>
	<maintenanceInformation>
		<maintenanceStatus value="new"/>
		<maintenanceAgency>
			<agencyCode type="organisationsnummer">1234567876</agencyCode>
				<agencyName>Kyrkostyrelsen</agencyName>
		</maintenanceAgency>
		<maintenanceHistory>
			<maintenanceEvent>
				<eventType value="created"/>
				<eventDateTime>2001-12-17T09:30:47</eventDateTime>
				<agent agentType="deliverer">
					<name>Public 360</name>
					<organisation>Tietoevry</organisation>
				</agent>
			</maintenanceEvent>
		</maintenanceHistory>
	</maintenanceInformation>
</control>
```

---

## 3.2. Element som används för information om elektroniska bilder.

### Elementlista 2. Information om bilder - ERMS standardelement

---

#### ERMS-SVK:85 - *Bild*

(ERMS129)

> Samlingselement med information om en bild.

> Obligatoriskt. Elementet kan upprepas.

> **XML-element:** `records/record`<br/>

---

#### ERMS-SVK:86 - *Identifikator*

(ERMS130)

> Identifikator för bilden i form av UUID. Identifikatorn anges
> automatiskt redan i det levererande systemet eller vid överföring till e-arkivet.

> Obligatoriskt.

> Värdet ska vara det samma som anges för *ObjektID*.
>
> Värdet för *Identifikator* måste också vara det samma som anges i elementet `xmpMM:DocumentID` i bildfilens XMP-struktur.

> **XML-element:** `record/@systemIdentifier`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:87 - *Handlingstyp*

(ERMS131)

> Övergripande typ av handling. Motsvarar **inte** handlingstyp i arkivredovisning/dokumenthanteringsplan.

> Obligatoriskt.
>
> Fast värde: "bild".

> **XML-element:** `record/@recordType`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:88 - *Form*

(ERMS132)

> Anger om handlingen bara finns i fysisk form, bara i digital form eller både och.

> Värdet väljs från [Värdelista 14](ERMS-SVK-ARENDE-vardelistor.md#erms-svk-arende-v%C3%A4rdelista-14---form).

> **XML-element:** `record/@recordPhysicalOrDigital`<br/>
> **Datatyp:** string

---

#### Exempel 18 – Bild

```xml
<record
	systemIdentifier="8dbbdc56-8ada-4ad5-a1ec-b8131a1086a2"
	recordPhysicalOrDigital="digital"
	recordType="bild">
</record>
```

#### ERMS-SVK:89 - *ObjektID*

(ERMS146)

> Obligatoriskt.
>
> Värdet ska vara det samma som anges för *Identifikator*
>
> Värdet för *ObjektID* måste också vara det samma som anges i elementet `xmpMM:DocumentID` i bildfilens XMP-struktur.

> **XML-element:** `objectId`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:93 - *Klassificering*

(ERMS196)

> Namnet på den process i den officiella klassificeringsstrukturen som har
> angivits som klassificering av bilden.

> **XML-element:** `classification`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:94 - *Klassificeringskod*

(ERMS75)

> Koden för den process som angivits under *Klassificering*.

> **XML-element:** `classification/@classificationCode`<br/>
> **Datatyp:** string

---

#### Exempel 20 – Klassificering

```xml
<record>
	<classification classificationCode="2.7">Ge service</classification>
</record>
```

---

#### ERMS-SVK:95 - *Nyckelord*

(ERMS152)

> Samlingselement för nyckelord.

> **XML-element:** `keywords`<br/>

---

#### ERMS-SVK:96 - *Nyckelord*

(ERMS153)

> Enskilt nyckelord.

> Elementet kan upprepas.

> De nyckelord som anges måste också anges i elementet `dc:subject` i bildfilens XMP-struktur.

> **XML-element:** `keyword`<br/>
> **Datatyp:** string

---

#### Exempel 21 – Nyckelord

```xml
<record>
    <keywords>
        <keyword>församlingsordning</keyword>
        <keyword>kyrkorådet</keyword>
    </keywords>
</record>
```
---

#### ERMS-SVK:97 - *Titel*

(ERMS)

> Titel på bilden.

> Den titel som anges måste också anges i elementet `dc:title` i bildfilens XMP-struktur.


> **XML-element:** `title`<br/>
> **Datatyp:** string

---

#### Exempel 22 – Titel

```xml
<record>
	<title>Handlingens titel</title>
	<otherTitle titleType="public">En offentlig titel</otherTitle>
</record>
```

---

#### ERMS-SVK:22 - *Sekretessmarkering*


(ERMS253, ERMS57)

>Samlingselement för uppgift om sekretess.
>I *SvKGS Bilder* används sekretessmarkering enbart i GDPR-syfte för markera bilder
>med personer som är i livet vid arkiveringstillfället.

>Elementet kan upprepas.
>
>Om elementet *Sekretess* används måste attributet `restrictionType` ha värdet ”gdpr”.

> **XML-element:**	`restriction`<br/>

---

#### ERMS-SVK:23 - *Förklarande text*

(ERMS253, ERMS57)

>Fritext som beskriver sekretessen.
>Fast värde: "Personfotografi".

> **XML-element:**	`explanatoryText`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:24 - *Lagrum*

(ERMS59)

>Hänvisning till paragraf i kyrkoordningens 54 kapitel, till Offentlighets- och sekretesslagen
>eller till annat lagrum som stöder den angivna sekretessen.
>Fast värde: "KO 54:11b"

> **XML-element:**	`regulation`<br/>
> **Datatyp:**	string

---

#### ERMS-SVK:25 - *Sekretessdatum*

(ERMS62)

>Datum från och med vilket sekretessen anses gälla.
>I regel samma datum som bilden har tagits.

>Om elementet *Sekretessdatum* används, måste attributet `dateType` ha värdet ”created”.

> **XML-element:**	`dates/date/@dateType="created"`<br/>
> **Datatyp:**	dateTime

---

#### Exempel 6 – Sekretessmarkering

```xml
<restriction restrictionType="gdpr">
    <explanatoryText>Personfotografi</explanatoryText>
    <regulation>KO 54:11b</regulation>
    <dates>
        <date dateType="created">2020-01-02T00:00:00</date>
    </dates>
</restriction>
```

---

#### ERMS-SVK:103 - *Aktörer*

(ERMS)

> Samlingselement för alla agerande parter.

> Obligatoriskt.
> 
> För mer information om elementet, se avsnittet [3.2.1. Aktörer](ERMS-SVK-ARENDE.md#321-aktörer).

> **XML-element:** `agents`<br/>

---

#### ERMS-SVK:104 - *Skapare*

(ERMS)

> Den som har skapat bilden, fotograf.

> Om elementet *Skapare* används, måste `agentType` ha värdet ”other”
> och `otherAgentType` ha värdet "photographer".

> Den skapare som anges måste också anges i elementet `dc:creator` i bildfilens XMP-struktur.

> **XML-element:** `agent/@agentType="creator`

---

#### Exempel 4 – Aktörer

```xml
<agents>
    <agent agentType="other" otherAgentType="photographer">
        <name>Anna Pettersson</name>
        <organisation>Kyrkstadens församling</organisation>
        <idNumber idNumberType="username">annpet</idNumber>
    </agent>
</agents>
```

#### ERMS-SVK:109 - *Beskrivning*

(ERMS)

> Obligatoriskt.

> Beskrivning av bilden.

> Den beskrivning som anges måste också anges i elementet `dc:description` i bildfilens XMP-struktur.

> **XML-element:** `description`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:110 - *Datum*

(ERMS)

> Samlingselement för alla datum som rör bilden.

> För mer information om elementet. se avsnittet [3.2.2. Datum](ERMS-SVK-ARENDE.md#322-datum) ovan.

> **XML-element:** `dates`<br/>

---

#### ERMS-SVK:111 - *Skapat*

(ERMS)

> Datum och tid då bilden skapades, fotograferades.

> Obligatoriskt.
>
> Om elementet *Skapat* används, måste `dateType` ha värdet ”created”.

> Det datum som anges måste också anges i elementet `exif:DateTimeOriginal` i bildfilens XMP-struktur.

> **XML-element:** `date/@dateType=”created”`<br/>
> **Datatyp:** dateTime

---

#### Exempel 5 – Datum

```xml
<dates>
    <date dateType="created">2020-05-20T00:00:00</date>
</dates>
```

---

#### ERMS-SVK:115 - *Utökad XML-data*

> *Utökad XML-data* är en del av Svenska kyrkans anpassning av ERMS.

> Obligatoriskt.
> 
> Se [Elementlista 7](ERMS-SVK-BILDER.md#elementlista-3-svenska-kyrkans-tilläggsinformation-om-bilder).

> **XML-element:** `additionalXMLData`<br/>

---

### Elementlista 3. Svenska kyrkans tilläggsinformation om bilder

---

#### ERMS-SVK:116 - *Tilläggsinformation*

> De element som inte ingår i ERMS utan är tillägg i Svenska kyrkans anpassning är samlade i elementet *Tilläggsinformation*.

> Obligatoriskt.

> **XML-element:** `additionalInformation/additionalXMLData/svk:ermsSvkArende/svk:ermsSvkRecord`<br/>

---

#### ERMS-SVK:83 - *Version av SvKGS Bilder*

> Anger vilken version av SvKGS Bilder som XML-dokumentet är kompatibelt med.

> Obligatoriskt.

> **XML-element:** `svk:ermsSvkArende/@ermsSvkBilderVersion="1.0"` (decimal)<br/>

---

#### ERMS-SVK:149 - *Bifogad fil*

> Uppgifter om fil som är kopplad till den registrerade bilden.

> I *SvKGS Bilder* kan endast *en* fil kopplas till elementet `record`. Det är en anpassning av ERMS-standard.
> 
> Se [Elementlista 4](ERMS-SVK-BILER.md#elementlista-4-bifogad-fil).

> **XML-element:** `svk:ermsSvkRecord/svk:svkAppendix`<br/>

---

## 3.5. Information om bifogade filer

I ERMS används för bifogade filer elementet record/additionalInformation/appendix.
I Svenska kyrkans anpassning av ERMS används i stället tilläggselementet
`record/additionalInformation/additionalXMLData/ermsSvkArende/ermsSvkRecord/svkAppendix`.

---

### Elementlista 4. Bifogad fil

---

#### ERMS-SVK:150 - *Bifogad fil*

> Samlingselement för uppgifter om en fil som är kopplad till en registrerad bild.

> Elementet kan upprepas.

> **XML-element:** `svk:svkAppendix`<br/>

---

#### ERMS-SVK:151 - *Appendix*

> Samlingselement för den information om filen som följer ERMS-standard.

> **XML-element:** `appendix`<br/>

---

#### ERMS-SVK:153 - *Namn*

> Filens namn.

> Obligatoriskt.

> **XML-element:** `appendix/@name`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:155 - *Filformat*

> Filens format.

> Obligatoriskt.
> 
> Anges i form av filnamnsändelse (max fyra tecken) utan punkt och med små bokstäver.
>
> Exempel: jpg, png

> **XML-element:** `appendix/@fileFormat`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:156 - *Originalfilformat*

> Om filen är konverterad till arkivformat, anges här originalfilens format.
 
> Anges i form av filnamnsändelse (max fyra tecken) utan punkt och med små bokstäver.
>
> Exempel: tif, heic

> **XML-element:** `appendix/@originalFileFormat`<br/>
> **Datatyp:** string

---

#### ERMS-SVK:157 - *Sökväg*

> Relativ sökväg till filens placering i arkivpaketet.
 
> Obligatoriskt.
> 
> Exempel: files/bild_01.jpg

> **XML-element:** `appendix/@path`<br/>
> **Datatyp:** string

---



#### ERMS-SVK:163 - *Filinformation*

> Samlingselement för utökad information om filen.
> 
> (Tillägg till ERMS-standard)

> **XML-element:** `svk:fileInfo`<br/>

---

#### ERMS-SVK:164 - *Skapad*

> Datum och tid då filen skapades (systeminformation).
> 
> Attributet `dateType` måste ha värdet "created".
>
> Se avsnittet [3.2.2. Datum](ERMS-SVK-ARENDE.md#322-datum) ovan.

> **XML-element:** `dates/date/@dateType="created"`<br/>
> **Datatyp:** dateTime

---

#### ERMS-SVK:165 - *Senast ändrad*

> Datum och tid då filen senast ändrades (systeminformation).
> 
> Attributet `dateType` måste ha värdet "modified".
>
> Se avsnittet [3.2.2. Datum](ERMS-SVK-ARENDE.md#322-datum) ovan.

> **XML-element:** `dates/date/@dateType="modified"`<br/>
> **Datatyp:** dateTime

---

#### Exempel 29 – svkAppendix

```xml
<svk:svkAppendix>
	<svk:appendix name="kyrkoinvigningen" path="filer/238093d5-5ae5-438f-a043-7c340738e5d1.jpg" fileFormat="jpg"/>
	<svk:fileInfo>
		<svk:dateCreated>2010-02-01T00:00:00</svk:dateCreated>
		<svk:dateLastEdited>2010-02-01T00:00:00</svk:dateLastEdited>
	</svk:fileInfo>
</svk:svkAppendix>
```
