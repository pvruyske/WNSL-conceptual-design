# General accounting

Legal entities

![A screenshot of a company structure AI-generated content may be
incorrect.](media/image1.png){width="6.268055555555556in"
height="3.4631944444444445in"}

Alle legal entities binnen de Winsol group zijn reeds actief in D365.

Accounting structure & financial dimensions

Algemeen uitgangspunt

- Business unit is verplicht voor elke transactie

- Cost center verplicht op elke kostentransactie

- Product group verplicht op elke verkooptransactie

- Winsol sales reference wordt ingevuld via facturatie interface (in
  latere fases overerving naar productie-entiteiten) + gehanteerd om
  kosten/opbrengsten boekhoudkundig toe te wijzen aan ordernummer (cfr.
  plaatsingsopvolging)

Verschillende LE's hebben verschillende accounting structures

  ----------------------------------------------
  Firma           Acc struct P&L  Acc struct BS
  --------------- --------------- --------------
  WNV             P&L - type 1    BS - Type 1

  ACT             P&L - type 1    BS - Type 1

  HLS             P&L - type 1    BS - Type 1

  WBL             P&L - type 1    BS - Type 1

  IND             P&L - type 1    BS - Type 1

  SFO             P&L - type 2    BS - Type 2

  INT             P&L - type 3    BS - Type 3

  GRP             P&L - type 3    BS - Type 3
  ----------------------------------------------

  ---------------------------------------------------------------------------------------------------
  Account     Main account     BU      Cost     Nbr     Personnel   Intercompany   Winsol   Product
  structure                            center   plate   nbt                        sales    Group
                                                                                   ref      
  ----------- ---------------- ------- -------- ------- ----------- -------------- -------- ---------
  P&L -- type 6\*;7\*          "";\*   "";\*    "";\*   "";\*       "";\*          "";\*    "";\*
  1                                                                                         

  P&L -- Type 6\*;7\*          "";\*   "";\*    "";\*   "";\*       "";\*          "";\*    "";\*
  2                                                                                         

  P&L -- type 6\*;7\*          "";\*   "";\*    "";\*   "";\*       "";\*                   
  3                                                                                         

  BS -- type  100000..599999   "";\*                                "";\*                   
  1                                                                                         

  BS -- type  100000..599999   "";\*                                "";\*                   
  2                                                                                         

  BS -- type  100000..599999   "";\*                                "";\*                   
  3                                                                                         
  ---------------------------------------------------------------------------------------------------

  -----------------------------------------------------------------------
  Account structure Advanced rule 1   Advanced rule 2   Advanced rule 3
  ----------------- ----------------- ----------------- -----------------
  P&L -- type 1     Prod Gr verplicht Cost center       Vendor 6\*
                    70\*              verplicht 6\*     ("";\*)

  P&L -- Type 2     Prod Gr verplicht Cost center       Vendor 6\*
                    70\*              verplicht 6\*     ("";\*)

  P&L -- type 3                       Cost center       Vendor 6\*
                                      verplicht 6\*     ("";\*)

  BS -- type 1      Winsol Sales ref  Vendor 444\*      
                    460000            ("";\*)           

  BS -- type 2      Winsol Sales ref  Vendor 444\*      
                    460000            ("";\*)           

  BS -- type 3      Winsol Sales ref  Vendor 444\*      
                    460000            ("";\*)           
  -----------------------------------------------------------------------

**BU -- Business units**

Verplicht voor elke boekhoudkundige transactie.

Defaultering mogelijk op:

- Klant/Leverancier

- Artikel

- Grootboekrekening

