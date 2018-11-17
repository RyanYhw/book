# Base64

## RFC
[rfc4648](https://tools.ietf.org/html/rfc4648)

## definition
base64 由64个字符以及一个填充字符组成, 能够统一字符, 减少不同设备对字符处理的不同造成的错误.  

```
  Table 1: The Base 64 Alphabet  
Value Encoding  Value Encoding  Value Encoding  Value Encoding  
    0 A            17 R            34 i            51   
    1 B            18 S            35 j            52 0  
    2 C            19 T            36 k            53 1  
    3 D            20 U            37 l            54 2  
    4 E            21 V            38 m            55 3  
    5 F            22 W            39 n            56 4  
    6 G            23 X            40 o            57 5  
    7 H            24 Y            41 p            58 6  
    8 I            25 Z            42 q            59 7  
    9 J            26 a            43 r            60 8  
    10 K            27 b            44 s            61 9  
    11 L            28 c            45 t            62 +  
    12 M            29 d            46 u            63 /  
    13 N            30 e            47 v  
    14 O            31 f            48 w         (pad) =  
    15 P            32 g            49 x  
    16 Q            33 h            50 y


    Table 2: The "URL and Filename safe" Base 64 Alphabet  
     Value Encoding  Value Encoding  Value Encoding  Value Encoding  
         0 A            17 R            34 i            51 z  
         1 B            18 S            35 j            52 0  
         2 C            19 T            36 k            53 1  
         3 D            20 U            37 l            54 2  
         4 E            21 V            38 m            55 3  
         5 F            22 W            39 n            56 4  
         6 G            23 X            40 o            57 5  
         7 H            24 Y            41 p            58 6  
         8 I            25 Z            42 q            59 7  
         9 J            26 a            43 r            60 8  
        10 K            27 b            44 s            61 9  
        11 L            28 c            45 t            62 - (minus)  
        12 M            29 d            46 u            63 _  
        13 N            30 e            47 v           (underline)  
        14 O            31 f            48 w  
        15 P            32 g            49 x  
        16 Q            33 h            50 y         (pad) =  

        62 跟 63 主要是为了替代url里的+跟/
```

base64 是用4个6位的字节表示3个8位的字节, 不满3个字节的在低位补0,  
补齐3个字节, 补齐的部分用'='代替(少几个字节就补几个=).  
6位1字节转为8位1字节, 只需要将高2位填0.  

```
+--first octet--+-second octet--+--third octet--+    
|7 6 5 4 3 2 1 0|7 6 5 4 3 2 1 0|7 6 5 4 3 2 1 0|  
+-----------+---+-------+-------+---+-----------+  
|5 4 3 2 1 0|5 4 3 2 1 0|5 4 3 2 1 0|5 4 3 2 1 0|  
+--1.index--+--2.index--+--3.index--+--4.index--+
```
