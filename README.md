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
```

```