+------------+------------------+----------------------------------+
| **Firma**  | **BU**           | **Opmerkingen**                  |
+============+==================+==================================+
| Winsol NV  | **B2B**          | **Toewijzing opbrengsten =\>     |
|            |                  | vanuit verkooporder**            |
|            |                  |                                  |
|            |                  | **Kosten zoveel mogelijk         |
|            |                  | defaulten**                      |
|            +------------------+                                  |
|            | **B2C**          |                                  |
|            +------------------+                                  |
|            | **PROJECTS**     |                                  |
|            +------------------+                                  |
|            | **GENERAL NV**   |                                  |
+------------+------------------+----------------------------------+
| Actuell    | **ALU**          | **Opbrengsten en kosten:**       |
|            |                  |                                  |
|            |                  | **- Defaulten op artikel**       |
|            |                  |                                  |
|            |                  | **- Toewijzing werknemers**      |
|            +------------------+                                  |
|            | **PVC**          |                                  |
|            +------------------+                                  |
|            | **GENERAL        |                                  |
|            | ACTUELL**        |                                  |
+------------+------------------+                                  |
| Industries | **SHUTTERS**     |                                  |
|            +------------------+                                  |
|            | **GARAGE DOORS** |                                  |
|            +------------------+                                  |
|            | **GENERAL        |                                  |
|            | INDUSTRIES**     |                                  |
+------------+------------------+                                  |
| Winbalu    | **RAILINGS**     |                                  |
|            +------------------+                                  |
|            | **GENERAL        |                                  |
|            | WINBALU**        |                                  |
+------------+------------------+                                  |
| Helios     | **SCREENS**      |                                  |
|            +------------------+                                  |
|            | **AWNINGS**      |                                  |
|            +------------------+                                  |
|            | **OTHER          |                                  |
|            | SUNPROTECTION**  |                                  |
|            +------------------+                                  |
|            | **TERRACE        |                                  |
|            | COVERS**         |                                  |
|            +------------------+                                  |
|            | **GENERAL        |                                  |
|            | HELIOS**         |                                  |
+------------+------------------+----------------------------------+
| ALL        | **GROUP**        |                                  |
+------------+------------------+----------------------------------+

**Product group**

Verplicht op elke verkooptransactie

Defaultering mogelijk op verkoopartikel, grootboekrekening, klant

**Intercompany**

Verplicht voor elke intercompany transactie

Gedefaulteerd op klant/leverancier

**Vendor**

Entity-backed dimension: voor elke leverancier in F&O wordt automatisch
een dimensiewaarde aangemaakt. Deze dient vervolgens op de leverancier
te worden gedefaulteerd

Doel: Leverancier zichtbaar in grootboek bij boeken te ontvangen
facturen

Allocations

On specific cost main accounts for specific legal entities some
allocation terms are setp on the main accounts.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image2.png){width="6.268055555555556in"
height="2.576388888888889in"}

Consilidatie

Speciale legal entity hiervoor?

Intercompany accounting

ICO transacties die doorgeboekt moeten worden aan een andere legal
entity worden via de functionaliteit intercomany accounting in D365
geboekt:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image3.png){width="6.268055555555556in"
height="3.24375in"}

# Accounts receivable

![A diagram of a customer AI-generated content may be
incorrect.](media/image4.png){width="6.268055555555556in"
height="2.723611111111111in"}

Verkoop process wordt momenteel uitgevoerd in AS400 aangezien er data
uit Wincal (CPQ tool) naar AS400 gestuurd wordt voor de factuur afdruk.
Een interface is opgezet tussen AS400 en D365 om financiële data in D365
beschikbaar te hebben.

Eenmaal de factuur gemaakt is in AS400 wordt er door een interface ook
een sales order gemaakt in D365. Hierop staan alle gegevens nodig voor
de factuur. Eenmaal de factuur gemaakt is in D365 vanuit het SO dan
wordt er een interface bericht gemaakt naar AS400 met alle info
(factuurtotaal, btw, ...) zodat in AS400 de factuur met dezelfde data
gemaakt kan worden als PDF en verstuurd worden naar de klant.

Klanten betalingen worden geregistreerd via de CODA functionaliteit van
D365. Hierbij worden dan ook de openstaande klantenfacturen gesettled.
De settlement wordt ook geinterfaced naar AS400 aangezien de aanmaningen
nog beheerd worden in AS400.

# Accounts payable

![A diagram of a process AI-generated content may be
incorrect.](media/image5.png){width="6.268055555555556in"
height="1.917361111111111in"}

