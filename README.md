# Supplemental Material

 __Supplemental Material for Submission:__

## "DroneWorld - A Platform for Simulating and Validating Mission-Critical Behavior of Small Unmanned Aerial Systems in Real-World Scenarios"

Flight-time failures of Small Unmanned Aerial Systems (sUAS) can have harmful impacts on people or the environment. It is, therefore, imperative to evaluate the ability of sUAS to operate safely within real-world scenarios including poor weather conditions, non-ideal lighting, wireless interference, loss of satellite connections, and congestion from other air traffic. This typically involves extensive simulations using high-fidelity simulation environments, as well as  performing tests with physical hardware to assess the suitability of the sUAS for the task at hand. However, while current sUAS simulation environments are equipped with sophisticated physics engines and mission execution capabilities, they provide limited support for validating the safe and correct behavior of sUAS in diverse environmental contexts and exhibit a rather ad-hoc-like, trial and error testing approach lacking a test harness that supports the structured planning, execution, and validation of acceptance tests for sUAS scenarios in realistic real-world environments. 
We address this challenge by presenting DroneWorld, a testing and simulation platform that allows sUAS developers to build diverse operating contexts, specify safety properties, and deploy their own sUAS systems in a high-fidelity 3D simulation environment.


### Data Sources:

- Collected SuAS incidents, news reports, etc.: [spreadsheet](data/report_overview.xls)

### Evaluation Data:

#### Use Case 1 - Video Collection at Pitch and Range:
For the first use case, we need to deploy two Hexacopters and a fixed wing drone at a test location of an active airbase with air traffic in close vicinity.

#### Use Case 2  - Emergency Response Demo:
For our second case, we deployed four Hexacopter sUAS in support of a live search-and-rescue demonstration at a beach area in collaboration with emergency responders and lifeguards.

| Test ID 	| Description                                                                                                                      	| Test Property Config                                    	| Environment Config                                    	|   	|
|---------	|----------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------------------	|-------------------------------------------------------	|---	|
| C1.1   	| The lateral distance must be maintained between all inflight sUAS at all times. <br> _Validation:_ ``Distance sUAS1(lat,lon) sUAS2(lat,lon) ALWAYS > 20 meters (for each pair of sUAS in air)``.  | [test_config_1.1.json](/data/eval/test_config_1.1.json) 	| [env_config_1.1.json](/data/eval/env_config_1.1.json) 	|   	|
| C1.2    	| The sUAS must not fly over no-fly zones including active taxiways or runways or areas designated as “actor” zones. <br> _Validation:_ ``sUAS location in the environment (lat,long, alt) ∩ No-Fly Zones (lat, long, alt) = φ`` 	| [test_config_1.2.json](/data/eval/test_config_1.2.json) 	| [env_config_1.2.json](/data/eval/env_config_1.2.json) 	|   	|
| C1.3    	| Any sUAS takeoff needs to be immediately aborted when the launch pad is not clear (e.g., humans or birds in the vicinity).<br> _Validation:_ ``Human Command = Abort IF (Mode(sUAS1)=Takeoff AND TargetPos =(lat=sUAS lat, long=sUAS long, alt > sUAS alt))`` 	| [test_config_1.3.json](/data/eval/test_config_1.3.json) 	| [env_config_1.3.json](/data/eval/env_config_1.3.json) 	|   	|
|         	|                                                                                                                                  	|                                                         	| 	|   	|
| C2.1    	| No search flights shall be conducted over the beach (given that it is highly populated with beachgoers).<br> _Validation:_ ``sUAS location in the environment (lat,long, alt) ∩ No-Fly Zones (lat, lon, alt) = φh``                                                                              	| [test_config_2.1.json](/data/eval/test_config_2.1.json) 	| [env_config_2.1.json](/data/eval/env_config_2.1.json) 	|   	|
| C2.2    	| No sUAS will land in the water or on the beach. All landings must be at home location. <br> _Validation:_ ``: if alt <= 1m then Distance  UAS(lat,lon) sUAS(home.lat,home.lon) ALWAYS < 8m``	| [test_config_2.2.json](/data/eval/test_config_2.2.json) 	| [env_config_2.2.json](/data/eval/env_config_2.2.json) 	|   	|
| C2.3    	| sUAS must perform a “safe” takeoff during the mission maintaining both lateral and altitude distance.  <br> _Validation:_``(Distance sUAS1(lat,lon) sUAS2(lat,lon) ALWAYS > 8 meters) AND (Distance sUAS1(lat,lon,alt) sUAS2(lat,lon,alt) ALWAYS > 20 meters) WHEN Mode(sUAS1)=Takeoff AND Mode(sUAS2)=Takeoff (for each pair of sUAS)`` | [test_config_2.3.json](/data/eval/test_config_2.3.json) 	| [env_config_2.3.json](/data/eval/env_config_2.3.json) 	|   	|
| C2.4    	| Routes must be completed successfully in winds up to 20mph.                                                                   	| [test_config_2.4.json](/data/eval/test_config_2.4.json) 	| [env_config_2.4.json](/data/eval/env_config_2.4.json) 	|   	|

_* Please note that geolocations (latitude, longitude) were obfuscated to meet double-blind requirements (We will release all original test results, logs and configurations in our public GitHub repository when the paper is accepted)._
