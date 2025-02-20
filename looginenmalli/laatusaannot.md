---
layout: "default"
description: ""
id: "laatusaannot"
status: "Luonnos"
---
# Laatusäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

## Yhteiset laatusäännöt

### UML-mallin mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-uml-mukaisuus" %}
Tietomallin loogisen tietomallin toteutusten tulee noudattaa tietomallin [UML-kielisen luokkakaavion](./uml/) määrityksiä luokkien attribuuttien ja assosiaatioiden kardinaliteetin ja tyypin suhteen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-uml-toteutus" %}
Kunkin fyysisen tietomallin kuvauksessa tulee määritellä minkälaista rakennetta ja tietotyyppiä kukin loogisen tietomallin luokka ja attribuutin tyyppi vastaa fyysisessä mallissa. Attribuutit ja assosiaatiot, joiden kardinaliteetti on loogisessa tietomallissa ```0..1``` tai ```0..*``` voivat puuttua fyysisen tietomallin mukaisista objekteista.
{% include common/clause_end.html %}

### Tunnisteet ja sisäisten viittausten eheys
{% include common/clause_start.html type="req" id="laatu/vaat-tunnukset-viittaukset" %}
Tietomallin versioitavilla tietokohteilla tulee olla yksilöivät tunnukset, joiden luomisessa ja käyttämisessä viittaamiseen toisiin tietokohteisiin tulee noudattaa elinkaarisääntöjen luvun [Tunnukset ja niiden hallinta](elinkaarisaannot.html#tunnukset-ja-niiden-hallinta) vaatimuksia.
{% include common/clause_end.html %}

### Elinkaarisääntöjen mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-elinkaarisaannot" %}
Tietomallin mukaisten aineistojen tulee noudattaa [elinkaarisääntöjen](elinkaarisaannot.html) vaatimuksia, ja niiden on suositeltavaa noudattaa elinkaarisääntöjen suosituksia. Vaatimukset ja suositukset on erotettu selkeästi elinkaarisääntöjen muusta sisällöstä.
{% include common/clause_end.html %}

### Merkkijonojen käyttö
#### Merkistöt
{% include common/clause_start.html type="req" id="laatu/vaat-merkisto-utf8" %}
Kaikki tietomallin tekstimuotoiset sisällöt on tiedonsiirtoa varten koodattava käyttäen UTF-8 -merkistökoodausta.
{% include common/clause_end.html %}

#### Monikielinen sisältö ja kielikoodit
Kaikki tietomallin tekstimuotoinen sisältö ilmaistaan ISO 19103 -standardin määrittelemän [LanguageString](dokumentaatio/#languagestring)-luokan avulla.

{% include common/clause_start.html type="req" id="laatu/vaat-monikielisyys-kielikoodi" %}
Kunkin LanguageString-luokan objektin tulee toteuttaa ```language```-attribuutti, jonka arvona on ISO 639-2 -standardin mukainen terminologinen, kolmekirjaiminen kielikoodi code (ISO 639-2/T).
{% include common/clause_end.html %}

{% include common/note.html content="ISO 639-2/T koodilistan mukaiset koodit Suomen virallisille kielille ovat ```fin``` (suomi), ```swe``` (ruotsi), ```smn``` (inarinsaami), ```sms```(koltansaami) ja ```sme``` (pohjoissaami). Muita Suomessa paljon puhuttujen kielten ISO 639-2/T -koodeja: ```rus``` (venäjä), ```est``` (viro), ```ara```(arabia),  ```eng``` (englanti), ```som``` (somali), ```kur``` (kurdi)." %}

Tekstimuotoiset attribuutit on määritelty siten, että ne sisältävät nolla tai enemmän LanguageString-tyyppisiä arvoja.

{% include common/clause_start.html type="req" id="laatu/vaat-yksi-teksti-per-kieli" %}
Kunkin tekstimuotoista sisältöä kuvaavan attribuutin arvoina tulee olla enintään yksi LanguageString-tyyppinen arvo kutakin kielikoodia (```language```-attribuutti) kohti.
{% include common/clause_end.html %}

#### Enimmäispituudet
{% include common/clause_start.html type="req" id="laatu/vaat-merkijono-pituus" %}
Kunkin yhdellä kielellä annetun LanguageString-tyyppisen merkkijonon enimmäispituus on 2048 merkkiä.
{% include common/clause_end.html %}

{% include common/note.html content="Valittu 2048 merkin raja perustuu arvioon tietomallissa tarvittavien merkkijonojen tyypillisistä pituuksista. Merkkijonojen enimmäispituuden määrääminen loogisen tietomallin tasolla on jossain määrin kajoamista mallin tekniseen toteutukseen, mutta yhteentoimivuuden takaamisen näkökulmasta on tärkeää, että kaikkissa fyysisissä tietomalleissa varataan yhtä suuri maksimimäärä merkkejä tekstisisältöjen tallentamiseen. Muutoin on riskinä oikeusvaikuttteisen tiedon katoaminen tiedonsiirrossa tai -käsittelyproseseissa." %}

### Geometriat

#### Geometriatyypit
{% include common/clause_start.html type="req" id="laatu/vaat-geom-piste-maar" %}
Pistemäiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Point```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-2d-alue-maar" %}
Aluemaiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Surface```-rajapinnan.
{% include common/clause_end.html %}

{% include common/note.html content="Tietomalli ei vaadi kaikkien ISO 19107 -standardin mukaisten geometriatyyppien tukemista. Loogisen tietomallin mukaiset fyysiset tietomallit voivat rajoittaa mahdollisia geometriatyyppejä ja niiden ominaisuuksia." %}

#### Sallitut koordinaatistot ja koordinaattijärjestys

Rakennetun ympäristön tietojärjestelmä tukee seuraavia koordinaatistoja:

Tiedon luovutuksen koordinaatistot
* EPSG:4326, WGS84
  * Käytössä myös IFC-mallissa 
* EPSG:3857, Google Web Mercator
* Tiedon luovutusrajapinnan käyttäjä voi pyytää vastauksen haluamassaan tuetussa koordinaatistossa, jolloin tietojärjestelmä muuntaa tarvittaessa varannossa olevan tiedon haluttuun kohdekoordinaatistoon.

Tiedon luovutuksen ja vastaanoton koordinaatistot
* EPSG:3067, valtakunnallinen koordinaatisto.
* EPSG:3873-3885 koordinaatistot tiedon luovutuksessa / tiedon vastaanotossa
* Tiedon toimituksen yhteydessä tulee tallentaa tieto koordinaattijärjestelmästä ja korkeusjärjestelmästä (N2000), jossa tieto toimitettu.

{% include common/clause_start.html type="req" id="laatu/vaat-koord-jarjestys" %}
Geometrioiden ilmaisemisessa tulee noudattaa kunkin koordinaatiston määritelmässä annettua virallista koordinaattijärjestystä.
{% include common/clause_end.html %}

#### Geometrinen ja topologinen eheys

{% include common/clause_start.html type="req" id="laatu/vaat-suljetut-ringit" %}
Mikäli viiva on osa aluemaisen geometrian reunaviivaa, on sen oltava suljettu, eli sen alku- ja loppuppisteiden on oltava samat.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-alue-kielletyt-leikkaukset" %}
Aluemaisen geometrian ulkoreunan ja reikien reunaviivat eivät saa leikata itseään tai toisiaan. Kukin reunaviiva saa koskettaa alueen ulkoreunaa tai reiän reunaa, mukaanlukien se itse, vain yksittäisissä pisteissä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-yhteneva-alue" %}
Aluemaisen geometrian sisäosan on oltava yhtenevä, eli minkä tahansa kahden alueen sisäpisteen välillä on voitava muodostaa yhtenäinen käyrä, joka kulkee kokonaan alueen sisällä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-mitattava-alue" %}
Aluemaisen geometrian sisäosan pinta-ala on oltava mitattavissa, eli alueeseen tulee sisältyä pisteitä, jotka eivät ole osa alueen ulkoreunaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-pinnan-orientaatio" %}
Aluemaisten geometrioiden kiertosuuntien tulee noudattaa ISO 19107 -standardin määritelmää: Geometrioiden reunojen kiertosuunnat tulee valita siten, että pinnan yläpuolelta katsottuna ulkorajan reunan kiertosuunta on vastapäivään ja pinnan mahdollisten reikien reunojen kiertosuunnat ovat myötäpäivään. Mikäli pinta on osa 3-ulotteisten geometrian ulkorajaa, ulkopuoli vastaa yläpuolta.
{% include common/clause_end.html %}

### Päivämäärät ja kelloanajat
Tietomallin yksittäisiä ajanhetkiä kuvaavat attribuutit ovat ISO 19108 -standardin määrittämää tyyppiä [TM_Instant](dokumentaatio/#tm_instant) ja aikavälejä kuvaavat attribuutit tyyppiä [TM_Period](dokumentaatio/#tm_period). Päivämäärät annetaan käyttäen Gregoriaanista kalenteria ja kellonajat käyttäen 24 tunnin kelloaikamuotoa alkaen kellonajasta 00:00:00.000  ja päättyen ajanhetkeen 23:59:59.999 (tunti, minuutti, sekunti, millisekunti).

{% include common/clause_start.html type="req" id="laatu/vaat-ajanhetki-tarkkuus" %}
Yksittäisiä ajanhetkiä kuvaavat attribuutit ilmaistaan joko pelkän päivämäärän tai päivämäärän ja kelloajan avulla. Päivämäärät ilmaistaan antamalla vuoden, kuukauden ja kuukauden päivän numeeriset arvot. Kellonajat ilmaistaan vähintään yhden minuutin ja enintään yhden millisekunnin tarkkuudella antamalla tunnin, minuutin, sekunnin ja millisekunnin numeeriset arvot.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-aikavyohykkeet" %}
Päivämäärien ja kellonaikojen yhteydessä voidaan antaa myös tieto aikavyöhykkeestä tai aikojen poikkeamasta UTC-ajasta. Mikäli muuta ei tietoa ei anneta, tulee ajanhetkitiedot tulkita siten, että ne kuvaavat Suomen aikaa noudattaen kyseisellä ajanhetkellä voimassaolleita asetuksia kesäaikaan liittyen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-ajanhetki-muoto" %}
Mikäli fyysinen tietomalli ei aseta ajanhetken muodolle rajoituksia, on suositeltavaa käyttää [IETF RFC 3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)-standardin määrittelemää syntaksia.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-aikavali-maar" %}
Aikavälejä kuvaavat attribuutit voidaan antaa joko sekä alku- että loppuajanhetken avulla tai vain joko alku- tai loppuajanhetken avulla. Mikäli alkuajanhetkeä ei anneta, tulkitaan aikavälin sisältävän minkä tahansa ajanhetken loppuajanhetkeen saakka. Vastaavasti mikäli loppuajanhetkeä ei anneta, tulkitaan aikavälin sisältävän minkä tahansa ajanhetken alkujanhetkestä lähtien.
{% include common/clause_end.html %}

## Luokkakohtaiset säännöt

### Rakentamis,- purkamis-, poikkeamis- ja maisematyölupa asiat

{% include common/clause_start.html type="req" id="laatu/vaat-lupa-asia-vaadittu-poikkeamislupa-asia" %}
Mikäli rakentamisluvan myöntämisen edellytyksenä on myönnetty poikkeamislupa, poikkeamislupa-asiaa kuvaava  {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#rakennetunympäristönlupaasia" title="RakennetunYmpäristönLupaAsia" %}-luokan objekti liitetään [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)-luokan objektiin assosiaation ```liittyväAsia``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupa-asia-hakemus" %}
Rakentamis,- purkamis-, poikkeamis-, ja maisematyölupa-asioihin liittyvät lupahakemukset tulee liittää [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)-, [PurkamislupaAsia](dokumentaatio/#purkamislupaasia)-, [PoikkemislupaAsia](dokumentaatio/#poikkeamislupaasia)-, [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)- ja [MaisematyölupaAsia](dokumentaatio/#maisematyölupaasia)-luokan objektiin assosiaatiolla ```hakemus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupa-asian-toimenpiteet" %}
[RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)- tai [PurkamislupaAsia](dokumentaatio/#purkamislupaasia)-luokan objektin ```toimenpide```-assosiaatioiden arvot kuvaavat ne rakentamis- ja purkamistoimenpiteet, joita koskevien lupien myöntämistä lupa-asiassa käsitellään.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupa-asian-aluerajaus" %}
[RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)-luokan objektin attribuutille ```aluerajaus``` arvoksi on annettava aluemainen tai monialuegeometria, joka sisältää kaikkien hakemuksella luvitettaviksi haluttujen toimenpiteiden rakennuspaikkojen sijannit.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupa-asian-liitteet" %}
Kukin lupahakemuksen liitetiedosto tulee kuvata [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)-, [PurkamislupaAsia](dokumentaatio/#purkamislupaasia)-, [PoikkemislupaAsia](dokumentaatio/#poikkeamislupaasia)-, [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)- ja [MaisematyölupaAsia](dokumentaatio/#maisematyölupaasia)-luokan objektin attribuutin ```asianLiite``` avulla, mukaanlukien hakemuksen mukana mahdollisesti toimitettavat BIM-suunnitelmamallit ja rakennussuunnitelmat.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupa-asian-elinkaaritila" %}
[RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)-, [PurkamislupaAsia](dokumentaatio/#purkamislupaasia)-, [PoikkemislupaAsia](dokumentaatio/#poikkeamislupaasia)-, [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)- ja [MaisematyölupaAsia](dokumentaatio/#maisematyölupaasia)-luokan ```elinkaaritila```-attribuuttien arvona tulee käyttää koodiston [RakennusvalvontaAsianElinkaaritila](dokumentaatio/#rakenusvalvontaasianelinkaaritila) arvoja.
{% include common/clause_end.html %}

### Rakentamislupahakemus

[Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objektiin tallennetaan lupahakemuksen tiedot.

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-jatetty" %}
Kun lupahakemus on jätetty, eikä sitä ole peruttu jättäjän toimesta, tulee [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objektin attribuutilla ```elinkaaritila``` olla arvo ```Jätetty```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-asia" %}
[Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objekti tulee liittää lupahakemusasiaan  assosiaatiolla ```asia```.
{% include common/clause_end.html %}

Yhteen [RakentamislupaAsiaan](dokumentaatio/#rakentamislupaasia) voidaan liittää myös useampi kuin yksi [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus). Esimerkiksi voidaan hakea ensin sijoitamislupaa ja täydentää sitä toteuttamislupahakemuksella. Lupa-asiassa voidaan tällöin tehdä päätös, jolla myönnetään vain yksi [Rakentamislupa](dokumentaatio/#rakentamislupa), jonka ```lupatyyppi``` on yhdistetty sijoittamis- ja toteuttamislupa. 

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-rakennussuunnitelma" %}
Mikäli hakemukseen on liitetty rakennussuunnitelma, se tulee kytkeä [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objektiin assosiaation ```rakennussuunnitelma``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-suunnitelmamallit" %}
Mikäli hakemukseen on liitetty BIM-suunnitelmamalleja, ne tulee kytkeä [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objektiin assosiaation ```suunnitelmamalli``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-lupatyyppi" %}
Haettavan luvan tyyppi (sijoittamis- tai toteuttamislupa tai niiden yhdistelmä) tulee ilmaista [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan attribuutin ```lupatyyppi``` avulla. Haetun luvan tyypin ei tarvitse olla sama kuin lupaprosessin lopputuloksena mahdollisesti myönnetyn luvan tyypin.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-huoneiston-huoneiden-lkm" %}
Kun [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objektin liittyy [RakentamislupaAsia](dokumentaatio/#rakentamislupaasia)- ja edelleen {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohteentoimenpide" title="RakennuskohteenToimenpide" %}-, {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohteenmuutos" title="RakennuskohteenMuutos" %}- ja {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#huoneistonmuutos" title="HuoneistonMuutos" %}-luokkien kautta luokan {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#huoneisto" title="Huoneisto" %} objekteja, niiden attribuutti ```huoneidenLukumäärä``` on annettava.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-haetut-poikkeamiset" %}
Lupahakemuksessa tunnistetut rakentamistoimenpiteen toteuttamisen vaatimat vähäiset poikkeamiset {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#alueidenkäyttöjarakentamismääräys" title="AlueidenkäyttöJaRakentamismääräys" %}-luokan avulla kuvatuista rakentamista koskevista määräyksistä kuvataan [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan perityn ```haettuPoikkeaminen```-attribuutin arvojen avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupahakemus-peruttu" %}
Kun lupahakemus on peruttu jättäjän toimesta, tulee [Rakentamislupahakemus](dokumentaatio/#rakentamislupahakemus)-luokan objektin attribuutilla ```elinkaaritila``` olla arvo ```Peruttu```.
{% include common/clause_end.html %}

### Rakentamislupa

{% include common/clause_start.html type="req" id="laatu/vaat-myonnetyt-poikkeamiset" %}
Lupapäätöksellä myönnetyt rakentamistoimenpiteen toteuttamisen vaatimat vähäiset poikkeamiset {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#alueidenkäyttöjarakentamismääräys" title="AlueidenkäyttöJaRakentamismääräys" %}-luokan avulla kuvatuista rakentamista koskevista määräyksistä kuvataan [Rakentamislupa](dokumentaatio/#rakentamislupa)-luokan perityn ```myönnettyPoikkeaminen```-attribuutin arvojen avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-lupamaaraykset" %}
Myönnettyyn rakentamislupaan sisältyvät lupamääräykset kuvataan {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/#lupamääräys" title="Lupamääräys" %}-luokan objektien avulla, ja ne liitetään osaksi luotavaa [Rakentamislupa](dokumentaatio/#rakentamislupa)-luokan objektia sen assosiaation ```määräys``` avulla. Rakentamislupaan kuuluvien määräysten ```määräyksenLaji```-attribuutin arvon tulee olla koodiston [RakentamislupamääryksenLaji](dokumentaatio/#rakentamislupamääräyksenlaji) koodi.
{% include common/clause_end.html %}
{% include common/clause_start.html type="req" id="elinkaari/vaat-myonnetty-poikkeamislupa" %}
Mikäli rakentamisluvan myöntämisen edellytyksenä on ollut erillinen poikkeamislupa, se liitetään luotavaan [Rakentamislupa](dokumentaatio/#rakentamislupa)-luokan objektiin assosiaation ```liittyväLupa``` avulla.
{% include common/clause_end.html %}


{% include common/clause_start.html type="req" id="laatu/vaat-rakentamisluvan-jarjestysnumero" %}
[Rakentamislupa](dokumentaatio/#rakentamislupa)-luokan objektilla tulee olla ```lupaTunnus```-attribuutin arvo, joka sisältää myönnetyn rakentamisluvan järjestysnumero. Merkkijonon tulee koostua merkeistä "A" - "Ö" ja "0" - "9", eikä se saa olla "000".
{% include common/clause_end.html %}

### ToimenpiteenJatkoaikapäätös

{% include common/clause_start.html type="req" id="laatu/vaat-toimepiteen-jatkoaika" %}
Myönnetyn rakentamisluvan piiriin kuuluvan rakentamiskohteen toimenpiteen aloittamisen jatkoajasta tehty päätös kuvataan tietomallissa [ToimenpiteenJatkoaikapäätös](dokumentaatio/#toimenpiteenjatkoaikapäätös)-luokan objektina. Assosiaation ```jatkettuLupa``` tulee kohdistua siihen [Rakentamislupa](dokumentaatio/#rakentamislupa)-luokan objektiin, johon kuuluvia toimenpiteitä jatkoaika koskee. Assosiaation ```toimenpide``` tulee viitata niihin {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohteentoimenpide" title="RakennuskohteenToimenpide" %}-luokan objekteihin, joiden aloittamista jatkoaikapäätös koskee. Jatkoaikapäätöksen ```jatkoajanPäättymispäivämäärä```-attribuutin arvoa käytetään kyseisen [Rakentamislupa](dokumentaatio/#rakentamislupa)-luokan objektin ```raukeamispäivämäärä```-attribuutin sijaan arvoitaessa rakentamisluvan voimassaoloa kyseisten rakentamiskohteen toimenpiteiden osalta. Luvan lainvoimaiseksi tullessa asetettua alkuperäistä Rakentamislupa-luokan ```raukeamispäivämäärä```-attribuutin arvoa ei muuteta jatkoaikapäätöksen yhteydessä.
{% include common/clause_end.html %}

### Rakentamishanke

Yhdessä Rakentamishankkeessa voidaan toteuttaa useiden eri rakentamislupaprosessien kautta luvitettuja toimenpiteitä, sekä toimenpiteitä, jotka eivät vaadi rakentamislupaa.

{% include common/clause_start.html type="req" id="laatu/vaat-rakentamishankkeen-luvat" %}
Mikäli rakentamishankkeen toteuttamiseen vaaditaan yksi tai useampi myönnetty rakentamislupa tai muu rakennetun ympäristön lupa, ne tulee liittää [Rakentamishanke](dokumentaatio/#rakentamishanke)-luokan objektiin assosiaation ```vaadittuLupa``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakentamishankkeeseen-ryhtyva" %}
Hankkeeseen ryhtyvän toimijan tiedot on annettava assosiaation ```hankkeeseenRyhtyvä``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakentamishankkeen-tyonjohtaja" %}
Hankkeen vastaavan työnjohtajan tiedot on annettava assosiaation ```vastaavaTyönjohtaja``` avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakentamishankkeen-tyonjohtaja" %}
Rakentamishankkeen pääsuunnittelija, {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennussuunnitelma" title="Rakennussuunnitelmista" %} vastaava rakennussuunnittelija ja {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#erityissuunnitelma" title="Erityissuunnitelmista" %} vastaavat erityissuunnittelijat tulee liittää [Rakentamishanke](dokumentaatio/#rakentamishanke)-luokan objektiin assosiaation ```suunnittelija``` avulla.
{% include common/clause_end.html %}

{% include common/question.html content="Onko tarvetta olla erilliset assosiaatiot hankkeen pääsuunnittelijalle, vastaavalle rakennussuunnittelijalle ja vastaaville erityissuunnittejoille?" %}

{% include common/clause_start.html type="req" id="laatu/vaat-rakentamishankkeeseen-paivamaarat" %}
Mikäli [Rakentamishanke](dokumentaatio/#rakentamishanke)-luokan objektille on annettu sekä ```aloittamispäivä```- että ```valmistumispäivämäärä```-attribuutin arvot, tulee ```valmistumispäivämäärä```-attribuutin päivämäärän olla myöhempi tai sama kuin ```aloittamispäivä```-attribuutin päivämäärä.

Mikäli [Rakentamishanke](dokumentaatio/#rakentamishanke)-luokan objektille ei ole annettu ```aloittamispäivä```-attribuutin arvoa, ei sillä saa olla ```valmistumispäivämäärä```-attribuutin arvoa.
{% include common/clause_end.html %}

### Katselmus

Katselmuksen tietoihin tulee sisällyttää viitaus sekä katselmoitavan {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohde" title="Rakennuskohteen" %} alkuperäisestä, luvan hakemisen aikaiseen tilaan (mikäli kyseessä ei ole uudisrakennus) että uusimpaan suunniteltuun tai toteutuneeseen Rakennnuskohteen tilaan katselmoinnin suorittamisen aikana.

{% include common/clause_start.html type="req" id="laatu/vaat-katselmuksen-kohde" %}
[Katselmus](dokumentaatio/#katselmus)-luokan objektin rakenteisen ```kohteenMuutos```-attribuutin assosiaation ```kohdeMuutoksenJälkeen``` tulee osoittaa {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohde" title="Rakennuskohde" %}-luokan objektin uusimpaan versioon, joka sisältää katselmoinnissa käsitellyt tiedot. Assosiaation ```kohdeEnnenMuutosta``` tulee osoittaa samaan {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohde" title="Rakennuskohde" %}-luokan objektin versioon, johon kyseistä rakennuskohdetta koskevan, ```katselmoituToimenpide```-assosiaatiolla viitatun {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohteentoimenpide" title="RakennuskohteenToimenpide" %}-luokan objektin rakenteisen attribuutin ```suunnniteltuMuutos``` assosiaatio ```kohdeEnnenMuutosta``` osoittaa. Uudisrakennuksen rakentamistoimenpiteen tapauksessa [Katselmus](dokumentaatio/#katselmus)- ja {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohteentoimenpide" title="RakennuskohteenToimenpide" %}-luokkien sisältämien {% include common/moduleLink.html moduleId="rakennuskohteet" path="looginenmalli/dokumentaatio/#rakennuskohteenmuutos" title="RakennuskohteenMuutos" %}-luokan ```kohdeEnnenMuutosta```-assosiaatioita ei tule käyttää.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-katselmuksen-toimittaja" %}
Katselmuksen toimittajan tiedot tulee antaa [Katselmus](dokumentaatio/#katselmus)-luokan ```toimittaja```-assosiaation avulla.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-katselmuksen-lasnaolijat" %}
Katselmuksen läsnäolijoiden tiedot tulee antaa [Katselmus](dokumentaatio/#katselmus)-luokan ```läsnäolija```-assosiaation avulla.
{% include common/clause_end.html %}

