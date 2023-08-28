# PUSCH Transmit Power Calculator
online calculate: https://dustinchen26.github.io/PUSCH_power

## Description & example
```
Enter the following parameters and press "Calculate" to get the PUSCH power

p0-NominalWithGrant: -70
p0: -10
μ: 1
Num RB: 16
α: 1
Pathloss: 32
Delta TF: 2
TPC Adjustment: 0

Calculate
PUSCH Transmit Power
=  P_PUSCH
=  min{ P_CMAX , P_O_PUSCH                          + 10*log(2^μ * M_PUSCH_RB)+ α * PL + ΔTF + f }
=  min{ MTPL   , P_O_NOMINAL_PUSCH   + P_O_UE_PUSCH + 10*log(2^μ * M_PUSCH_RB)+ α * PL + ΔTF + f }
=  min{ MTPL   , p0-NominalWithGrant + p0           + 10*log(2^μ * NumRB) + alpha * Pathloss + Delta_TF + TPC_Adjustment }
=  p0-NominalWithGrant + p0   + 10 * log(2^μ* NumRB ) + alpha * Pathloss + Delta_TF + TPC_Adjustment
=   -70               + (-10) + 10 * log10(2^1 * 16)  +  1   *   32      +   2     +   0
= -30.95 dBm

=========================================================================================================================

// DU xml
        <nSsbPwr>-15</nSsbPwr>
        <puschPwrCfg>
            <msg3deltaPreamble>0</msg3deltaPreamble>
            <p0nominal>-70</p0nominal>
            <msg3alpha>ALL</msg3alpha>
            <p0>-10</p0>
            <alpha>ALL</alpha>
            <deltaMcsEnabled>true</deltaMcsEnabled>
            <isAccumulated>true</isAccumulated>
        </puschPwrCfg>

// UE log
07:59:43.496	[0xB821]	BCCH_DL_SCH / SystemInformationBlockType1
          uplinkConfigCommon 
          {
            frequencyInfoUL 
            {
              scs-SpecificCarrierList 
              {
                {
                  subcarrierSpacing kHz30, //μ=1
                }
              },
              p-Max 33
            },
            initialUplinkBWP 
            {
              genericParameters 
              {
                subcarrierSpacing kHz30 //μ=1
              },
              pusch-ConfigCommon setup : 
                {
                  p0-NominalWithGrant -70 //p0-NominalWithGrant = -70
                },
          ss-PBCH-BlockPower -15 // Pathloss = ss-PBCH-BlockPower - RSRP = (-15) - (-46.28) = 31.28 near 32
        },

// RSRP = -46.28
07:59:43.614	[0xB97F]	NR5G ML1 Searcher Measurement Database Update Ext
      -----------------------------------------------------------------------------------------------------------------------------------------
      |   |      |      |     |            |            |Detected Beams                                                                       |
      |   |      |      |     |            |            |   |     |RX Beam Info           |NR2NR       |NR2NR       |L2NR        |L2NR        |
      |   |      |PBCH  |Num  |Cell Quality|Cell Quality|   |SSB  |RX Beam|               |Filtered Tx |Filtered Tx |Filtered Tx |Filtered Tx |
      |#  |PCI   |SFN   |Beams|RSRP        |RSRQ        |#  |Index|Id     |RSRP           |Beam RSRP L3|Beam RSRQ L3|Beam RSRP L3|Beam RSRQ L3|
      -----------------------------------------------------------------------------------------------------------------------------------------
      |  0|     1|   804|    1|     -46.281|     -10.359|  0|    0|     NA|        -46.266|     -46.281|     -10.359|          NA|          NA|
      |   |      |      |     |            |            |   |     |     NA|        -48.594|            |            |            |            |

07:59:43.640    [0xB821]    DL_CCCH / RRC Setup
                              p0-AlphaSets 
                              {
                                {
                                  p0-PUSCH-AlphaSetId 0,
                                  p0 -10, //p0=-10
                                  alpha alpha1 //alpha=1
                                }

// (808,19) PUSCH Num RB=16
07:59:43.665    [0xB883]    NR5G MAC UL Physical Channel Schedule Report
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

// (808,19) PUSCH Pathloss=32, Delta TF=2, TPC Adjustment=0, PUSCH Transmit Power = -30
07:59:43.693    [0xB8D2]    NR5G LL1 FW MAC TX IU Power
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
