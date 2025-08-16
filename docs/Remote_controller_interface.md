
# Messages

Observing the traffic on the bus we can see there are different units. These are the SRC address found on the 12 bus : 

|ADDRESS|UNIT |
|--|--|
| 41 | Hi-Mit remote controller  |
| 47 | Hi-Mit remote controller |
| 50 | Indoor Unit |
| 57 | Hi-Mit remote controller |
| 63 | Hi-Mit remote controller |
| 34 |  |
| 35 | Outodoor Unit |
| [[#Address-146]] | Indoor Unit |
| 242 |  |
| 243 |  |



# REQUESTS / REPLIES ANALYSIS
 Here I try to report any communication pattern I can find :

## 41 - 146 interaction
Messages exchanged between Hi-mit interface and indoor unit
WIP

#### Status update request
Every 60s there is a status update request from 41. The request is acknowledged and replied to from 146.

|41|0|9|202|161|9|1|97|11|
<span style="color:green">ACK from 146</span>
|146|0|48|9|1|9|0|97|62|0|8|1|6|12|45|28|0|0|0|24|28|28|28|28|28|28|28|0|0|0|0|224|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|184|
<span style="color:green">ACK from 41</span>

#### Working mode change on master controller

When there is a change of the working mode on the master controller if leads to a parameters update message from 146.The message is ackowledged from 41.

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | - | - | - | MODE: | VALUE | CYCLE1 SET TEMP: | VALUE | CYCLE2 SET TEMP: | VALUE | ROOM1 SET TEMP: | VALUE  | ROOM? SET TEMP: | VALUE | ROOM? SET TEMP: | VALUE | ROOM? SET TEMP: | VALUE | ROOM? SET TEMP: | VALUE | ROOM? SET TEMP: | VALUE | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|32|9|1|9|0|99|62|1|8|3|6|4|12|10|23|11|28|12|28|13|28|14|28|15|28|16|28|17|28|115|

<span style="color:green">ACK from 41</span>

## 47 - 242 interaction
<span style="color:darkorange">|47|0|10|202|160|1|1|108|0|12|</span>
<span style="color:green">ACK from 242</span>
|242|0|48|1|1|1|1|108|62|0|31|129|129|27|0|0|0|0|0|0|0|22|0|0|0|0|0|0|0|20|60|50|7|24|25|129|129|0|100|3|0|0|8|0|4|0|0|7|
<span style="color:green">ACK from 47</span>

## 50 - 35 interaction

<span style="color:darkorange">|50|0|9|1|1|1|0|240|248|</span>
<span style="color:green">ACK from 35</span>
|35|0|36|1|0|1|1|255|0|40|32|0|0|0|2|0|3|34|128|31|0|31|128|18|170|0|0|0|41|41|1|3|241|208|0|106|
<span style="color:green">ACK from 50</span>
<span style="color: darkorange">|50|0|28|1|1|1|0|255|24|32|0|7|24|33|129|34|30|30|0|0|25|0|62|0|6|0|2|100|</span>
<span style="color:green">ACK from 35</span>
|35|0|14|1|0|1|1|254|16|32|16|32|0|241|
<span style="color:green">ACK from 50</span>
<span style="color: darkorange">|50|0|32|1|1|1|0|159|31|129|129|20|60|0|7|129|31|26|100|3|0|0|0|0|0|0|0|0|0|2|0|111|</span>
<span style="color:green">ACK from 35</span>

## 63 - 243 interaction

<span style="color:darkorange">|63|1|9|202|160|1|0|0|99|</span>
<span style="color:green">ACK from 243</span>
|243|1|48|1|0|0|255|192|6|0|0|2|0|0|0|0|0|0|0|0|0|66|34|18|178|0|0|60|20|31|0|9|31|0|145|0|0|0|0|33|0|24|0|30|0|0|0|92|
<span style="color:darkorange">|63|1|9|202|160|1|0|1|98|</span>
<span style="color:green">ACK from 243</span>
|243|1|48|1|0|0|255|193|6|0|0|0|0|26|0|0|0|0|7|0|0|0|129|0|0|0|31|0|0|100|31|0|0|0|0|3|129|0|0|0|0|0|129|0|0|0|0|243|

## DEVICE DISCOVERY
When the Hi-mit interface is looking for devices on H-LINK bus the following messages are sent: (This messages were logged with **no device connected**  on H-LINK bus)

| SRC | CTRL |LEN | | DSW1 ADDR| | | |CRC |
|--|--|--|--|--|--|--|--|--|
|41|0|9|202|160|255|255|241|146|

| SRC | CTRL |LEN | | DSW1 ADDR  | | | |  |CRC |
|--|--|--|--|--|--|--|--|--|--|
|57|3|10|202|160|255|255|0|0|99|

## AUTODISCOVERY ??
From time to time these messages appears on the bus, they are not always grouped together and they are not acknowledged, maybe they are used to report their presence ?


|35|0|10|1|0|1|255|15|20|238| <- UPDATE: VALUE 15 & 20 CHANGE OVER TIME, ARE THEY TEMPERATURE ?
|50|0|9|1|1|1|255|241|6|
|41|0|9|202|160|255|255|241|146|

|35|0|28|1|0|1|255|242|3|34|128|31|0|31|128|18|170|0|0|0|41|41|1|3|241|208|0|171| -> This is a status update but it seems no one requests or acknowledge

## ALL MESSAGES
Here are reported all the messages captured :

Note: DSW8 ADDR field is the binary encoded value +1
Example: 
![](clipboard-202508070058-zy4vb.png)
In the image above DSW8 ADDR is equal to 8+1 = **9**

DSW1 field is thebynary encoded value set on the Hi-mit interface

### ADDRESS 41 ( HI-MIT INTERFACE )

Request (KEEP ALIVE/ DISCOVERY ?) sent every 30s.
| SRC | CTRL |LEN | | DSW1 ADDR | | | |CRC |
|--|--|--|--|--|--|--|--|--|
|41|0|9|202|160|255|255|241|146|

Status update request sent every 60s. Acknoledged from 146.
| SRC | CTRL |LEN | | DSW1 ADDR | DSW8 ADDR | | |CRC |
|--|--|--|--|--|--|--|--|--|
|41|0|9|202|160|1|1|97|2|


Request sent when there is a remote command.
| SRC | CTRL | LEN | | DSW1 ADDR | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |  | |  | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|41|0|48|202|160|1|1|107|62|31|8|255|11|12|45|24|0|0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|211|

Request sent when there is a remote command.
| SRC | CTRL | LEN | | DSW1 ADDR | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|41|0|48|202|160|1|1|107|62|0|8|0|11|12|45|24|0|0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|51|

## Address 146
Messages coming from 146 seems to be associated with machine operation parameters that could be stored in the INDOOR UNIT. This is the common header:

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | - | OP | - | 
|--|--|--|--|--|--|--|--|--|
|146|0| xx |1|1|1|0| 99 |62| 

**OP** is set to **99** when the message is generated by a single or multiple parameters update; it is set to **97** when it provides a status update in reply to a request from 41.

For example the following message is sent when there is a parameter change made on the master controller:
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | - | OP | - | PARAMETER ID | SET VALUE | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|12|1|1|1|0| 99 |62| **x** | **x** | xx |




Multiple parameters can also be concatenated in a message  in the following way: 
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | - | OP | - | PARAMETER ID 1 | SET VALUE 1 |PARAMETER ID 2 | SET VALUE 2 |PARAMETER ID n | SET VALUE n | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0| 10+(n*2) |1|1|1|0| 99 |62| xx | xx |xx| xx |xx | xx | xx |

#### PARAMETERS ID
These are the parameters ID :
| DESCRIPTION |PARAMETER ID |
|--|--|
| **MODE**              | 1 |
| CYCLE MODE?           | 2 |
| **CYCLE1 WATER TEMP** | 3 |
| **CYCLE2 WATER TEMP** | 4 |
| **DHW SET TEMP**      | 5 |
| **POOL SET TEMP**     | 6 |
| **ERROR CODE**     | 7 |
| ?     | 8 |
| ?     | 9 |
| **CYCLE1 ROOM1 SET TEMP**        | 10 |
| CYCLE1 ROOM2 SET TEMP **?**     | 11 |
| CYCLE1 ROOM3 SET TEMP **?**     | 12 |
| CYCLE1 ROOM4 SET TEMP **?**     | 13 |
| CYCLE2 ROOM1 SET TEMP **?**     | 14 |
| CYCLE2 ROOM2 SET TEMP  **?**   | 15 |
| CYCLE2 ROOM3 SET TEMP **?**    | 16 |
| CYCLE2 ROOM4 SET TEMP **?**    | 17 |
| **ROOM ENABLE**       | 18 |
| **ROOM ECO MODE?**       | 19 |
| DHW CONFIG ?           | 20 |
| **PUMP STATUS**  | 21 |
| WATER PUMP CONFIG?        | 22 |

#### MODE

| BIT 7 | BIT 6  | BIT 5 | BIT 4 | BIT 3 | BIT 2 |  BIT 1| BIT 0 |
|--|--|--|--|--|--|--|--|
| | HEAT MODE |  |  | COOL MODE | AUTO MODE | CYCLE 2 ENABLE | CYCLE1 ENABLE |

This parameter sets the working mode of the unit: HEAT / COOL / AUTO. Only one of the 3 mode can be active at a time.


#### CYCLE MODE: 16 (CYCLE1 ECO MODE OFF),17 (CYCLE1 ECO MODE ON)

| BIT 7 | BIT 6  | BIT 5 | BIT 4 | BIT 3 | BIT 2 |  BIT 1| BIT 0 |
|--|--|--|--|--|--|--|--|
|? | ? | ? |  PUMP ENABLE ? | ? | ? |CYCLE2 ECO MODE| CYCLE1 ECO MODE |

#### DHW CONFIG
0 DHW BOOST OFF, 128 DHW BOOST ON

#### PUMP STATUS
0 PUMP OFF, 128 PUMP RUNNING

#### WATERPUMP CONFIG? :  SEEN VALUES: 32,128,160,192,224

192 ->(HEAT MODE SELECTED)

|BIT 7 |BIT 6 |BIT 5 |BIT 4 |BIT 3 |BIT 2 |BIT 1 |BIT 0 |
|--|--|--|--|--|--|--|--|
| WP ECO MODE HEAT | WP ECO MODE COOL  | 1 | 0 | 0 | 0 | 0 | 0 |

#### STATUS UPDATE MESSAGE

This status update message is requested periodically from 41. **OP** is now set to **97**

The parameter are in the same order as the table above: 1) MODE, 2)PUMP, 3) WATER SET TEMP, ETC ..
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | OP | - | | MODE | CYCLE MODE | WATER SET TEMP CYCLE1 | WATER SET TEMP CYCLE2 | DHW SET TEMP | POOL SET TEMP | ERROR CODE | | | CYCLE1 ROOM1 SET TEMP | CYCLE1 ROOM2 SET TEMP| CYCLE1 ROOM3 SET TEMP | CYCLE1 ROOM4 SET TEMP | CYCLE2 ROOM1 SET TEMP| CYCLE2 ROOM2 SET TEMP| CYCLE2 ROOM3 SET TEMP | CYCLE2 ROOM4 SET TEMP | ROOM ENABLE | | DHW CONFIG | PUMP STATUS | WATERPUMP CONFIG | | | | | | |  | |  |  | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|48|1|1|1|0|97|62|0|8|0| **11** |12|45|24|0|0|0|26|28|28|28|28|28|28|28|0|0|0|0|160|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|242|

