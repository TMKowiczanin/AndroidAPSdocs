# Accu-Chek Insight pomp

**Deze software is onderdeel van een doe-het-zelf oplossing en is geen kant-en-klaar product, maar vraagt JOU te lezen, leren en te begrijpen hoe het systeem werkt en hoe je het kunt gebruiken. Het neemt niet je gehele diabetes management van je over, maar stelt je wel in staat om je diabetes beter onder controle te krijgen en je kwaliteit van leven te verhogen, als je bereid bent de benodigde tijd erin te investeren. Haast je niet, maar geef jezelf de tijd om te leren. Jij alleen bent verantwoordelijk voor wat je ermee doet.**

* * *

## ***WARNING:** If you have been using the Insight with **SightRemote** in the past, please **update to the newest AAPS version** and **uninstall SightRemote**.*

## Benodigde hardware en software

* Een Roche Accu-Chek Insight pomp (firmware maakt niet uit, ze werken allemaal) <br />Opmerking: AAPS zal alleen het **eerste basaal-profiel van de pomp** gebruiken.
* Een Android-telefoon (in principe werkt elke Android-versie, maar AndroidAPS zelf vereist minstens Android 5 (Lollipop).)
* The AndroidAPS app installed on your phone

## Pomp koppelen

* De Insight pomp mag aan één apparaat tegelijk gekoppeld zijn. Wanneer je de afstandsbediening (meter) eerder hebt gebruikt, moet je de meter verwijderen uit de lijst van gekoppelde apparaten in jouw pomp: Menu > Instellingen > Communicatie> Apparaat verwijderen > Meter
    
    ![Screenshot van Insight Verwijderen Meter](../images/Insight_RemoveMeter.png)

* In de [Configurator](../Configuration/Config-Builder) van AndroidAPS: selecteer Accu-Chek Insight in de pomp sectie
    
    ![Screenshot van Insight Config Builder](../images/Insight_ConfigBuilder.png)

* Tik op het tandwiel-icoon naast Insight om de instellingen te openen.

* In de instellingen: tik op de knop 'Insight koppelen' bovenaan het scherm. Als het goed is zie je nu een lijst van alle nabijgelegen bluetooth apparaten (links onder).
* Op de Insight pomp, ga naar Menu > Instellingen > Communicatie > Apparaat toevoegen. De pomp zal het volgende scherm (rechts onder) weergeven met het serienummer van de pomp.
    
    ![Screenshot van Insight Pairing 1](../images/Insight_Pairing1.png)

* Ga terug naar je telefoon, tik op het pomp serienummer in de lijst van bluetooth apparaten. Tik vervolgens op Koppelen om te bevestigen.
    
    ![Screenshot van Insight Pairing 2](../images/Insight_Pairing2.png)

* Zowel op je pomp als op je telefoon zal vervolgens een code verschijnen. Controleer of de codes op beide apparaten hetzelfde zijn en bevestig op zowel pomp als telefoon.
    
    ![Screenshot van Insight Pairing 3](../images/Insight_Pairing3.png)

* Succes! Geef jezelf een schouderklopje voor het succesvol koppelen van je pomp met AndroidAPS.
    
    ![Screenshot van Insight Pairing 4](../images/Insight_Pairing4.png)

* Om te controleren of alles goed is gegaan, ga je terug naar de Configurator in AndroidAPS en tik op het tandwiel-icoontje bij de Insight pomp om in de Insight-instellingen te komen. Tik vervolgens op Insight Pairing en je zult wat informatie te zien krijgen over de pomp:
    
    ![Screenshot van Insight Pairing Informatie](../images/Insight_PairingInformation.png)

Opmerking: Er zal geen permanente verbinding zijn tussen pomp en telefoon. Een verbinding zal alleen tot stand worden gebracht als dat nodig is (d.w.z. instellen van tijdelijke basaalstand, bolus geven, pomp geschiedenis uitlezen...). Anders zouden de batterij van telefoon en pomp te snel leeglopen.

## Instellingen in AAPS

![Screenshot van Insight Settings](../images/Insight_pairing.png)

In de Insight-instellingen in AndroidAPS kun je de volgende opties inschakelen:

* "Infuuswissel noteren": Dit zal automatisch een insuline ampul wissel noteren in AndroidAPS wanneer je het "vul canule" programma op de pomp gebruikt.  
    <font color="red">Opmerking: Een canule wissel reset ook Autosens</b></font>
* "Slangwissel noteren": Dit voegt een notitie toe aan de AndroidAPS database wanneer je het "infusieset vullen" programma op de pomp gebruikt.
* "Batterijwissel noteren": Dit voegt een notitie toe aan AndroidAPS wanneer je een nieuwe batterij in de pomp plaatst.
* "Werkingsmodus-wissel noteren": Hiermee voegt je een notitie toe in de AndroidAPS database wanneer je de pomp start, stopt of pauzeert.
* "Alarm noteren": Dit maakt een notitie in AndroidAPS wanneer de pomp een alarm geeft (behalve herinneringen, bolus en tijdelijke basaalstand annulering - deze worden niet geregistreerd).
* "TBR-emulatie inschakelen": De Insight pump kan alleen tijdelijke basaalstanden (TBRs) instellen tot maximaal 250%. Om deze beperking te omzeilen, zal TBR-emulatie ervoor zorgen dat de pomp een vertraagde bolus gebruikt als je een TBR van meer dan 250% nodig hebt.  
    <font color="red">Opmerking: gebruik slechts één vertraagde bolus tegelijkertijd omdat meerdere vertraagde bolussen tegelijkertijd, fouten kunnen veroorzaken.</font>
