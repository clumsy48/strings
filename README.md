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

Time complexity : O( (n-m)*m) ~ O(n*m)
```
2) KMP

**LPS**
```
vector<int> getLPS(string pattern){
  int len = pattern.length();
  vector<int> lps(len);
  int i=1;
  int j=0;
  lps[0] = 0;
  while(i<len){
    if(pattern[i]==pattern[j]){
       lps[i] = j+1;
       i++,j++;
    }else{
      if(j!=0){
        j = lps[j-1];  
      }else{
        lps[i] = 0;
        i++;
      }
    }
  }
  return lps;
}
```
