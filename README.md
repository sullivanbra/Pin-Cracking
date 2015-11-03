# Pin-Cracking
Senior project where we are formulating a code to crack PIN numbers on debit cards.

// ConsoleApplication1.cpp : Defines the entry point for the console application.
//

#include "stdafx.h"
#include<iostream>
#include<cstring>
#include<ctime>
#include<cstdlib>
using namespace std;

int main()
{
	int a[1000];
	int length;
	int random;
	int b[1000] = { 33 };
	unsigned long long tries = 0;
	bool cracked = false;

	cout << "Enter a password length: ";
	cin >> length;

	srand(time(NULL));
	for (int i = 0; i<length; i++){
		do {
			random = (rand() % 94) + 33;
		} while (random == 45);
		a[i] = random;
		cout << char(a[i]);
	}cout << endl;

	do{
		b[0]++;
		for (int i = 0; i<length; i++){
			if (b[i] >= 94 + 33){
				b[i] -= 94;
				b[i + 1]++;
			}
			else break;
		}
		cracked = true;
		for (int k = 0; k<length; k++)
		if (b[k] != a[k]){
			cracked = false;
			break;
		}
		if ((tries & 0x7ffffff) == 0)
			cout << "\r       \r   ";
		else if ((tries & 0x1ffffff) == 0)
			cout << ".";
		tries++;
	} while (cracked == false);

	cout << "\r       \n";
	for (int i = 0; i<length; i++)
		cout << char(b[i]);
	cout << "\nNumber of tries: " << tries << endl;

	return 0;
}

