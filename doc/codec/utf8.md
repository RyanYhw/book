# UTF-8

## RFC

[rfc3629](https://tools.ietf.org/html/rfc3629)

## definition

字符的范围为U+0000..U+10FFFF. 被编码为1到4个8位字节.  

<pre>
Char. number range  |        UTF-8 octet sequence
      (hexadecimal)    |              (binary)  
   --------------------+---------------------------------------------  
   0000 0000-0000 007F | 0xxxxxxx  
   0000 0080-0000 07FF | 110xxxxx 10xxxxxx    
   0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx    
   0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx  
   第一个字节决定了该字符占几个字节, 汉字一般为3个字节
</pre>

## other

[complete character list for utf-8](http://www.fileformat.info/info/charset/UTF-8/list.htm)
