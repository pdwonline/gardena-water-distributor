#Lawn sprinkler and microdrip using Gardena water distributor and Home Assistant

As an alternative to complex and expansive valve systems to automate the irrigation of my garden, I found the Gardena water distributor

This device enables me to controll up to 6 zones. Gardena offers a timer controler to automate the process, but you can do it simpler: using Home Assistant to controll the Gardena water distributor!

The distributor will switch as soon as the water pressure stops. Controlling the device means you have to start/stop the water pressure at a certain sequence. This is what the Gardena controler does.

I emulated this in a couple of automations. the automation uses a switch in my case to switch on/off a pump for water supply. But you could also use a valve to open/close the water supply. (Gardena also has a smart controller with only the on/off function available for this)

Since the Gardena water distributor is pure mechanical and it does not return any status, I modified a water sensor (standard flood sensor) to sense if there is water in zone 1 f it is selected. This enables me to kalibrate the system so it will detect when it is on zone 1 and then counts on to the correct zone.

I did'nt create a complete integration yet (maybe someone can help me with that), but is consists of a couple of automations and some helpers.

Depends on:

switch to switch on/off the water pressure
flood sensor to sense water on zone 1
Helpers for: zone selection, timer value, number of zones, water pressure on delay and dry time for zone 1.
Hass variables custom integration
For the UI, I used some extentions (but you could also do without it):

fold_entity_row for uncluttering the UI
Numberbox for easier number selection
Secondaryinfo Entity Row for adding secondary_info to some controls
gardena_kalibartion This automation will perform a fully automatic calibration. It requires the water sensor connected to zone 1 and used a helper to configure how many zones are enabled on your Gardene water distributor. It will set a persistant variable to indicate the current zone of the distributor.
