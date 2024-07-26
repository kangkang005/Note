## Pin Description
|Name |Feature |Type |Description|
|--- |--- |--- |---|
|Ck | |Input |Clock input|
|CEB | |Input |Chip enable, active low|
|GWEB | |Input |Global write enable, active low. Need to open bit write option in compiler.|
|WEB[n-1:0] | |Input |Write enable, active low. When bit write option is ON, WEB becomes a bus. Otherwise, WEB is a single pin.|
|A[m-1:0] | |Input |Address input|
|DI[m-1:0] | |Input |Data input|
|EMCE | |Input |Extra margin adjustment enable|
|EMC[3:0] | |Input |Extra margin adjustment option|
|LS |G |Input |Light Sleep mode enable|
|DS |G |Input |Deep Sleep mode enable|
|SD |G |Input |Shut down mode enable|
|POFF |D |Input |Periphery off with array retention|
|POFFADJ |D |Input |Periphery off with array turnoff|
|PUD |D |Output |Wakeup ready signal for command|
|VDDC |D |Inout |Array power supply|
|VDD |D |Inout |Periphery power supply|
|ETC |S |Input |External timing control|
|REDAD |C |Input |IO Redundancy address scan input|
|REDCK |C |Input |IO Redundancy address scan clock|
|REDRST |C |Input |IO Redundancy address reset|
|REDEN |C |Input |IO Redundancy enable|
|REDSCOUT |C |Output |IO Redundancy address scan output|
|DO[w-1:0] | |Output |Data output|
|VSS | |Inout |Ground|