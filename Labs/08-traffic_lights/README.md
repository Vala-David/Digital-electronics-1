link na repozitář: https://github.com/Vala-David/Digital-electronics-1

1.úkol

|Input P|Clock|State|Output R|
|-------|-----|-----|--------|
|0      |↑    |A    |0       |
|0      |↑    |A    |0       |
|1      |↑    |B    |0       | 
|1      |↑    |C    |0       |
|0      |↑    |C    |0       | 
|1      |↑    |D    |1       | 
|0      |↑    |A    |0       | 
|1      |↑    |B    |0       |
|1      |↑    |C    |0       | 
|1      |↑    |D    |1       | 
|1      |↑    |B    |0       | 
|0      |↑    |B    |0       | 
|0      |↑    |B    |0       | 
|1      |↑    |C    |0       | 
|1      |↑    |D    |1       | 
|1      |↑    |B    |0       | 


|Input P |-|0|0|1|1|0|1|0|1|1|1|1|0|0|1|1|1|
|Clock   |-|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|↑|
|State   |-|A|A|B|C|C|D|A|B|C|D|B|B|B|C|D|B|
|Output R|-|0|0|0|0|0|1|0|0|0|1|0|0|0|0|1|0|

|RGB LED|Pin names  |Red  |Yellow|Green|
|LD16   |N15,M16,R12|1,0,0|1,1,0 |0,1,0|
|LD17   |N16,R11,G14|1,0,0|1,1,0 |0,1,0|
