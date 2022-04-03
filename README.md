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

## 3Sum

### Solution
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) 
    {
    
        vector<vector <int>> res;

        vector<int> temp_res;

        sort(nums.begin(), nums.end());
        
        int i;
    
        for (auto it = nums.begin(); it != nums.end(); ++it)
        {   
            i = distance(nums.begin(), it);
            if (nums[i] > 0)
            {
                break;
            }
            if (i > 0 and nums[i] == nums[i-1])
            {
                continue;
            }

            int l = i + 1, r = distance(nums.begin(), nums.end()) - 1;
            while (l < r)
            {
                int threeSum = nums[i] + nums[l] + nums[r];
            
                if (threeSum > 0)  
                {
                    --r;
                }
                else if (threeSum < 0)
                {   
                    ++l;
                }   
                else 
                {   
                    temp_res.push_back(nums[i]);
                    temp_res.push_back(nums[l]);
                    temp_res.push_back(nums[r]);
                    res.push_back(temp_res);
                    temp_res = {};
                    ++l;
                    while (nums[l] == nums[l-1] && l < r)
                    {   
                        ++l;
                    };
                };   
            };   
        };
        return res;
    };    
};

```