Aankoopfacturen worden via mail verstuurd of manueel opgeladen in Kofax.
Kofax is de OCR tool die alle info capteert. Bij ontbrekende gegevens
wordt er manueel door een gebruiker ingegrepen in Kofax. Eenmaal deze
daar volledig is herkend wordt deze doorgestuurd naar D365 met de pdf
als bijlage.

Deze factuur komt terecht in de 9A Raptor DHW module. Hier wordt deze
verder verwerkt:

- Indien geen PO dan wordt er een invoice journaal van gemaakt, hierbij
  vult de gebruiker de nodige financiële data verder aan (main account,
  btw, ...)

- Indien een PO dan wordt deze verwerkt via een pending vendor invoice
  waarbij het 3way matching principe wordt toegepast.

Na verwerking kan er simultaan 2 goedkeuringen gegeven worden:

- Goedkeuring voor boeking

- Goedkeuring voor betaling

Na goedkeuring voor boeking wordt de factuur geboekt. Na goedkeuring
voor betaling kan de factuur betaald worden via een vendor payment
journaal.

# Fixed assets

![A diagram of a company structure AI-generated content may be
incorrect.](media/image6.png){width="6.268055555555556in"
height="3.6444444444444444in"}

Vaste activa groepen zij gelijk in elke LE behalve in SFO (franse
entiteit) en zijn gebaseerd op de main accounts. Er wordt slechts 1 boek
gebruikt op de vaste activa groepen maar een 2e boek (non-fiscal) is
opgezet om toe te voegen aan de nodige fixed assets zelf.

Enkel lineaire afschrijvingen zijn toegestaan.

**Creatie:** nieuwe fixed assets worden ALTIJD EERST manueel aangemaakt
door finance. Fin dim BU en CC zijn hier zeer belangrijk.

Service life wordt gebruikt om te bepalen of alle acquisities geboekt
zijn en of er dus afgeschreven mag worden. Om te vermijden dat je reeds
begint af te schrijven vooraleer de slotfactuur ontvangen is, dient de
placed in service datum op 1/1/2099 geplaatst te worden.

**Acquisitie:** acquisitie van vast actief wordt gedaan via PO factuur
(procurement category) of invoice journaal.

**Afschrijvingen:** worden gedaan via de standaard functionaliteit
'depreciation proposal'.

**Verkopen:** worden gedaan via vrije tekst factuur

OF

Verkoopfactuur komt via de interface binnen in D365 en wordt geboekt op
de 700 rekening. Vast actief wordt dan gekoppeld door diverse boeking
van 700 naar 741 (excl. Btw) en daarna wordt vast actief verkocht via
fixed asset journaal

**Herclassificatie:** volgens de procedure dienen activa niet
geherclassificeerd te worden. In geval van activa in aanbouw dient het
actief aangemaakt te worden op de juiste klasse en pas afgeschreven te
worden vanaf in dienst neming. Dit kan door de \'placed in service\'
datum aan te passen.

# Month end tasks

Ledger calendar

Periodes worden door finance 'on hold' gezet.

Financial reporting

Trial balance wordt gebruikt als basis voor rapportering.

Specifieke finance rapporten zijn gemaakt in

Ledger settlements

Bepaalde main accounts worden manueel gesettled met de functionaliteit
'ledger settlements'

BTW

[Verder uitwerken na meeting]{.mark}

Tax calculation service wordt NIET gebruikt.

Voor de intervat aangifte wordt er gebruik gemaakt van de standaard
'Belgian sales tax reporting'. Er wordt nog niet gewerkt met electronic
messages (via electronic reporting).

![A diagram of a computer AI-generated content may be
incorrect.](media/image7.png){width="6.268055555555556in"
height="2.9965277777777777in"}

**BTW-eenheid**

Winsol group is 1 btw-eenheid waardoor het settlen van de btw gebeurd in
Winsol International enkel wanneer alle individuele btw aangifte
ingediend zijn. Achteraf worden alle LE's apart gesettled.

Intrastat

De Intrastat aangifte dient enkel voor de aankopen van Helios (en
Actuell?) te gebeuren. Wat de verkopen betreft, in fase 1 blijft alles
verlopen via AS400, waardoor ook de intrastat aangifte vandaaruit
gebeurt.

