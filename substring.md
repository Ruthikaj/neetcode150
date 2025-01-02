Here is the code with an embedded dry run using comments for the input string **"abcabcbb"**:

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> mpp(256, -1); // Initialize vector to store last seen index of each character, all set to -1 initially.
        
        int left = 0, right = 0; // Sliding window pointers. Both start at 0.
        int n = s.size();        // Length of the string.
        int len = 0;             // To store the length of the longest substring.

        while (right < n) {      // Iterate through the string using the `right` pointer.
            // Dry Run: For input "abcabcbb"
            
            if (mpp[s[right]] != -1) { // If the current character has been seen before:
                // Update the left pointer to skip the repeated character if it's within the current window.
                left = max(mpp[s[right]] + 1, left); 
                // Example at right=3 ('a'): mpp['a']=0, left becomes max(0+1, 0)=1.
            }

            // Update the last seen index of the current character.
            mpp[s[right]] = right; 
            // Example at right=0 ('a'): mpp['a'] = 0.
            // Example at right=1 ('b'): mpp['b'] = 1.
            // Example at right=2 ('c'): mpp['c'] = 2.

            // Calculate the length of the current window and update the maximum length.
            len = max(len, right - left + 1); 
            // Example at right=0 ('a'): len = max(0, 0-0+1) = 1.
            // Example at right=2 ('c'): len = max(2, 2-0+1) = 3.
            // Example at right=3 ('a'): len remains 3 (3-1+1).

            right++; // Move the `right` pointer to the next character.
        }

        // Final length of the longest substring without repeating characters.
        return len; 
    }
};
```

---

### Detailed Dry Run:
#### Input: `"abcabcbb"`

| **Step** | **Right** | **Char (s[right])** | **Left** | **Window** | **Len** | **mpp updates** |
|----------|-----------|---------------------|----------|------------|---------|-----------------|
| 1        | 0         | `'a'`              | 0        | `'a'`      | 1       | `mpp['a'] = 0`  |
| 2        | 1         | `'b'`              | 0        | `'ab'`     | 2       | `mpp['b'] = 1`  |
| 3        | 2         | `'c'`              | 0        | `'abc'`    | 3       | `mpp['c'] = 2`  |
| 4        | 3         | `'a'`              | 1        | `'bca'`    | 3       | `mpp['a'] = 3`  |
| 5        | 4         | `'b'`              | 2        | `'cab'`    | 3       | `mpp['b'] = 4`  |
| 6        | 5         | `'c'`              | 3        | `'abc'`    | 3       | `mpp['c'] = 5`  |
| 7        | 6         | `'b'`              | 5        | `'b'`      | 3       | `mpp['b'] = 6`  |
| 8        | 7         | `'b'`              | 7        | `'b'`      | 3       | `mpp['b'] = 7`  |

---

### Explanation in Code Comments for Dry Run:
- **Initialization**:
  - The `mpp` array stores the last seen indices of characters.
  - Pointers `left` and `right` define the current substring window.
  - `len` keeps track of the maximum substring length without repeating characters.

- **Iteration (Dry Run for "abcabcbb")**:
  - At **`right = 0`**, the character `'a'` is not seen before, so:
    - Update `mpp['a'] = 0`, calculate length `len = max(0, 0-0+1) = 1`.
  - At **`right = 1`**, the character `'b'` is not seen before:
    - Update `mpp['b'] = 1`, calculate length `len = max(1, 1-0+1) = 2`.
  - At **`right = 2`**, the character `'c'` is not seen before:
    - Update `mpp['c'] = 2`, calculate length `len = max(2, 2-0+1) = 3`.
  - At **`right = 3`**, the character `'a'` is seen at index `0`:
    - Update `left = max(0+1, 0) = 1`, update `mpp['a'] = 3`.
    - Length of current substring: `len = max(3, 3-1+1) = 3`.
  - Continue similarly for all characters, updating `left`, `right`, and `len` as needed.

---

### Final Output:
- Longest substring without repeating characters: `"abc"`.
- Length: **`3`**.
