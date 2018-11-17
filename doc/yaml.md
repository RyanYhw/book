# yaml

只记录了一些简单的用法

## Collections

### 数组

'- ' (dash and space) 开头

```
- Mark McGwire
- Sammy Sosa
- Ken Griffey

翻译

[ 'Mark McGwire', 'Sammy Sosa', 'Ken Griffey' ]
```

### map

': ' (colon and space) 开头

```
hr:  65    # Home runs
avg: 0.278 # Batting average
rbi: 147   # Runs Batted In

翻译

{ hr: 65, avg: 0.278, rbi: 147 }
```

### Collections 事例

map 的 value 为 数组
```
american:
  - Boston Red Sox
  - Detroit Tigers
  - New York Yankees
national:
  - New York Mets
  - Chicago Cubs
  - Atlanta Braves

翻译
{ american: [ 'Boston Red Sox', 'Detroit Tigers',   'New York Yankees' ],
  national: [ 'New York Mets', 'Chicago Cubs', 'Atlanta Braves' ] 
}

```

数组 的值为 map

```
-
  name: Mark McGwire
  hr:   65
  avg:  0.278
-
  name: Sammy Sosa
  hr:   63
  avg:  0.288

翻译
[ 
    { name: 'Mark McGwire', hr: 65, avg: 0.278 },
    { name: 'Sammy Sosa', hr: 63, avg: 0.288 } 
]
```

数组 的值为 数组

```
- [name        , hr, avg  ]
- [Mark McGwire, 65, 0.278]
- [Sammy Sosa  , 63, 0.288]

翻译
[ [ 'name', 'hr', 'avg' ],
  [ 'Mark McGwire', 65, 0.278 ],
  [ 'Sammy Sosa', 63, 0.288 ] ]
```

map 的值为 map

```
Mark McGwire: {hr: 65, avg: 0.278}
Sammy Sosa: {
    hr: 63,
    avg: 0.288 
}

翻译
{ 'Mark McGwire': { hr: 65, avg: 0.278 },
  'Sammy Sosa': { hr: 63, avg: 0.288 } }
```

## Structures

yaml 可以由多个document(文档)组成，使用 '---' 作为分隔符， '...' 作为一个文档结束的标记

yaml 使用 '&' 和 '*' 来做变量的引用。

### Structures 事例

单个文档

```
---
hr: # 1998 hr ranking
  - Mark McGwire
  - Sammy Sosa
rbi:
  # 1998 rbi ranking
  - Sammy Sosa
  - Ken Griffey

翻译
{
  "hr": [
    "Mark McGwire", 
    "Sammy Sosa"
  ], 
  "rbi": [
    "Sammy Sosa", 
    "Ken Griffey"
  ]
}
```

注意，上边的例子 Sammy Sosa 出现了两次，可以使用'&'和'*'来简化
```
--- 
hr:
  - Mark McGwire
  # Following node labeled SS
  - &SS Sammy Sosa
rbi:
  - *SS # Subsequent occurrence
  - Ken Griffey

翻译
{
  "hr": [
    "Mark McGwire", 
    "Sammy Sosa"
  ], 
  "rbi": [
    "Sammy Sosa", 
    "Ken Griffey"
  ]
}
```

## Scalars

‘|’ 将一块作为一行处理，换行符会保留
'>' 将一块作为一行处理，换行符变空格

```
lines: |
    458 Walkman Dr.
    Suite #292
city    : Royal Oak

翻译
{
  "city": "Royal Oak", 
  "lines": "458 Walkman Dr.\nSuite #292\n"
}
```

```
--- >
  Mark McGwire's
  year was crippled
  by a knee injury.

翻译
"Mark McGwire's year was crippled by a knee injury."
```

## Tags

