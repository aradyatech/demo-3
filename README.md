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
