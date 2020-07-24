1. 字符串不能直接改变其中的某一个字符的值，例s[2]='a'为错误写法。可以用下面的方法：

   ```js
   function replaceChat(source,pos,newChar){
        if(pos<0||pos>=source.length||source.length==0){
            return "invalid parameters...";
        }
        var iBeginPos= 0, iEndPos=source.length;
        var sFrontPart=source.substr(iBeginPos,pos);
        var sTailPart=source.substr(pos+1,source.length);
        var sRet=sFrontPart+newChar+sTailPart;
        return sRet;
    }
       alert(replaceChat("happy",1,"b"));
   
   ```

2. 