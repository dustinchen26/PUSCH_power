# PUSCH Transmit Power Calculator
online calculate: https://dustinchen26.github.io/PUSCH_power

## Description & example
```
Ref: ETSI TS 138 213 chap 7 Uplink Power control
PUSCH Transmit Power = p0-NominalWithGrant+ 10*log(2^mu* Num RB )+ p0 + alpha* Pathloss + Delta TF + TPC Adjustment  

example:
p0-NominalWithGrant: -70
mu: 1
Num RB: 16
p0: -10
alpha: 1
Pathloss: 32
Delta TF: 2
TPC Adjustment: 0

Calculate
PUSCH Transmit Power:
= -70 + 10 * log10(2^1 * 16) + -10 + 1 * 32 + 2 + 0
= -30.95 

// log example

07:59:43.496	[0xB821]	BCCH_DL_SCH / SystemInformationBlockType1
            initialUplinkBWP 
            {
              genericParameters 
              {
                subcarrierSpacing kHz30 //mu=1
              },
              pusch-ConfigCommon setup : 
                {
                  p0-NominalWithGrant -70 //p0-NominalWithGrant
                },
				
07:59:43.640	[0xB821]	DL_CCCH / RRC Setup
                              p0-AlphaSets 
                              {
                                {
                                  p0-PUSCH-AlphaSetId 0,
                                  p0 -10,
                                  alpha alpha1 //alpha=1
                                }

// (808,19) PUSCH Num RB=16
07:59:43.665	[0xB883]	NR5G MAC UL Physical Channel Schedule Report
   ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   |   |                     |       |Carriers                                                                                                                                      
   |   |                     |       |       |              |                                   |      |                                                                            
   |   |                     |       |       |              |                                   |      |PUSCH Data                                                                  
   |   |                     |       |       |              |                                   |      |            |      |       |    |    |                |    |       |       |
   |   |                     |       |       |              |                                   |Dual  |            |      |       |    |    |                |DMRS|       |       |
   |   |System Time          |Num    |Carrier|              |                                   |Pol   |Is Second   |Start |Num    |HARQ|    |                |Add |RB     |       |
   |#  |Slot|Numerology|Frame|Carrier|ID     |RNTI Type     |Phychan Bit Mask                   |Status|Phychan     |Symbol|Symbols|ID  |MCS |MCS Table       |Pos |Start  |Num RBs|
   ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   |  0|  19|     30kHz|  808|      1|      0|        C_RNTI|                              PUSCH|     0|           0|     0|     12|   0|   9|           64QAM|   1|      0|     16|
   
// (808,19) PUSCH Pathloss=32, Delta TF=2, TPC Adjustment=0
07:59:43.693	[0xB8D2]	NR5G LL1 FW MAC TX IU Power
         System Frame Number       = 808
         SCS                       = 1
         Slot Number               = 19
      Power Info
         --------------------------------------------------------------------------
         |   |       |       |CarrierIdType                                        
         |   |       |       |PUSCH Data                                          |
         |   |Carrier|Channel|Transmit|        |TPC       |PHR |Delta|Is  |Minimum|
         |#  |Id     |Type   |Power   |Pathloss|Adjustment|MTPL|TF   |Msg3|Power  |
         --------------------------------------------------------------------------
         |  0|      0|  PUSCH|     -30|      32|         0|  21|    2|   0|    -38|
```
