#  {#section .TOC-Heading}

# Contents

[Contents [1](#_Toc207112548)](#_Toc207112548)

[CustomDevs [4](#customdevs)](#customdevs)

[ISVs [4](#isvs)](#isvs)

[Specific configuration
[4](#specific-configuration)](#specific-configuration)

[Batch jobs [4](#batch-jobs)](#batch-jobs)

[1 Introduction [5](#introduction)](#introduction)

[2 Accounts payable [5](#accounts-payable)](#accounts-payable)

[2.1 Master data [5](#master-data)](#master-data)

[2.2 Factuurverwerking [5](#factuurverwerking)](#factuurverwerking)

[2.3 Betalingen [5](#betalingen)](#betalingen)

[2.4 Speciale processen [5](#speciale-processen)](#speciale-processen)

[2.5 Rapportering [6](#rapportering)](#rapportering)

[2.6 Uitdagingen en problemen
[6](#uitdagingen-en-problemen)](#uitdagingen-en-problemen)

[3 Accounts receivable [7](#accounts-receivable)](#accounts-receivable)

[3.1 Master data [7](#master-data-1)](#master-data-1)

[3.2 Verkooporders & Facturatie
[7](#verkooporders-facturatie)](#verkooporders-facturatie)

[3.3 Betalingen & Settlements
[7](#betalingen-settlements)](#betalingen-settlements)

[3.4 Rapportering [7](#rapportering-1)](#rapportering-1)

[4 Cost accounting [8](#cost-accounting)](#cost-accounting)

[4.1 Cost Centers & Dimensions
[8](#cost-centers-dimensions)](#cost-centers-dimensions)

[4.2 Allocaties [8](#allocaties)](#allocaties)

[4.3 Accruals [8](#accruals)](#accruals)

[5 Inventory valuation [9](#inventory-valuation)](#inventory-valuation)

[5.1 Item Groups & Model Groups
[9](#item-groups-model-groups)](#item-groups-model-groups)

[5.2 Inventory Closing & Adjustment
[9](#inventory-closing-adjustment)](#inventory-closing-adjustment)

[5.3 Rapportering [9](#rapportering-2)](#rapportering-2)

[6 Treasury & cash management
[10](#treasury-cash-management)](#treasury-cash-management)

[6.1 Bankrekeningen & Journaal
[10](#bankrekeningen-journaal)](#bankrekeningen-journaal)

[6.2 CODA Integratie [10](#coda-integratie)](#coda-integratie)

[6.3 Cash Pooling & Intercompany
[10](#cash-pooling-intercompany)](#cash-pooling-intercompany)

[6.4 Rapportering [10](#rapportering-3)](#rapportering-3)

[7 Tax management [11](#tax-management)](#tax-management)

[7.1 Master data [11](#master-data-2)](#master-data-2)

[7.2 BTW Aangifte & Rapportering
[11](#btw-aangifte-rapportering)](#btw-aangifte-rapportering)

[7.3 Speciale processen
[11](#speciale-processen-1)](#speciale-processen-1)

[7.4 Jaarlijkse rapporten
[11](#jaarlijkse-rapporten)](#jaarlijkse-rapporten)

[8 Financial closing & reporting
[12](#financial-closing-reporting)](#financial-closing-reporting)

[8.1 Periodebeheer [12](#periodebeheer)](#periodebeheer)

[8.2 Diverse boekingen & Templates
[12](#diverse-boekingen-templates)](#diverse-boekingen-templates)

[8.3 Jaarafsluiting [12](#jaarafsluiting)](#jaarafsluiting)

[8.4 Rapportering [12](#rapportering-4)](#rapportering-4)

[9 Obsolete -- to check and delete
[13](#obsolete-to-check-and-delete)](#obsolete-to-check-and-delete)

[9.1 Masterdata [13](#masterdata)](#masterdata)

[9.1.1 AR [13](#ar)](#ar)

[9.1.2 AP [13](#ap)](#ap)

[9.1.3 Ledger / Chart of accounts / Account structure
[13](#ledger-chart-of-accounts-account-structure)](#ledger-chart-of-accounts-account-structure)

[9.1.4 Financial dimensions
[13](#financial-dimensions)](#financial-dimensions)

[9.1.5 Items [13](#items)](#items)

[9.1.6 9A document management -- Parameters
[13](#a-document-management-parameters)](#a-document-management-parameters)

[9.1.7 Calculation groups
[13](#calculation-groups)](#calculation-groups)

[9.1.8 Creatie bankrekening
[13](#creatie-bankrekening)](#creatie-bankrekening)

[9.1.9 Intercompany accounting
[13](#intercompany-accounting)](#intercompany-accounting)

[9.2 AR -- Accounts Receivable
[13](#ar-accounts-receivable)](#ar-accounts-receivable)

[9.2.1 Introductie [13](#introductie)](#introductie)

[9.2.2 Fakturatie interface
[13](#fakturatie-interface)](#fakturatie-interface)

[9.2.3 Coda [14](#coda)](#coda)

[9.2.4 LCR [14](#lcr)](#lcr)

[9.2.5 Customer payments = CODA
[14](#customer-payments-coda)](#customer-payments-coda)

[9.2.6 Customer settlements
[14](#customer-settlements)](#customer-settlements)

[9.2.7 Customer creditsaldo -- Supplier debetsaldo
[14](#customer-creditsaldo-supplier-debetsaldo)](#customer-creditsaldo-supplier-debetsaldo)

[9.3 AP -- Accounts Payable
[15](#ap-accounts-payable)](#ap-accounts-payable)

[9.3.1 Introductie [15](#introductie-1)](#introductie-1)

[9.3.2 Aankooporders [15](#aankooporders)](#aankooporders)

[9.3.3 Kofax (AP Essentials)
[15](#kofax-ap-essentials)](#kofax-ap-essentials)

[9.3.4 PO tegendraaien (via nulfactuur)
[16](#po-tegendraaien-via-nulfactuur)](#po-tegendraaien-via-nulfactuur)

[9.3.5 Corrigeren PO bij foute receptie
[16](#corrigeren-po-bij-foute-receptie)](#corrigeren-po-bij-foute-receptie)

[9.3.6 Ledger accruals [16](#ledger-accruals)](#ledger-accruals)

[9.3.7 3 way matching [17](#way-matching)](#way-matching)

[9.3.8 Approval flow [17](#approval-flow)](#approval-flow)

[9.3.9 Goedkeuring facturen in legacy systeem
[17](#goedkeuring-facturen-in-legacy-systeem)](#goedkeuring-facturen-in-legacy-systeem)

[9.3.10 Vendor payments [17](#vendor-payments)](#vendor-payments)

[9.3.11 Plaatsing [17](#plaatsing)](#plaatsing)

[9.3.12 BTW met verlegging van heffing bij import
[17](#btw-met-verlegging-van-heffing-bij-import)](#btw-met-verlegging-van-heffing-bij-import)

[9.4 Afsluit [17](#afsluit)](#afsluit)

[9.4.1 Periodebeheer [17](#periodebeheer-1)](#periodebeheer-1)

[9.4.2 Templates import [17](#templates-import)](#templates-import)

[9.5 Taks [17](#taks)](#taks)

[9.5.1 BTW aangifte [17](#btw-aangifte)](#btw-aangifte)

[9.5.2 Franse BTW [17](#franse-btw)](#franse-btw)

[9.5.3 Franse BTW in NV [17](#franse-btw-in-nv)](#franse-btw-in-nv)

[9.5.4 BTW eenheid settlement
[17](#btw-eenheid-settlement)](#btw-eenheid-settlement)

[9.5.5 Intrastat [17](#intrastat)](#intrastat)

[9.5.6 IC aangifte [17](#ic-aangifte)](#ic-aangifte)

[9.5.7 Klantenlisting aangifte (jaarlijks)
[17](#klantenlisting-aangifte-jaarlijks)](#klantenlisting-aangifte-jaarlijks)

[9.5.8 Fiche 281.50 [17](#fiche-281.50)](#fiche-281.50)

[9.5.9 Interfaces [17](#interfaces)](#interfaces)

# CustomDevs

- [Devops](#_Toc206529931)

# ISVs

- [9A kickstart :](#_Toc206530153)

# Specific configuration

**No table of figures entries found.**

# Batch jobs

- [Batch job ...](#_Toc206530206)

# 

# Introduction

Basis voor dit chapter = [End user training -
Finance.url](https://winsolgroup.sharepoint.com/:o:/s/ERP-sharedDLW/EpNctTPP3YRPghYaLf1vinkBUhiZUNtEOetsBZPCG1Is0g?e=TYKRmf)

# Accounts payable

## Master data

- Leveranciers worden aangemaakt via het Global Address Book, met
  controle op BTW/ondernemingsnummer.

  - Periodieke synchronisatie vanuit D365FSCM naar Kofax

- Sensitiviteit van leveranciers (Low/Medium/High) bepaalt
  toegangsrechten.

- Betaalmethodes (SEPA, SEPA+++, DOM) worden per bank en leverancier
  ingesteld.

- Default bankrekeningen en grootboekrekeningen worden op de
  leveranciersfiche gedefinieerd.

## Factuurverwerking

- 3-way matching is standaard: bestelling, levering, factuur.

- Facturen worden verwerkt via Kofax (automatisch of manuele upload).

  - Automatisch: bijlagen vanuit AP mailbox

    - Tool (Anthony) dat de pdf-bijlagen uit de mails haalt en
      importeert in Kofax

    - Vereiste: 1 bestand per factuur; geen gegroepeerde facturen in 1
      bestand

    - Prefix in bestandsnaam wordt gebruikt om de factuur in de juiste
      legal entity te importeren

    - Prefix afhankelijk van de AP mailbox (1 per legal entity)

    - Vervaldatum wordt leeggelaten, zodat teruggevallen wordt op de
      payment conditions in D365 (master data per leverancier)

  - Manueel: rechtstreeks in Kofax importeren

- Document type

  - PO invoice (standaard)

  - Expense invoice (als er geen PO is)

- Bij afwijkingen in matching (\>2% of \>20€) is extra goedkeuring
  vereist.

- Invoice setup (= 9A ISV)

  - Regels om het gewenste journaal te gebruiken

  - AF1 en AF2 voor even vs. oneven boekjaren

## Betalingen

- Vendor payments verlopen via Vendor Payment Journal, met bridging
  accounts (581000).

- Betalingen kunnen manueel of via payment proposal.

- Cash discounts en deelbetalingen worden ondersteund.

- Afpunting van betalingen gebeurt via settle transactions.

## Speciale processen

- Tegendraaien PO via nulfactuur (procurement category 'Reverse PO').

- Correctie van PO bij foute receptie via Receive \> Journals \> Product
  receipt \> Correct.

- Ledger accruals voor kosten spreiden over meerdere maanden.

- Kosten van bedrijfswagens

  - Worden op nummerplaat geboekt

  - Een gewoon invoice journal loopt vast gezien het groot aantal lijnen
    (tot 200 lijnen)

  - Workaround: gebruiken van aparte journal name waarbij de
    automatische taksberekening uitgeschakeld is (INV_JOURNTEMP).

## Rapportering

- Vendor aging rapporten beschikbaar.

- Openstaande betalingen en debetsaldo's kunnen geraadpleegd worden.

## Uitdagingen en problemen

- Combinatie van

  - Laattijdige recepties

  - Maandafsluiting

  - Korting contante betaling

  - Generieke MTO items

- Workflow state is approved, maar factuur geraakt niet approved

# Accounts receivable

## Master data

- [Klanten worden aangemaakt via Global Address Book, met controle op
  BTW-nummer.]{.mark}

- Default grootboekrekeningen en bankrekeningen worden ingesteld.

- Facturatie verloopt via interface met AS400.

## Verkooporders & Facturatie

- Verkooporders worden geregistreerd en gefactureerd in F&O.

- Facturatie-interface controleert op volledigheid en correctheid van
  orders.

- Foutmeldingen bij facturatie (bv. ontbrekende dimensies,
  afrondingsverschillen) worden opgelost via masterdata-aanpassingen.

## Betalingen & Settlements

- Manuele klantbetalingen via General Journals.

- Afpunting van betalingen via settle transactions.

- Overboeken van betalingen tussen klanten via diverse journaal.

- Korting contant wordt automatisch berekend bij settlement.

## Rapportering

- Customer aging rapporten beschikbaar.

- Klantensaldo-opvolging tussen AS400 en D365 via dashboard.

# Cost accounting

## Cost Centers & Dimensions

- Kostenplaatsen zijn gedefinieerd (1000 gebouw, 2000 regio, 3000 B2B,
  etc.).

- Cost center is verplicht op elke kostentransactie.

- Productgroep wordt gebruikt voor P&L per verkoopskanaal/productgroep.

## Allocaties

- Automatische verdeelsleutels (allocation terms) kunnen ingesteld
  worden.

<!-- -->

- Allocatie via Excel-integratie mogelijk.

## Accruals

- Expense facturen kunnen via ledger accruals gespreid worden over
  meerdere maanden.

*[**Opmerking:** Gedetailleerde informatie over cost accounting
methodologieën, rapportages en analyses ontbreekt in de
documentatie.]{.mark}*

# Inventory valuation

## Item Groups & Model Groups

- Item group bepaalt boekingsprofiel (voorraad, aankoop, verkoop).

- Item model group bepaalt waarderingsmodel (FIFO, FIFO_NoLdg, Service,
  etc.).

## Inventory Closing & Adjustment

- Maandelijkse controles: aansluiting inventory value list met general
  ledger, inventory closing & adjustment.

- Dagelijkse batch job berekent voorraadwaarde.

- Aanpassingen mogelijk via adjustment \> transactions (cost price,
  fixed cost price, amount, value, percent).

## Rapportering

- Inventory aging rapporten beschikbaar.

- Voorraadwaarde wordt gereconcilieerd met trial balance.

*[**Opmerking:** Specifieke details over costing methods,
voorraadwaardering per entiteit, en integratie met productie
ontbreken.]{.mark}*

# Treasury & cash management

## Bankrekeningen & Journaal

- Bankrekeningen worden aangemaakt via Cash and Bank Management \> Bank
  Accounts.

- Grootboekrekening bank start met 5500xxx, main account category
  'CA-54/58'.

- Bankjournaal en voucher series worden per bank ingesteld.

## CODA Integratie

- CODA-bestanden worden geïmporteerd en verwerkt voor reconciliatie van
  banktransacties.

- CODA-definities worden per bank en firma ingesteld.

- Afpunting van centralisatierekening leveranciersbetalingen (581000)
  via ledger settlements.

## Cash Pooling & Intercompany

- Intercompany accounting voor cashpooling tussen entiteiten.

- ICO journaal met ICO receivable/payable rekeningen.

## Rapportering

- Bankkosten met BTW worden uitgesplitst.

- Zero-balancing rekeningen voor factoring.

# Tax management

## Master data

- Sales tax codes, sales tax groups en item sales tax groups bepalen
  sturing naar BTW-aangifte vakken.

- Sales tax group op leverancier, item sales tax group op artikel.

## BTW Aangifte & Rapportering

- BTW-aangifte via Tax \> Declarations \> Report sales tax for
  settlement period.

- Intervat aangifte genereren en indienen via XML.

- Controle rapporten beschikbaar voor aankoop- en verkoopfacturen.

## Speciale processen

- Verlegging van heffing bij import via dummy accounts en vendors.

- Franse BTW aangifte via Excel.

- Intrastat aangifte voor aankopen (Helios, Actuell).

- IC aangifte via EU Sales list, XML upload.

## Jaarlijkse rapporten

- Klantenlisting aangifte via invoice turnover report.

- Fiche 281.50 via commission codes op rekeningen en leveranciers.

# Financial closing & reporting

## Periodebeheer

- Perioden worden geopend/gesloten via General Ledger \> Period Close \>
  Ledger Calendars.

- Status 'on hold' aanbevolen bij afsluiting.

## Diverse boekingen & Templates

- General journals voor diverse boekingen, loonboekingen, bank, kas,
  openingsbalans, afsluitingen.

- Import templates voor general journals en invoices via
  Excel-integratie.

## Jaarafsluiting

- Year-end close via General Ledger \> Period Close \> Year end close.

- Slotbalans wordt automatisch gepost; mogelijkheid tot reverse.

## Rapportering

- Trial balance, grootboekrekeningen detail, aging rapporten (inventory,
  klanten, leveranciers).

- Vast actief rapporten: acquisities, transacties, disposals, movements,
  balances, roll forward.

# Obsolete -- to check and delete

## Masterdata

### AR

### AP

- Leveranciers worden aangemaakt via het Global Address Book, met
  controle op BTW/ondernemingsnummer.

- Sensitiviteit van leveranciers (Low/Medium/High) bepaalt
  toegangsrechten.

- Betaalmethodes (SEPA, SEPA+++, DOM) worden per bank en leverancier
  ingesteld.

- Default bankrekeningen en grootboekrekeningen worden op de
  leveranciersfiche gedefinieerd.

#### Buitenlandse leverancier met Belgisch BTW

### Ledger / Chart of accounts / Account structure

### Financial dimensions

### Items

#### item groups

#### item model groups

### 9A document management -- Parameters

### Calculation groups

### Creatie bankrekening

### Intercompany accounting

## AR -- Accounts Receivable

### Introductie

### Fakturatie interface

Enkel voor uitgaande facturatie voor alle companies behalve INT

INT (is rechtstreeks in F&O) : vb IT, Finance die wordt doorgerekend aan
de firma's

WinPro : Dashboard (Dynamics F&O)

To send invoices to Dynamics 365

Je mag hier enkel de huidige datum zien staan\
= Is het verstuurd ? Is de gemaakte JSON correct (bestaat klant, item,
taks code, dossiernr, ...)

Invoices to process in Dynamics 365

Alle facturen die verstuurd werden, je moet terugkoppeling ervoor
krijgen = Is het correct verwerkt geweest ? "RedId" wordt als key
gebruikt

In 9A Integrations : "Not posted journals"

D365 \> Accounts Receivable \> Orders \> All sales orders : status =
open (= niet gefactureerde sales orders)

Berichten in 9A Integrations (in sync met het dashboard in WinPro (voor
"XML payments" en "XML settlements")

CustPaytransOut... payments

CustSettleOUT... settlements

### Coda

Beschreven in OneNote

Wat ?

In **[België]{.underline}** is een CODA-bestand een gestandaardiseerd
digitaal bestand dat banktransacties bevat, zoals afschriften en
bijlagen. Het is een elektronische weergave van papieren bankafschriften
en wordt gebruikt voor de automatische verwerking van bankgegevens in
boekhoudsoftware of andere financiële systemen

Vooral gebruikt in WNV voor klanten

Waarop wordt gematcht ?

1.  OP gestructureerde mededeling

2.  OP Factuurnr of Bankrekening nr

Timing ? Dagelijks

Het opladen wordt manueel gedaan (zou in batch kunnen werken...)

CODA \> Process detail lines = duurt "tergend" langzaam

Ondanks dat alles matching juist is, wordt TOCH soms nog op een andere
leverancier geboekt...???\... Systeem vindt echter geen match en zet het
op een bepaalde leverancier

### LCR

= direct debet-achtig

LCR zit in het oude systeem. AS400 heeft LCR opgemaakt en uitgestuurd

In CODA weet het systeem geen details ivm de betaling van die LCR...

General ledger \> Journal entries \> General journals \> "Upload
settlement" = maatwerk

### Customer payments = CODA

### Customer settlements

### Customer creditsaldo -- Supplier debetsaldo

## AP -- Accounts Payable

### Introductie

### Aankooporders

### Kofax (AP Essentials)

Via aparte link (niet via D365)

Aparte AP mailbox per firma

Pgm-Anthony haalt de bijlages uit de mailbox per firma -- uploaden kan
ook rechtstreeks in Kofax (per company !)

Er is link met D365 (sync leverancier is noodzakelijk, ook PO's worden
gesynct))

Documenttype : expense / PO invoice (herkenning "leert" het systeem ook
afh van leverancier)

Bij PO invoice : factuurnr , factuurdatum, bestelbonnr (kunnen er heel
veel zijn), MVH, BTW, totaal bedrag

Er zit "learning" in Kofax zodat hij het bij de volgende keren herkent
(niet altijd direct..)

Bestelbonnr : er is sync met PO's, maar er is **geen controle** of ze
bestaan of niet (je kan gelijk wat insteken)

Proces is manueel ! Het is tekstherkenning en gaat uit van de PO flow.

Dit zou allemaal veel sneller moeten (soms tot 1u / factuur)

We vinden tool niet zo goed

Nieuwe users moeten aangevraagd worden bij 9A -- niet handig

#### Verwerken factuur Kofax in F&O

9A Raptor DWH -- Invoices

Import functionaliteit :

Invoice setup : regels met sequentie

Invoice journal : INV_JOURN

AF1 = voor oneven jaren

AF2 = voor even jaren

Bij jaarwissel moet je dit dan aanpassen !!!

Ook "Journal names" & "Posting journal" aanpassen (datum range)

CORR_INV = wordt niet gebruikt

INV_JOURNTEMP = facturen voor bedrijfswagens w op license plate
aangemaakt

INV_PO = voor PO's

Invoices \> All unposted invoices : Hier staan alle facturen die via
KOFAX zijn binnen gekomen

Knop "reinitialize invoice" : Workflow slaat tilt, best eerst cancellen

Invoice Type (2) : Invoice journal / Pending vendor invoice. Soms komt
er toch een "blanko" in terecht...???\... =\> Knop "Change invoice type"
mag men NIET uitvoeren !

Maatwerk voor Intrastat ! Op onze masterdata (items) hebben we de data
niet staan (vb : gewichten).

Op expense facturen kan je maar 1 intrastat code ingeven (via "Enter
intrastat"), wij hebben facturen met meerdere intrastat codes !

Moeilijke flows :

- ALUK : controle duurt heel lang (maand einde, kan nooit afgewerkt zijn
  tegen dan) -- geleverd maar niet gereceptioneerd (en misschien schade
  erop...)

- Glas : gebroken glas (geen receptie als gebroken, herbestelling,
  nieuwe PO, hoe wordt het gefactureerd door leverancier en naar wat
  verwijst leverancier ?\...)

Issues :

- Zie ook hoger

- Workflow approved, maar invoice is niet approved =\> 9A kan het niet
  reproduceren... Hierdoor kan je de factuur niet betalen\
  Kjeld doet dan (per firma) : "Approve for payment" = Manueel

- GA's : te vermijden anders kan je nooit de kostprijzen goed krijgen.
  Minstens hebben we varianten nodig !

- Rechtstreeks boeken op een 44-rek wat niet mag

- CODA verwerkingen die naar verkeerde rekening gaan (44-, 99-) of
  mappen naar verkeerde leverancier (komt op financieel directeur)

- Faktuur is betaald maar niet approved : In Coda kan je die niet
  "settlen" omdat ze niet approved is (is std functionaliteit, maar soms
  wil je dat echt wel zo doen...)

### PO tegendraaien (via nulfactuur)

### Corrigeren PO bij foute receptie

### Ledger accruals

= Maatwerk

Vb factuur voor licentie van 3 jaar =\> kan je splitsen over 3 jaar
(periodes openen en terug sluiten)

### 3 way matching

### Approval flow

### Goedkeuring facturen in legacy systeem

### Vendor payments

#### Methods of payment

- SEPA (zonder gestructureerde mededeling)

- SEPA+++ (gestructureerde mededeling)

### Plaatsing

= rapportage en terugmeldingen (interfaces)

### BTW met verlegging van heffing bij import

Doen ze met dummy leverancier

## Afsluit

### Periodebeheer

### Templates import

...

## Taks

### BTW aangifte

### Franse BTW

### Franse BTW in NV

### BTW eenheid settlement

### Intrastat

### IC aangifte

### Klantenlisting aangifte (jaarlijks)

### Fiche 281.50

### Interfaces

#### Verkoopfakturen

#### Project

##### Projects

##### Verbruiken

#### Payments

#### Settlements

#### Installation expenses for sales

#### Plaatsing

In B2C doet men de planning in WinPlan (hieruit kn PO's voor D365 komen
! HOE ?)

Accounts payables \> All purchase orders \> PO voor onderaannemers

= plaatsingskosten (RB.... staat in customer reference RB =ReceptieBon)

Wij geven dus op hoe onderaannemer zijn factuur mag maken (via die PO)

Vb PO001559 in WNV

Cost center voor deze moet met "4" beginnen wat al deze zijn voor
plaatsingskosten waarvoor we een interne rapportering hebben voor het
plaatsingsrendement

Plaatsing willen we ook in de toekomst (F2) zeker kunnen
opvolgen/rapporteren
