/*
Input a file name when prompted, be sure to include an extension.

If the file is C++ or C, the code will check for the balance of the following characters: ([{

If the file is HTML, the code will check for a balance of tags. (Note that lone tags that have been "commented-out" are still accounted for)
*/

#include "stdafx.h"
#include <iostream>
#include <fstream>
#include <stack>
#include <string>

using namespace std;

class schtack { //Create stack class
	char stk[30];
	int top;
public:
	schtack()
	{
		top = -1;
	}
	void push(char x)
	{
		if (top > 30)
		{
			cout << "stack overflow\n"; //output stack overflow
			return;
		}
		stk[++top] = x;
	}
	char pop()
	{
		if (top <0)
		{
			cout << "stack underflow\n"; //output stack underflow
			return 'z';
		}
		return stk[top--];
	}
	bool isempty()
	{
		if (top<0)
			return true;
	}
};


int main() {
	string sfile;

	cout << "Please enter a file name: "; //Ask for user input
	cin >> sfile;
	ifstream file(sfile.c_str()); //Take in an HTML/C/C++ file
	int pos = sfile.find("."); //Get postion based on "."
	++pos;

	if (sfile.substr(pos) == "html" || sfile.substr(pos) == "htm") { //if HTML, check tag balance
		char c;
		stack<string> myStack;
		while (file >> c) {
			string tag = "";
			if (c == '<') {
				while (file >> c) {
					if (c == '>')
						break;
					tag += c;
				}
				if (tag[0] != '/') myStack.push(tag);
				else {
					if (tag.substr(1).compare(myStack.top()) == 0) {
						myStack.pop();
					}
					else {
						cout << "ILLEGAL\n";
						return 0;
					}
				}
			}
		}
		if (myStack.empty()) cout << "LEGAL\n"; //If Stack is empty: LEGAL
		else cout << "ILLEGAL\n";
	}
	else if (sfile.substr(pos) == "c" || sfile.substr(pos) == "cpp" || sfile.substr(pos) == "h") { //If  C or C++, check character balance
		char ch, popout;
		schtack st;
		while (file >> ch)
		{
			if (ch == '{' || ch == '[' || ch == '(')
				st.push(ch);
			else if (ch == '}')
			{
				popout = st.pop();
				if (popout != '{')
				{
					cout << "ILLEGAL\n";
					return 0;
				}
			}
			else if (ch == ']')
			{
				popout = st.pop();
				if (popout != '[')
				{
					cout << "ILLEGAL\n";
					return 0;
				}
			}
			else if (ch == ')') {
				popout = st.pop();
				if (popout != '(')
				{
					cout << "ILLEGAL\n";
					return 0;
				}
			}
		}
		if (!st.isempty()) { //If stack class is empty: ILLEGAL
			cout << "ILLEGAL\n";
			return 0;
		}
		else {
			cout << "LEGAL\n";
			return 0;
		}
	}
	else {
		cout << "Invalid File Type\n"; //If user input is not HTML/C/C++
		return 0;
	}
}
