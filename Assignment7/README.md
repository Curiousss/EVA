# EVA

r0 = 1, jin = 1

| layer    | kernel |stride| RF | jout |
|----------|--------|------|----|------|
|1.Conv    | 7x7    |   2  |  7 |  2   |
|2.MaxPool | 3x3    |   2  | 13 |  4   |
|3.LRNorm  |        |      | 13 |  4   |
|4.Conv    | 1x1    |   1  | 13 |  4   |
|5.Conv    | 3x3    |   1  | 21 |  4   |
|6.LRNorm  |        |      | 21 |  4   |
|7.MaxPool | 3x3    |   2  | 29 |  8   |
|8.Conv    | 1x1    |   1  | 29 |  8   |
|9.Conv    | 5x5    |   1  | 61 |  8   |
|10.DepthConcat|    |      | 61 |  8   |
|11.Conv    | 1x1   |   1  | 61 |  8   |
|12.Conv   | 5x5    |   1  | 93 |  8   |
|13.DepthConcat|    |      | 93 |  8   |
|14.MaxPool| 3x3    |   2  |109 | 16   |
|15.Conv    | 1x1   |   1  |109 |  16  |
|16.Conv   | 5x5    |   1  |109 |  16  |
|17.DepthConcat|    |      |109 |  16  |
|Softmax|

