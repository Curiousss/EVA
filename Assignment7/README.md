# EVA

r0 = 1, jin = 1

| layer    | kernel |stride| RF | jout |
|----------|--------|------|----|------|
|1.Conv    | 7x7    |   2  |  7 |  2   |
|2.MaxPool | 3x3    |   2  | 13 |  4   |
|3.LRNorm1 |        |      | 13 |  4   |
|4.Conv    | 1x1    |   1  | 13 |  4   |
|5.Conv    | 3x3    |   1  | 21 |  4   |
|6.LRNorm2 |        |      | 21 |  4   |
|7.MaxPool | 3x3    |   2  | 29 |  8   |
|8.Conv    | 1x1    |   1  | 29 |  8   |
|9.Conv    | 5x5    |   1  | 61 |  8   |
|10.DepthConcat 1|  |      | 61 |  8   |
|11.Conv    | 1x1   |   1  | 61 |  8   |
|12.Conv   | 5x5    |   1  | 93 |  8   |
|13.DepthConcat 2|  |      | 93 |  8   |
|14.MaxPool| 3x3    |   2  |109 | 16   |
|15.Conv    | 1x1   |   1  |109 |  16  |
|16.Conv   | 5x5    |   1  |109 |  16  |
|17.DepthConcat 3|  |      |109 |  16  |
|Softmax 0|
|18. Conv  | 1x1   |  1    |109 |  16  |
|19. Conv  | 5x5   |  1    |173 |  16  |
|20.DepthConcat 4| |       |173 |  16  |
|21.Conv   | 1x1   | 1     |173 |  16  |
|22.Conv   | 5x5   | 1     |237 |  16  |
|23.DepthConcat 5| |       |237 |  16  |
|24.Conv   | 1x1   | 1     |237 |  16  |
|25.Conv   | 5x5   | 1     |301 |  16  |
|26.DepthConcat 6| |       |301 |  16  |
|27.Conv   | 1x1   | 1     |301 |  16  |
|28.Conv   | 5x5   | 1     |365 |  16  |
|29.DepthConcat 6| |       |365 |  16  |
|30.Maxpool| 3x3   |  2    |397 |  32  |
|31.Conv   | 1x1   |  1    |397 |  32  |
|32.Conv   | 5x5   |  1    |525 |  32  |
|33.DepthConcat 7| |       |525 |  32  |
|34.Conv   | 1x1   |  1    |525 |  32  |
|35.Conv   | 5x5   |  1    |653 |  32  |
|36.DepthConcat 8| |       |653 |  32  |
|37.AvgPool| 7x7   |  1    |845 |  32  |