#### EXAMPLES
These are some example messages

This is sent when the MASTER CONTROLLER POOL water set temp is changed to 27°C :
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | POOL WATER TEMP | SET TEMP | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|12|1|1|1|0| 99 |62| **6** | **27** |77| 

This is sent when HEAT MODE is selected on MASTER CONTROLLER:
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | | MODE ?  |  | |  | | |  | | | | | | | | | | |  | | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|30|1|1|1|0|99|62|1| **64** |3|20|4|20|11|22|12|22|13|22|14|22|15|22|16|22|17|22|24|

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | | | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|12|1|1|1|0|99|62|22|128|198|

This is sent when COOL MODE is selected on MASTER CONTROLLER:
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | | MODE ?  |  | |  | | |  | | | | | | | | | | |  | | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|30|1|1|1|0|99|62|1| **8** |3|13|4|16|11|28|12|28|13|28|14|28|15|28|16|28|17|28|71|

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | | | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|12|1|1|1|0|99|62|22|160|230|

This is sent when AUTO MODE is selected on MASTER CONTROLLER:
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | |  MODE ? |  | |  | | |  | | | | | | | | | |  | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|28|1|1|1|0|99|62|1| **4** |3|28|11|0|12|0|13|0|14|0|15|0|16|0|17|0|80|

