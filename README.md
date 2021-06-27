# Home Assistant irrigation using Gardena water distributor


This is my project for garden irrigation using Home assistant. As an alternative to a complex and expansive set of valves and controllers using OpenSprinkler for example, I found an alternative using the [Gardena water distributor](https://www.gardena.com/int/products/watering/water-controls/water-distributor-automatic/966749301/). This device enables me to control up to 6 zones. It is pure mechanical and will switch to the next zone as soon as the water pressure stops. Controlling the device means you have to start/stop the water pressure at a certain sequence. 

I was inspired when I saw that Gardena offers a [timer controler ](https://www.gardena.com/int/products/watering/water-controls/water-control-master/967927801/) that is able to automtically select a zone on the water distributor. I wondered how it works bought the Gardena water distributor and started experimenting with it. Now I can use Home Assistant to control the water distributor and fully automate the irrigation over 6 zones in my garden.

![Gardena water distributor](https://hqvcdn3.azureedge.net/qs_mh=530&mw=850&ver=20210615T082014&hcsh=8CBABCC416FFFA2763FDEFC4FD51204C/_$$_/media/aprimo/gardena/water%20controls/photos/studio/ga210-00xxxx/ga210-0007b.png)

Alhought it would be woth creating an full integration, I just created a couple of automations in the first place. (maybe someone can help me with that later on) The automations use a switch control water supply. I my case this is done by switching on/off a pump for water supply. NOTE: Gardena does not recommend using a hydrophore pump for the water distributor, because is is a mechanical device that could break if the water is not clean. However, I mounted a water filter in front of the device and decided to take te risk. You could alternative switch on/off the regular water supply using a single valve. There are many alternatives for this like a [Zwave valve](https://www.amazon.com/Automation-Z-Wave-Shutoff-Compatiable-Smartthings/dp/B083DNGQRZ/ref=sr_1_5?dchild=1&keywords=zwave+water+valve&qid=1624622632&sr=8-5) or even a [simple Gardena controller](https://www.gardena.com/int/products/smart/smart-system/smart-water-control-set/967048901/)

The Gardena water distributor is pure mechanical and does not return any status. The Gardena controller apparantly depends on reliable water pressure to keep in sync with the water distrinutor. I decided add a water sensor in zone 1, so there is a means of detecting the current water zone of the distributor. This is handled by the Gardena Calibration automation. It will switch on/off the water pressure until it detects water and then resets the current zone information. When all available zones have been tested this way and no water is detected something might be wrong with the water supply or with the distributor.

Another automation (select and play) selects the desire zone and opens the water supply for a desired time. Zone and time can be defined in the UI by some helpers. Finally for each zone can be created a script that sets the desired zone and time and fires the select and play automation. This enables to create some sort of definition per zone. I used the great [scheduler-component](https://github.com/nielsfaber/scheduler-component) to easily create a schedule for each zone.

![UI selecting zone](https://raw.githubusercontent.com/pdwonline/gardena-water-distributor/main/Gardena_2.png) ![UI selecting zone](https://raw.githubusercontent.com/pdwonline/gardena-water-distributor/main/Gardena_1.png)
![UI configuration](https://raw.githubusercontent.com/pdwonline/gardena-water-distributor/main/Gardena_instellingen.png)

In order to share this project, I am creating blueprints for the automations. Updated soon..

## Dependencies:
- switch to switch on/off the water pressure
- flood sensor to sense water on zone 1
- rain sensor (I used a template based on buienalarm to emulate this)
- [Hass variables custom integration](https://github.com/Wibias/hass-variables) for persistant variables

Helpers for: 
- zone selection, timer value
- number of zones, water pressure on delay and dry time for zone 1.

For the UI, I used some extentions (but you could also do without it):
- fold_entity_row for uncluttering the UI
- Numberbox for easier number selection
- Secondaryinfo Entity Row for adding secondary_info to some controls

