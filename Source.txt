#include<iostream>
#include<conio.h>
#include<ctime>
#include<stdlib.h>
#include<string.h>
#include<string>

using namespace std;
//node structure that can store int
struct node {
	int data; //store the char
	node *next;
	node() {
		data = 0;
		next = NULL;
	}
};


//list class, declare data members as discussed and write constructor
class stack {

private:
	int size;//len use for lenght
	node *stop;
public:
	stack() {
		size = 0;
		stop = NULL;
	}
	~stack();
	bool  push(int);
	const void display();
	int pop();
	int sizes();
	int sizebypoi();
	bool push(node);
	int get(int x);

};

// enter char in list and return ture if add add incrase the list size
bool stack::push(int x) {
	node *t = new node();
	if (size == 0) {
		t->data = x;
		stop = t;
		size++;
		return true;
	}
	else
		t->data = x;
	t->next = stop;
	stop = t;
	size++;
	return true;
}
//display the lsit 
const void stack::display() {
	node *t;
	t = stop;
	while (t != NULL) {
		cout << t->data << endl;
		t = t->next;
	}
}
//remove  data in list and reduce the size of list and return the number 
int stack::pop() {
	node *t = stop;
	int a;
	if (stop == NULL) {
		return -999;

	}
	else


		stop = t->next;
	a = t->data;
	t->data = NULL;
	delete t;
	size--;
	return a;

}
//return size off list
int stack::sizes() {

	return size;
}
// return size but calculated from loop
int stack::sizebypoi() {
	node *t = stop;
	while (t != NULL) {
		t = t->next;
		size++;

	}
	return size;
}
//Constructer delete all the lite node
stack::~stack() {
	node *t = stop;
	while (t != NULL) {
		t = stop;
		stop = stop->next;
		delete t;

	}

}
// put complete node in list and return true  
bool stack::push(node num) {
	node * t = new node();
	t->data = num.data;
	t->next = stop;
	stop = t;
	size++;
	return true;
}

// return the data of index that give user en
int stack::get(int x) {
	node * t = stop;
	if (size == 0 || x >= size) {
		return -9999;
	}
	for (int i = 0; i<x; i++) {
		t = t->next;
	}
	return t->data;
}
// chaeck box is empty or not and how much filled
bool check(stack s) {
	if (s.sizebypoi()<4) {
		return false;
	}

	//that loop check the number present in descending order 
	for (int i = 0; i<3; i++) {
		if (s.get(i)<s.get(i + 1)) {
			return false;
		}
	}
	return true;
}
void main() {
	stack A;
	string s = "39 2 3 + - ";
	string w = "";

	for (int i = 0; i < s.size(); i++)
	{
		w = "";
		while (s[i] != ' ') {
			w += s[i];
			i++;
		}




		int x, y;


		if (w == "+" || w == "-" || w == "/" || w == "*") {

			if (w == "*") {
				y = A.pop();
				x = A.pop();
				A.push(x*y);

			}
			else	if (w == "+") {
				y = A.pop();
				x = A.pop();
				A.push(x + y);


			}
			else	if (w == "-") {
				y = A.pop();
				x = A.pop();
				A.push(x - y);
			}
			else	if (w == "/") {
				y = A.pop();
				x = A.pop();
				A.push(x / y);
			}

		}

		else {
			int n = atoi(w.c_str());
			A.push(n);
		}




	}
	if (A.sizes() < 2) {



		A.display();
	}
	else {
		cout << "Expression is wrong ";
		_getch();
	}
	_getch();
}
