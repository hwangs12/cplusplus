# Leetcode With C++

## Partition Labels

### Solution 

```c++
class Solution 
{
public:
    vector<int> partitionLabels(string s) 
    {
        int i = s.size()-1;
        string helper;
        vector<int> tempPart;
        
        while (!s.empty()) 
        {
            if (s[0] == s[i]) 
            {
                helper = s.substr(0, i+1);
                s = s.substr(i+1);
                int j = s.size() - 1;
                while (j >= 0)
                {
                    if (helper.find(s[j]) != string::npos)
                    {
                        helper = helper + s.substr(0, j+1);
                        s = s.substr(j+1);
                        j = s.size()-1;
                    }
                    else
                    {
                        j--;
                    };
                };
                tempPart.push_back(helper.size());
                i = s.size()-1;
            } 
            else 
            {
                i--;
            };
        };
        return tempPart;
    };
};
```

### Another Solution
```c++
class Solution 
{
public:
    vector<int> partitionLabels(string s) 
    {
        vector<int> letterIndices(26, 0);
      
        for (int i=0; i < s.length(); i++)
        {
            letterIndices[s.at(i)-'a'] = i;
        };
        
        int j = 0, anchor = 0;
        vector<int> ans;
        
        for (int i=0; i < s.length(); i++)
        {
            j = max(j, letterIndices[s.at(i)-'a']);
            if (i == j)
            {
                ans.push_back(i - anchor+1);
                anchor = i+1;
            };
        };
        
        return ans;
    };
};
```
