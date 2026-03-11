# Overzicht

Winsol werkt met een **hybride IT-landschap** waarin Microsoft Dynamics
365 Finance & Operations (D365 F&O) fungeert als centrale ERP-oplossing.
De bedrijfsprocessen worden daarnaast ondersteund door meerdere
gespecialiseerde **CPQ-tools** voor productconfiguratie en offertes,
geïntegreerd via de **Invictus-communicatiebus**.\
Aanvullende systemen faciliteren documentbeheer, urenregistratie,
ticketing en dataopslag.

<https://winsolgroup.sharepoint.com/sites/BusinessAnalyse/Business%20analyse/IT%20application%20landscape.pptx?web=1>

![A screenshot of a computer screen AI-generated content may be
incorrect.](media/image1.png){width="6.268055555555556in"
height="3.5256944444444445in"}

# Kernsystemen

## ERP -- Microsoft Dynamics 365 F&O

**Opgedeeld in meerdere fases**

**Fase 1 : met go live in November 2024 : finance & procure to pay**

- Integraties: CPQ-tools, BI, Invictus, webshop

Fase 2 : productie -- nog niet opgestart in augustus 2025

Fase 3 : CRM functionaliteit binnen Dynamics.

## CPQ-tools (Configure Price Quote):

CPQ tools dienen om prijs offertes op te maken voor klanten in functie
van hun gewenste configuratie : bv luifel van 5m x 2m met zwart doek en
spotjes. De info van CPQ stroom door naar CTO om tot een productie order
te komen met specifieke componenten en productie instructies.

- **WinCal**: Luifels, rolluiken, poorten

- **WinsolCom**: Ramen en deuren

- **Chacal**: Projectoffertes voor ramen/deuren worden rechtstreeks in
  de CTO gemaakt.

- **Tekla** : offertes voor balustrade projecten lopen via Tekla
  software

## CTO-tools (Configure to Order vroeger CTP genoemd -- configure to production):

Eenmaal een product via CPQ geconfigueerd werd en besteld wordt,
passeert het via de CTO software om tot de nodige productie en
aankooporders te leiden.

- AS400 : Luifels, poorten, rolluiken, screens

- XLS : pergola SO & ZIP

- Chacal : ramen & deuren

De output van CTO software zijn werkorders, aankooporders en bijhorende
instructies.

Voor F1 van D365 worden ook aankooporders aangemaakt : bv het glas voor
in een raam wordt vanuit Chacal aangemaakt als PO in D365. Met F2 zal
Chacal een product variant aanmaken voor het glas en zal het PO via MRP
gemaakt worden vanuit de behoefte van het bovenliggende werkorder.

<https://winsolgroup.sharepoint.com/sites/BusinessAnalyse/Business%20analyse/CTO%20Helios%20architectuur.pptx?web=1>

![A diagram of a computer program AI-generated content may be
incorrect.](media/image2.png){width="3.969650043744532in"
height="2.769870953630796in"}

![A diagram of a ctp AI-generated content may be
incorrect.](media/image3.png){width="6.268055555555556in"
height="3.5145833333333334in"}

![A diagram of a computer AI-generated content may be
incorrect.](media/image4.png){width="6.268055555555556in"
height="3.527083333333333in"}

## 4 CRM

Anno 2025 draait CRM as AS/400. CRM omvat volgende scope

- Aanmaken klanten op basis van leads / sales input

- Beheer van klantenbezoeken en lead-contacten

## 5 Integraties

Integraties intern tussen D365 en AS400 lopen grotendeels over het
Invictus platform van Codit. Volgende integraties zijn operationeel met
go live F1.

<https://winsolgroup.sharepoint.com/sites/BusinessAnalyse/Business%20analyse/D365%20interfaces%20overview.pptx?web=1>

![A screenshot of a computer AI-generated content may be
incorrect.](media/image5.png){width="6.268055555555556in"
height="3.5381944444444446in"}

![A diagram of a server AI-generated content may be
incorrect.](media/image6.png){width="6.268055555555556in"
height="3.5243055555555554in"}

![A diagram of a server AI-generated content may be
incorrect.](media/image7.png){width="6.268055555555556in"
height="3.504166666666667in"}
