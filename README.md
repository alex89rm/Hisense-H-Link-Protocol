# Hisense H-Link-Protocol

# Project description 
This project aims to reverse engineer the H-Link protocol used in the Hi-Therma unit lineup, allowing direct control of the machines without depending on the Hisense cloud platform.. A custom Home Assistant component will be developed too.

* H-NET PROTOCOL
  * Physical level
  * Data frame  
* COMMUNICATION INTERFACES
  * Master Controller Interface
    * Units
      * SRC 33
      * SRC 18
  * Remote Controller Interface
    * Units
      * SRC 34
      * SRC 35
      * SRC 41
      * SRC 47
      * SRC 50
      * SRC 57
      * SRC 63
      * SRC 146
      * SRC 242
      * SRC 243
    * Request/Reply Analysis

## System description

Hisense Hi-Therma lineup is composed of both monobloc and split heatpumps. The unit I have under test is a 8kW monobloc type AHZ-080HCDS1.

![](https://climaconvenienza.it/cdn/shop/files/immagine-1-pompa-di-calore-reversibile-monoblocco-hisense-hi-terma-ahz-080hcds1-r-32-wi-fi-optional-con-comando-incluso_grande.jpg?v=1750325295)

## Communication interfaces

There are 2 HBS interfaces present on the indoor unit; one is used for the communication with the master controller ( HSXM-FE01 ) while the other one is used for the communication between outdoor/indoor unit (in my case they are both outdoor) and remote control with the auxilliary Hi-mit II remote controller (HCCS-H64H2C1M). Both can be found at CN1 of PCB1 and they are routed differently between the monobloc/split units. Pin 3,4 are the ones used for the master controller and are labeled as A,B on the terminal block TB4 present on PCB4. Pin 1,2 of CN1 are reserved for the communication with indoor unit / remote interface and are available on TB4 in split units. These pin on the monobloc unit are wired to PCB6 and are also available on the terminal block on PCB7.

![](clipboard-202508020131-gnawr.png)

## Disclaimer
All information provided in this project is based solely on independent research and reverse engineering performed for educational and interoperability purposes.
No proprietary code, confidential documentation, or copyrighted material from Hisense or any third party has been used.
This project is not affiliated with, endorsed by, or sponsored by Hisense.
No copyright infringement is intended.
