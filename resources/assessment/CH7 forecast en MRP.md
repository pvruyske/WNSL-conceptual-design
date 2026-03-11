# Contents

[Contents [1](#_Toc206535784)](#_Toc206535784)

[CustomDevs [2](#customdevs)](#customdevs)

[ISVs [2](#isvs)](#isvs)

[Specific configuration
[2](#specific-configuration)](#specific-configuration)

[Batch jobs [2](#batch-jobs)](#batch-jobs)

[1 Introduction [3](#introduction)](#introduction)

[2 MRP voor aankoop orders
[3](#mrp-voor-aankoop-orders)](#mrp-voor-aankoop-orders)

[2.1 Link met PA's [3](#link-met-pas)](#link-met-pas)

[2.2 Gebruik in winsol [3](#gebruik-in-winsol)](#gebruik-in-winsol)

[3 MRP voor halffabrikaten
[4](#mrp-voor-halffabrikaten)](#mrp-voor-halffabrikaten)

# CustomDevs

**No table of figures entries found.**

# ISVs

**No table of figures entries found.**

# Specific configuration

**No table of figures entries found.**

# Batch jobs

**No table of figures entries found.**

# Introduction

Wordt in alle fabrieken gebruikt in min of meerdere mate. Momenteel
wordt geen gebruik gemaakt van echte consumptie forecasts in D365. MRP
wordt op min/max stock level gebruikt. De scope is vnl HLS momenteel.
Voor bevestigingsmaterialen, verpakkingsmaterialen, lakpoeders, ...

Door seizoenaliteit worden de min/max stocklevels periodiek aangepast om
zo de MRP bestellingen te laten triggeren

Voor Halffabrikaten wordt mrp ook gebruikt; waarbij min stocks
gedefinieerd zijn op de halffabrikaten (enkel top level HF, eventueel
tussenlevels worden nu niet in mrp betrokken). In dit geval wordt een
planned production order gemaakt. Dit PPO order wordt niet uitgevoerd,
er wordt uiteindelijk een bom journal gebruikt om het HF te maken.

ALU wordt besteld zonder MPR daar loopt een andere forcast op XLS op, de
bestelvoorstellen worden binnen getrokken naar D365

# MRP voor aankoop orders

Er zijn 3 MRP-plannen gedefinieerd voor HF, verpakking en poeders. Deze
plannen staan los van elkaar. De driver om verschillende plannen te
hebben is gedreven door het feit dat ze door 3 verschillende mensen
gedraaid en verwerkt (bestellen) worden.

> Let op : gezien de stock nog niet continu geconsumeerd wordt, maar we
> vaak via tellingen werken, betekent dit dat de MRP enkel zinvol kan
> gelopen worden na een telling, in de praktijk is dit dus
> wekelijks/maandelijks ifv van de case.

De MRP plannen worden manueel getriggerd en verwerkt (bestellen).

De output van de MRP wordt geselecteerd per leverancier en zo wordt een
PO aangemaakt met alle behoeftes voor die levernacier.

## Link met PA's

Het is mogelijk dat er items in MRP verschijnen die onder PA vallen. Dan
zal D365 automatisch de PA voorstellen.

## Gebruik in winsol

- HLS : voor aankoop en HF

- IND : via de critial on hand list

- WBL : willen we nog uitrollen

- ACT : via critical on hand + firmen van PPO-orders

# MRP voor halffabrikaten

De leadtime zit op default order settings.
