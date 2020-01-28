# strings

Pattern Searching

## 1) Naiive:

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
## 2) KMP

**LPS**. Longest proper prefix which is also a suffix at index i for substring 0 to i
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
//OR
vector<int> getLPS(string s) {
    int n = (int)s.length();
    vector<int> pi(n);
    for (int i = 1; i < n; i++) {
        int j = pi[i-1];
        while (j > 0 && s[i] != s[j])
            j = pi[j-1];
        if (s[i] == s[j])
            j++;
        pi[i] = j;
    }
    return pi;
}
```

```
void kmpSearch(string pattern,string text){
    int tl = text.length();
    int pl = pattern.length();
    vector<int> lps = getLPS(pattern);
    int i=0,j=0;
    while(i<tl && j<pl){
        if(pattern[j] == text[i]){
            i++,j++;
        }else{
            if(j!=0){
                j = lps[j-1];
            }else{
                i++;
            }
        }
        if(j==pl){
            cout << i-1 << " ";
            j = lps[j-1];
        }
    }
    return ;
}
```
