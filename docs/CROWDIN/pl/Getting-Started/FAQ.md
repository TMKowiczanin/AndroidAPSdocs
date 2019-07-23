# FAQ for loopers


Jak dodawać pytania do FAQ: Instruckję znajdziesz [tutaj](../make-a-PR.md)
## General

### Can I just download the AndroidAPS installation file?
### Czy mogę sciągnąć instalator AndroidAPS?
Nie. Nie został przygotowany plik instalacyjny dla aplikacji AndroidAPS. Aplikację musisz [zbudować](../Installing-AndroidAPS/Building-APK.md) samodzielnie. Powód takiej decyzji jest następujący:

Aplikacja AndroidAPS jest wykorzystywana do kontroli Twojej pompy insulinowej i kontrolowania dawkowania insuliny. Zgodnie z obecnymi przepisami w Europie systemy medyczne klasy IIa lub IIb wymagają odpowiedniej certyfikacji  poprzedzonej badaniami. Dystrybucja urządzeń tego typu bez odpowiednich certyfikatów jest nielegalna. Podobne regulacje obowiązują w pozostałych częściach świata. 

Regulacje te nie są ograniczone tylko do sprzedaży ale także do każdego sposobu ich dystrybucji (także rozpowszechniania za darmo).
Tworzenie urządzeń medycznych na własny użytek to jedyny sposób na to, by było to legalne.

Jest to powód, dla którego aplikacja nie jest dostępna.


### Jak zacząć?
Na początku potrzebny będzie **sprzęt dający się zapętlić**:


