# Contents

[Contents [1](#_Toc209806010)](#_Toc209806010)

[CustomDevs [3](#customdevs)](#customdevs)

[ISVs [3](#isvs)](#isvs)

[1 Introduction [4](#introduction)](#introduction)

[1.1 Purchase order driven procurement
[4](#purchase-order-driven-procurement)](#purchase-order-driven-procurement)

[1.1.2 Van offerte naar aankoopproces
[5](#van-offerte-naar-aankoopproces)](#van-offerte-naar-aankoopproces)

[1.1.3 Normale aankopen -- voorraadgestuurd en voorspelbaar
[5](#normale-aankopen-voorraadgestuurd-en-voorspelbaar)](#normale-aankopen-voorraadgestuurd-en-voorspelbaar)

[1.1.4 Ordergerelateerde aankopen -- maatwerk en complexiteit
[6](#ordergerelateerde-aankopen-maatwerk-en-complexiteit)](#ordergerelateerde-aankopen-maatwerk-en-complexiteit)

[1.1.5 Waar de last toeneemt
[6](#waar-de-last-toeneemt)](#waar-de-last-toeneemt)

[1.1.6 De prijsuitdaging [7](#de-prijsuitdaging)](#de-prijsuitdaging)

[1.1.7 Van levering tot facturatie
[7](#van-levering-tot-facturatie)](#van-levering-tot-facturatie)

[1.2 Procurement without purchase orders
[7](#procurement-without-purchase-orders)](#procurement-without-purchase-orders)

[2 Master data [7](#master-data)](#master-data)

[2.1 Items [7](#items)](#items)

[2.2 Suppliers [7](#suppliers)](#suppliers)

[2.3 Prices [8](#prices)](#prices)

[2.4 Putaway locations [8](#putaway-locations)](#putaway-locations)

[3 Purchase agreements [9](#purchase-agreements)](#purchase-agreements)

[3.1 Business scenarios [9](#business-scenarios)](#business-scenarios)

[3.2 Creation [10](#creation)](#creation)

[3.3 Confirmation [10](#confirmation)](#confirmation)

[4 Purchase orders [11](#purchase-orders)](#purchase-orders)

[4.1 Process overview [11](#process-overview)](#process-overview)

[4.2 Business scenarios
[11](#business-scenarios-1)](#business-scenarios-1)

[4.3 Purchase order creation
[12](#purchase-order-creation)](#purchase-order-creation)

[4.3.1 General [12](#general)](#general)

[4.3.2 Manual [15](#manual)](#manual)

[4.3.3 Interface [16](#interface)](#interface)

[4.3.4 Release order from purchase agreement
[18](#release-order-from-purchase-agreement)](#release-order-from-purchase-agreement)

[4.3.5 Firmed from planned order (master planning)
[18](#firmed-from-planned-order-master-planning)](#firmed-from-planned-order-master-planning)

[4.4 Purchase order confirmation
[18](#purchase-order-confirmation)](#purchase-order-confirmation)

[4.4.1 General [18](#general-1)](#general-1)

[4.4.2 Manual [19](#manual-1)](#manual-1)

[4.4.3 EDI [19](#edi)](#edi)

[4.4.4 Automatic [19](#automatic)](#automatic)

[4.5 Purchase order supplier confirmation
[19](#purchase-order-supplier-confirmation)](#purchase-order-supplier-confirmation)

[4.5.1 General [19](#general-2)](#general-2)

[4.5.2 Manual processing [20](#manual-processing)](#manual-processing)

[4.5.3 EDI processing [21](#edi-processing)](#edi-processing)

[4.6 Purchase order product receipt and putaway
[21](#purchase-order-product-receipt-and-putaway)](#purchase-order-product-receipt-and-putaway)

[4.6.1 General [21](#general-3)](#general-3)

[4.6.2 Item arrival journal
[22](#item-arrival-journal)](#item-arrival-journal)

[4.6.3 Load (WMS) [24](#load-wms)](#load-wms)

[4.6.4 Product receipt on purchase order
[26](#product-receipt-on-purchase-order)](#product-receipt-on-purchase-order)

[4.7 Special cases [26](#special-cases)](#special-cases)

[4.7.1 Returns [26](#returns)](#returns)

[4.7.2 Underdeliveries [26](#underdeliveries)](#underdeliveries)

[5 Vendor invoice processing
[27](#vendor-invoice-processing)](#vendor-invoice-processing)

# CustomDevs

- [Change request 681: CR-010: Surface area en net weight toevoegen aan
  trade agreement lines (+data entiteit) 🡺 Deze is niet
  operationeel](#_Toc209805817)

- [Change request 485: CR-005 \"Location\" op released product (voor
  niet-WMS artikelen)](#_Toc209805818)

- [Change request 1847: Item inquiry: winsol locations zichtbaar
  maken](#_Toc209805819)

- [Change request 717: CR-011 Purchase agreement
  document](#_Toc209805820)

- [Change request 1272: CR-036 Financiële dimensies - Order gerelateerde
  stock PVC/ALU](#_Toc209805821)

- [Change request 1505: CR-038 Project doorkopiëren naar
  WinsolSalesReference op PO line (uitbreiding op
  CR-036)](#_Toc209805822)

- [Change request 503: CR-009: Winsol velden op purchase order
  line](#_Toc209805823)

- [Change request 1535: CR-039 Interne opmerking op PO voor
  magazijn](#_Toc209805824)

- [Change request 1020: CR-019 Boolean \"On demand\" op PO
  header](#_Toc209805825)

- [Change request 954: CR-018 Automatic config id
  creation](#_Toc209805826)

- [Change request 875: CR-013 Copy Winsol attributes](#_Toc209805827)

- [Change request 1885: PO copy lines: exclude certain Winsol
  attributes](#_Toc209805828)

- [Change request 349: CR-008: Project id\'s van AO-regels aan PO
  bevestiging hangen als tag](#_Toc209805829)

- [Change request 876: CR-014 Default location on item arrival journal
  lines + BOM journal lines](#_Toc209805830)

- [Change request 1389: CR-037 Item arrival document
  glasreceptie](#_Toc209805831)

- [Change request 1590: CR-040 Uitbreiding item arrival journal document
  (CR-021)](#_Toc209805832)

- [Change request 1072: CR-022 Load details document](#_Toc209805833)

# ISVs

- [9A kickstart : gebruik van purchase entry unit](#_Toc209373503)

# Introduction

## Purchase order driven procurement

![](media/image1.png){width="7.874015748031496in"
height="7.881727909011373in"}

Om de specificiteit van het Winsol aankoop proces te demonstreren wordt
een voorbeeld uitgewerkt : van offerte in CPQ tot productie en
facturatie van leveranciers

#### Startpunt: klantofferte via CPQ

Wanneer een klant bij Winsol aanklopt voor een nieuw product ---
bijvoorbeeld een raam, deur of poort --- start het traject met een
bezoek van een verkoper. Die meet het product nauwkeurig op en voert
alle gegevens in de **CPQ-tool** (Configure, Price, Quote).

In die tool worden de afmetingen, materialen, kleuren en extra opties
vastgelegd. De CPQ berekent direct een verkoopprijs en maakt een
offerte.

Neem als voorbeeld een raam van 1,36 meter breed en 2,05 meter hoog, met
dubbel glas, zonwerende folie en in een donkerbruine RAL-kleur, satijn
afgewerkt en geanodiseerd. Wat in CPQ simpelweg als "bruin" verschijnt,
wordt technisch vertaald naar een RAL-nummer, een poedercode, eventuele
leverancierskleurcode, een glansafwerking en een vlag voor anodisatie.
Dat detailniveau is cruciaal, want alle partijen in de keten moeten
exact dezelfde kleurinformatie hanteren.

**Korte samenvatting:**

- Verkoper meet en voert info in CPQ-tool.

- Klant ziet eenvoudige opties, technisch vertaald naar volledige
  specificaties (RAL, poedercode, afwerking, anodisatie).

- Offerte wordt automatisch berekend en opgemaakt.

### Van offerte naar aankoopproces

Zodra de klant akkoord gaat, start de inkoop van onderdelen. Winsol kent
hierin twee duidelijk verschillende stromen: **normale aankopen** en
**ordergerelateerde aankopen**. Beide leveren onderdelen aan de
productie, maar verschillen sterk in aanpak, voorspelbaarheid en
administratieve belasting.

**Korte samenvatting:**

- Twee aankoopstromen: voorraadgestuurd (normaal) en projectgestuurd
  (ordergerelateerd).

- Grootste uitdagingen zitten in ordergerelateerde stroom.

### Normale aankopen -- voorraadgestuurd en voorspelbaar

Normale aankopen gaan over onderdelen die altijd op voorraad liggen,
zoals hoekverbindingen, schroeven of rubbers. Elk artikel heeft een
uniek itemnummer, gekoppeld aan minstens één voorkeurleverancier. In het
ERP staan prijsafspraken, kortingen en levertijden vastgelegd in *trade
agreements*.

Het bestelproces is grotendeels geautomatiseerd: het systeem monitort
minimum- en maximumvoorraden en triggert een bestelling zodra nodig. De
bestelling wordt nog manueel ingelegd. De leverancier kent het artikel
precies via het interne en externe itemnummer, en levert volgens de
afgesproken condities.

**Korte samenvatting:**

- Standaardcomponenten met uniek itemnummer.

- Voorkeurleverancier en condities staan vast.

- Bestelling gebaseerd op voorraaddrempels.

- Lage complexiteit, weinig handwerk.

### Ordergerelateerde aankopen -- maatwerk en complexiteit

Ordergerelateerde aankopen zijn volledig uniek voor één klantorder. In
plaats van specifieke artikelnummers gebruikt Winsol generieke nummers,
aangevuld met vrije tekst en soms technische tekeningen.

Voorbeeld: een profielset voor een raam in een specifieke kleur en
afwerking. Dat profiel start als ruw aluminium, wordt gelakt in de
juiste RAL-kleur met poedercode, in mat of satijn, en soms geanodiseerd.
Leverancierskleurcodes worden ook vastgelegd, zodat er geen
misverstanden ontstaan.

Bij plooiwerk is een beschrijving vaak onmogelijk zonder tekening. Het
aankooporder verwijst dan naar een PDF-tekening (PO-attachment), zodat
de leverancier exact weet wat te maken.

**Korte samenvatting:**

- Unieke onderdelen per klantorder.

- Generieke artikelcodes + vrije tekst of tekening.

- Extra complexiteit bij kleur (RAL, poedercode, afwerking, anodisatie).

- Leverancierskleurcodes worden gekoppeld voor eenduidige communicatie.

### Waar de last toeneemt

In normale situaties kan één order meerdere identieke producten
bevatten. Bij ordergerelateerde aankopen is dat niet zo: elk product is
uniek. Waar je normaal één order met één orderlijn hebt voor 100 stuks,
heb je hier 100 orders met elk één orderlijn.

Dat verschil merk je in elke stap: bij orderinvoer, bij het verwerken
van orderbevestigingen en bij factuurcontrole. Vooral bij **firma
Actuel** (ramen en deuren) leidt dit tot extreem grote facturen van soms
50 pagina's met honderden orderlijnen, waarvan de verwerking uren kan
duren.

**Korte samenvatting:**

- Elk product is een aparte bestelling.

- Veel meer transacties en administratie.

- Bij Actuel is \>80% van aankopen ordergerelateerd.

- Facturen zijn omvangrijk en tijdrovend om te verwerken.

### De prijsuitdaging

Exacte prijzen vooraf kennen is bij maatwerk lastig. Om dit te doen, zou
Winsol de CPQ-tool van elke leverancier moeten nabouwen --- iets wat in
de praktijk onhaalbaar is.

Daarom wordt de prijs overgenomen uit de orderbevestiging van de
leverancier. Dat bespaart voorbereidend werk, maar is arbeidsintensief
en geeft weinig controle: afwijkingen komen vaak pas laat aan het licht.

**Korte samenvatting:**

- Exacte prijs vooraf kennen is praktisch onhaalbaar.

- Prijs wordt overgenomen uit orderbevestiging.

- Arbeidsintensief en beperkt in controle.

### Van levering tot facturatie

Bij levering worden voorraadartikelen gewoon op stock geboekt.
Ordergerelateerde artikelen krijgen een **projectdimensie** mee: een
koppeling naar het specifieke verkooporder.

Wanneer het verkooporder wordt afgerond, verdwijnt die voorraad
automatisch, zodat de waardering klopt en in rapportages precies
zichtbaar blijft hoeveel er in het order is geïnvesteerd.

De factuurverwerking verloopt bij voorraadartikelen vlot: prijzen en
aantallen komen overeen met wat vastligt. Bij ordergerelateerde
artikelen is de controle veel intensiever, omdat elke factuurlijn met
het juiste order moet worden gematcht.

**Korte samenvatting:**

- Voorraadartikelen: simpel boeken en controleren.

- Ordergerelateerd: voorraad wordt gelabeld op order.

- Factuurcontrole kost veel tijd door unieke lijnen.

## Procurement without purchase orders

Uitzonderlijk worden er ook supply chain relevante items besteld zonder
purchase order. In dat geval wordt de factuur geboekt als expense en is
er geen fysieke ontvangst van de goederen.

# Master data

## Items

Cf. chapter 5

## Suppliers

Cf. chapter 5

## Prices

+----------------------+-----------+---------------+-----------------------------------+
| **Scenario**         | **Master  | **Companies** |                                   |
|                      | system**  |               |                                   |
+======================+===========+===============+===================================+
| ***MTO-aankopen:     | Geen      |               | Geen prijzen in ERP               |
| standaard***         |           |               |                                   |
|                      |           |               | Eventueel manueel bijgewerkt in   |
|                      |           |               | PO bij ontvangst van bevestiging  |
|                      |           |               | leverancier                       |
+----------------------+-----------+---------------+-----------------------------------+
| ***MTO-aankopen:     | Excel     | WBL           | Geen prijzen in ERP               |
| glas***              |           |               |                                   |
|                      |           |               | Wordt via Excel add-in bijgewerkt |
|                      |           |               | op PO lines.                      |
+----------------------+-----------+---------------+-----------------------------------+
| ***MTS-aankopen:     | D365FSCM  |               | Prijzen op trade agreements       |
| standaard***         |           |               |                                   |
+----------------------+-----------+---------------+-----------------------------------+
| ***MTS-aankopen: alu | Excel     | HLS?          | Geen prijzen in ERP, gezien       |
| profielen***         |           |               | maandelijkse marktprijs.          |
|                      |           |               |                                   |
|                      |           |               | Wordt via Excel add-in bijgewerkt |
|                      |           |               | op PO lines.                      |
+----------------------+-----------+---------------+-----------------------------------+
| ***MTO/MTS-aankopen: | D365FSCM  | ACT           | Prijzen in trade agreements       |
| gelakt***            |           |               | volgens kleurcategorie            |
|                      |           |               | (productdimensie "configuration") |
+----------------------+-----------+---------------+-----------------------------------+
| ***MTS-aankopen:     | D365FSCM  |               | Prijzen in purchase agreements    |
| bulk***              |           |               | (cf. volgende paragraaf)          |
+----------------------+-----------+---------------+-----------------------------------+

CustomDev 1: [[]{#_Toc209805817 .anchor}Change request
681](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/681):
CR-010: Surface area en net weight toevoegen aan trade agreement lines
(+data entiteit)\
🡺 Deze is niet operationeel

## Putaway locations

Verschillende mogelijkheden:

  -----------------------------------------------------------------------
                          **Item heeft vaste      **Item heeft geen vaste
                          locatie**               locatie**
  ----------------------- ----------------------- -----------------------
  **Locaties zijn gekend  Locatie bijgehouden als Locatie wordt afgeleid
  in D365 WMS**           fixed product location  via de location
                          op item                 directives

  **Locaties zijn niet    Locatie bijgehouden als Generieke GEN locatie
  gekend in D365 WMS**    vrije tekst in veld     wordt gebruikt
                          "Winsol location(s)" op 
                          item                    
  -----------------------------------------------------------------------

![CustomDev 2: [[]{#_Toc209805818 .anchor}Change request
485](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/485): CR-005
\"Location\" op released product (voor niet-WMS
artikelen)](media/image2.png){alt="Afbeelding met tekst, schermopname, software, nummer Door AI gegenereerde inhoud is mogelijk onjuist."
width="8.889419291338582in" height="4.639712379702537in"}

CustomDev 3: [[]{#_Toc209805819 .anchor}Change request
1847](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1847): Item
inquiry: winsol locations zichtbaar maken

# Purchase agreements

## Business scenarios

- Leveranciers waarmee je een volumecontract hebt; typisch voor kleine
  bulk items met lange lead tiems

  - Bv. supplier "global supplies" heeft een prijs op jaarvolume en
    importeert uit China en zij leggen het op stock in BE en wij kunnen
    afroepen

  - Eén keer per jaar wordt een aanvraag gedaan voor een lijst van items
    met een bepaald volume, waarna de purchase agreement tot stand komt

- Actuell (ACT): ook gebruikt voor volumeprijzen

- Aluminium op afroep

  - Soms worden volumes in tonnage vastgelegd voor een bepaalde prijs.
    De concrete bestelde profielen zijn dan nog vrij te kiezen binnen
    dit tonnage. Op vandaag wordt dit niet beheerd in D365, maar in XLS.

  - Uitdagingen om dit in een purchase agreement te krijgen:

  - De link tussen het volume in ton en de specifieke profielen. Dit
    betekent dat de effectief aangekochte items zouden gelinkt moeten
    worden aan brut-alu item. Tegelijk dient de PA dan afgeboekt te
    worden in functie van de effectief geconsumeerde tonnages van de
    specifieke items.

  - De prijssetting bestaat niet enkel uit brut alu. Hoewel een prijs
    voor het brut alu in ton wordt overeengekomen kan de effectieve
    prijs van de items nog afwijken. Bv een gelakt item waar nog een CNC
    operatie opzit krijgt dan een prijs als volgt :

    - Afgesproken brut prijs per ton

    - \+ lak operatie in functie van gekozen kleur (zie chapter COLs) en
      m²

    - \+ CNC operatie prijs

    - = totaal prijs

Analyse van de UAT-database (dd. 26/09/2025):

  ----------------------------------
  **VendorDataAreaId**     **Count**
  ---------------------- -----------
  act                              3

  hls                             47

  ind                              1

  wbl                              4
  ----------------------------------

## Creation

- Altijd manueel aangemaakt

- Winsol attributes zijn niet voorzien op purchase agreements

  - De attributes worden wel ingevuld op de PO lijn bij het releasen van
    een PA naar een PO

## Confirmation

- Bij confirmation wordt er een document gegenereerd, dat ook
  geëxporteerd wordt naar Raptor.

CustomDev 4: [[]{#_Toc209805820 .anchor}Change request
717](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/717): CR-011
Purchase agreement document

# Purchase orders

## Process overview

![A screenshot of a computer AI-generated content may be
incorrect.](media/image3.png){width="11.475in"
height="7.722916666666666in"}

## Business scenarios

- HLS: stockbestelling

- ACT: glasbestelling (Chacal)

- HLS: SO! bestelling (Excel)

- ACT: horren (WinCal)

- WBL: Tekla-bestelling

- WBL: purchase agreement bestelling

- HLS: MRP-bestelling

## Purchase order creation

### General

#### Leveradres

Levering op de werf is mogelijk (bv. bij grote hoeveelheden glas voor
projecten)

- Adres wordt manueel overschreven

  - One-time address dient aangevinkt te worden, maar dit wordt vaak
    vergeten.

- Warehouse wordt manueel aangepast naar "ONSITE"

#### Financial dimensions

Cf. [Handleiding - PO business unit &
kostenplaats.docx](https://winsolgroup.sharepoint.com/:w:/s/ERP/EQw7dnSPlgRKrtBuuhR-asgBuPFgknQfsRChriUweqYu3w?e=Ckac1F)

+----------------------+----------------------------------------------------+
| BusinessUnit         | - Kostenplaats                                     |
|                      |                                                    |
|                      | - Afgeleid vanaf de project tracking dimension     |
|                      |   (kolom business unit)                            |
|                      |                                                    |
|                      |   - WNV: bv. je koopt een bus silicone aan voor    |
|                      |     een B2B vs. B2C project                        |
|                      |                                                    |
|                      |   - ACT: bv. gemeenschappelijke componenten voor   |
|                      |     ALU en PVC onderscheiden                       |
|                      |                                                    |
|                      | - Kan ook gedefaulteerd worden op item             |
+======================+====================================================+
| CostCenter           | - Kostendrager                                     |
|                      |                                                    |
|                      | - Gedefaulteerd vanaf item                         |
|                      |                                                    |
|                      | - In WNV vaak overschreven, gezien afhankelijk van |
|                      |   de transactie (bv. marketing voor B2C vs. B2B)   |
+----------------------+----------------------------------------------------+
| Intercompany         | -                                                  |
+----------------------+----------------------------------------------------+
| NumberPlate          | - Voor bedrijfswagens                              |
+----------------------+----------------------------------------------------+
| PersonnelNumber      | - Voor personeel                                   |
+----------------------+----------------------------------------------------+
| ProductGroup         | -                                                  |
+----------------------+----------------------------------------------------+
| Vendor               | -                                                  |
+----------------------+----------------------------------------------------+
| WinsolSalesReference | - Afgeleid vanaf de project tracking dimension,    |
|                      |   behalve wanneer de tracking dimension = "STOCK"  |
+----------------------+----------------------------------------------------+

: CustomDev : [[]{#_Toc209805821 .anchor}Change request
1272](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1272):
CR-036 Financiële dimensies - Order gerelateerde stock PVC/ALU

CustomDev : [[]{#_Toc209805822 .anchor}Change request
1505](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1505):
CR-038 Project doorkopiëren naar WinsolSalesReference op PO line
(uitbreiding op CR-036)

#### Purchase order line tekst

Bevat een manueel ingevulde omschrijving. Vaak gebruikt bij GA artikelen
om exact te specifiëren wat nodig is bij de supplier.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image4.png){width="2.941547462817148in"
height="1.8452220034995626in"}

#### Units

Voor aankoop bestellingen zijn er de "purchase unit" en de **"entry
unit"**, naast de "inventory unit".

- Voorbeeld: screendoek

  - Inventory unit = lopende meter (gezien dit zo verbruikt wordt;
    kleinste unit)

  - Purchase unit = vierkante meter (gezien de prijszetting en
    facturatie per vierkante meter gebeurt)

  - Purchase entry unit = rol (gezien per rol besteld wordt)

- Voor generieke items is dit moeilijk inzetbaar. Daarvoor staat de unit
  quasi altijd op pcs.

- Gebruik

  - Bij aanmaak van een PO kan men de ingave via zowel entry als
    standaard unit doen. Deze wordt in twee richtingen omgerekend
    volgens de unit conversions.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image5.png){width="6.268055555555556in"
height="2.7694444444444444in"}

- Integratie met AS400

  - AS400 kent geen verschil in bestel / stock / verbruik UOM. Om dit op
    te vangen werden UOM's gedefinieerd als "lopende meter lengte". Wat
    aangeeft dat bestellingen in meter gebeuren en stock bijgehouden
    wordt in volle lengtes (=pcs). Er zijn dus mapping issues tussen
    D365 en AS400

  - De UOM op zich wordt niet geïntegreerd met andere applicaties. Toch
    is het een cruciaal aandachtspunt. Bv de PO's worden gesynct met
    AS400. In AS400 bestaan heel andere UOM's dan in D365. Er is een
    enorme opkuis in hoeveelheid UOMs gebeurd. Geeft dat eigenlijk
    problemen op vandaag -- bij de PO sync ? AS400 items ziujn in UOM
    gelijk gezet aan D365, zodat dit geen issues geeft

ISV : []{#_Toc209373503 .anchor}9A Kickstart

#### Price unit

Staat quasi altijd op 1000, om afrondingsfouten te vermijden.

#### Warehouse & location

Bij de bestelling wordt in Actuell & Winbalu vaak een WMS location
ingevuld.

- ACT: om een receptie rechtstreeks uit de PO te kunnen doen (product
  receipt)

  - Typisch wanneer tracking dimension = STOCK (dus
    niet-ordergerelateerde bestellingen)

- WBL: om goederen te bestellen voor een specifieke werfleider. Iedere
  werfleider heeft zo zijn locatie.

Ontvangst met WMS -scanner is niet compatibel met deze locatie. Gebruik
van locatie op PO is dus niet compatibel met WMS ontvangsten.

#### Custom velden

De Winsol-attributen zijn als custom veld aanwezig op het PO-lijnobject,
met uitzondering van de kleurattributen. Deze kleurattributen worden
weergegeven op basis van de interne kleurcode uit de masterdata (zie ook
hoofdstuk over masterdata).

CustomDev 7: [[]{#_Toc209805823 .anchor}Change request
503](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/503):
CR-009: Winsol velden op purchase order line

#### Delivery dates

- Requested delivery date

  - HLS: veelal ingevuld vanaf de gekende lead time (trade agreement)

  - ACT: altijd manueel ingevuld, gezien Chacal geen gevraagde leverdata
    kent en doorstuurt

#### Attention information

Standaard vrijtekstveld op PO header. Wordt gebruikt voor interne
communicatie maar komt ook op het document, vnl. in de ALU afdeling. Bv.
er werd gebeld naar de supplier en een lijn zal later zijn of ... In de
praktijk vormt het geen probleem, gezien de PDF gemaakt wordt voor men
de attention information invult.

Daarnaast bestaat er ook een customisatie om de note-attachments
(DocuRef) van een PO-lijn te tonen in een arrival journal. Deze
customisatie wordt echter niet meer gebruikt, waardoor deze overbodig is
geworden.

CustomDev 9: [[]{#_Toc209805824 .anchor}Change request
1535](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1535):
CR-039 Interne opmerking op PO voor magazijn

#### On demand & requester

On demand = op afroep. Deze vlag wordt gezet indien de bestelling pas op
afroep mag geleverd worden. Dit wordt gebruikt in ACT projecten, B2B en
glas.

Indien het veldje on demand wordt opgezet, dient een requester te worden
ingevuld. Dit voor flows waarbij iets specifiek op vraag van iemand
besteld wordt. In dit geval verschijnen de contactgegevens van de
requester op de aankoop PDF.

CustomDev 10: [[]{#_Toc209805825 .anchor}Change request
1020](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1020):
CR-019 Boolean \"On demand\" op PO header

### Manual

Bij manuele creatie is het mogelijk om ad-hoc een dimensiewaarde voor de
productdimensie "Configuration" aan te maken als deze optie geactiveerd
is op de dimensiegroep:

![CustomDev 11: [[]{#_Toc209805826 .anchor}Change request
954](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/954): CR-018
Automatic config id
creation](media/image6.png){alt="A screenshot of a computer AI-generated content may be incorrect."
width="7.874015748031496in" height="3.834747375328084in"}

Een wijziging werd doorgevoerd zodat de Winsol product attributes
gekopieerd worden vanaf de originele PO lijn bij het gebruik van "copy
lines".

CustomDev : [[]{#_Toc209805827 .anchor}Change request
875](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/875): CR-013
Copy Winsol attributes

Bij het kopiëren van een orderlijn voor een herbestelling, zijn er
specifieke **Winsol-attributen** die **niet langer mogen worden
mee-gekopieerd**. Dit is om te vermijden dat foutieve of irrelevante
data wordt overgenomen in de nieuwe orderlijn. De attributen die **niet
mogen worden gekopieerd**, zijn:

- **Department**

  - Wordt afgeleid uit de optimalisatie en kan verschillen bij
    herbestellingen.

  - Enkel voor bepaalde artikels (zoals glas) mag dit niet meegekopieerd
    worden.

- **Installation Method**

  - Is niet noodzakelijk gelijk aan de originele bestelling.

- **Date location**

  - Betreft leveringsinformatie die bij ordercreatie nog niet gekend is.

- **External License Plate**

  - Ook gerelateerd aan levering en dus mogelijk foutief bij kopiëren.

- **Broken**

  - Mag niet meegekopieerd worden, zeker in garantiegevallen.

Deze aanpassing aan bovenstaand maatwerk werd nog niet uitgevoerd:

CustomDev : [[]{#_Toc209805828 .anchor}Change request
1885](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1885): PO
copy lines: exclude certain Winsol attributes

### Interface

Gezien het volume van ordergerelateerde bestellingen en de details die
er zijn om een specifiek glas / doek / profiel te bestellen, lopen een
aantal bestellingen via interfaces. In dit geval wordt vanuit de
CTO-tooling een interface naar D365 gestuurd om de bestelling op te
maken. In alle gevallen dient de bestelling nog manueel gevalideerd en
geconfirmeerd te worden.

+------------+-------------+------------------+------------------------------------+
| **Source** | **Interface | **Applicable     | **Context**                        |
|            | type**      | business         |                                    |
|            |             | scenarios**      |                                    |
+============+=============+==================+====================================+
| *Chacal*   | JSON        | - ACT: glas      | Voor ramen wordt het volledige     |
|            |             |                  | dossier (= verkoop order of        |
|            |             |                  | project) opgemaakt in Chacal met   |
|            |             |                  | alle technische details.           |
|            |             |                  | Uiteindelijk komt er een JSON uit  |
|            |             |                  | Chacal met de verschillende        |
|            |             |                  | ordergerelateerde bestellingen bij |
|            |             |                  | de verschillende leveranciers voor |
|            |             |                  | dit dossier.                       |
|            |             |                  |                                    |
|            |             |                  | Een orderverwerker dient dus na de |
|            |             |                  | afwerking van zijn dossier in      |
|            |             |                  | Chacal naar Dynamics te gaan om de |
|            |             |                  | bestellingen voor dit dossier      |
|            |             |                  | effectief uit te sturen            |
|            |             |                  |                                    |
|            |             |                  | - Glas: met al zij details (LxBxH, |
|            |             |                  |   refs, leverplaatsen, productie   |
|            |             |                  |   informatie, ...)                 |
|            |             |                  |                                    |
|            |             |                  |   - Gevraagde leverdatum: vandaag  |
|            |             |                  |     -- manueel aan te passen in    |
|            |             |                  |     D365                           |
|            |             |                  |                                    |
|            |             |                  |   - Werflevering: leveradres en    |
|            |             |                  |     warehouse manueel aan te       |
|            |             |                  |     passen in D365                 |
|            |             |                  |                                    |
|            |             |                  |   - Attachments: voor speciale     |
|            |             |                  |     gevallen (kleinhouten of       |
|            |             |                  |     afgerond) maakt Chacal een     |
|            |             |                  |     tekening, dewelke wordt        |
|            |             |                  |     opgeladen in Raptor en meekomt |
|            |             |                  |     met de PO-confirmation mail.   |
|            |             |                  |     De upload van Chacal naar      |
|            |             |                  |     Raptor gebeurt automatisch.    |
|            |             |                  |                                    |
|            |             |                  | - Profielen (Aluk)                 |
|            |             |                  |                                    |
|            |             |                  |   - De precieze afmetingen van de  |
|            |             |                  |     profielen in Chacal worden     |
|            |             |                  |     vertaald naar volle lengtes of |
|            |             |                  |     dus pieces om te bestellen     |
|            |             |                  |                                    |
|            |             |                  |   - Typisch items met              |
|            |             |                  |     configuration ID's voor de     |
|            |             |                  |     prijsbepaling (cf.             |
|            |             |                  |     kleurcategorieën)              |
|            |             |                  |                                    |
|            |             |                  | - Andere                           |
|            |             |                  |                                    |
|            |             |                  | Chacal berekent een prijs. Deze    |
|            |             |                  | prijs wordt voor enkele            |
|            |             |                  | leverancier overgenomen in de PO   |
|            |             |                  | (Renson, Harinck), voor andere     |
|            |             |                  | wordt toch een 0-prijs op de PO    |
|            |             |                  | genomen.                           |
|            |             |                  |                                    |
|            |             |                  | De uitgaande interface van Chacal  |
|            |             |                  | zelf is een BOM lijst. Er is een   |
|            |             |                  | post processing programma (Chacal  |
|            |             |                  | interface, custom develop by       |
|            |             |                  | Winsol) dat op basis van een       |
|            |             |                  | masterdatalijst "te bestellen      |
|            |             |                  | item" bepaalt welke bomlijnen een  |
|            |             |                  | bestelling en dus een json nodig   |
|            |             |                  | hebben.                            |
|            |             |                  |                                    |
|            |             |                  | Er bestaat ook een mapping tussen  |
|            |             |                  | chacal-ID's en dynamics items.     |
|            |             |                  | Deze is niet noodzakelijk 1-1. Er  |
|            |             |                  | zijn bv mappings om met product    |
|            |             |                  | varianten om te gaan voor ALUK.    |
+------------+-------------+------------------+------------------------------------+
| *Excel*    | Excel       | - HLS: SO!       | Bij een pergola SO! of ZIP kunnen  |
|            | add-in      |   pergola        | verschillende onderdelen           |
|            |             |                  | ordergerelateerd bij suppliers     |
|            |             |                  | besteld worden. Bv een houten      |
|            |             |                  | zijwand, of een glazen schuifwand  |
|            |             |                  | wordt op zijn geheel bij een       |
|            |             |                  | leverancier besteld. Vanuit de     |
|            |             |                  | CTO-XLS worden JSON's aangemaakt   |
|            |             |                  | die naar bestellingen vertaald     |
|            |             |                  | worden binnen Dynamics             |
+------------+-------------+------------------+------------------------------------+
| *WinCal*   | JSON        | - ACT: horren    | Een specifiek geval zit bij de     |
|            |             |                  | losse bestelling van een hor in    |
|            |             |                  | wincal. Deze wordt op zijn geheel  |
|            |             |                  | besteld bij Byttebier. Er komt een |
|            |             |                  | JSON uit wincal met de nodige      |
|            |             |                  | details, deze wordt opgepikt door  |
|            |             |                  | D365 om deze hor te kunnen         |
|            |             |                  | bestellen bij Byttebier.           |
|            |             |                  |                                    |
|            |             |                  | Als er in Chacal een bestelling is |
|            |             |                  | met een hor bij dan gaat er een    |
|            |             |                  | JSON van Chacal naar WinCal om die |
|            |             |                  | hor te kunnen bestellen.           |
+------------+-------------+------------------+------------------------------------+
| *Tekla*    | ?           | - WBL: glas voor | In Winbalu worden balustrades      |
|            |             |   ballustrades   | getekend in het programma Tekla.   |
|            |             |                  | De resulterende bestellingen       |
|            |             |                  | (enkel glas) komen ook hier als    |
|            |             |                  | JSON uit om door D365 opgepikt te  |
|            |             |                  | worden.                            |
+------------+-------------+------------------+------------------------------------+
| *WinPro\   | ?           | - HLS: Sunconfex | Enkel voor doeken op maat          |
| (AS400)*   |             |                  |                                    |
+------------+-------------+------------------+------------------------------------+
| *Winplan*  | ?           | - WNV:           | Een onderaanneming krijgt een      |
|            |             |   onderaanneming | voorziene vergoeding voor zijn     |
|            |             |                  | werk, hiervoor wordt een PO        |
|            |             |                  | aangemaakt uit winplan (=plantool  |
|            |             |                  | voor plaatsing). Dit werkt met     |
|            |             |                  | zogenaamde ReceptieBonnen (RB's)   |
+------------+-------------+------------------+------------------------------------+

### Release order from purchase agreement

Aankooporders worden ook gemaakt door een release actie uit te voeren
vanaf een purchase agreement.

Enkele details:

- Entry unit kan ook in dit proces gebruikt worden.

- Winsol attributes die gekend zijn in master data worden ook bij
  creatie vanaf een purchase agreement gedefaulteerd op de PO lijn.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image7.png){width="7.874015748031496in"
height="1.9403455818022748in"}

### Firmed from planned order (master planning)

Uit analyse van de UAT database blijkt dat deze functionaliteit niet
algemeen gebruikt wordt:

  --------------------------------------------
  **DataAreaId**   **ReqPlanId**     **Count**
  ---------------- --------------- -----------
  hls              MASTERPLAN               16

  wnv              MASTERPLAN                4
  --------------------------------------------

## Purchase order confirmation

### General

Bij het genereren van de purchase order confirmation wordt de bestelling
formeel doorgestuurd naar de leverancier (hetzij als pdf via mail,
hetzij via EDI).

Voor het opmaken van het pdf-document wordt gebruik gemaakt van business
documents (electronic reporting).

### Manual

De PO wordt geconfirmeerd via "confirmations". Dan wordt via settings
bepaald dat een mail klaargezet wordt naar het mail adres van de
leverancier (rol XXX). Deze mail vertrekt vanuit de mailbox van de
besteller Daarnaast wordt de PDF gegenereerd via MS biz docs. Deze zit
als attachment in de mail. De PDF voor de PO wordt ook toegevoegd aan
raptor. Telkens je de PO wijzigt en opnieuw confirmt wordt de nieuwe PDF
opnieuw opgeslaan in Raptor. Zo heb je de volledige historiek in Raptor.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image8.png){width="4.629441163604549in"
height="2.0187773403324583in"}

### EDI

Het vinkje "send using EDI" in het PO confirmation scherm wordt
automatisch ingevuld op basis van supplier. Op moment dat de gebruiker
de PO confirmeert wordt de EDI uitgestuurd in functie van dit vinkje.
Dit is soms vervelend omdat een EDI te veel wordt uitgestuurd. Bv. bij
een wijziging van een bestelling wordt de EDI per ongeluk dubbel
uitgestuurd met mogelijk een dubbele levering tot gevolg.

### Automatic

Telkens een PO gewijzigd wordt, wordt de PO weer op approved gezet ipv
op confirmed. Via een standaard batch job worden alle PO's die ooit
confirmed waren en nu weer op approved staan, weer confirmed. Dit heeft
geen side-effects, enkel een status update.

## Purchase order supplier confirmation

### General

Wanneer Winsol een aankooporder (PO) verstuurt, volgt er vrijwel altijd
een reactie van de leverancier: de **orderbevestiging** (OB of OC). Dit
document bevestigt officieel dat de leverancier het order heeft
ontvangen en welke condities daarbij horen.

In de meeste gevallen komt de orderbevestiging per e-mail binnen, met
als bijlage een PDF-bestand. Soms wordt de bevestiging echter via
**EDI** verzonden, wat het proces automatiseert. EDI is actief voor
leverancier ALUK, VIN en AGC.

De OB mail komt toe in een gecentraliseerde mailbox per company (HLS) of
afdeling (PVC/ALU) of in de mailbox van de besteller (NV). Hier is een
migratie naar centrale mailboxen aangewezen.

De orderbevestiging bevat een aantal essentiële elementen voor Winsol:

- **Referentie naar het aankooporder** en de bijbehorende **orderlijn**.
  Samen vormen deze de sleutel om de bevestiging correct aan het juiste
  order te koppelen in het systeem.

- **Leverdata**, die soms voor het hele order gelden (headerniveau) en
  soms per orderlijn verschillen (lijnniveau).

- Het **ordernummer van de leverancier**. Dit is bijzonder belangrijk,
  want in alle vervolgcommunicatie verwijst de leverancier liever naar
  zijn eigen ordernummer dan naar het Winsol-aankoopordernummer.

- **Prijzen**, die afhankelijk van de aankoopstroom (normaal of
  ordergerelateerd) al dan niet worden overgenomen in het
  Winsol-systeem.

In sommige scenario's stuurt een leverancier meerdere orderbevestigingen
voor hetzelfde order. Een voorbeeld is **ALU-K**, leverancier van
gelaste onderdelen en profielen. Bij ALU-K verloopt het zo:

1.  Kort na het plaatsen van het order stuurt de leverancier een eerste
    bevestiging met een initiële leverdatum en prijs.

2.  Enkele dagen voor de werkelijke levering volgt een tweede
    bevestiging, vaak met aangepaste aantallen en/of prijzen.

Dit kan ertoe leiden dat Winsol in eerste instantie bevestiging krijgt
voor bijvoorbeeld 20 profielen met leverdatum 10 september, maar dat op
8 september een update binnenkomt waarin nog maar 15 profielen vermeld
staan. In zo'n geval is het cruciaal dat deze wijziging tijdig in het
systeem verwerkt wordt, zodat planning en factuurcontrole kloppen.

De confirmed receipt date wordt gesynct met **AS400**, gezien deze nog
productie aanstuurt. Zo hebben mensen daar zicht op de voorziene
leverdatums.

**Korte samenvatting:**

- Orderbevestiging = officiële reactie leverancier op aankooporder.

- Bevat PO-referentie, PO-lijn, leverdata, leveranciersordernummer en
  prijzen.

- Leveranciersordernummer is cruciaal voor verdere communicatie.

- Kan per e-mail (PDF) of via EDI worden ontvangen.

- Sommige leveranciers sturen meerdere bevestigingen (initieel + update
  vlak voor levering).

- Voorbeeld: ALU-K stuurt eerst leveringsplan, daarna update met
  gewijzigde aantallen en prijzen.

### Manual processing

PDF wordt manueel geïnterpreteerd, geïmporteerd in Raptor. De prijzen en
leverdata worden manueel overgenomen op de PO-lijnen

Alle orderconfirmaties komen in Raptor als PDF en worden gelinkt aan de
PO en het project nummer van Winsol. Ze worden manueel gedrag-dropt in
Raptor en de tag PO wordt manueel gekoppeld.

CustomDev : [[]{#_Toc209805829 .anchor}Change request
349](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/349):
CR-008: Project id\'s van AO-regels aan PO bevestiging hangen als tag

### EDI processing

[Glas wordt via EDI DESADV aangekondigd. Hierbij wordt de arrival
journal klaargezet.]{.mark}

> [Glas arrivals komen binnen via EDI. Er zit een controle flow voor we
> deze EDI's processen in Dynamics om evt fouten te corrigeren]{.mark}
>
> [Er is een customisatie om losse EDI's samen te voegen naar wat een
> geleverde vrachtwagen zal worden. Als EDI's binnenkomen worden ze
> gebundeld per leverdatum (en nog iets) . in een journal. Zoalng het
> journal niet afgedrukt werd, komen nieuwe EDI's voor dezelfde bundel
> (datum, ..) in hetzelfde journal. Eenmaal de journal geprint wordt een
> nieuw journal aangemaakt.]{.mark}
>
> [Er is een specifiek arrival journal layout voor glas : screenshot; en
> waarom is het anders]{.mark}

- [Boknummer : uitleggen]{.mark}

> [DESADV willen we ook opzetten voor andere flows: bv ALUK.]{.mark}

## Purchase order product receipt and putaway

### General

+--------------+----------------+---------------+---------------------------+
| **Product    | **Business     | **Companies** | **Remarks**               |
| receipt      | scenarios**    |               |                           |
| process**    |                |               |                           |
+==============+================+===============+===========================+
| ***Item      | Default        | ACT           |                           |
| arrival      |                |               |                           |
| journal***   |                | HLS           |                           |
|              |                |               |                           |
|              |                | WBL           |                           |
|              |                |               |                           |
|              |                | IND           |                           |
|              +----------------+---------------+---------------------------+
|              | Glass          | ACT           |                           |
|              +----------------+---------------+---------------------------+
|              | Alu            | ACT           | Hier bestaat wél behoefte |
|              |                |               | aan locaties, maar wordt  |
|              |                |               | nog gewerkt met een       |
|              |                |               | oudere                    |
|              |                |               | **AS400-implementatie**.  |
|              |                |               | De ontvangst wordt in dit |
|              |                |               | geval zowel in Dynamics   |
|              |                |               | als in AS400              |
|              |                |               | geregistreerd. Zo kunnen  |
|              |                |               | de goederen in Dynamics   |
|              |                |               | administratief worden     |
|              |                |               | ontvangen, en tegelijk in |
|              |                |               | AS400 worden toegewezen   |
|              |                |               | aan een specifieke        |
|              |                |               | fysieke locatie.          |
+--------------+----------------+---------------+---------------------------+
| ***Loads     | Default        | HLS           |                           |
| (WMS)***     |                |               |                           |
|              |                | WBL           |                           |
|              |                |               |                           |
|              |                | IND           |                           |
|              +----------------+---------------+---------------------------+
|              | Profielen      | HLS           | WMS-locatie per fysiek    |
|              |                |               | rek                       |
|              |                |               |                           |
|              |                |               | License plate = 1 pak     |
|              |                |               | profielen = 1 pallet      |
|              |                |               |                           |
|              |                |               | LP verdwijnt van zodra    |
|              |                |               | het op de picking locatie |
|              |                |               | wordt neergezet           |
+--------------+----------------+---------------+---------------------------+
| ***PO        | On-site        |               |                           |
| product      | delivery       |               |                           |
| receipt***   |                |               |                           |
|              +----------------+---------------+---------------------------+
|              | Services       |               |                           |
|              +----------------+---------------+---------------------------+
|              | Exceptional    |               | Als de fysieke ontvanger  |
|              |                |               | en diegene die het item   |
|              |                |               | arrival journal zou       |
|              |                |               | boeken dezelfde persoon   |
|              |                |               | is                        |
+--------------+----------------+---------------+---------------------------+

De zendnota's van leveranciers worden toegevoegd aan Raptor:

- Voor HLS, IND en WBL worden uitsluitend de per e-mail ontvangen
  documenten (pdf) in Raptor geplaatst.

- Voor ACT worden alle zendnota's ingescand en in Raptor gezet. Daarbij
  worden ze getagd met PO-nummers.

  - Dit gebeurt omdat ontvangsten bij ACT op verschillende plaatsen
    voorkomen.

  - Als er een probleem is met de ontvangst, kunnen de zendnota\'s via
    Raptor worden teruggevonden om te achterhalen wat er is gebeurd.

  - Het scannen en koppelen aan PO's in Raptor is een tijdsintensief
    proces: elk document wordt afzonderlijk gescand en gelinkt.

### Item arrival journal

![](media/image9.png){width="9.84251968503937in"
height="4.679627077865267in"}

**Proces:**

- Op basis van de zendnota wordt een arrival journal aangemaakt.

  - Fixed product locations worden middels de maatwerkknop "Fill in
    locations" ingevuld op de journal lines.

    - Indien de finale locatie gekend is als WMS-locatie in D365 wordt
      deze ingevuld en afgedrukt op het document.

    - Indien de finale locatie niet gekend is als WMS-locatie in D365
      wordt de locatie "GEN" voorgesteld en wordt de finale locatie
      afgeleid van het maatkwerkveld "Winsol location" op een item, en
      zo afgedrukt op het document.

CustomDev 14: [[]{#_Toc209805830 .anchor}Change request
876](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/876): CR-014
Default location on item arrival journal lines + BOM journal lines

- Van dit journaal wordt tevens een fysiek arrival journal-document
  gegenereerd via SSRS. Er zijn twee varianten beschikbaar: de
  standaardversie en een specifieke versie voor glas bij Actuell. Het
  arrival document vermeldt de Winsol-locaties, waarmee de
  magazijnmedewerker efficiënt kan worden aangestuurd tijdens het
  wegzetten van goederen.

![CustomDev 15: [[]{#_Toc209805831 .anchor}Change request
1389](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1389):
CR-037 Item arrival document
glasreceptie](media/image10.jpeg){alt="A bar code on a white background AI-generated content may be incorrect."
width="6.268055555555556in" height="3.0521741032370953in"}

CustomDev : [[]{#_Toc209805832 .anchor}Change request
1590](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1590):
CR-040 Uitbreiding item arrival journal document (CR-021)

- De levering vindt vervolgens plaats met zowel de zendnota van de
  leverancier als het arrival document, waarna de goederen naar de
  juiste opslaglocatie worden gebracht. Zo worden bijvoorbeeld doeken na
  ontvangst bij de receptie doorgestuurd naar de opslagafdeling voor
  verdere verwerking.

- Eventuele correcties worden duidelijk aangegeven op het fysieke
  arrival document.

- Indien er afwijkingen zijn, voert de backoffice handmatige correcties
  door in het arrival journal binnen D365, bijvoorbeeld bij verschillen
  in hoeveelheid of kwaliteitsproblemen.

- Ten slotte vindt de finale posting van het arrival journal plaats.

**Opmerkingen en bedenkingen:**

- Arrival journals staan soms lang open, wat vervelend is bij het
  afsluiten van de maand.

  - Bv. ALUK wordt fysiek ontvangen en wordt gecontroleerd op
    hoeveelheid en kwaliteit. Dit kan tot 2 weken duren.

### Load (WMS)

![](media/image11.png){width="8.661417322834646in"
height="5.258092738407699in"}

**Proces:**

- Load wordt gemaakt vanaf de Inbound load planning workbench op basis
  van de zendnota die de leverancier doorgestuurd heeft.

- Het Load details document (SSRS) wordt afgedrukt en klaargelegd aan de
  receptie.\
  ![A close up of a receipt AI-generated content may be
  incorrect.](media/image12.png){width="7.086614173228346in"
  height="5.03112532808399in"}

CustomDev 17: [[]{#_Toc209805833 .anchor}Change request
1072](https://dev.azure.com/WinsolGroup/D365/_workitems/edit/1072):
CR-022 Load details document

- De loadontvangst wordt gestart vanuit de WMS scanner ("Load
  receiving"), waarbij het load ID gescand wordt vanaf het fysieke load
  details document (QR-code).\
  ![A screenshot of a computer AI-generated content may be
  incorrect.](media/image13.png){width="5.1924125109361325in"
  height="2.2701979440069993in"}

  - Bij het starten van de ontvangst worden de LP labels afgedrukt.

> ![A close up of a paper AI-generated content may be
> incorrect.](media/image14.png){width="2.7124146981627297in"
> height="4.068622047244094in"}

- De magazijnier doorloopt de ontvangststappen via de scanner:

  - Bevestigen van items en hoeveelheden

  - Wegzetten op de finale locatie op basis van de location directives.

- Het fysieke load details document gaat samen met de fysieke zendnota
  naar de eigenlijke ontvanger. Dit kan elders in de fabriek zijn. Zij
  posten dan de product receipt voor de load.

### Product receipt on purchase order

Een aantal PO's wordt rechtstreeks op de PO geregistreerd, zonder
gebruik te maken van een load of een item arrival journal. Dit gebeurt
in de volgende situaties:

- Wanneer de levering niet direct kan worden gecontroleerd doordat de
  ontvangst plaatsvindt op een externe locatie, zoals een bouwterrein
  (bijvoorbeeld glasleveringen op de werf, goederen bestemd voor
  projecten).

- Indien de magazijnmedewerker zowel het aanmaken van de arrival journal
  als de ontvangst uitvoert, is het opsplitsen in twee afzonderlijke
  stappen weinig efficiënt.

- Diensten: goederen die niet fysiek worden ontvangen, zoals de huur van
  een hoogwerker op locatie of consultancyactiviteiten.

**Opmerkingen en aandachtspunten:**

- De registratie via rechtstreekse PO-boeking biedt minder transparantie
  bij logregistratie, waardoor probleemopsporing bemoeilijkt kan worden.
  Tracering verloopt efficiënter met gebruik van arrival journals.

- Bij het uitvoeren van een productontvangst op PO kunnen vastgelegde
  opslaglocaties (fixed product locations) niet standaard ingesteld
  worden op de PO-regels. In dat geval dient de magazijnmedewerker deze
  locaties per artikel handmatig op te zoeken indien noodzakelijk.

## Special cases

### Returns

[Aan te vullen]{.mark}

### Underdeliveries

[Aan te vullen]{.mark}

# Vendor invoice processing

Cf. CH9 record to report
