# ix-rnp-100G

Especificação na Nota:
OPT-8PLHG10D-LR1 - TRANSCEPTOR ÓPTICO, 100GB, SINGLE LAMBDA WITH FEC, LC CONNECTOR, 10KM, WITH DDM (LR1)

> O módulo de fibra óptica 100G QSFP28 LR1 de 10km é com apenas 1 via, mas o lado elétrico é com 4 vias

Datasheet:
[Link](https://github.com/davinunes/ix-rnp-100G/blob/main/Datasheet%20100Gb%2010km%20LR1%20(1).pdf)

Comando de diagnostico 1:
```
<PatioBrasil-S6730-H24X6C>display transceiver diagnosis interface 100GE 0/0/3
Port 100GE0/0/3 transceiver diagnostic information:
Parameter        Current       Low Alarm    High Alarm
  Type            Value        Threshold    Threshold    Status
-------------   ---------      ---------    ----------   --------
TxPower(dBm)    2.84  (lane0)  -2.00        6.30         abnormal
                -40.00(lane1)
                -40.00(lane2)
                -40.00(lane3)
RxPower(dBm)    -8.64 (lane0)  5.93         6.30         abnormal
                -40.00(lane1)
                -40.00(lane2)
                -40.00(lane3)
Current(mA)     70.18 (Lane0)  5.00         120.00       abnormal
                0.00  (Lane1)
                0.00  (Lane2)
                0.00  (Lane3)
Temp.(▒▒C)      37.31          -5.00        75.00        normal
Voltage(V)      3.39           3.13         3.47         normal

<PatioBrasil-S6730-H24X6C>
```

Comando de Diagnostico2:
```
<PatioBrasil-S6730-H24X6C>display transceiver interface 100GE 0/0/3 verbose

100GE0/0/3 transceiver information:
-------------------------------------------------------------
Common information:
  Transceiver Type               :100GBASE_SR4_QSFP28
  Connector Type                 :LC
  Wavelength(nm)                 :1311
  Transfer Distance(m)           :10km(SMF),10(Optical Cable)
  Digital Diagnostic Monitoring  :YES
  Vendor Name                    :OPTLASER
  Vendor Part Number             :OPT-8PLHG10D-LR1
  Ordering Name                  :
-------------------------------------------------------------
Manufacture information:
  Manu. Serial Number            :2243A00025
  Manufacturing Date             :2022-10-17
  Vendor Name                    :OPTLASER
-------------------------------------------------------------
Diagnostic information:
  Temperature(▒▒C)              :37.31
  Temp High Threshold(▒▒C)      :75.00
  Temp Low  Threshold(▒▒C)      :-5.00
  Voltage(V)                    :3.39
  Volt High Threshold(V)        :3.47
  Volt Low  Threshold(V)        :3.13
  Bias Current(mA)              :70.24|0.00(Lane0|Lane1)
                                 0.00|0.00(Lane2|Lane3)
  Bias High Threshold(mA)       :120.00
  Bias Low  Threshold(mA)       :5.00
  RX Power(dBM)                 :-8.64|-40.00(Lane0|Lane1)
                                 -40.00|-40.00(Lane2|Lane3)
  RX Power High Warning(dBM)    :5.30
  RX Power Low  Warning(dBM)    :-9.20
  RX Power High Threshold(dBM)  :6.30
  RX Power Low  Threshold(dBM)  :5.93
  TX Power(dBM)                 :2.85|-40.00(Lane0|Lane1)
                                 -40.00|-40.00(Lane2|Lane3)
  TX Power High Warning(dBM)    :5.30
  TX Power Low  Warning(dBM)    :-1.00
  TX Power High Threshold(dBM)  :6.30
  TX Power Low  Threshold(dBM)  :-2.00
  Transceiver phony alarm       : Yes
-------------------------------------------------------------
<PatioBrasil-S6730-H24X6C>
```

Status da interface:
```
[PatioBrasil-S6730-H24X6C]display interface 100GE 0/0/3
100GE0/0/3 current state : DOWN
Line protocol current state : DOWN
Description:IX-DF-RNP-LACP
Switch Port, Link-type : trunk(configured),
PVID :    1, TPID : 8100(Hex), The Maximum Frame Length is 9000
IP Sending Frames' Format is PKTFMT_ETHNT_2, Hardware address is 20df-73a8-fa90
Last physical up time   : 2025-08-08 20:04:34
Last physical down time : 2025-08-09 20:41:49
Current system time: 2025-08-11 14:35:12
Port Mode: COMMON FIBER, Transceiver: 100GBASE_SR4_QSFP28
Speed : 100000, Loopback: NONE
Duplex: FULL,   Negotiation: DISABLE
Mdi   : -,      Flow-control: DISABLE
FEC   : NONE
Last 300 seconds input rate 0 bits/sec, 0 packets/sec
Last 300 seconds output rate 0 bits/sec, 0 packets/sec
Input peak rate 0 bits/sec, Record time: -
Output peak rate 8840 bits/sec, Record time: 2025-08-08 17:18:05

Input:  0 packets, 0 bytes
  Unicast:                          0,  Multicast:                           0
  Broadcast:                        0,  Jumbo:                               0
  Discard:                          0,  Pause:                               0

  Total Error:                      0
  CRC:                              0,  Giants:                              0
  Runts:                            0,  Fragments:                           0
  Alignments:                       0,  Symbols:                             0
  Ignoreds:                         0

Output:  101718 packets, 16078056 bytes
  Unicast:                          0,  Multicast:                      101718
  Broadcast:                        0,  Jumbo:                               0
  Discard:                          0,  Pause:                               0


    Input bandwidth utilization threshold : 80.00%
    Output bandwidth utilization threshold: 80.00%
    Input bandwidth utilization  :    0%
    Output bandwidth utilization :    0%

[PatioBrasil-S6730-H24X6C]
```

Config da Interface
```
[PatioBrasil-S6730-H24X6C-100GE0/0/3]dis this
#
interface 100GE0/0/3
 fec mode none
 description IX-DF-RNP-LACP
 eth-trunk 3
#
return
```

Config do LACP:
```
[PatioBrasil-S6730-H24X6C-Eth-Trunk3]dis this
#
interface Eth-Trunk3
 description IX-DF-RNP-LACP
 port link-type trunk
 undo port trunk allow-pass vlan 1
 port trunk allow-pass vlan 51 371 1141 2052 to 2053
 mode lacp
 jumboframe enable 9000
#
return
```

Foto:
<img width="1549" height="633" alt="image" src="https://github.com/user-attachments/assets/bad75597-0c7f-4503-9fc5-4f814d4b6fa0" />