* "Herstel duur": Dit definieert hoe lang AndroidAPS zal wachten na een mislukte verbindingspoging voordat hij het opnieuw probeert. Je kunt een getal kiezen van 0 tot 20 seconden. Als je verbindingsproblemen ondervindt, kies je een langere wachttijd.   
      
    Voorbeeld voor min. herstel duur = 5 en max. herstel duur = 20   
      
    geen verbinding -> wacht **5** sec.   
    probeer opnieuw -> geen verbinding -> wacht **6** sec.   
    probeer opnieuw -> geen verbinding -> wacht **7** sec.   
    probeer opnieuw -> geen verbinding -> wacht **8** sec.   
    ...   
    probeer opnieuw -> geen verbinding -> wacht **20** sec.   
    probeer opnieuw -> geen verbinding -> wacht **20** sec.   
    ...

* "Verbindingsvertraging ": Dit bepaalt hoe lang (in seconden) AndroidAPS zal wachten met het verbreken van de pompverbinding nadat een opdracht is uitgevoerd. Standaard waarde is 5 seconden.

Voor perioden waarin de pomp gestopt is geweest, zal AAPS een tijdelijke basaalstand noteren van 0%.

In AndroidAPS toont het Accu-Chek Insight tabblad de huidige status van de pomp. Er zijn hier twee knoppen:

* "Vernieuw": Vernieuwt de pomp status
* "Activeer/deactiveer melding van TBR einde": Een Insight pomp is standaard ingesteld om een alarm af te geven wanneer een TBR (tijdelijke basaalstand) eindigt. Met deze knop kun je dit alarm activeren of deactiveren zonder dat je hiervoor speciale Accucheck configuratie-software nodig hebt.
    
    ![Screenshot van Insight Status](../images/Insight_Status2.png)

## Instellingen in de pomp

Configureer alarmen in de pomp als volgt:

* Menu > Instellingen > Apparaat-instellingen > Instellingen modus > Zacht > Signaal > Geluid Menu > Instellingen > Apparaatinstellingen > Instellingen modus > Zacht > Volume > 0 (verwijder alle balken)
* Menu > Modi > Signaalmodus > Zacht

Met deze instellingen gaan alle alarmen vanuit de pomp af in stilte. AndroidAPS krijgt de alarmen wel binnen, en beslist vervolgens of een alarm relevant voor jou is. Niet-relevante alarmen worden bevestigd in de pomp door AndroidAPS, hiervan zul jij dus niks merken. Wel-relevante alarmen worden door AndroidAPS niet bevestigd, waarna het volume van het alarm zal toenemen (eerst piepen, dan trillen) en jij als gebruiker het alarm moet bevestigen.

Insight pompen met nieuwere firmware zullen kort trillen wanneer een bolus wordt afgeleverd (bijvoorbeeld wanneer AndroidAPS een SMB afgeeft of wanneer AndroidAPS een vertraagde bolus afgeeft om een hoge tijdelijke basaalstand te simuleren). Dit trilalarm kan niet worden uitgeschakeld. Oudere pompen zullen hierbij niet trillen.

## Batterij vervangen

De Insight pomp heeft een kleine interne batterij om essentiële functies zoals de interne klok, te kunnen laten doorgaan terwijl jij de batterij verwisselt. Als het wisselen van de batterij te lang duurt, kan deze interne batterij leegraken. Dan wordt de interne klok gereset en wordt je gevraagd een nieuwe tijd en datum in te voeren nadat je een nieuwe batterij in de pomp hebt gedaan. Als dit gebeurt, zullen alle behandelingen in AndroidAPS voorafgaand aan de batterijwissel niet meer in berekeningen (zoals COB, IOB) worden opgenomen, omdat de juiste tijd niet kan worden vastgesteld.

## Insight specifieke foutmeldingen

### Vertraagde bolus

Gebruik slechts één vertraagde bolus tegelijk, omdat meerdere uitgebreide bolussen tegelijkertijd fouten kunnen veroorzaken.

### Time-out

Soms kan het gebeuren dat de Insight niet antwoordt wanneer AndroidAPS probeert te verbinden met je pomp. In dat geval zal AAPS het volgende bericht weergeven: "Time-out tijdens verbinden - reset bluetooth".

![Insight Reset Bluetooth](../images/Insight_ResetBT.png)

Om dit op te lossen, schakel je bluetooth uit op je pomp EN op je telefoon gedurende ongeveer 10 seconden. Zet bluetooth daarna weer aan op je pomp en telefoon.

## Wisselen van tijdzone met de Insight

Lees alles over reizen in verschillende tijdzones op de pagina [Wisselen van tijdzone](../Usage/Timezone-traveling#insight).