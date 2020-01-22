# strings

Pattern Searching

1) Naiive:

```
bool isMatches(string text,string pat){
   int n = text.length();
   int m = pat.length();
   
   for(int i=0;i<(n-m);++i){
       bool found = true;
       for(int j=0;j<m;++j){
         if(pat[j]!=text[i+j]){
           found = false;
           break;
         }
       }
      if(found)return true;
   }
   return false;
}
```