* [Obsługiwane pompy](Pump-Choices.md), 
* [Smartpjony z Androidem](Phones.md) (Apple iOS nie jest obsługiwany przez AndroidAPS - możesz sprawdzić  [Pętle na iOS](https://loopkit.github.io/loopdocs/)) oraz
* [system ciągłego monitorowania gligemi](../Configuration/BG-Source.md). 

Po drugie, musisz **skonfigurować twój sprzęt **. Zapoznaj się z  [przykładową konfiguracją krok po korku](Sample-Setup.md).

Po trzecie, musisz **skonfigurować twoje oprogramowanie**: AndroidAPS oraz sygnały CGM/FGM .

Fourthly, you have to learn and **understand the OpenAPS reference design to check your treatment factors**. The founding principle of closed looping is that your basal rate and carb ratio are accurate. All recommendations assume that your basal needs are met and any peaks or troughs you're seeing are a result of other factors which therefore require some one off adjustments (exercise, stress etc). The adjustments the closed loop can make for safety have been limited (see maximum allowed temporary basal rate in [OpenAPS Reference Design](https://openaps.org/reference-design/)), which means that you don't want to waste the allowed dosing on correcting a wrong underlying basal. If for example you are frequently low temping on the approach of a meal then it is likely your basal needs adjusting. You can use [autotune](http://openaps.readthedocs.io/en/latest/docs/Customize-Iterate/autotune.html#phase-c-running-autotune-for-suggested-adjustments-without-an-openaps-rig) to consider a large pool of data to suggest whether and how basals and/or ISF need to be adjusted, and also whether carb ratio needs to be changed. Or you can test and set your basal the [old fashioned way](http://integrateddiabetes.com/basal-testing/).

### What practicalities of looping do I have?

* If you don't want your preferences to be easily changed then you can password protect the preferences menu by selecting in the preferences menu "password for settings" and type the password you choose. The next time you go into preferences menu it will ask for that password before going any further. If you later want to remove the password option then go into "password for settings" and delete the text.

* If you plan to use the android wear app to bolus or change settings then you need to ensure notifications from AndroidAPS are not blocked. Confirmation of action comes via notification.

* If you take your pump off for showering/bathing/swimming/sport etc then press and hold on the "Open Loop"/"Closed Loop" text on the main homepage and select "disconnect for..." however many hours you plan to disconnect for. This will set your basal to zero for that time period. The minimum length of time for a disconnection is due to the minimum length of TBRs that can be set on the pump so if you wish to disconnect for a shorter period of time, or you connect your pump sooner than expected then press and hold "Suspended (X mins)" and select "Resume". Your IOB will then be accurate for calculations on your return to the pump.

* For safety, recommendations made are based on not one CGM reading but the average delta. Therefore if you miss some readings it may take a while after getting data back before AndroidAPS kicks in looping again.

* There are several blogs with good tips to help you understand the practicalities of looping:
  
  * [Fine-tuning Settings](http://seemycgm.com/2017/10/29/fine-tuning-settings/) See my CGM
  * [Why DIA matters](http://seemycgm.com/2017/08/09/why-dia-matters/) See my CGM
  * [Limiting meal spikes](https://diyps.org/2016/07/11/picture-this-how-to-do-eating-soon-mode/) #DIYPS
  * [Hormones and autosens](http://seemycgm.com/2017/06/06/hormones-2/) See my CGM

### What emergency equipment is recommended to take with me?

First of all, you have to take the same emergency equipment with you like every other T1D with insulin pump therapy. As looping with AndroidAPS, it is strongly recommended to have the following additional equipment with or near to you:

* Accu pack for the energy of your smartphone, wear and (maybe) BT reader
* Backup in the cloud (Dropbox, Google Drive...) of the apps you use like: your latest AndroidAPS-APK and your key store password, AndroidAPS settings file, xDrip settings file, patched Dexcom app, ...
* Pump batteries

### How to safely attach the CGM/FGM?

You can tape it: There are getting sold pre-perforated 'overpatches' for common CGM systems (ask google or ebay). Some loopers use the cheaper standard kinesiotape or rocktape.

You can fix it: There are getting sold upper arm braclets that fix the CGM/FGM with a rubber band (ask google or ebay).

## AndroidAPS settings

### Impact of settings

This table aims to help you optimise settings. It may be best to start at the top and work to the bottom. Aim to get one setting right before changing another. Work in small steps rather than making large changes at once. You can use [Autotune](https://autotuneweb.azurewebsites.net/) to guide your thinking, although it should not be followed blindly: it may not work well for you or in all circumstances. Note that settings interact with one another - you can have 'wrong' settings that work well together in some circumstances (eg if a too-high basal happens to be at the same time as a too-high CR) but do not in others. This means that you need to consider all the settings and check they work together in a variety of circumstances.<table class="tg" border=1> 

<th class="tg-0pky">
  Setting
</th>

<th class="tg-0pky">
  Description & testing
</th>

<th class="tg-0pky">
  Impact
</th>

<td class="tg-0pky">
  Duration of insulin activity (DIA)
</td>

<td class="tg-0pky">
  The length of time that insulin decays to zero.<br /><br />This is quite often set too short. Most people will want at least 5 hours, potentially 6 or 7.
</td>

<td class="tg-0pky">
  Too short DIA can lead to low BGs. And vice-versa.<br /><br />If DIA is too short, AAPS thinks too early that your previous bolus is all consumed, and, at still elevated glucose, will give you more. (Actually, it does not wait that long, but predicts what would happen, and keeps adding insulin). This essentially creates ‘insulin stacking’ that AAPS is unaware of.<br /><br />Example of a too-short DIA is a high BG followed by AAPS over-correcting and giving a low BG.
</td>

<td class="tg-0pky">
  Basal rate schedule (U/hr)
</td>

<td class="tg-0pky">
  The amount of insulin in a given hour time block to maintain BG at a stable level.<br /><br />Test your basal rates by suspending loop, fasting, waiting for say 5 hours after food, and seeing how BG changes. Repeat a few times.<br /><br />If BG is dropping, basal rate is too high. And vice-versa.
</td>

<td class="tg-0pky">
  Too high basal rate can lead to low BGs. And vice-versa.<br /><br />AAPS ‘baselines’ against the default basal rate. If basal rate is too high, a ‘zero temp’ will count as a bigger negative IOB than it should. This will lead to AAPS giving more subsequent corrections than it should to bring IOB ultimately to zero.<br /><br />So a basal rate too high will create low BGs both with the default rate, but also some hours hence as AAPS corrects to target.<br /><br />Conversely a basal rate too low can lead to high BGs, and a failure to bring levels down to target.
</td>

<td class="tg-0pky">
  Insulin sensitivity factor (ISF) (mmol/l/U or mg/dl/U)
</td>

<td class="tg-0pky">
  The drop in BG expected from dosing 1U of insulin.<br /><br />Assuming correct basal, you can test this by suspending loop, checking IOB is zero, and taking a few glucose tablets to get to a stable ‘high’ level.<br /><br />Then take an estimated amount of insulin (as per current 1/ISF) to get to your target BG.<br /><br />Be careful as this is quite often set too low. Too low means 1 U will drop BG faster than expected.
</td>

<td class="tg-0pky">
  Lower ISF = a smaller drop in BGs for each unit of insulin (also can be called ‘more severe / aggressive’ or ‘stronger’). If too low, this can lead to low BGs.<br /><br />Higher ISF = a bigger drop in BGs for each unit of insulin (also can be called ‘less severe / aggressive’ or ‘weaker’). If too high, this can lead to high BGs.<br /><br />An ISF that is too low (not uncommon) can result in ‘over corrections’, because AAPS thinks it needs more insulin to correct a high BG than it actually does. This can lead to ‘roller coaster’ BGs (esp when fasting). In this circumstance you need to increase your ISF. This will mean AAPS gives smaller correction doses, and this will avoid over-correcting a high BG resulting in a low BG.<br /><br />Conversely, an ISF set too high can result in under-corrections, meaning your BG remains above target – particularly noticeable overnight.
</td>

<td class="tg-0pky">
  Carbohydrate to insulin ratio (CR) (g/U)
</td>

<td class="tg-0pky">
  The grams of carbohydrate for each unit of insulin.<br /><br />Assuming correct basal, you can test by checking IOB is zero and that you are in-range, eating exactly known carbs, and take an estimated amount of insulin based on current 1/CR. Best is to eat food your normally eat at that time of day and count its carbs precicely.
</td>

<td class="tg-0pky">
  Lower CR = less food per unit, ie you are getting more insulin for a fixed amount of carbs. Can also be called ‘more aggressive’.<br /><br />Higher CR = more food per unit, ie you are getting less insulin for a fixed amount of carbs. Can also be called ‘less aggressive’.<br /><br />If after meal has digested and IOB has returned to zero, your BG remains higher than before food, chances are CR is too large. Conversely if your BG is lower than before food, CR is too small.
</td></table> 

### APS algorithm

#### Why does it show "dia:3" in the "OPENAPS AMA"-tab even though I have a different DIA in my profile?

![AMA 3h](../../images/Screenshot_AMA3h.png) In AMA, DIA actually doesn't mean the 'duration of insulin acting'. It is a parameter, which used to connected to the DIA. Now, it means, 'in whích time should the correction be finished'. It has nothing to do with the calculation of the IOB. In OpenAPS SMB, there is no need for this parameter anymore.

### Profile

#### Why using min. 5h DIA (insulin end time) instead of 2-3h?

Well explained in [this article](http://www.diabettech.com/insulin/why-we-are-regularly-wrong-in-the-duration-of-insulin-action-dia-times-we-use-and-why-it-matters/). Don't forget to `ACTIVATE PROFILE` after changing your DIA.

#### What causes the loop to frequently lower my BG to hypoglycemic values without COB?

First of all, check your basal rate and make a no-carb basal rate test. If it is correct, this behaviour is typically caused by a too low ISF. A too low ISF looks typically like this:

![ISF too low](../images/isf.jpg)

#### What causes high postprandial preaks in closed loop?

First of all, check your basal rate and make a no-carb basal rate test. If it is correct and your BG is falling to your target after carbs are fully absorbed, try to set an 'eating soon' temp target in AndroidAPS some time before the meal or think about an appropriate prebolus time with your endocrinologist. If your BG is too high after the meal and still too high after carbs are fully absorbed, think about decreasing your IC with your endocrinologist. If your BG is too high while COB and too low after carbs are fully absorbed, think about increasing your IC and an appropriate prebolus time with your endocrinologist.

## Other settings

### Nightscout settings

#### AndroidAPS NSClient says 'not allowed' and does not upload data. What can I do?

In NSClient check 'Connection settings'. Maybe you actually are not in an allowed WLAN or you have activated 'Only if charging' and your charging cable is not attached.

### CGM settings

#### Why does AndroidAPS say 'BG source doesn't support advanced filtering'?

If you do use another CGM/FGM than Dexcom G5 or G6 in xDrip native mode, you'll get this alert in AndroidAPS openAPS-tab. See [Smoothing blood glucose data](../Usage/Smoothing-Blood-Glucose-Data-in-xDrip.md) for more details.

## Pump

### Where to place the pump?

There are innumerable possibilities to place the pump. It does not matter if you are looping or not. If you rather would have a tubeless insulin pump and have a Dana for looping, check the 30cm catheter with the original belly belt.

### Batteries

Looping can reduce the pump battery faster than normal use because the system interacts through bluetooth far more than a manual user does. It is best to change battery at 25% as communication becomes challenging then. You can set warning alarms for pump battery by using the PUMP_WARN_BATT_P variable in your nightscout site. Tricks to increase battery life include:

* reduce the length of time the LCD stays on (within pump settings menu)
* reduce the length of time the backlight stays on (within pump settings menu)
* select notification settings to a beep rather than vibrate (within pump settings menu)
* only press the buttons on the pump to reload, use AndroidAPS to view all history, battery level and reservoir volume.
* AndroidAPS app may often be closed to save energy or free RAM on some phones. When AndroidAPS is reinitialized at each startup it establishes a Bluetooth connection to the pump, and re-reads the current basal rate and bolus history. This consumes battery. To see if this is happening, go to Preferences > NSClient and enable 'Log app start to NS'. Nightscout will receive an event at every restart of AndroidAPS, which makes it easy to track the issue. To reduce this happening, whitelist AndroidAPS app in the phone battery settings to stop the app power monitor closing it down.
* clean battery terminals with alcohol wipe to ensure no manufacturing wax/grease remains.
* for DanaR/RS pumps the startup procedure draws a high current across the battery to purposefully break the passivation film (prevents loss of energy whilst in storage) but it doesn't always work to break it 100%. Either remove and reinsert battery 2-3 times until it does show 100% on screen, or use battery key to briefly short circuit battery before insertion by applying to both terminals for a split second.
* see also more tips for [particular types of battery](../Usage/Accu-Chek-Combo-Tips-for-Basic-usage#battery-type-and-causes-of-short-battery-life)

### Changing reservoirs and canulas

The change of cartridge can not be done via AndroidAPS, but must be carried out as before directly via the pump.

* Long press on "Open Loop"/"Closed Loop" on the Home tab of AndroidAAPS and select 'Suspend Loop for 1h'
* Now disconnect the pump, and change the reservoir as per pump instructions.
* Once reconnected to the pump continue the loop by long pressing on 'Suspended (X m)'.

The change of a canula however does not use the "prime infusion set" function of the pump, but fills the infusion set and/or canula using a bolus which does not appear in the bolus history. This means it does not interrupt a currently running temporary basal rate. On the Actions (Act) tab, use the PRIME/FILL button to set the amount of insulin needed to fill the infusion set and start the priming. If the amount is not enough, repeat filling. You can set default amount buttons in the Preferences > Other > Fill/Prime standard insulin amounts. See the instruction booklet in your canula box for how many units should be primed depending on needle length and tubing length.

## Hygiene

### What to do when taking a shower or bath?

You can remove the pump while taking a shower or bath. For this short period of time you'll usually won't need it. But you should tell it to AAPS so that the IOB calculations are right. Push on the light blue field 'Open loop / Closed loop' on top of the homescreen. Select **'Disconnect pump for XY min'** depending on the estimated time. Once you have been reconnected your pump you can select 'Continue' in the same field or just wait until the chosen time of disconnection is over. The loop will continue automatically.

## Working

Depending on the kind of your job, maybe you use different treatment factors on workdays. As a looper you should think of a profile switch for your estimated working day (e.g. more than 100% for 8h when sitting around or less than 100% when you are active), a high or low temporary target or a time shift of your profile when standing up much earlier or later than regular. If you are using Nightscout profiles, you can also create a second profile (e.g. 'home' and 'workday') and do a daily profile switch to the profile you actually need.

## Leasure activities

## Sports

## Sex

You can remove the pump to be 'free', but you should tell it to AAPS so that the IOB calculations are right. Push on the light blue field 'Open loop / Closed loop' on top of the homescreen. Select **'Disconnect pump for XY min'** depending on the estimated time. Once you have been reconnected your pump you can select 'Continue' in the same field or just wait until the chosen time of disconnection is over. The loop will continue automatically.

## Drinking alcohol

Drinking alcohol is risky in closed loop mode as the algorythm cannot predict the alcohol influenced BG correctly. You have to check out your own method for treating this using the following functions in AndroidAPS:

* Deactivating closed loop mode and treating the diabetes manually or
* setting high temp targets and deactivating UAM to avoid the loop increasing IOB due to an unattended meal or
* do a profile switch to noticeably less than 100% 

When drinking alcohol you always have to have an eye on your CGM to manually avoid a hypoglycemia by eating carbs.

## Sleeping

### How can I loop during the night without mobile and WIFI radiation?

Many users turn the phone into airplane mode at night. If you want the loop to support you when you are sleeping, proceed as follows (this will only work with a local BG-source such as xDrip+ or patched Dexcom app, it will NOT work if you get the BG-readings via nightscout):

1. Turn on airplane mode in your mobile.
2. Wait until the airplane mode is active.
3. Turn on Bluetooth.

You are not receiving calls now, nor are you connected to the internet. But the loop is still running.

## Travelling

### How to deal with timezone changes?

With DanaR and DanaR Korean you don't have to do anything. For other pumps see [timezone travelling](../Usage/Timezone-traveling.md) page for more details.

## Hospitalization

If you want to share some information about AndroidAPS and DIY looping with your clinicians, you can print out the [guide to AndroidAPS for clinicians](../Resources/clinician-guide-to-AndroidAPS.md).

## Medical appointment with your endocrinologist

### Reporting

You can either show your nightscout reports (https://YOUR-NS-SITE.com/report) or check [Nightscout Reporter](https://nightscout-reporter.zreptil.de/)