#### UNKNOWN MESSAGE
This message appears very rarely:

|146|0|34|9|1|9|0|100|153|120|182|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|16|

### ADDRESS 50 ( INDOOR UNIT )
| SRC | CTRL |LEN | DSW8 ADDR | - | DSW8 ADDR | - | - | CRC |
|--|--|--|--|--|--|--|--|--|
|50|0|9|1|1|1|0|240|248|

| SRC | CTRL |LEN | DSW8 ADDR | - | DSW8 ADDR | - | - | CRC |
|--|--|--|--|--|--|--|--|--|
|50|0|9|1|1|1|255|241|6|


|SRC | CTRL | LEN | DSW8 ADDR |- | DSW8 ADDR |- |- |- | MODE | PUMP ? | WATER SET TEMP | ? | IDU GAS TEMPERATURE |- | IDU LIQUID TEMPERATURE | ~~WATER OUT PHEX TEMP~~ NOT SURE | WATER INLET TEMP | | | | | | | | |  | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|50|0|28|1|1|1|0|255|24|32| *0* |22|24| **16** |129|20| **11** |12|0|0|22|0|62|0|6|0|2|122|

MODE is 32 when CYCLE 1 is OFF, when COOL MODE on CYCLE1 is enabled it changes to 9.
PUMP ? becomes 1 when cooling is enabled. Change to 17 when water pump is running. <- **EDIT: NOT 100% SURE** (PUMP SEEMS TO RUN EVEN WHEN PUMP=1 , MAYBE 1->CYCLE 1 ENABLED AND 17-> CYCLE1&ROOM1 ENABLED)
WATER SET TEMP IS SET WHEN CYCLE 1 IS ENABLED

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | - | - | WATER OUT TEMP ? | | | ? | | | WATER SET TEMP | | AMBIENT TEMP (SIMILAR VALUE) |  | REQUESTED PUMP PWM | | FLOW ?| | | | | | | | | ? | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|50|0|32|1|1|1|0|159|30|129|129|20|60|0|7|129|30|26|100|3|0|0|0|0|0|0|0|0|0|2|0|111|

