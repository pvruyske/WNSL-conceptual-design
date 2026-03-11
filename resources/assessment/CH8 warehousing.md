# CH8 Inventory to deliver {#ch8-inventory-to-deliver .TOC-Heading}

# Contents

[1 Introduction [2](#_Toc206064742)](#_Toc206064742)

[1.1 Voorbeeld [2](#_Toc206064743)](#_Toc206064743)

[1.1.1 Startpunt: klantofferte via CPQ
[2](#_Toc206064744)](#_Toc206064744)

[1.1.2 Van offerte naar aankoopproces
[3](#_Toc206064745)](#_Toc206064745)

[1.1.3 Normale aankopen -- voorraadgestuurd en voorspelbaar
[3](#_Toc206064746)](#_Toc206064746)

[1.1.4 Ordergerelateerde aankopen -- maatwerk en complexiteit
[3](#_Toc206064747)](#_Toc206064747)

[1.1.5 Waar de last toeneemt [4](#_Toc206064748)](#_Toc206064748)

[1.1.6 De prijsuitdaging [4](#_Toc206064749)](#_Toc206064749)

[1.1.7 Van levering tot facturatie [5](#_Toc206064750)](#_Toc206064750)

[2 Masterdata [5](#_Toc206064751)](#_Toc206064751)

[2.1 Items =\> zie CH5 [5](#_Toc206064752)](#_Toc206064752)

[2.2 Suppliers =\> zie CH5 [5](#_Toc206064753)](#_Toc206064753)

[2.3 Trade agreements [5](#_Toc206064754)](#_Toc206064754)

[3 UOM -- units of measurement [5](#_Toc206064755)](#_Toc206064755)

[3.1 UOM in AS400 [6](#_Toc206064756)](#_Toc206064756)

[3.2 Integraties [6](#_Toc206064757)](#_Toc206064757)

[4 Types of purchase order process [6](#_Toc206064758)](#_Toc206064758)

[5 Purchase order process (normal -- non order related)
[7](#_Toc206064759)](#_Toc206064759)

[5.1 Order confirmations [7](#_Toc206064760)](#_Toc206064760)

[5.1.1 AS400 [8](#_Toc206064761)](#_Toc206064761)

[5.1.2 Raptor [8](#_Toc206064762)](#_Toc206064762)

[5.2 Receptie [8](#_Toc206064763)](#_Toc206064763)

[5.3 Wegzetten -- Putaway [8](#_Toc206064764)](#_Toc206064764)

[6 Purchase order process (order related)
[9](#_Toc206064765)](#_Toc206064765)

[7 Purchase order process (profiles)
[9](#_Toc206064766)](#_Toc206064766)

[8 Puchase order process (glass) [9](#_Toc206064767)](#_Toc206064767)

[]{#_Toc206064742 .anchor}

# CustomDevs

- [devops 635 - CR-012: Materiaalverbruik fase 1: registreer het
  dossiernummer/project bij boeking verbruik
  (teljournaal)](#_Toc206536126)

- [CR : order number lijkt ook custom te zijn](#_Toc206536127)

- [CR xx : defaulten van waardes in de scan app voor](#_Toc206536128)

- [CR om de hoeveelheid niet te tonen bij het uitscannen om te vermijden
  dat ze alle stock per ongeluk weggooien](#_Toc206536129)

- [Wss een custom](#_Toc206536130)

- [Devops 178 - CR-004: automate stock consumption (Phase
  1)](#_Toc206536131)

# ISVs

**No table of figures entries found.**

# Specific configuration

**No table of figures entries found.**

# Batch jobs

**No table of figures entries found.**

# Change requests

# Introduction

Warehousing : bewegingen in en tussen de magazijnen = vloer gelinkt

Inventory : beheer van de hoeveelheid stock = eerder MRP gelinkt

# Maand tellingen

## Introductie

Consumpties worden niet altijd live geregistreerd. Dit maakt dat de
stock totaal niet juist staat in Dynamics. Dit wordt rechtgezet door
einde maand de stock te gaan tellen.

Gezien er geen BOM's zijn, dient alles manueel ingevuld te worden. Er
wordt ook niet gebackflusht. Consumeren van stock is op vandaag
behoorlijk arbeidsintensief, waardoor een afweging dient gemaakt te
worden tussen live consumeren vs maandtellen.

De vloer stock dient soms wel geteld te worden bij maandafsluit omdat de
waarde te hoog en te variablel is om het zomaar te laten passeren.

Het nadeel van maandtellen is dat MRP en min/max stock bestellingen een
maand extra blind zijn.

## Scope : 

  --------------------------------------------------------------------
  Comp              Stock             flow
  ----------------- ----------------- --------------------------------
  HLS               Vloerstock        maandtelling

  HLS               Doeken            uitscannen

  HLS               Profielen         Uitscannen op order

  ACT               OG stock          Backflush via Interface
  --------------------------------------------------------------------

## Maand Tellingen via tellijsten

Er zijn tellijsten per zone opgesteld

Wat is de linkt met locaties ? , deze lijst bevat alle items op die
locatie ??

De on hand stock wordt aangezet op de tellijst, zodat je als teller ziet
wat er zou moeten liggen. Dat heeft voordelen en nadelen 😉.

### Tellijst document

Invoegen documnet

## Maandtellingen via scanner

Gezien we geen detail locaties hebben , is werken met de scanner niet
mogelijk voor de stock die nu maandelijks geteld wordt. (scanner stelt
alle items voor in een random volgorde op die ene "general" locatie)

Gezien we niet met gedetaillleerde locaties gebruiken , is het tellen
met scanner op basis van locatie niet bruikbaar. De teller dient dan
constant te verlopen in het magzijn om de "random" volgorde van de
100-en items op die locatie te volgen van de scanner.

# Cycle counting

Cycle counting kunnen we enkel doen op locaties waar de stock live
geconsumeerd wordt (niet met maandtellingen)

## Tellen via scanner : spotcounting

Waar detail locaties bestaan, kunnen we spotcycle counting gebruiken in
D365. Vandaag betreft dit enkel het profielen magz van HLS. Dit wordt
gebruikt voor ad hoc tellingen als vermoeden is dat iets niet klopt of
bij einde jaar.

Op 1 locatie kunnen soms 2 of 3 soorten profielen liggen, maar voor spot
counting vormt dit geen probleem.

# Stockcorrecties + verbruiken

## Via Dynamics

Er wordt een counting journal geboekt met de correctie. Volgende velden
worden specifiek voor Winsol gebruikt

- De project tracking : consumptie voor een AS400 order / project

  - Let op : voor OG stock staat dit ingevuld, voor goederen met de
    STOCK dimensie blijft de project tracking op stock staan.

- Order number : wordt gebruikt voor consumpties voor een order

  - Voor manuele verbruiken van STOCK-dimensie artikelen.

  - Wordt niet ingevuld bij het backflushen van OG stock, gezien de
    waarde al in de project tracking dimensie zit.

- counting reason. Zo kunnen we bijhouden waarom de correctie gedaan
  werd. Bv maandtelling / correctie / ...

CustomDev : []{#_Toc206536126 .anchor}devops 635 - CR-012:
Materiaalverbruik fase 1: registreer het dossiernummer/project bij
boeking verbruik (teljournaal)

CustomDev : []{#_Toc206536127 .anchor}CR : order number lijkt ook custom
te zijn

## Via scanner

Correcties kunnen ook gedaan worden via de scanner. In een aantal niet
WMS magazijn wordt dit ook gebruikt omdat de operator gemakkelijker hun
weg vinden met de scanner dan via de D365 interface. Het normale Winsol
proces vereist 6 stappen op de scanner (source location, order, qty,
item, ... ). Via een CR xxx is voorzien dat we enkele van deze stappen
kunnen laten defaulten om zo een lichter proces te bekomen.

CustomDev : []{#_Toc206536128 .anchor}CR xx : defaulten van waardes in
de scan app voor

CustomDev : []{#_Toc206536129 .anchor}CR om de hoeveelheid niet te tonen
bij het uitscannen om te vermijden dat ze alle stock per ongeluk
weggooien

## Scope

Via dynamics kan overal gebruikt worden. Correcties via scanner worden
gebruikt in HLS profielen en HLS doeken.

## Types verbruik

### Waste

### Rework

### Production

Scannen voor productie bestaat uit volgende stappen :

- Voor productie wordt als eerste stap het order ingescand

CustomDev : []{#_Toc206536130 .anchor}Wss een custom 😊

- 

## Automatisch verbruik van OG stock 

Order gerelateerde stock wordt automatisch verbruikt door een interface
vanuit AS400 om alle stock gelinkt aan een AS400-order of
D365-project-dimensie te verwijderen. Deze interface vult een lijst in
van te verbruiken project-dimensies

Screenshot van die liist

Via een batchjob wordt dan alle stock die gelinkt zit aan de projecten
in de lijst verwijderd. Dat betekent dat de stock die in de toekomst zal
ontvangen worden ook zal verwijderd worden voor projecten in de lijst.

De trigger in AS400 om deze IF te sturen is bij start productie order.
In de praktijk is dit dus een preflushing logica.

CustomDev 6: []{#_Toc206536131 .anchor}Devops 178 - CR-004: automate
stock consumption (Phase 1)

# Verplaatsingen tussen Business units : PVC \<-\> ALU

We willen de goederen die van ALU in PVC verbruikt worden en vice versa
helder krijgen om de kosten correct toe te wijzen.

Daar loopt het proces nog niet vlot.

# Halffabrikaten aanmaken 

Halffabrikaten worden gebruikt in volgende scenario's:

- Winterwerk

- Lakwerk bij een onderaannemer of INCO

bovenstaande uitleg staat wss al in masterdata

## Via bom journal

Er wordt een bom-jrl aangemaakt om de output te maken. Deze bevat ook
een project dimensie. De BOM is opgezet in masterdata waardoor de
journal lines de output en de verschillende inputs bom-lijnen bevat.
Deze BOM lijnen kunnen ook arbeid bevatten als item.

Nadat de bom jrl lijnen juist gezet zijn, wordt het bom jrl gepost.
Waarbij de nodige voorraad wordt op- en afgeboekt.

## HF via INCO

## HF lakwerk via INCO of SUBCO

Indien lakwerk voor IND gebeurt in HLS is dit een INCO-subco operatie.
Dan wordt het bom jrl geboekt in IND en wordt het gevlagd op locatie
subcontractor (op de bom-lijnen).

Manueel wordt de stock verlegd naar de subco locatie. Zodat dit bij het
tellen ook goed komt. Er is maar 1 subco locatie voor alle subco's. De
specifieke supplier kan teruggevonden worden op de PO en lakbon.

Er wordt manueel een PO aangemaakt voor de aankoop van het werk in
subco. Bijhorend wordt in AS400 een lakbon aangemaakt met de specifieke
instructies voor de onderaannemer.

### Prijzen

De orderconfirmatie of worst case levernota bevat de prijzen. Deze
worden eerst ingevuld op de PO alvorens de PO te ontvangen.

### Lakbon

De lakbon bevat de specifieke instructies voor de onderaannemer om te
lakken. O.A. de kleur informatie.

Wat triggert de lakbon precies ? de PO ?

## Scope

De HF via bomjournals zijn actief in HLS, WBL, IND.

In ACT zijn er ook HF, maar die lopen niet via Dynamics.
