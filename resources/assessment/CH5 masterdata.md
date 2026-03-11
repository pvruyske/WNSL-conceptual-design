# Contents

[Contents [1](#_Toc209630211)](#_Toc209630211)

[CustomDevs [1](#customdevs)](#customdevs)

[ISVs [1](#isvs)](#isvs)

[1 Klanten [1](#klanten)](#klanten)

[2 Leveranciers [1](#leveranciers)](#leveranciers)

[2.1 General [1](#general)](#general)

[2.1.1 AS400 structure [1](#as400-structure)](#as400-structure)

[2.1.2 D365 structure [1](#d365-structure)](#d365-structure)

[2.2 Integrations [1](#integrations)](#integrations)

[2.3 Security [1](#security)](#security)

[3 Projecten [1](#projecten)](#projecten)

[3.1 General [1](#general-1)](#general-1)

[3.2 Tracking dimension "Project"
[1](#tracking-dimension-project)](#tracking-dimension-project)

[3.2.1 MTO transacties [1](#mto-transacties)](#mto-transacties)

[3.2.2 Niet-MTO transacties
[1](#niet-mto-transacties)](#niet-mto-transacties)

[3.3 Financial dimension "WinsolSalesReference"
[1](#financial-dimension-winsolsalesreference)](#financial-dimension-winsolsalesreference)

[4 Items [1](#items)](#items)

[4.1 General [1](#general-2)](#general-2)

[4.1.1 AS400 structure [1](#as400-structure-1)](#as400-structure-1)

[4.1.2 D365 structure [1](#d365-structure-1)](#d365-structure-1)

[4.2 Specifieke items (distinct)
[1](#specifieke-items-distinct)](#specifieke-items-distinct)

[4.2.1 Subtype: product [1](#subtype-product)](#subtype-product)

[4.2.2 Subtype: product master
[1](#subtype-product-master)](#subtype-product-master)

[4.3 Generieke items [1](#generieke-items)](#generieke-items)

[4.3.1 Subtype: product [1](#subtype-product-1)](#subtype-product-1)

[4.3.2 Subtype: product master
[1](#subtype-product-master-1)](#subtype-product-master-1)

[4.4 Item specific custom fields
[1](#item-specific-custom-fields)](#item-specific-custom-fields)

[4.5 Indeling naar soort en aantal
[1](#indeling-naar-soort-en-aantal)](#indeling-naar-soort-en-aantal)

[4.5.1 Shared products [1](#shared-products)](#shared-products)

[4.5.2 Released products [1](#released-products)](#released-products)

[5 Winsol product attributes
[1](#winsol-product-attributes)](#winsol-product-attributes)

[5.1 Attributes in master data
[1](#attributes-in-master-data)](#attributes-in-master-data)

[5.2 Attributes in transactional data
[1](#attributes-in-transactional-data)](#attributes-in-transactional-data)

[5.3 Vendor color codes [1](#vendor-color-codes)](#vendor-color-codes)

# CustomDevs

- [Change request 1505: CR-038 Project doorkopiëren naar
  WinsolSalesReference op PO line (uitbreiding op
  CR-036)](#_Toc209630245)

- [Customization 45: CUS-018: Legacy system (AS400) identification
  number for Vendor, Customer, Products](#_Toc209630246)

- [Task 745: Chacal ID on released product](#_Toc209630247)

- [Change request 1015: Surface area toevoegen aan Released products
  V2](#_Toc209630248)

- [Change request 183: CR-XXX: add attributes to released
  products](#_Toc209630249)

- [Devops 1228 -- CR028 - Extra Winsol attribute: Fabric Colour
  Code](#_Toc209630250)

- [Change request 1305: CR-033 Externe kleurencodes AluK - optimaliseren
  kleurattributen](#_Toc209630251)

# ISVs

- [9A Advanced Manufacturing - Advanced projects](#_Toc209630295)

- [9A Kickstart](#_Toc209630296)

# Klanten

+-------------------+--------------------------------------------------+
| **Master          | AS400                                            |
| systeem**         |                                                  |
+===================+==================================================+
| **Interface       | [Creatie klant of periodiek?]{.mark}             |
| trigger**         |                                                  |
+-------------------+--------------------------------------------------+
| **Interface       | - Klantnummer                                    |
| inhoud**          |                                                  |
|                   | - Klantnaam                                      |
|                   |                                                  |
|                   | - Klantengroep: STD of INCO                      |
|                   |                                                  |
|                   | - Btw-nummer (indien van toepassing)             |
|                   |                                                  |
|                   | - Adres                                          |
|                   |                                                  |
|                   |   - Enkel land                                   |
|                   |                                                  |
|                   | - Business unit als financiële dimensie          |
|                   |                                                  |
|                   | - Legacy ID (= ID uit AS400)                     |
+-------------------+--------------------------------------------------+
| **Interface       | - CustIN                                         |
| document type**   |                                                  |
|                   | - CustIN_NoBU                                    |
+-------------------+--------------------------------------------------+
| **Sample XML**    | \<CustTable type=\"Record\" log=\"\"             |
|                   | status=\"0\" ref=\"5637341840\"\>                |
|                   |                                                  |
|                   |   \<AccountNum type=\"Field\" log=\"\"           |
|                   | status=\"0\"\>C00017401\</AccountNum\>           |
|                   |                                                  |
|                   |   \<ALTLegacyCustID type=\"Field\" log=\"\"      |
|                   | status=\"0\"\>00017401\</ALTLegacyCustID\>       |
|                   |                                                  |
|                   |   \<CustGroup type=\"Field\" log=\"\"            |
|                   | status=\"0\"\>STD\</CustGroup\>                  |
|                   |                                                  |
|                   |   \<Currency type=\"Field\" log=\"\"             |
|                   | status=\"0\"\>EUR\</Currency\>                   |
|                   |                                                  |
|                   |   \<BusinessUnitDimension type=\"Field\"         |
|                   | log=\"\"                                         |
|                   | status=\"0\"\>B2C\</BusinessUnitDimension\>      |
|                   |                                                  |
|                   |   \<DirPartyTable type=\"Record\" log=\"\"       |
|                   | status=\"0\"\>                                   |
|                   |                                                  |
|                   |     \<Name type=\"Field\" log=\"\"               |
|                   | status=\"0\"\>DESMET ELINE\</Name\>              |
|                   |                                                  |
|                   |     \<LanguageId type=\"Field\" log=\"\"         |
|                   | status=\"0\"\>nl-BE\</LanguageId\>               |
|                   |                                                  |
|                   |     \<LogisticsPostalAddress type=\"Record\"     |
|                   | log=\"\" status=\"0\"\>                          |
|                   |                                                  |
|                   |       \<CountryRegionId type=\"Field\" log=\"\"  |
|                   | status=\"0\"\>BEL\</CountryRegionId\>            |
|                   |                                                  |
|                   |     \</LogisticsPostalAddress\>                  |
|                   |                                                  |
|                   |     \<DirPartyLocation type=\"Record\" log=\"\"  |
|                   | status=\"0\"\>                                   |
|                   |                                                  |
|                   |       \<IsPrimary type=\"Field\"                 |
|                   | fieldtype=\"Enum\"\>Yes\</IsPrimary\>            |
|                   |                                                  |
|                   |     \</DirPartyLocation\>                        |
|                   |                                                  |
|                   |   \</DirPartyTable\>                             |
|                   |                                                  |
|                   | \</CustTable\>                                   |
+-------------------+--------------------------------------------------+

# Leveranciers

Leveranciers worden gemaakt in D365 en gesynct naar AS400. De sync naar
AS400 is nodig omdat de aankooporder nog gesynct worden naar AS400, dit
ter ondersteuning van productie.

## General

### AS400 structure

In AS400 zitten leveranciers in aparte tabellen per company. Dit
betekent dat dezelfde leverancier onder verschillende nummers kon
voorkomen in AS400.

### D365 structure

In D365 worden leveranciers ook per company bijgehouden, maar door de
link met het cross-company object "Party" is er wel een link tussen deze
leveranciers. Bijvoorbeeld: ALUK BELGIUM

![A screenshot of a computer AI-generated content may be
incorrect.](media/image1.png){width="2.9801859142607174in"
height="3.5257403762029744in"}

## Integrations

+-------------------+--------------------------------------------------+
| **Source system** | D365FSCM                                         |
+===================+==================================================+
| **Destination     | - AS400                                          |
| system(s)**       |                                                  |
|                   | - Kofax                                          |
+-------------------+--------------------------------------------------+
| **Interface       | Creatie of update van leverancier (database      |
| trigger**         | event)                                           |
+-------------------+--------------------------------------------------+
| **Interface       | - Legacy ID (Winsol field)                       |
| inhoud**          |                                                  |
|                   | - Account number                                 |
|                   |                                                  |
|                   | - Vendor name                                    |
|                   |                                                  |
|                   | - Terms of payment                               |
|                   |                                                  |
|                   | - Tax registration number                        |
|                   |                                                  |
|                   | - Email address                                  |
+-------------------+--------------------------------------------------+
| **Interface       | - VendOUT                                        |
| document type**   |                                                  |
+-------------------+--------------------------------------------------+
| **Sample XML**    | [TBC -- no sample found in UAT/PRD]{.mark}       |
+-------------------+--------------------------------------------------+

## Security

Aanmaken/wijzigen van leveranciers finance-info zit bij Finance.
Contactgegevens kunnen door SCM gewijzigd worden.

Zeker de bankaccount is afgeschermd -- dit gebeurt middels een block
role voor iedereen gecombineerd met database logging & reporting.

# Projecten

## General

Het concept "project" heeft twee betekenissen binnen Winsol:

- Een project in de **projectcel**: bv. ramen & deuren voor een volledig
  appartementsgebouw of een volledige sociale woonwijk

- Een **AS400 order**, wat voor B2C en B2B equivalent is aan een
  verkooporder. Een project uit projectcel wordt opgedeeld in deelorders
  die binnen een beperkter timewindow afwerkbaar zijn. Bv:

  - sociale woningen: 1 huis = 1 project

  - appartement: 1 project per verdiep (of per deel van een verdiep)

## Tracking dimension "Project"

Een extra tracking dimension werd geactiveerd als onderdeel van de 9A
Advanced manufacturing ISV, en werd "project" genoemd. De tracking
dimension is geconfigureerd als planningsrelevant ("Coverage plan by
dimension" is geactiveerd op de tracking dimension group).

ISV 1: []{#_Toc209630295 .anchor}9A Advanced Manufacturing - Advanced
projects

### MTO transacties

Elk verkooporder in AS400 wordt een nieuwe dimensiewaarde voor de
project tracking dimension binnen D365. Hiervoor is een interface
opgezet. De project dimensie wordt binnen D365 bijgehouden op alle
voorraadtransacties (momenteel beperkt tot aankooporders en verbruiken).
Er is een interface voorzien om de voorraad voor artikelen met een
specifiek project te verbruiken (equivalent aan backflush verbruik op
een werkorder). Dit wordt besproken in het hoofdstuk "inventory to
deliver".

![A screenshot of a computer AI-generated content may be
incorrect.](media/image2.png){width="6.268055555555556in"
height="2.6256944444444446in"}

### Niet-MTO transacties

Voor niet-ordergerelateerde aankooporders wordt de dimensiewaarde
"STOCK" als projectdimensie gebruikt. Het is technisch mogelijk om met
een lege project dimensie te bestellen, deze gedragen zich uiteindelijk
gelijkaardig aan STOCK-dimensie bestellingen.

Aandachtspunt: nogal wat customisaties in binnen procure to pay en
inventory to deliver identificeren deze niet-MTO transacties door
hard-coded te checken op de dimensiewaarde "STOCK".

## Financial dimension "WinsolSalesReference"

Bij het aanmaken van een nieuwe PO-lijn of inventory journal-lijn wordt
de waarde die is ingevuld als project tracking dimension overgenomen in
de WinsolSalesReference financiële dimensie. Hierdoor kunnen de
boekingen die voortkomen uit processen rond aankoop en verbruik worden
getraceerd tot op projectniveau.

CustomDev 1: [[]{#_Toc209630245 .anchor}Change request
1505](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1505):
CR-038 Project doorkopiëren naar WinsolSalesReference op PO line
(uitbreiding op CR-036)

# Items

## General

Items worden apart aangemaakt in AS400 als in D365. Eerst aanmaken in
AS400, daarna in D365! Er is geen automatische sync tussen beide. AS400
heeft de items nog steeds nodig voor aansturing productie en voor de
sync rond aankooporders.

Items worden typisch niet gedeeld overheen legale entiteiten, hoewel er
wel items zijn die fysiek zowel in company A als B gebruikt worden en
identiek zijn. De business unit die owner is van het item kan dus
eenvoudigweg afgeleid worden op basis van de legale entiteit. Gezien
Actuell twee business units heeft (alu en pvc) wordt de product owner
daar aangeduid door de buyer group (prefix "ALU" of "PVC").

### AS400 structure

In AS400 is de unique item reference een 5-digit number. Deze bestaan
per company. Doorheen het verleden is er geen inspanning geleverd
geweest om deze items gelijk te houden per company. Dit betekent dat
dezelfde bus silicone in verschillende companies een ander nummer kan
hebben. Omgekeerd kan hetzelfde itemnummer iets anders zijn in een
andere company.

In AS400 was het hebben van een item voor een aankoop order ook niet
noodzakelijk. PO's konden gemaakt worden met enkel een omschrijving.
Gegeven het groot volume MTO aankoop was er dus weinig incentive om de
items proper te onderhouden.

Halffabrikaten, aankoop en verkoop items zitten in aparte tabellen in
AS400. In principe is hier dus ook overlap mogelijk.

### D365 structure

In D365 hebben de items een gemeenschappelijke master over de companies
heen. Toch blijven de verschillende items met zelfde naam bestaan in de
companies. Dit werd opgelost door na ieder item in D365 een letter van
de company te plaatsen. Zo wordt gegarandeerd dat alle items uniek
blijven over de companies.

Binnen de 5-digit names is er geen structuur voorzien. De structuur die
bestaat is eerder vanuit vermijden-van-duplicate-nummers in AS400. Bv de
97xxx reeks was vrij in alle companies en is gebruikt voor generieke
artikels (= GA's).

#### Legacy ID

De legacy ID linkt het item terug aan zijn AS400 naam.

![CustomDev 1: [[]{#_Toc209630246 .anchor}Customization
45](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/45): CUS-018:
Legacy system (AS400) identification number for Vendor, Customer,
Products](media/image3.png){alt="A screenshot of a computer AI-generated content may be incorrect."
width="4.220365266841645in" height="1.5542311898512686in"}

#### Chacal ID

Context in [Task
745](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/745): Chacal
ID on released product

> *Doel van dit veld zou zijn om een \"mapping tabel\" bij te houden in
> D365 ipv extern (ook voor latere integratie tussen Chacal en d365).
> Zodanig dat als chacal een artikelnummer mee geeft (is uniek), dat
> D365 kan weten over welk artikel het gaat. Niet nodig op variant, want
> voor:*

- *glas: 1 generiek artikel dat chacal altijd kan meegeven*

- *horren/roosters: 2 generieke artikelen (één voor ALU, één voor PVC),
  Chacal zal weten welkeen van de 2 hij moet doorgeven*

Echter, momenteel is dit veld voor alle items leeg.

CustomDev 2: [[]{#_Toc209630247 .anchor}Task
745](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/745): Chacal
ID on released product

## Specifieke items (distinct)

### Subtype: product

- Scope:

  - Aankoopartikelen die zowel op voorraad gehouden worden (project
    tracking dimension = STOCK)

    - bv. schroeven, motoren, aluminiumprofielen\
      ![A screenshot of a product AI-generated content may be
      incorrect.](media/image4.png){width="4.512928696412948in"
      height="1.4204768153980751in"}

  - Aankoopartikelen die ordergerelateerd aangekocht worden (project
    tracking dimension = %ProjectNum%)

    - Bv. scharnier in standaardkleur

  - Halffabrikaten

### Subtype: product master

- Scope:

  - Aankoopartikelen die altijd ordergerelateerd besteld worden (zowel
    configuration product dimension als project tracking dimension =
    %ProjectNum%), waarbij de configuratiedimensie ad-hoc bij purchase
    order creatie kan gemaakt worden (cf. procure to pay hoofdstuk).\
    ![A screenshot of a computer AI-generated content may be
    incorrect.](media/image5.png){width="8.354166666666666in"
    height="2.2916666666666665in"}

- Gevolgen van specifieke variant per behoefte:

  - EDI is mogelijk

  - Cost price by variant

  - Unieke identificatie van een item doorheen de volledige supply chain

## Generieke items

### Subtype: product

- Scope:

  - Generieke aankoopartikelen

    - Codificatie: 97xxx

    - Product name: begint met GA

    - Gevolgen gezien generiek item:

      - Specificaties worden op transactieniveau (bv. PO-lijn)
        bijgehouden

      - Project tracking dimension is verplicht (om het verbruik te
        sturen)

      - Valuation method: FIFO

      - Geen trade agreements

      - Geen item cost price

      - Geen EDI mogelijk, gezien je geen eenduidige leverancier kan
        koppelen

    - Bijvoorbeeld: ~~een raam van glas met een bepaalde dikte en
      afmetingen, specifiek voor deze verkooporder.~~ Of een standaard
      deurklink bij een leverancier (MTS) , die wij niet in ons
      standaard verkoop assortiment opnemen.\
      ![A screenshot of a computer AI-generated content may be
      incorrect.](media/image6.png){width="6.268055555555556in"
      height="1.9986111111111111in"}

  - Generieke verkoopartikelen

    - Codificatie SAxxx

    - Item type: service

    - Bijvoorbeeld: SO pergola\
      ![A screenshot of a computer AI-generated content may be
      incorrect.](media/image7.png){width="5.202613735783027in"
      height="2.709372265966754in"}

### Subtype: product master

- Scope:

  - Generieke items in te delen in kleurcategorieën

    - Verschillende leveranciers hanteren COL kleurklassen om de prijs
      te bepalen van kleuren. Bv alle standaard kleuren vallen onder de
      COL1 prijs, speciale kleuren onder COL2 en hele speciale onder
      COL3. Dit gaat tot 5 COL's. Deze COL's zijn ook gekend in Chacal.\
      ![A screenshot of a computer AI-generated content may be
      incorrect.](media/image8.png){width="8.707245188101487in"
      height="2.562179571303587in"}

    - Trade agreements per kleurcategorie (config dimensie)

- Gevolgen gezien generiek item:

  - Specificaties worden op transactieniveau (bv. PO-lijn) bijgehouden

  - Project tracking dimension is verplicht (om het verbruik te sturen)

  - Valuation method: FIFO

  - Geen item cost price

  - Geen EDI mogelijk, gezien je geen eenduidige leverancier kan
    koppelen

## Item specific custom fields

Volgende custom velden bestaan op een item:

- LegacyId (cf. [4.1.2.1](#legacy-id))

- ChacalId (cf. [4.1.2.2](#chacal-id))

- SurfaceArea

  - Dit veld maakt deel uit van de 9A kickstart oplossing. [Te bekijken
    hoe dit gebruikt wordt.]{.mark}

ISV 1: []{#_Toc209630296 .anchor}9A Kickstart

- Er werd een customisatie uitgevoerd om dit veld op te nemen in de
  Released products V2 data entiteit.

CustomDev 4: []{#_Toc209630248 .anchor}Change request 1015: Surface area
toevoegen aan Released products V2

## Indeling naar soort en aantal

### Shared products

Het totaal aantal shared products bedraagt ongeveer 43.000 products,
hoewel er overheen alle companies samen slechts 17.000 items bestaan. Er
zijn dus heel wat shared products die in geen enkele company gereleased
werden en dus operationeel niet gebruikt worden. Mogelijks is deze
situatie ontstaan door een vergissing tijdens de master data migratie.

Slechts 288 products bestaan als item in meerdere companies. In
voorkomend geval zijn dit altijd service items.

+----------------------------------------------------------------+
| **Aantal products gereleased naar meerdere companies**         |
+===============+===============+================+===============+
| Number of     | Item type:    | Item type:     | **Grand       |
| companies     | item          | Service        | Total**       |
+---------------+---------------+----------------+---------------+
| 2             | 0             | 210            | **210**       |
+---------------+---------------+----------------+---------------+
| 3             | 0             | 7              | **7**         |
+---------------+---------------+----------------+---------------+
| 4             | 0             | 46             | **46**        |
+---------------+---------------+----------------+---------------+
| 5             | 0             | 3              | **3**         |
+---------------+---------------+----------------+---------------+
| 6             | 0             | 22             | **22**        |
+---------------+---------------+----------------+---------------+
| **Grand       | **0**         | **288**        | **288**       |
| Total**       |               |                |               |
+---------------+---------------+----------------+---------------+

### Released products

Schatting: 20 à 30 nieuwe artikelen / maand

# Winsol product attributes

## Attributes in master data

- Winsol productattributen zijn kenmerken die aan producten worden
  toegekend waardoor het mogelijk is om zonder de overhead van het
  masteren van een nieuw item toch gedetailleerde (aankoop)bestellingen
  te kunnen doen, vooral bij producten die op maat gemaakt worden (MTO).

<!-- -->

- De verschillende attributen zijn een vaste lijst onder de vorm van
  custom velden op een aankooporder, en gedeeltelijk ook in master data
  per product (niet released product dus).

- De verschillende mogelijke waarden per attribuut zijn ook vooraf
  gedefineerd in een aparte master data tabel.

Voor attributen waarvan in de masterdata standaardwaarden zijn
vastgelegd, kunnen deze uitsluitend worden gedefinieerd op het niveau
van het shared product. Het is niet mogelijk om deze attributen toe te
wijzen aan afzonderlijke released products of product variants.

![CustomDev 4: [[]{#_Toc209630249 .anchor}Change request
183](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/183):
CR-XXX: add attributes to released
products](media/image9.png){width="7.874015748031496in"
height="0.7672451881014873in"}

CustomDev 5: []{#_Toc209630250 .anchor}Devops 1228 -- CR028 - Extra
Winsol attribute: Fabric Colour Code

## Attributes in transactional data

De attributen kunnen vanzelfsprekend ook op PO-lijn ingevuld worden.

Deze worden bij het aanmaken van een PO-lijn overgenomen uit master
data, maar kunnen ook telkens overschreven worden bij PO creatie (cf.
tabel hieronder). Sommige attributen worden niet bijgehouden in master
data en zijn altijd op transcationeel niveau te definiëren (al dan niet
via interfacing; cf. procure to pay hoofdstuk).

+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| **Attribute field (PO line)**        | **Defaulted | **Master Data Table**      | **Gebruik**                                         |
|                                      | from master |                            |                                                     |
|                                      | data**      |                            |                                                     |
+======================================+=============+============================+=====================================================+
| ALTInsideInternalColourCodeRefRecId  | TRUE        | ALTWinsolProductAttributes | Winsol kleur referentie van de binnenkant           |
|                                      |             |                            | kleinhouten                                         |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTOutsideInternalColourCodeRefRecId | TRUE        | ALTWinsolProductAttributes | Winsol kleur referentie van de buitenkant           |
|                                      |             |                            | kleinhouten                                         |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTCollection                        | TRUE        | ALTWinsolProductAttributes |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTDiameter                          | TRUE        | ALTWinsolProductAttributes |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTDepartment                        | TRUE        | ALTWinsolProductAttributes | Sturing waar artikel naartoe moet:                  |
|                                      |             |                            |                                                     |
|                                      |             |                            | - Atelier/klant                                     |
|                                      |             |                            |                                                     |
|                                      |             |                            | - Baannr van PVC glas na optimalisatie              |
|                                      |             |                            |                                                     |
|                                      |             |                            | - Afdeling in Helios​                                |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTVentType                          | TRUE        | ALTWinsolProductAttributes |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTDrawingNr                         | TRUE        | ALTWinsolProductAttributes |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTFabricColourCode                  | TRUE        | ALTWinsolProductAttributes |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTProfileType                       | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTLatticeType                       | FALSE       |                            | Kleinhouten: kleinhouten zijn stukken in een groot  |
|                                      |             |                            | raam die de indruk geven dat het raam uit vele      |
|                                      |             |                            | kleine raampjes bestaat                             |
|                                      |             |                            |                                                     |
|                                      |             |                            | ![](media/image10.png){width="0.9647725284339458in" |
|                                      |             |                            | height="1.1394958442694663in"}                      |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTInstallationMethod                | FALSE       |                            | Wordt voorlopig enkel gebruikt voor glas:           |
|                                      |             |                            |                                                     |
|                                      |             |                            | - LW = levering werf                                |
|                                      |             |                            |                                                     |
|                                      |             |                            | - LP = levering productie                           |
|                                      |             |                            |                                                     |
|                                      |             |                            | - ML = los meeleveren                               |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTGrindingType                      | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTControls                          | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTControlsLocation                  | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTOutsideFabricSide                 | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTFabricName                        | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTFabricFinish                      | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTWindingDirection                  | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTGlassType                         | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTGlassIncluded                     | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTBroken                            | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTDateLocation                      | FALSE       |                            |                                                     |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+
| ALTExternalLicensePlate              | FALSE       |                            | Het bok nummer waarop het glas te vinden is. Op een |
|                                      |             |                            | bok staan gemiddeld 20 glazen, en er staan 10       |
|                                      |             |                            | bokken op een vrachtwagen. Het is dus cruciaal voor |
|                                      |             |                            | Winsol om het glas snel terug te vinden.            |
+--------------------------------------+-------------+----------------------------+-----------------------------------------------------+

## Vendor color codes

Het definiëren van een kleur vereist aanzienlijk meer specificiteit dan
het toekennen van een RAL-kleurnummer. Aspecten zoals poederlak en de
gebruikte voor- of nabehandeling dienen in acht genomen te worden,
waardoor er specifieke kleurattributen zijn geïntroduceerd. Om elke
unieke combinatie van kleurattributen en lak-leverancier efficiënt te
kunnen identificeren, is er een interne kleurencode vastgesteld. Deze
interne kleurencode fungeert als één van de eerder benoemde
Winsol-attributen en zorgt voor een eenduidige referentie binnen het
systeem.

  -------------------------------------
  **Field name
  (ALTInternalColourCodesPerVendor)**
  -------------------------------------
  InternalColourCode (= unieke key)

  Colour

  PresurfaceTreatment

  Finish

  PowderCode

  ExternalColourCode

  PowderSupplier

  VendorPriceClass

  VendAccountNum

  VendAccountDataAreaId
  -------------------------------------

![CustomDev : []{#_Toc209630251 .anchor}Change request 1305: CR-033
Externe kleurencodes AluK - optimaliseren
kleurattributen](media/image11.png){alt="A screenshot of a computer AI-generated content may be incorrect."
width="7.82589457567804in" height="2.4727963692038495in"}

**Verdere details:**
<https://winsolgroup.sharepoint.com/sites/BusinessAnalyse/Business%20analyse/kleuren%20architectuur.pptx?web=1>
