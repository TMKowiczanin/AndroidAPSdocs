# Veelgestelde vragen

Om vragen toe te voegen aan de Veelgestelde Vragen: volg deze [instructies](../make-a-PR.md)

## Algemeen

### Kan ik de AndroidAPS app gewoon downloaden?

Nee. Er is geen downloadbaar apk bestand voor AndroidAPS. Je moet het zelf [bouwen](../Installing-AndroidAPS/Building-APK.md). Omdat:

AndroidAPS wordt gebruikt om je pomp te bedienen en insuline te geven. Volgens de huidige regelgeving vallen dit soort systemen onder klasse Ia of IIb voor medische hulpmiddelen. Dat betekent dat die een wettelijke goedkeuring (CE-markering) vereisen, waarvoor verschillende studies en verificaties nodig zijn. Het verspreiden van een ongereguleerd medisch hulpmiddel is illegaal. In andere delen van de wereld bestaat vergelijkbare regelgeving.

Deze regelgeving beperkt zich niet tot verkoop (in de zin dat er geld voor wordt gevraagd), maar is van toepassing op elke vorm van distributie (zelfs gratis weggeven). Het bouwen van een medisch apparaat voor jouzelf is de enige manier om niet onder deze regelgeving te vallen.

Dat is waarom een kant-en-klare app niet beschikbaar is.

### Hoe begin ik?

Ten eerste, moet je alle **fysieke onderdelen van een closed loop** verzamelen:

