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
