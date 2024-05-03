# Programming-Assignment-3
#include <iostream>
#include <string>

class Node {
public:
    char data;
    Node* next;
    Node(char val) : data(val), next(nullptr) {}
};

class Stack {
private:
    Node* top;

public:
    Stack() : top(nullptr) {}
    
    void push(char val) {
        Node* newNode = new Node(val);
        newNode->next = top;
        top = newNode;
    }
    
    void pop() {
        if (top != nullptr) {
            Node* temp = top;
            top = top->next;
            delete temp;
        }
    }
    
    char peek() {
        if (top != nullptr) {
            return top->data;
        }
        return '\0';
    }
    
    bool isEmpty() {
        return top == nullptr;
    }
};

bool checkBalancedParentheses(const std::string& expression) {
    Stack stack;
    
    for (char c : expression) {
        if (c == '(') {
            stack.push(c);
        } else if (c == ')') {
            if (stack.isEmpty()) {
                return false;
            }
            stack.pop();
        }
    }
    
    return stack.isEmpty();
}

int main() {
    std::string input;
    std::cout << "Enter an expression: ";
    std::cin >> input;
    
    if (checkBalancedParentheses(input)) {
        std::cout << "Balanced";
    } else {
        std::cout << "Not Balanced";
    }
    
    return 0;
}