IC-aangifte

IC-aangifte verloopt via de standaard functionaliteit van D365.

![A blue sign with white text AI-generated content may be
incorrect.](media/image8.png){width="4.817084426946631in"
height="1.0584251968503937in"}

Jaarlijkse klantenlisting

Hiervoor wordt het standaard rapport 'Invoice turnover report --
Belgium' gebruikt.

CR:

Voor bepaalde toegekende commissies, makelaarslonen, restorno's,
toevallige of niet-toevallige vacatiegelden of erelonen, gratificaties
of voordelen van alle aard die voor de ontvanger belastbare
beroepsinkomsten zijn, moet er een zogenoemde **fiscale fiche
281.50** worden opgesteld.

Year-end close

Op het einde van het boekjaar dient de openingsbalans in het nieuwe
boekjaar geboekt te worden. Hiervoor wordt de standaard year-end-close
functialiteit gebruikt.

Op jaareinde moeten volgende zaken gebeuren inzake de journalen en
vouchers:

- Resetten van journaalnummer (er zijn journal names voor oneven en even
  jaren)

- Resetten van vouchernummer

- De beboekbare periode van de journalen definiëren (bv.
  1/1/25-31/12/25)

# Inventory accounting

Item groups

Volgend onderscheid is gemaakt in de item groups:

**Verkoopartikel**

- Voorschotten: ADV-PAY

- Eindproduct: FP

- Plaatsing: INST

- Scrap: \"SCRAP-\" gevolgd door materiaaltype

- Doorgerekende kosten: \"ICO-\" gevolgd door type kost

**- Goederen in bewerking in fase 1 nog manueel geboekt (ze SFP nog niet
gebruikt)**

**- Handelsgoederen**

- Item model group \"TG\"

**- Grondstoffen**

- Item group begint met \"RM-\" gevolgd door afkorting van het
  materiaaltype

- Grootboekrekeningen voorzien om voorraad en voorraadwijzigingen bij te
  houden

**- Halffabricaten (in de zin van \"grondstof!\" bv electronics)**

- Item group: te behandelen zoals grondstoffen (\"RM-\")

- Deelcomponenten:

  - Goederen: \"RM-\"

  - Handeling (intern): \"SERV_BOM\"

  - Handeling (extern/aankoop): \"SC-TREAT\"

**- Hulpstoffen**

- Item group \"SG\"

- Boekhoudkundig geen voorraad =\> indien toch stock bijhouden dan item
  model group \"FIFO_NoIdg\"

**- Subcontracting/dienst**

- Productie (foliëren, lakken, ...): SC-TREAT

- Plaatsing: SC-INSTALL

**- Overige plaatsingskosten**

- Huur (hoogtewerkers, materialen): INST-RENT

- Overige kosten: INST-OTHER

**- Maintenance**

- Item group \"MNT-\" gevolgd door type kost

- Boekhoudkundig geen voorraad =\> indien toch stock bijhouden dan item
  model group \"FIFO_NoIdg\"

**- Werkkledij**

- Item group \"EMP-CLOTH\"

**- Prestaties derden**

- Prestaties derden (non-recurring): \"EMP-TEMP\"

- Consulting: Item group \"CON-FEES\"

**- Marketing**

- Item group \"MKT-\" gevolgd door type kost

- Boekhoudkundig geen voorraad =\> indien toch stock bijhouden dan item
  model group \"FIFO_NoIdg\"

Item model groups

Volgend onderheid is gemaakt in item model groups:

- FIFO

  - Item

  - Stock: Financieel en fysiek

- FIFO_NoLdg        

  - Item

  - Stock: fysiek (Financieel expense)

- SERV        

  - Service

  - Stock: geen

- SERV-STOCK        

  - Indien artikel/service deel kan uitmaken van halffabricaat (nu of in
    de toekomst) dan SERV-STOCK

Inventory close

Maandelijks moet er voor de voorraad 2 grote controles gebeuren:

- Aansluiten van de inventory value list met de general ledger (via
  trial balance)

- Het controleren van de inventory closing and adjustment
