---
id:   Odd-String-Difference
title:   Odd String Difference
sidebar_label: 2451-Odd String Difference
tags: [dsa, leetcode]
description: Problem solution of  Count Days Spent Together
---

## Problem Statement 

### Problem Description

You are given an array of equal-length strings words. Assume that the length of each string is n.

Each string words[i] can be converted into a difference integer array difference[i] of length n - 1 where difference[i][j] = words[i][j+1] - words[i][j] where 0 <= j <= n - 2. Note that the difference between two letters is the difference between their positions in the alphabet i.e. the position of 'a' is 0, 'b' is 1, and 'z' is 25.

For example, for the string "acb", the difference integer array is [2 - 0, 1 - 2] = [2, -1].
All the strings in words have the same difference integer array, except one. You should find that string.
### Examples

#### Example 1
```
Input: words = ["adc","wzy","abc"]
Output: "abc"
Explanation: 
- The difference integer array of "adc" is [3 - 0, 2 - 3] = [3, -1].
- The difference integer array of "wzy" is [25 - 22, 24 - 25]= [3, -1].
- The difference integer array of "abc" is [1 - 0, 2 - 1] = [1, 1]. 
The odd array out is [1, 1], so we return the corresponding string, "abc".
```

### Example 2
```
Input: words = ["aaa","bob","ccc","ddd"]
Output: "bob"
Explanation: All the integer arrays are [0, 0] except for "bob", which corresponds to [13, -13].
```

### Constraints

- `3 <= words.length <= 100`
- `n == words[i].length`
- `2 <= n <= 20`
- `words[i] consists of lowercase English letters.`
## Solution of Given Problem

### Intuition and Approach

The problem can be solved using a brute force approach or an optimized Technique.

<Tabs>
<tabItem value="Brute Force" label="Brute Force">

### Approach 1:Brute Force (Naive)


Brute Force Approach: 
- Calculate the difference integer array for each string in the input list.
- Compare each difference array to find the unique one.
#### Codes in Different Languages

<Tabs>
<TabItem value="C++" label="C++" default>
<SolutionAuthor name="@AmruthaPariprolu"/>

```cpp
#include <vector>
#include <string>
#include <unordered_map>

using namespace std;

vector<int> calculateDifferenceArray(const string& word) {
    vector<int> diff;
    for (int i = 0; i < word.length() - 1; ++i) {
        diff.push_back(word[i + 1] - word[i]);
    }
    return diff;
}

string findUniqueDifferenceStringBruteForce(vector<string>& words) {
    vector<vector<int>> differences;
    for (const string& word : words) {
        differences.push_back(calculateDifferenceArray(word));
    }
    
    for (int i = 0; i < differences.size(); ++i) {
        int count = 0;
        for (int j = 0; j < differences.size(); ++j) {
            if (differences[i] == differences[j]) {
                ++count;
            }
        }
        if (count == 1) {
            return words[i];
        }
    }
    return "";
}



```
</TabItem>
<TabItem value="Java" label="Java">
<SolutionAuthor name="@AmruthaPariprolu"/>

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

public class Solution {
    private List<Integer> calculateDifferenceArray(String word) {
        List<Integer> diff = new ArrayList<>();
        for (int i = 0; i < word.length() - 1; ++i) {
            diff.add(word.charAt(i + 1) - word.charAt(i));
        }
        return diff;
    }

    public String findUniqueDifferenceStringBruteForce(List<String> words) {
        List<List<Integer>> differences = new ArrayList<>();
        for (String word : words) {
            differences.add(calculateDifferenceArray(word));
        }
        
        for (int i = 0; i < differences.size(); ++i) {
            int count = 0;
            for (int j = 0; j < differences.size(); ++j) {
                if (differences.get(i).equals(differences.get(j))) {
                    ++count;
                }
            }
            if (count == 1) {
                return words.get(i);
            }
        }
        return "";
    }
}


```


</TabItem>
<TabItem value="Python" label="Python">
<SolutionAuthor name="@AmruthaPariprolu"/>

```python
def calculate_difference_array(word):
    return [ord(word[i + 1]) - ord(word[i]) for i in range(len(word) - 1)]

def find_unique_difference_string_brute_force(words):
    differences = [calculate_difference_array(word) for word in words]
    
    for i in range(len(differences)):
        count = sum(1 for j in range(len(differences)) if differences[i] == differences[j])
        if count == 1:
            return words[i]
    return ""


