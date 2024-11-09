#include <iostream>
#include <stack>
#include <string>
#include <cctype>
#include <sstream>
#include <map>
#include <stdexcept>
#include <math.h>
#include <regex>
using namespace std;
    stack<string> postfixVec;
    stack<string> shuffleVec;
    vector<string> postEvaVec;
    
class classCalc {
    public:
    classCalc() {
        string userInput;
        getline(cin, userInput);
        cout << userInput << endl;
        classCalcBrain(userInput);
        evaluatorFunc(postfixVec);
    }
int precedence(string op);
void classCalcBrain(string userInput);
void evaluatorFunc (stack<string>& inputStack);
void printStack(stack<string> stack);
double operations(double num1, double num2, char oper);
};

//sets the level of importance according to PEMDAS
int classCalc::precedence(string op) {
    if (op == "+" || op == "-") return 1;
    if (op == "*" || op == "/") return 2;
    if (op == "^") return 3;
    else return 0;
}

void classCalc::classCalcBrain(const string userInput) {
        stringstream ss(userInput);
        string currentToken;
    for(auto i = 0; i < userInput.length() + 1; i++) {
        char part = userInput[i];
        if (isspace(part)) continue;
        //pushes and creates tokenized digits
        if (isdigit(part) || part == '.') {
            currentToken += part;  
        } else {
            if (!currentToken.empty()) {
            postfixVec.push(currentToken);
            currentToken.clear(); 
            }
        }

        //what to do when theres parenthesis
        if(part == '(') {
            string str(1, part);
            shuffleVec.push(str);
        } else if (part == ')') {
            //loop that pushes all symbols onto main when the closing parenthesis is found
            while(!shuffleVec.empty() && shuffleVec.top() != "(") {
                postfixVec.push(shuffleVec.top());
                shuffleVec.pop();
            }
            if (!shuffleVec.empty()) shuffleVec.pop();
        }
            
        //what happens with symbols
        if(part == '+' || part == '-' || part == '*' || part == '/' || part == '^') {
            string part1(1, part);
            //if its empty, it pushes whatever   
            if (shuffleVec.empty() || precedence(shuffleVec.top()) <= precedence(part1)) {
                shuffleVec.push(part1);
            } else {
                //if its not, precedence comes into play
                while (!shuffleVec.empty() && precedence(shuffleVec.top()) >= precedence(part1)) {
                postfixVec.push(shuffleVec.top()); 
                shuffleVec.pop();
                }
                shuffleVec.push(part1);
            }
        }
            
            

    }
    //after everything, pushes all left overs onto main
    if (!currentToken.empty()) postfixVec.push(currentToken);
            
    while(!shuffleVec.empty()) {
    postfixVec.push(shuffleVec.top());
    shuffleVec.pop();
    }
}


void classCalc::evaluatorFunc (stack<string>& inputStack) {
vector<double> numHold;

    //pushes everything from the stack onto a vector for better calculation handling
    while(!inputStack.empty()) {
    postEvaVec.push_back(inputStack.top());
    inputStack.pop();
    }

for (int i = postEvaVec.size() - 1; i >= 0; i--) {
        string token = postEvaVec[i];
        
        //if its a digit, it pushes it onto a vector
        if (isdigit(token[0])) {  
            numHold.push_back(stod(token));  
        } else { 
            //if its a symbol, it pops the latest 2 elements and creates them into numerical values
            //and the symbol gets converted into a character so it can be used in switch cases
            char oper = token[0];  

            double num2 = numHold.back(); numHold.pop_back();  
            double num1 = numHold.back(); numHold.pop_back();  

            double result = operations(num1, num2, oper); 
            //pushes the result back into the holding vector
            numHold.push_back(result); 
        }
    }
    //prints the remaining element of the holding vector which is the resultant
    cout << "= " << numHold.back() << endl;
}

//does the actual calculations
double classCalc::operations(double num1, double num2, char oper) {
    switch(oper) {
        case '+': return num1 + num2;
        case '-': return num1 - num2;
        case '*': return num1 * num2;
        case '^': return pow(num1, num2);
        case '/': if (num2 == 0) {
                    cout << "Error - dividing by zeros" << endl; break;
                    }
                  else return num1 / num2;
    }
}

int main() {
    classCalc obj;
}



