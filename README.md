//тема проекта "Система учета библиотечных книг"
#include <iostream>
#include <stdio.h>


using namespace std;

struct book {
	char namebook[50];
	char avtor[50];
	int year;
};

struct reader {
	char name[20];
	char familia[20];
	int nomber_bilets;
	int counts_books;
};


void bubble_sort(book* arr, int MAX_BOOKS) {
	for (int i = 0; i < MAX_BOOKS; i++) {
		for (int j = i + 1; j < MAX_BOOKS; ++j) {
			if ((arr + i) -> year > (arr + j) -> year) {
				book temp = *(arr + i);
				*(arr + i) = *(arr + j);
				*(arr + j) = temp;
			}
		}
	}
}


void print_sort(book* arr, int MAX_BOOKS) {
	for (int i = 0; i < MAX_BOOKS; i++) {
		cout << "Years of publishing books in order: " << (arr + i) -> year << endl;
	}
}



void AddBook(int numbooks, int MAX_BOOKS, book* books) {
	if (numbooks < MAX_BOOKS) {
		cout << "Input namebook: ";
		cin >> books[numbooks].namebook;
		cout << "Input name avtor: ";
		cin >> books[numbooks].avtor;
		cout << "Input the year of publication of the book: ";
		cin >> books[numbooks].year;
		numbooks++;
		cout << "You have successfully entered book information!" << endl;
	}
	else {
		cout << "Library is full, can't add more books!" << endl;
	}
}


void AddReader(int numreaders, int MAX_READERS, reader* readers) {
	if (numreaders < MAX_READERS) {
		cout << "Enter  the reader's name: ";
		cin >> readers[numreaders].name;
		cout << "Enter  the reader's last name: ";
		cin >> readers[numreaders].familia;
		cout << "Enter your library card number: ";
		cin >> readers[numreaders].nomber_bilets;
		cout << "Enter the number of books the reader has: ";
		cin >> readers[numreaders].counts_books;
		numreaders++;
		cout << "You have successfully entered reader information!" << endl;
	}
	else {
		cout << "Library is full, can't add more readers!" << endl;
	}
}


void findBook(char* searchs, int numbooks, book* books) {
	for (int i = 0; i < numbooks; i++) {
		if ((books + i) -> namebook == searchs || (books + i) -> avtor == searchs) {
			cout << "Book found!" << endl;
			cout << "Book title: " << (books + i) -> namebook << endl;
			cout << "Avtor: " << (books + i) -> avtor << endl;
			cout << "Year of publication of the book: " << (books + i) -> year << endl;
			return;
		}
	}
	cout << "Book not found" << endl;
}


void findReader(int cardnumber, int numreaders, reader* readers) {
	for (int i = 0; i < numreaders; i++) {
		if (readers[i].nomber_bilets == cardnumber) {
			cout << "Reader found!" << endl;
			cout << "Name and last name: " << readers[i].name << " " << readers[i].familia << endl;
			cout << "Number of books on hand: " << readers[i].counts_books << endl;
			return;
		}
	}
	cout << "Reader not found!" << endl;
}


int main() {

	const int MAX_BOOKS = 50;
	const int MAX_READERS = 50;
	struct book books[MAX_BOOKS];
	struct reader readers[MAX_READERS];
	int numbooks = 0;
	int numreaders = 0;
	int choice = 0;

	int countsb = 0;
	cout << "Enter the counts books(up to 50): ";
	cin >> countsb;
	while (countsb > 50) {
		cout << "Enter the counts books try again! UP TO 50: ";
		cin >> countsb;
	}
	
	int countsr = 0;
	cout << "Enter the counts readers(up to 50): ";
	cin >> countsr;
	while (countsr > 50) {
		cout << "Enter the counts readers try again! UP TO 50: ";
		cin >> countsr;
	}
	cout << " " << endl;

	do {
		cout << "****************";
		cout << "\nLIBRARY MANAGER\n";
		cout << "****************" << endl;
		cout << " " << endl;
		cout << "!!!!!For convenience, enter in order!!!!!" << endl;
		cout << "1. Adding a book" << endl;
		cout << "2. Adding a reader" << endl;
		cout << "3. Found a book" << endl;
		cout << "4. Found a reader" << endl;
		cout << "5. Exit..." << endl;
		cout << "Enter your choice: ";
		cin >> choice;


		char Artur[50];
		switch (choice) {
		case 1:
			AddBook(numbooks, MAX_BOOKS, books);
			break;
		case 2:
			AddReader(numreaders, MAX_READERS, readers);
			break;
		case 3:
			cout << "Enter name book or name/last name avtor: ";
			cin >> Artur;
			findBook(Artur, numbooks, books);
			break;
		case 4:
			int cardnumber;
			cout << "Enter your library card number: ";
			cin >> cardnumber;
			findReader(cardnumber, numreaders, readers);
			break;
		case 5:
			cout << "Exit out programm..." << endl;
		default:
			cout << "Wrong choice. Try again. Up to 5." << endl;
		}
	}
	while (choice != 5);

	bubble_sort(books, countsb);
	print_sort(books, countsb);

	return 0;
}