AMBIENT TEMP -> **COULD BE TEMP SENSOR INSIDE INDOOR UNIT REPORTING A SIMILAR VALUE TO OUTDOOR AMBIENT TEMP**
REQUESTED PUMP PWM -> I THINK IT IS REQUESTED PWM BECAUSE WHEN VALUE IS 100 (PWM 100 MEANS OFF) SOMETIME THE PUMP IS STILL ON
?->CYCLE1 HEAT ON : 4 CYCLE 1 HEAT OFF: 0, CYCLE 1 COOL ON: 6, CYCLE 1 COOL OFF: 2

### ADDRESS 35 ( OUTDOOR UNIT )

|SRC | CTRL | LEN | DSW8 ADDR | | DSW8 ADDR | | | | CRC |
|--|--|--|--|--|--|--|--|--|--|
|35|0|10|1|0|1|255|15|20|238|

|SRC | CTRL | LEN | DSW8 ADDR | | DSW8 ADDR | | | | | | |  | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|35|0|14|1|0|1|1|254|16|32|16|32|0|241|

|SRC | CTRL | LEN | DSW8 ADDR | | DSW8 ADDR | | | | | | EVAP GAS TEMP | | DISCHARGER TEMPERATURE | | ~~IDU LIQUID TEMP~~ | | FREQUENCE | CURRENT | EVO% | | | | | | |  | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|35|0|28|1|0|1|255|242|3|22|128| **25** |0| **51** |128| **17** |110|0|0|0|41|41|1|3|241|208|0|114|



