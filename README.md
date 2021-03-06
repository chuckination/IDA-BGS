# IDA-BGS
An EDMC plugin that gathers system/faction data for specific systems and sends JSON formatted data to webapi

## Version  
Version 0.66  

## What it does:  
Whenever a user jumps from one system to another, upon landing in the destination system, an event is created in the ED journal file.  
Whenever a user docks at a station, another event is created in the ED journal file.  
This plugin reads these events (FSDjump and Docked), and ONLY these events, gathers system/station/faction data, and pushes JSON formatted data to the [IDA-BGS API](https://github.com/ZTiKnl/IDA-BGS-API).  
Data sent to the API can be reported in a Discord channel by the [IDA-BGS Bot](https://github.com/ZTiKnl/IDA-BGS-Bot)  

## What else can it do:  
Whenever a user completes a mission, sells exploration data, cashes in a bounty or delivers cargo (market), an event is created in the ED journal file.  
If enabled, this plugin reads these events, gathers related data, and pushes JSON formatted data to the [IDA-BGS API](https://github.com/ZTiKnl/IDA-BGS-API).  
This is an *optional* feature, OPT-IN, which means users do not participate, unless they manually place a checkmark in the settings tab.  

## How to use:  
1. Clone the repo to the EDMC plugin folder, or download and unzip to the EDMC plugin folder  
   (default: `c:\Users\%USERNAME%\AppData\Local\EDMarketConnector\plugins`)  
2. Request API key on webinterface  
3. Start up EDMC  
4. Insert API key into plugin by going to File -> Settings, tab IDA-BGS, enter/paste the key, and hit OK  
5. Optional: add checkmark to approve additional data packages  

There is an extra row in the main window of EDMC, labeled IDA-BGS.  
This row can have 5 different values:  
- `Idle`  
  Not doing anything, waiting for any event to be triggered  

- `Success: BGS/INF/EXPL/BNT/DLVR data n/a`  
  Just processed FSDjump event, but destination system does not contain our faction  
  Just processed MissionCompleted event, but the target and recipient are not our faction  

- `Success: BGS/INF/EXPL/BNT/DLVR data sent`  
  Just processed FSDjump event, our faction is present here, data sent without errors  
  Just processed MissionCompleted event, mission is for or from our faction, data sent without errors  

- `Success: API not ready`  
  The API received data, but isnt ready yet to process it, please wait until I built that functionality  

- `Fail: error code - short error message`  
  could be many things, the error code and short error message will be a hint/clue  
  The full error message can be found in EDMC log file, usually located in `%TMP%/EDMarketConnector.log`  

## Changes to make for use by another faction
Want to make this work for another faction, all you need to change here are 2 instances of 'IDA-BGS' and 2 instances of the server url to push data to `https://ida-bgs.ztik.nl/api.php`  
One more change will be required for the webapi, which does the filtering of systems where the faction has a presence or not

## Disclaimer
This plugin is still under construction, ~~bugs~~ new features WILL appear unexpectedly.  
Patches are always welcome.  

## Thanks
- Everybody who helped test the EDMC Plugin  
  (devnull, Optimus Stan)  
- HammerPiano, wouldnt have gotten the plugin working so fast without your advice  
- [EliteBGS Tick Bot](https://EliteBGS.app)  
- Everyone at EDCD: Community Developers Discord channel  
  (Phelbore, Athanasius, Gazelle, tez,  Garud,  T'kael, VerticalBlank, anyone else I missed?)