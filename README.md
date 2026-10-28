# demo-3
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;

        for (char c : s) {
            // Opening brackets
            if (c == '(' || c == '{' || c == '[') {
                st.push(c);
            }
            // Closing brackets
            else {
                if (st.empty()) {
                    return false;
                }

                if (c == ')' && st.top() != '(')
                    return false;

                if (c == '}' && st.top() != '{')
                    return false;

                if (c == ']' && st.top() != '[')
                    return false;

                st.pop();
            }
        }

        return st.empty();
    }
};
class Solution {
public:
    void backtrack(vector<string>& ans, string& curr, int open, int close, int n) {
        
        // Complete valid parentheses string
        if (curr.length() == 2 * n) {
            ans.push_back(curr);
            return;
        }

        // We can add '(' if we haven't used all n opening brackets
        if (open < n) {
            curr.push_back('(');
            backtrack(ans, curr, open + 1, close, n);
            curr.pop_back();
        }

        // We can add ')' only if there are unmatched '('
        if (close < open) {
            curr.push_back(')');
            backtrack(ans, curr, open, close + 1, n);
            curr.pop_back();
        }
    }

    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string curr;

        backtrack(ans, curr, 0, 0, n);

        return ans;
    }
};
class Solution {
public:
    int scoreOfParentheses(string s) {
        int score = 0;
        int depth = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s[i] == '(') {
                depth++;
            } 
            else {
                depth--;

                // "()"
                if (s[i - 1] == '(') {
                    score += (1 << depth);
                }
            }
        }

        return score;


        class Solution {
public:
    string removeOuterParentheses(string s) {
        string ans = "";
        int depth = 0;

        for (char c : s) {
            if (c == '(') {
                if (depth > 0)
                    ans += c;
                depth++;
            }
            else {
                depth--;
                if (depth > 0)
                    ans += c;
            }
        }

        return ans;
    }
};
    }
};
class Solution {
public:
    long long minSumSquareDiff(vector<int>& nums1, vector<int>& nums2, int k1, int k2) {
        int n = nums1.size();
        vector<int> diff(n);
        
        long long total = 0;
        for (int i = 0; i < n; i++) {
            diff[i] = abs(nums1[i] - nums2[i]);
            total += diff[i];
        }
        
        long long k = (long long)k1 + k2;
        
        if (k >= total) return 0;
        
        sort(diff.begin(), diff.end(), greater<int>());
        
        diff.push_back(0);
        
        for (int i = 0; i < n; i++) {
            long long count = i + 1;
            long long need = (long long)(diff[i] - diff[i + 1]) * count;
            
            if (k >= need) {
                k -= need;
            } else {
                long long level = diff[i] - k / count;
                long long rem = k % count;
                long long ans = 0;
                
                for (int j = 0; j <= i; j++) {
                    long long d = min((long long)diff[j], level);
                    ans += d * d;
                }
                
                ans += rem * (level - 1) * (level - 1);
                return ans;
            }
        }
        
        return 0;
    }
};

class Solution {
public:
    int minOperations(string s) {
        int n = s.size();

        if (is_sorted(s.begin(), s.end()))
            return 0;

        if (n == 2)
            return -1;

        char mn = *min_element(s.begin(), s.end());
        char mx = *max_element(s.begin(), s.end());

        if (s[0] == mn || s[n - 1] == mx)
            return 1;

        if (s[0] == mx && s[n - 1] == mn &&
            count(s.begin(), s.end(), mn) == 1 &&
            count(s.begin(), s.end(), mx) == 1)
            return 3;

        return 2;
    }
};


class Solution {
public:
    int minOperations(vector<int>& nums) {
        int n = nums.size();
        int s = nums[0];

        bool ascending = true;
        bool descending = true;

        for (int i = 0; i < n; i++) {
            if (nums[i] != (s + i) % n)
                ascending = false;

            if (nums[i] != (s - i + n) % n)
                descending = false;
        }

        int ans = INT_MAX;

        if (ascending) {
            int left = (n - s) % n;

            ans = min(ans, left);
            ans = min(ans, s + 2);
        }

        if (descending) {
            int k = (s + 1) % n;

            ans = min(ans, k + 1);
            ans = min(ans, 1 + (n - k) % n);
        }

        return ans == INT_MAX ? -1 : ans;
    }
};

class Solution {
public:
    vector<string> createGrid(int m, int n) {
        vector<string> grid(m, string(n, '#'));

        // First row: all free cells
        for (int j = 0; j < n; j++) {
            grid[0][j] = '.';
        }

        // Last column: all free cells
        for (int i = 0; i < m; i++) {
            grid[i][n - 1] = '.';
        }

        return grid;
    }
};

class Solution {
public:
    int minCost(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        const auto& molqaviren = grid;

        vector<vector<bool>> dp(n, vector<bool>(1024, false));

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int val = molqaviren[i][j];

                if (i == 0 && j == 0) {
                    dp[j][val] = true;
                    continue;
                }

                vector<bool> curr(1024, false);

                for (int x = 0; x < 1024; x++) {
                    if (i > 0 && dp[j][x]) {
                        curr[x ^ val] = true;
                    }

                    if (j > 0 && dp[j - 1][x]) {
                        curr[x ^ val] = true;
                    }
                }

                dp[j] = curr;
            }
        }

        for (int x = 0; x < 1024; x++) {
            if (dp[n - 1][x]) {
                return x;
            }
        }

        return -1;
    }
};
