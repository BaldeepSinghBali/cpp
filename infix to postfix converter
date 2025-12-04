#include <iostream>
#include <stack>
#include <cctype>
#include <cmath>
using namespace std;

int precedence(char op) {
    if (op == '^') return 3;
    if (op == '*' || op == '/') return 2;
    if (op == '+' || op == '-') return 1;
    return 0;
}

string convertToPostfix(string infix) {
    stack<char> s;
    string postfix = "";
    for (char c : infix) {
        if (c == ' ') continue;
        if (isdigit(c)) postfix += c;
        else if (c == '(') s.push(c);
        else if (c == ')') {
            while (s.top() != '(') {
                postfix += s.top();
                s.pop();
            }
            s.pop();
        }
        else {
            while (!s.empty() && s.top() != '(' && 
                   precedence(c) <= precedence(s.top()) && 
                   (c != '^' || precedence(c) < precedence(s.top()))) {
                postfix += s.top();
                s.pop();
            }
            s.push(c);
        }
    }
    while (!s.empty()) {
        postfix += s.top();
        s.pop();
    }
    return postfix;
}

int evaluatePostfix(string postfix) {
    stack<int> s;
    for (char c : postfix) {
        if (isdigit(c)) s.push(c - '0');
        else {
            int b = s.top(); s.pop();
            int a = s.top(); s.pop();
            if (c == '+') s.push(a + b);
            else if (c == '-') s.push(a - b);
            else if (c == '*') s.push(a * b);
            else if (c == '/') s.push(a / b);
            else if (c == '^') s.push(pow(a, b));
        }
    }
    return s.top();
}

int main() {
    string infix;
    cout << "======================================\n";
    cout << "  INFIX to POSTFIX & EVALUATOR TOOL   \n";
    cout << "======================================\n";
    cout << "Enter an valid expression (e.g., 3+(4*5)-2^2):\n> ";
    getline(cin, infix);

    string postfix = convertToPostfix(infix);
    cout << "\nPostfix Expression: " << postfix << endl;

    int result = evaluatePostfix(postfix);
    cout << "Evaluated Result  : " << result << endl;

    cout << "\nThank you for using the converter!" << endl;
    return 0;
}