* Een [geschikte insulinepomp](Pump-Choices.md), 
* een [Android smartphone](Phones.md) (Apple iOS wordt niet ondersteund door AndroidAPS - je kunt wel [iOS Loop](https://loopkit.github.io/loopdocs/) gebruiken) en 
* een [glucose sensor](../Configuration/BG-Source.md). 

Ten tweede, moet je de **fysieke onderdelen instellen**. Zie het [gebruiksvoorbeeld](Sample-Setup.md) met stap voor stap instructies.

Ten derde, moet je alle **software bouwen en instellen**: AndroidAPS en CGM/FGM bron.

Ten vierde moet je leren en **begrijpen hoe het algoritme is ontworpen om jouw behandelingsfactoren** correct in te kunnen stellen. Het grondbeginsel van closed loopen is dat jouw basaalstanden en koolhydraatratio's correct zijn. Alle aanpassingen die de closed loop doet, gaan er vanuit dat jouw basaalstand klopt. Alle pieken en dalen die je ziet zijn dus een gevolg van andere, tijdelijke factoren (beweging, stress etc) die dan worden opgelost met een tijdelijke insulineaanpassing. De aanpassingen die de closed loop kan maken zijn uit veiligheid beperkt (zie maximaal toegestane basaalstand in [OpenAPS Reference Design](https://openaps.org/reference-design/)). Dit betekent dat je de closed loop niet moet inzetten om een fout afgestelde basaalstand te verhelpen. Wanneer je bijvoorbeeld vaak een lage waarde hebt vlak voor een maaltijd, dan moet waarschijnlijk je basaal omlaag. Je kunt [autotune](http://openaps.readthedocs.io/en/latest/docs/Customize-Iterate/autotune.html#phase-c-running-autotune-for-suggested-adjustments-without-an-openaps-rig) aan de hand van een grote hoeveelheid gegevens, suggesties laten doen voor verbeteringen aan je basaalstanden, ISF en/of koolhydraatratio. Of je kunt je basaalstanden op de [ouderwetse manier](http://integrateddiabetes.com/basal-testing/) testen en instellen.

### Zijn er nog praktische tips?

* Als je niet wilt dat jouw instellingen gemakkelijk worden aangepast, dan kun je het instellingen menu voorzien van een wachtwoord. Ga naar "Wachtwoord voor instellingen" in het instellingen menu en typ een zelfgekozen wachtwoord. De volgende keer dat je het instellingen menu opent, moet je het wachtwoord intypen om verder te kunnen. Wanneer je later geen wachtwoord meer wilt gebruiken, ga dan naar het "Wachtwoord voor instellingen" veld en verwijder de tekst.

* Wanneer je in de toekomst de Android Wear app wilt gebruiken om vanaf een smartwatch te kunnen bolussen of instellingen te wijzigen, dan moet je instellen dat notificaties van AndroidAPS niet geblokkeerd worden. Bevestiging van opdrachten die je op je smartwatch invoert, komen namelijk via een notificatie binnen op je telefoon.

* Als je de pomp wilt afkoppelen voor douchen/sporten etc, houd dan "Open-Loop" / "Closed Loop" tekst op het Overzicht-scherm ingedrukt en selecteer "verbreek verbinding ..min/u met pomp" voor hoelang je de pomp wilt afkoppelen. Hiermee zet je de basaal op nul voor de tijdsduur die je hebt gekozen. De minimale tijdsduur die je kunt kiezen komt door de minimale tijdsduur van TBRs die jouw pomp toestaat. Wanneer je een kortere tijd wilt kiezen, of je koppelt je pomp sneller aan dan je had gedacht, dan kun je "Verbinding verbroken (..m)" ingedrukt houden en "Opnieuw verbinden" kiezen. Op deze manier zal jouw IOB correct berekend worden nadat je je pomp weer hebt aangekoppeld.

* Uit veiligheidsoogpunt zal AAPS aanpassingen doen op basis van een gemiddelde glucosewaarde ('gemiddeld verschil'), nooit op basis van één enkele waarde. Daarom zal het even duren voordat de loop weer iets doet nadat je even geen glucosewaardes hebt ontvangen.

* Er zijn verschillende blogs met goede tips om jou te helpen om de loop goed in te stellen (in het Engels):
  
  * [Fine-tuning Settings](http://seemycgm.com/2017/10/29/fine-tuning-settings/) See my CGM
  * [Why DIA matters](http://seemycgm.com/2017/08/09/why-dia-matters/) See my CGM
  * [Limiting meal spikes](https://diyps.org/2016/07/11/picture-this-how-to-do-eating-soon-mode/) #DIYPS
  * [Hormones and autosens](http://seemycgm.com/2017/06/06/hormones-2/) See my CGM

### Welke spullen moet ik bij me hebben voor noodgevallen?

Allereerst, je moet dezelfde spullen bij je hebben als iedere andere persoon die een insulinepomp gebruikt. Als aanvulling daarop, wordt voor mensen die loopen met AndroidAPS aanbevolen om de volgende extra dingen bij je of binnen handbereik te hebben:

* Losse accu (powerbank) zodat je je smartphone, smartwatch en (wellicht) bluetooth reader kunt opladen
* Digitale backup (Dropbox, Google Drive, ...) van de apps die je gebruikt, zoals jouw meest recente AndroidAPS apk-bestand en jouw key store (digitale handtekening), AndroidAPS instellingenbestand, xDrip instellingenbestand, aangepaste Dexcom app, ...
* Batterijen voor je insulinepomp

### How to safely attach the CGM/FGM?

Je kunt hem vastplakken: door je huid van te voren in te smeren met speciale lijm (zoals Skintac). Ook zijn er op maat gemaakte 'fixeerpleisters' voor veelgebruikte CGM-systemen verkrijgbaar. Die plak je over de originele sensor/pleister heen. Vraag jouw diabetesverpleegkundige, hulpmiddelenleverancier of op een online forum/facebook. Of gebruik google. Je kunt ze ook zelf op maat knippen van kinesiotape of een eilandpleister.

Er bestaan ook speciale bandjes voor om je bovenarm die de CGM/FGM op zijn plek houden. Die zijn online verkrijgbaar (even googelen).

## AndroidAPS instellingen

### Invloed van instellingen

Deze tabel is bedoeld om te helpen met het optimaliseren van jouw instellingen. De beste volgorde is deze van boven naar beneden te doorlopen. Focus je eerst op één instelling en zorg dat die correct is, voordat je de volgende gaat optimaliseren. Werk in kleine stapjes in plaats van meteen grote veranderingen te maken. En bekijk een verandering gedurende meerdere dagen; geen dag is hetzelfde met diabetes! Je kunt [Autotune gebruiken](https://autotuneweb.azurewebsites.net/) om aanwijzingen voor verbeteringen te krijgen, hoewel je het niet blindelings moet volgen: het werkt misschien niet goed voor jou of in alle omstandigheden. Merk op dat alle instellingen met elkaar samenhangen - je kunt 'verkeerde' instellingen hebben die in sommige omstandigheden goed samenwerken (bijvoorbeeld als een te hoge basaal toevallig samenvalt met een te hoge CR) maar niet in andere omstandigheden. Dit betekent dat je met alle instellingen rekening moet houden bij veranderingen, en ze zo afstemmen dat ze voor jou goed werken in verschillende omstandigheden.<table class="tg" border=1> 

<th class="tg-0pky">
  Instelling
</th>

<th class="tg-0pky">
  Definitie & Hoe te testen
</th>

<th class="tg-0pky">
  Invloed op BG
</th>

<td class="tg-0pky">
  Duur van insuline activiteit (DIA)
</td>

<td class="tg-0pky">
  Hoe het lang duurt na een bolus totdat de hoeveelheid insuline weer is afgenomen naar nul. <br /><br />Dit hebben veel mensen te kort ingesteld. Dit zou je op ten minste 5 uur moeten zetten, mogelijk 6 of 7. Let op: AndroidAPS stelt automatisch 5 in, wanneer je een kleiner getal kiest!
</td>

<td class="tg-0pky">
  Te korte DIA kan zorgen voor te lage BGs. En omgekeerd: te lange DIA kan zorgen voor te hoge BGs.<br /><br />Als DIA te kort is, denkt AAPS te vroeg dat je eerdere bolus helemaal is uitgewerkt, en, bij hoog blijvende glucosewaardes, zal hij je meer insuline gaan geven. (Eigenlijk wacht AAPS niet zo lang, maar voorspelt wat er zou gebeuren en zal hij steeds insuline bijgeven). Dit zorgt voor “insuline stapeling” waar AAPS zich niet bewust van is.<br /><br />Voorbeeld van een te korte DIA is een hoge BG gevolgd door een overcorrectie en daarmee een te lage BG.
</td>

<td class="tg-0pky">
  Basaalstanden (E/uur)
</td>

<td class="tg-0pky">
  De hoeveelheid insuline per uur in een bepaald tijdsblok, om BG stabiel te houden.<br /><br />Test jouw basaalstanden door te 'open loopen' en te vasten. Start met jouw basaaltest 5 uur na je laatste voedsel+bolus, en bekijk vanaf dat moment hoe jouw BG verandert. Je hoeft geen hele dag te vasten, maar doe het per dagdeel. Kies normale, gemiddelde dagen qua beweging, stress etc. Herhaal een paar keer.<br /><br />Als BG daalt, is je basaal te hoog. En omgekeerd.
</td>

<td class="tg-0pky">
  Te hoge basaal kan leiden tot lage BGs. En omgekeerd.<br /><br />AAPS houdt jouw ingestelde basaalstanden aan als 'nullijn'. Hij is altijd geneigd om jouw IOB uiteindelijk naar nul te brengen. Als je basaal te hoog is, zal hij een 'zero temp' (basaalstand van 0) meetellen als een te sterk negatieve IOB. Als reactie op die negatieve IOB zal AAPS meer correcties geven dan hij zou moeten doen, vanwege de neiging om jouw IOB naar nul te willen brengen.<br /><br />Dus een te hoge basaal zal lage BGs creëren: zowel door de ingestelde standaardbasaal die je krijgt, als door de correctie-insuline die AAPS geeft om het streefdoel te bereiken.<br /><br />Omgekeerd kan een te lage basaal leiden tot hoge BGs en zal het AAPS niet lukken om je omlaag te brengen naar het streefdoel.
</td>

<td class="tg-0pky">
  Insuline gevoeligheids factor (Insulin Sensitivity Factor, ISF) (mmol/l/E of mg/dl/E)
</td>

<td class="tg-0pky">
  Hoeveel jouw BG zou moeten dalen na het nemen van 1E insuline.<br /><br />Zorg dat je eerst jouw basaal goed hebt ingesteld, daarna kun je ISF testen door AAPS op 'open loop' te zetten bij een vlakke BG, terwijl IOB nul is en je geen voedsel in je maag hebt. Neem dan een paar glucose tabletten zodat je BG op een plateau van een hogere waarde komt. (NB: Kies tijdens deze test BG waardes rond jouw normale gebied, bijvoorbeeld een start BG van 5mmol/l of 90mg/dl en breng hem omhoog naar 9mmol/l of 160 mg/dl).<br /><br />Neem vervolgens een hoeveelheid insuline (op basis van jouw huidige ISF) om naar jouw streefBG te komen. Wanneer de BG enkele uren later gestabiliseerd is, weet je of jouw ISF klopt.<br /><br />NB: De ISF is bij veel mensen te laag ingesteld. 'Te laag' betekent dat 1E insuline jouw BG te veel zal laten zakken.
</td>

<td class="tg-0pky">
  Lagere ISF = een kleinere daling van BGs voor elke eenheid insuline (wordt ook wel ‘heftiger / agressiever’ of ‘sterker’ genoemd). Een te lage ISF zal leiden tot lage BGs.<br /><br />Hogere ISF = een grotere daling in BGs voor elke eenheid insuline (wordt ook wel ‘minder sterk / minder agressief’ of ‘zwakker’ genoemd). Een te hoge ISF kan leiden tot hoge BGs.<br /><br />Een ISF die te laag is (niet ongebruikelijk) kan leiden tot ‘overcorrecties’, omdat AAPS denkt dat meer insuline nodig is om een hoge BG te corrigeren dan dat hij feitelijk nodig heeft. Dit kan leiden tot een "golfbeweging / achtbaan" in je glucosegrafiek (vooral tijdens vasten). In deze omstandigheden moet je je ISF verhogen. Dit betekent dat AAPS kleinere correctie doses zal geven, en dit voorkomt dat een hoge BG wordt overgecorrigeerd met daarna een lage BG. <br /><br />Omgekeerd kan een ISF die te hoog is, leiden tot ondercorrectie, wat betekent dat jouw BG boven het streefdoel blijft – met name zichtbaar gedurende de nacht.
</td>

<td class="tg-0pky">
  Koolhydraat ratio (KH ratio) (g/E)
</td>

<td class="tg-0pky">
  Hoeveel gram koolhydraten jij kunt eten voor 1E insuline.<br /><br />Zorg dat je eerst jouw basaal + ISF goed hebt ingesteld, daarna kun je CR testen door AAPS op 'open loop' te zetten, op een moment dat IOB nul is en je geen voedsel in je maag hebt. Neem dan een maaltijd waarvan je de koolhydraten precies weet, en injecteer een hoeveelheid insuline op basis van je huidige KH ratio. Wanneer de BG enkele uren later gestabiliseerd is, weet je of jouw KH ratio klopt. Je kunt bij deze test het beste kiezen voor voedsel dat je normaal gesproken ook zou eten rond dat tijdstip. En zorg dat je het aantal koolhydraten exact weet (pak weegschaal + koolhydratentabel erbij).
</td>

<td class="tg-0pky">
  Lagere KH ratio = minder voedsel per eenheid. Oftewel je gebruikt meer insuline voor dezefde hoeveelheid koolhydraten. Kan ook ‘agressiever’ worden genoemd.<br /><br />Hogere KH ratio = meer voedsel per eenheid, oftewel je gebruikt minder insuline voor dezelfde hoeveelheid koolhydraten. Kan ook ‘minder agressief’ worden genoemd.<br /><br />Als jouw BG hoger uitkomt nadat een maaltijd is verteerd en IOB weer is teruggekomen naar nul, dan is jouw KH ratio te groot. En omgekeerd: als je BG lager uitkomt, dan is KH ratio te laag.
</td></table> 

### APS algoritme

#### Waarom zie ik "dia:3" in de "OPENAPS AMA"-tab ook al heb ik een andere DIA in mijn profiel?

![AMA 3u](../../images/Screenshot_AMA3h.png) In AMA, DIA actually doesn't mean the 'duration of insulin acting'. Het is een parameter die vroeger wel gelinkt was aan de DIA. Nu betekent het 'binnen welke tijd zou de correctie moeten zijn afgerond'. En heeft het niets meer te maken met de berekening van de IOB. In OpenAPS SMB wordt deze parameter niet meer gebruikt.

### Profiel

#### Waarom minimaal een 5 uur DIA (Duur van Insuline Actie) gebruiken in plaats van 2-3 uur?

Goed uitgelegd in [dit artikel](http://www.diabettech.com/insulin/why-we-are-regularly-wrong-in-the-duration-of-insulin-action-dia-times-we-use-and-why-it-matters/). Don't forget to `ACTIVATE PROFILE` after changing your DIA.

#### Waarom zorgt de loop ervoor dat mijn bloedsuiker vaak zo ver zakt dat ik een hypo krijg, terwijl mijn COB (koolhydraten aan boord) nul is?

Controleer als eerste of jouw basaalinstellingen correct zijn, en test je basaalstanden door met een stabiele bloedglucose een tijdlang niets te eten. Pas je basaalstanden aan indien nodig. Nadat je zeker bent dat je basaalstanden goed zijn ingesteld, kun je naar je ISF kijken. Het kan ook zijn dat die waarde te laag is. Een typisch voorbeeld van een te lage ISF ziet er zo uit:

![ISF te laag](../images/isf.jpg)

#### Waarom heb ik hoge glucosepieken na een maaltijd terwijl ik een closed loop gebruik?

Controleer als eerste of jouw basaalinstellingen correct zijn, en test je basaalstanden door met een stabiele bloedglucose een tijdlang niets te eten. Pas je basaalstanden aan indien nodig. Nadat je zeker bent dat je basaalstanden goed zijn ingesteld, én je ziet dat jouw glucosewaarde wel weer zakt naar je streefdoel wanneer alle koolhydraten zijn geabsorbeerd dan kun je proberen om enige tijd voorafgaand aan je maaltijd een 'Eet binnenkort' tijdelijk laag streefdoel in te stellen. Of overleg met je behandelaars of je een bepaalde hoeveelheid tijd tussen bolus en maaltijd kunt nemen (pre-bolussen). Wanneer je bloedglucose te hoog is na de maaltijd, en hoog blijft nadat al je koolhydraten zijn geabsorbeerd, dan kun je vragen aan je behandelaars of je jouw KH ratio kunt verlagen. Wanneer je bloedglucose te hoog is terwijl je nog COB hebt, en je te laag uitkomt nadat alle koolhydraten geabsorbeerd zijn, dan kun je vragen aan je behandelaars of je jouw KH ratio kunt verhogen én een bepaalde hoeveelheid tijd te nemen tussen bolus en maaltijd.

## Overige instellingen

### Nightscout instellingen

#### AndroidAPS NSClient zegt 'Not allowed' (niet toegestaan) en wil geen gegevens uploaden. Wat kan ik doen?

Controleer 'Verbindingsinstellingen' in NSClient. Misschien heb je geen wifi verbinding of je hebt 'Enkel tijdens opladen' geactiveerd en jouw oplaadkabel is niet aangesloten.

### CGM instellingen

#### Waarom zegt AndroidAPS dat 'de gekozen BG bron geen optimale filtering toepast'?

Als je een andere CGM/FGM dan Dexcom G5 en G6 in xDrip Native-modus gebruikt, dan krijg je deze waarschuwing in de AndroidAPS OpenAPS-tab. Zie [Filteren van glucosewaardes](../Usage/Smoothing-Blood-Glucose-Data-in-xDrip.md) voor meer informatie.

## Pomp

### Waar moet ik mijn pomp dragen?

Er zijn talloze mogelijkheden om de pomp te dragen. Het maakt niet uit of je loop gebruikt of niet. Als je eigenlijk liever een slangloze pomp zou willen hebben, maar je hebt voor een Dana gekozen om te kunnen loopen, dan kun je ook kiezen voor een infuusset van 30cm en die gebruiken met de bijgeleverde buikband.

### Batterijen

Bij loopen kan de pompbatterij sneller leegraken dan bij normaal gebruik, omdat je telefoon veel vaker interactie heeft met de pomp dan een normale gebruiker zou hebben. We raden aan om de batterij al te vervangen als hij nog voor 25% vol is, omdat communicatie tussen telefoon en pomp dan al achteruit kan gaan. Je kunt een batterij-alarm in Nightscout instellen, door de variabele PUMP_WARN_BATT_P in te stellen. Tips om de levensduur van de batterij te verlengen:

* de tijd dat het LCD-scherm van de pomp aan staat, verkorten (in instellingen menu van de pomp)
* de tijd dat de achtergrondverlichting van het beeldscherm aan staat, verkorten (in instellingen menu van de pomp)
* stel meldingen in op geluid in plaats van trillen (in instellingen menu van de pomp)
* gebruik de knoppen van de pomp alleen bij het vullen van de pomp. Bekijk alle andere informatie op je telefoon (batterijduur, reservoir inhoud, geschiedenis etc).
* op sommige telefoons wordt AndroidAPS app vaak afgesloten om de batterij of het RAM geheugen te besparen. Elke keer dat AndroidAPS dan weer opnieuw wordt gestart, maakt je telefoon weer verbinding met de pomp om opnieuw de bolus geschiedenis en huidige basaalstand uit te lezen vanuit het pompgeheugen. Hierdoor raakt de batterij van de pomp leeg. Om te zien of dit gebeurt, ga naar Instellingen > NSClient en schakel 'Log app start naar NS' in. Hiermee zul je iedere keer dat de app herstart, een notificatie terugzien op je AAPS hoofdscherm in de glucosegrafiek, en ook in Nightscout. Wanneer je ziet dat de app vaak opnieuw gestart wordt, dan moet je dit uitzetten. Ga naar je telefooninstellingen, ergens onder energiebeheer/accuoptimalisatie moet je instellen dat de AndroidAPS app in de achtergrond mag blijven draaien en niet automatisch wordt afgesloten.
* maak de contactpunten van de batterij schoon met een alcoholdoekje, om te voorkomen dat er nog vet of olie van het productieproces is achtergebleven.
* bij DanaR/DanaRS pompen wordt er na een batterijwissel een grotere hoeveelheid stroom door de batterij gestuurd. In elke nieuwe batterij zit een inactiveringsfilm die voorkomt dat hij voor ingebruikname langzaam leeg zou lopen. De grotere hoeveelheid stroom zorgt ervoor dat de inactiveringsfilm van de batterij doorbroken wordt. Wanneer een nieuwe batterij geen 100% aangeeft nadat de pomp is opgestart, kun je 2-3 keren de batterij verwijderen en terugdoen in de pomp, of je kunt met een metalen voorwerp beide polen kort (fractie van een seconde) contact laten maken.
* bekijk meer tips over [specifieke soorten batterijen](../Usage/Accu-Chek-Combo-Tips-for-Basic-usage#battery-type-and-causes-of-short-battery-life) voor de Combo-pomp

### Verwisselen van reservoirs en canules

Wisselen van het reservoir kan niet worden gedaan via AndroidAPS maar rechtstreeks via de pomp, zoals beschreven in de handleiding van de pompfabrikant.

* Houd "Open Loop" / "Closed Loop" op het Overzicht-scherm van AndroidAPS lang ingedrukt en selecteer 'Verbreek verbinding 1u met pomp'
* Koppel nu de pomp af en verwissel het reservoir volgens de instructies van de pompfabrikant.
* Wanneer je daarmee klaar bent, koppel je de pomp weer aan en houd 'Verbinding verbroken (.. m)' lang ingedrukt. Selecteer 'Hervatten'.

Het 'Ontlucht/vul' scherm van AAPS gebruikt niet de functie van "prime infusie set" van de pomp, maar vult de infusie set en/of canule met behulp van een bolus die niet in de geschiedenis van AAPS verschijnt. Dit betekent dat een lopende tijdelijke basaalstand niet zal worden onderbroken. Selecteer op het Acties (Act) tabblad, de knop ONTLUCHT/VUL en kies de hoeveelheid insuline die nodig is om de infuusset/canule te vullen en druk op OK. Wanneer er nog lucht in de infuusset zit, herhaal de vorige stap. Je kunt standaardhoeveelheden instellen in Instellingen > Andere > Vul standaard hoeveelheid. Hoeveel eenheden nodig zijn staat in het instructieboekje in de doos met infuussets, dit verschilt per type infuusset en is afhankelijk van de lengte van de canule en de lengte van de slang.

## Hygiëne

### Wat te doen tijdens het douchen?

Je kunt de pomp afkoppelen bij het douchen. Voor deze korte tijd kun je meestal wel zonder je pomp. But you should tell it to AAPS so that the IOB calculations are right. Op het Overzicht-scherm van AAPS houd "Open loop / Closed loop" lang ingedrukt. Selecteer **'Verbreek verbinding ...min/u met pomp'** afhankelijk van jouw behoefte. Nadat je je pomp weer hebt aangesloten, dan kun je in datzelfde menu op 'Hervatten' drukken. Of wachten totdat de door jou gekozen tijd is verstreken, de loop zal dan automatisch weer worden hervat.

## Werken

Afhankelijk van het soort werk dat je doet, kun je verschillende instellingen kiezen (basaalstanden, ISF, KH factor) op werkdagen. Als AndroidAPS gebruiker kun je kiezen om een profielwissel te doen voor de duur van jouw werkdag (bijv. meer dan 100% gedurende 8 uur bij zittend werk, of juist minder dan 100% wanneer je fysiek actief werk doet). Je kunt ook kiezen voor een hoger of lager tijdelijk streefdoel, of voor een tijdverschuiving van jouw profiel wanneer je eerder of later dan normaal opstaat. Wanneer je Nightscout profielen gebruikt, kun je ook een specifiek profiel (bijv. 'thuis' of 'werkdag') aanmaken, en dagelijks het profiel activeren dat je op dat moment nodig hebt.

## Vrije tijd

## Sporten

## Sex

Je kunt de pomp loskoppelen voor wat 'vrijheid', maar je moet AAPS wel vertellen dat je dat doet. Zodat jouw IOB juist wordt berekend. Op het Overzicht-scherm van AAPS houd "Open loop / Closed loop" lang ingedrukt. Selecteer **'Verbreek verbinding ...min/u met pomp'** afhankelijk van jouw behoefte. Nadat je je pomp weer hebt aangesloten, dan kun je in datzelfde menu op 'Hervatten' drukken. Of wachten totdat de door jou gekozen tijd is verstreken, de loop zal dan automatisch weer worden hervat.

## Alcohol

Alcohol drinken in de closed loop modus heeft als risico dat het algoritme niet goed kan voorspellen welke invloed de alcohol heeft op jouw bloedglucose. Je zult voor jezelf een manier moeten vinden om hiermee om te gaan. AndroidAPS heeft verschillende functies die je hierbij kunt gebruiken:

* De closed loop uitschakelen en je diabetes handmatig onder controle houden
* Een hoger tijdelijk streefdoel instellen en onaangekondigde maaltijden (UAM, UnAnnounced Meals) uitschakelen, om te voorkomen dat je extra IOB krijgt toegediend
* een profielwissel, naar beduidend minder dan 100% 

Bij het drinken van alcohol moet je altijd je CGM in de gaten houden, om op tijd wat koolydraten te nemen en zo een hypo te kunnen voorkomen.

## Slapen

### Hoe kan ik 's nachts closed loopen zonder mobiele of WIFI straling?

Veel gebruikers zetten 's nachts hun telefoon in vliegtuigmodus. Wanneer je wilt dat de loop werkt in vliegtuigmodus, volg dan deze stappen (dit werkt alleen als je een locale BG-bron hebt zoals xDrip+ of de gepatchte Dexcom app, het werkt NIET wanneer jouw BG-waardes via Nightscout binnenkomen):

1. Zet de telefoon in vliegtuigmodus.
2. Wacht totdat de vliegtuigmodus actief is.
3. Schakel Bluetooth in.

Je kunt nu niet bellen of gebeld worden, en je bent ook niet verbonden met internet. Maar de closed loop werkt nog wel.

## Reizen

### Hoe kan ik wisselen van tijdzone?

Met DanaR en DanaR Koreaans hoef je niets te doen. Zie voor andere pompen de [wisselen van tijdzone](../Usage/Timezone-traveling.md) pagina voor meer details.

## Ziekenhuis

Wanneer je jouw behandelaar informatie wilt geven over AndroidAPS en doe-het-zelf loopen, dan kun je de [Informatie voor zorgprofessionals](../Resources/clinician-guide-to-AndroidAPS.md) uitprinten.

## Afspraak met je internist of diabetesverpleegkundige

### Rapporten

Je kunt rapporten op jouw nightscout site (https://YOUR-NS-SITE.com/report) laten weergeven of gebruik [Nightscout Reporter](https://nightscout-reporter.zreptil.de/)