```

</TabItem>
</Tabs>


### Complexity Analysis

- Time Complexity: $O(n*m^2)$
-  We compare each difference array with every other array, where 
n is the number of words and m is the length of each word.
- Space Complexity: $O(n*m)$
-   We store all difference arrays, where n is the number of words and m is the length of each word.
</tabItem>
<tabItem value="Optimized approach" label="Optimized approach">

### Approach 2: Optimized approach

Optimized Approach: 
- Calculate the difference integer array for each string in the input list.
- Use a hash map to count the occurrences of each difference array.
- Identify the difference array that appears only once and return the corresponding string.
#### Code in Different Languages

<Tabs>
<TabItem value="C++" label="C++" default>
<SolutionAuthor name="@AmruthaPariprolu"/>

```cpp
#include <vector>
#include <string>
#include <unordered_map>

using namespace std;

vector<int> calculateDifferenceArray(const string& word) {
    vector<int> diff;
    for (int i = 0; i < word.length() - 1; ++i) {
        diff.push_back(word[i + 1] - word[i]);
    }
    return diff;
}

string findUniqueDifferenceStringOptimized(vector<string>& words) {
    unordered_map<string, int> diffCount;
    unordered_map<string, string> diffMap;
    
    for (const string& word : words) {
        vector<int> diff = calculateDifferenceArray(word);
        string diffStr;
        for (int d : diff) {
            diffStr += to_string(d) + ",";
        }
        diffCount[diffStr]++;
        diffMap[diffStr] = word;
    }
    
    for (const auto& entry : diffCount) {
        if (entry.second == 1) {
            return diffMap[entry.first];
        }
    }
    return "";
}




```
</TabItem>
<TabItem value="Java" label="Java">
<SolutionAuthor name="@AmruthaPariprolu"/>

```java
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Solution {
    private List<Integer> calculateDifferenceArray(String word) {
        List<Integer> diff = new ArrayList<>();
        for (int i = 0; i < word.length() - 1; ++i) {
            diff.add(word.charAt(i + 1) - word.charAt(i));
        }
        return diff;
    }

    public String findUniqueDifferenceStringOptimized(List<String> words) {
        Map<String, Integer> diffCount = new HashMap<>();
        Map<String, String> diffMap = new HashMap<>();
        
        for (String word : words) {
            List<Integer> diff = calculateDifferenceArray(word);
            StringBuilder diffStr = new StringBuilder();
            for (int d : diff) {
                diffStr.append(d).append(",");
            }
            String diffString = diffStr.toString();
            diffCount.put(diffString, diffCount.getOrDefault(diffString, 0) + 1);
            diffMap.put(diffString, word);
        }
        
        for (Map.Entry<String, Integer> entry : diffCount.entrySet()) {
            if (entry.getValue() == 1) {
                return diffMap.get(entry.getKey());
            }
        }
        return "";
    }
}


```


</TabItem>
<TabItem value="Python" label="Python">
<SolutionAuthor name="@AmruthaPariprolu"/>

```python
def calculate_difference_array(word):
    return [ord(word[i + 1]) - ord(word[i]) for i in range(len(word) - 1)]

def find_unique_difference_string_optimized(words):
    diff_count = {}
    diff_map = {}
    
    for word in words:
        diff = calculate_difference_array(word)
        diff_str = ','.join(map(str, diff))
        diff_count[diff_str] = diff_count.get(diff_str, 0) + 1
        diff_map[diff_str] = word
    
    for diff_str, count in diff_count.items():
        if count == 1:
            return diff_map[diff_str]
    return ""


```

</TabItem>
</Tabs>

#### Complexity Analysis

- Time Complexity: $O(n*m)$
- We compute difference arrays and use hash maps to count occurrences, where n is the number of words and m is the length of each word.
- Space Complexity: $O(n*m)$
-  We store difference arrays in hash maps for counting and mapping, where n is the number of words and m is the length of each word.

</tabItem>
</Tabs>


## Video Explanation of Given Problem

    <LiteYouTubeEmbed
      id="M2UkMvkRaII"
      params="autoplay=1&autohide=1&showinfo=0&rel=0"
      title="Problem Explanation | Solution | Approach"
      poster="maxresdefault"
      webp 
    />

---

<h2>Authors:</h2>

<div style={{display: 'flex', flexWrap: 'wrap', justifyContent: 'space-between', gap: '10px'}}>
{['AmruthaPariprolu'].map(username => (
 <Author key={username} username={username} />
))}
</div>