|SRC | CTRL | LEN | DSW8 ADDR | | DSW8 ADDR | | | | | | | | | | | | OUTDOOR TEMP | | EVAP GAS TEMP | | DISCHARGER TEMPERATURE |  | ~~IDU LIQUID TEMP~~ | | FREQUENCE | CURRENT | EVO% | | | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|35|0|36|1|0|1|1|255|0|40|32|0|0|0|2|0|3|20|128| **22** |0| **42** |128| **14**| 100|0|0|0|41|41|1|3|241|208|0|178|

Message similar to the previous one with added 8 byte.

|35|240|8|9|224|9|255|231| -> SENT WHEN THERE IS NO COMMUNICATION WITH OUDOOR UNIT ? LOOKS LIKE A DISCOVERY MESSAGE

### ADDRESS 47 ( HI-MIT INTERFACE )

Unit 47 seems to send only this request that 242 replies to

|SRC | CTRL | LEN | - | DSW1 ADDR | DSW8 ADDR | ? | ? | ? | CRC |
|--|--|--|--|--|--|--|--|--|--|
|47|0|10|202|160|1|1|108|0|12|

### ADDRESS 57 ( HI-MIT INTERFACE )

This message is seen during device discovery

|SRC | CTRL | LEN | - | DSW1 ADDR | ? | ? | ? | ? | CRC |
|--|--|--|--|--|--|--|--|--|--|
|57|3|10|202|160|255|255|0|0|99|

### ADDRESS 63 ( HI-MIT INTERFACE )
Unit 63 seems to only send request that 243 replies to. No other messages are captured at this time.

|SRC | CTRL |LEN | - | DSW1 ADDR | DSW8 ADDR | ? | ? |CRC |
|--|--|--|--|--|--|--|--|--|
|63|1|9|202|160|1|0|0|99|

|SRC | CTRL |LEN | - | DSW1 ADDR | DSW8 ADDR | ? | ? |CRC |
|--|--|--|--|--|--|--|--|--|
|63|1|9|202|160|1|0|1|98|

### ADDRESS 242 (UNKNOWN)

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | - | - | - | |WATER TEMP | | | CYCLE1 ROOM1 TEMP ? |  | | | | | | | CYCLE1 ROOM1 SET TEMP | | | | | | | | | | | WATER SET TEMP | | | | | | WATER PUMP SPEED | | WATER FLOW (1 digit) | | IDU CAPACITY? | ? | | ? | ? | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|242|0|48|1|1|1|1|108|62|0| **7** |129|129|27|0|0|0|0|0|0|0|22|0|0|0|0|0|0|0|20|60|50|20|24|12|129|129|0| **14** |3| **14** |0|24|2|4|1|1|111|

### ADDRESS 243 (UNKNOWN)
Unit 243 seems to reply to 63 requests.
|SRC | CTRL | LEN | DSW8 ADDR  | - | - | - | OP | | | | | | | | | | | FREQUENCY | | TARGET FREQUENCY | | OUTDOOR TEMP | | | | | | | DISCHARGER TEMP | | | | | | | | |  | | FREQUENCE | | | EVAP GAS TEMP | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|243|1|48|1|0|0|255|192|6|0|0|2|0|0|0|0|0|0|0|0|0|64|30|17|159|0|0|60|20|30|0|1|30|0|145|0|0|0|0|34|0|24|0|29|0|0|0|68|

|SRC | CTRL | LEN | DSW8 ADDR | - | - | - | OP | | | | | | | | FREQUENCE |  | | | | | | | | | | | |  | WATER PUMP SPEED? | | | | | | | | |  | |  | WATER FLOW? | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|243|1|48|1|0|0|255|193|6|0|0|0|0|26|0|0|0|0|7|0|0|0|129|0|0|0|29|0|0|100|29|0|0|0|0|3|129|0|0|0|0|0|129|0|0|0|0|243|
