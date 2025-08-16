# Remote control

In this page are reported the messages exchanged when the operation of the machine is controlled by the remote app. The communication is started by SRC 41 ( Hi-mit controller )

### CYCLE 1 OFF WATER TEMP SET TO 11°C

| SRC | CTRL | LEN | | DSW1 ADDR | | | | | ? | MODE | | CYCLE 1 WATER SET TEMP | CYCLE 2 WATER SET TEMP | DHW SET TEMP | POOL SET TEMP | CYCLE1 ENABLE | CYCLE2 ENABLE? | CYCLE1 ROOM1 SET TEMP | CYCLE1 ROOM2 SET TEMP | CYCLE1 ROOM3 SET TEMP| CYCLE1 ROOM4 SET TEMP | CYCLE2 ROOM1 SET TEMP | CYCLE2 ROOM2 SET TEMP | CYCLE2 ROOM3 SET TEMP | CYCLE4 ROOM1 SET TEMP| ROOM ENABLE | | | | | | | | | | |  | | | | | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|41|0|48|202|160|1|1|107|62| **31** |8|255| **11** |12|45|24|0|0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|211|

<span style="color:green">ACK from 146</span>

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | |  |  | | |CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|14|1|1|1|0|99|62|0|31|9|255|187|

<span style="color:green">ACK from 41</span>

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | CYCLE1 WATER TEMP | SET TEMP | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|12|1|1|1|0|99|62|3| 11 |88|

<span style="color:green">ACK from 41</span>

| SRC | CTRL | LEN | | DSW1 ADDR | | | | | ? | | | CYCLE 1 WATER SET TEMP | CYCLE 2 WATER SET TEMP | DHW SET TEMP | POOL SET TEMP | CYCLE1 ENABLE | CYCLE2 ENABLE? | ROOM 1 SET TEMP | | | | | | | | ROOM1 ENABLE | | | | | | | | | | |  | | | | | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|41|0|48|202|160|1|1|107|62| **0** |8|0| 11 |12|45|24|0|0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|51|

<span style="color:green">ACK from 146</span>

|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | |  |  | | |CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|14|1|1|1|0|99|62|0|0|9|0|91|

<span style="color:green">ACK from 41</span>

### CYCLE 1 OFF WATER TEMP SET TO 13°C

| SRC | CTRL | LEN | | DSW1 ADDR | | | | | ? | | | CYCLE 1 WATER SET TEMP | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|41|0|48|202|160|1|1|107|62|31|8|255| 13 |12|45|24|0|0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|213|

<span style="color:green">ACK from 146</span>
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | |  |  | | |CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|14|1|1|1|0|99|62|0|31|9|255|187|

<span style="color:green">ACK from 41</span>
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | | CYCLE1 WATER TEMP | SET TEMP | CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|12|1|1|1|0|99|62|3| 13 |94|

<span style="color:green">ACK from 41</span>

| SRC | CTRL | LEN | | DSW1 ADDR | | | | | ? | | | CYCLE 1 WATER SET TEMP | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | CRC | 
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|41|0|48|202|160|1|1|107|62|0|8|0| 13 |12|45|24|0|0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|53|

<span style="color:green">ACK from 146</span>
|SRC | CTRL | LEN | DSW8 ADDR | - | DSW8 ADDR | | | |  |  | | |CRC |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|146|0|14|1|1|1|0|99|62|0|0|9|0|91|

<span style="color:green">ACK from 41</span>

### CYCLE 1 ON WATER TEMP SET TO 13°C
|41|0|48|202|160|1|1|107|62|31|8|255| 13 |12|45|24| 1 |0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|212|
<span style="color:green">ACK from 146</span>
|146|0|14|1|1|1|0|99|62|0|31|9|255|187|
<span style="color:green">ACK from 41</span>
|146|0|12|1|1|1|0|99|62|1|9|88|
<span style="color:green">ACK from 41</span>
|146|0|12|1|1|1|0|99|62| 2 | 16 |66| <- THESE TWO BYTES CHANGED !
<span style="color:green">ACK from 41</span>
|50|0|14|1|1|1|0|1|9|2|1|3|13|10|
<span style="color:green">ACK from 35</span>
|41|0|48|202|160|1|1|107|62|0|8|0| 13 |12|45|24| 1 |0|26|28|28|28|28|28|28|28|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|52|
<span style="color:green">ACK from 146</span>
|146|0|14|1|1|1|0|99|62|0|0|9|0|91|
<span style="color:green">ACK from 41</span>
