# Module-7-Group-Project---Dictionary-Code
This is a GitHub Repository link to the Module 7 Group Project for PBSC COP2360-1 which consists of Carlos Gonzalez, Marcello Gonzalez, Octtavio Magarelli, Dimitri Finley, and Megan Camiel.

#include <iostream>
#include <string>
#include <vector>
#include <algorithm> // for sorting
using namespace std;
// Define a struct to represent a book with title and owner
struct Book {
  string title;
  string owner;
};
// Function prototypes for book catalog management
void display_catalog(const vector<Book>& catalog);
void add_book(vector<Book>& catalog);
void append_book(vector<Book>& catalog);
void remove_book(vector<Book>& catalog);
void sort_catalog(vector<Book>& catalog);
int main() {
  // Pre-populate the book catalog with initial entries
  vector<Book> book_catalog = {
      {"The Great Gatsby, Francis Scott Fitzgerald 1925", "Carlos"},
      {"The Old Man and the Sea, Ernest Hemingway 1952", "Marcello"},
      {"How Do You Live, Genzaburo Yoshino 1937", "Dimitri"},
      {"To Kill A Mockingbird, Harper Lee 1960", "Ottavio"},
      {"The Color Purple, Alice Walker 1982", "Megan"},
  
  };
  while (true) {
    // Menu for book catalog operations
    cout << "\nBook Catalog Menu:\n";
    cout << "1. Display Catalog\n";
    cout << "2. Add Book\n";
    cout << "3. Append Book\n";
    cout << "4. Remove Book\n";
    cout << "5. Sort Catalog\n";
    cout << "X. Exit\n";
    char choice;
    cin >> choice;
    switch (choice) {
      case '1':
        display_catalog(book_catalog);
        break;
      case '2':
        add_book(book_catalog);
        break;
      case '3':
        append_book(book_catalog);
        break;
      case '4':
        remove_book(book_catalog);
        break;
      case '5':
        sort_catalog(book_catalog);
        break;
      case 'X':
      case 'x':
        cout << "Exiting the program.\n";
        return 0;
      default:
        cout << "Invalid choice. Please try again.\n";
    }
  }
  return 0; // Shouldn't be reached due to the loop
}
// Function to display the book catalog using a range-based for loop (enumeration)
void display_catalog(const vector<Book>& catalog) {
  if (catalog.empty()) {
    cout << "The catalog is currently empty.\n";
    return;
  }
  cout << "Book Catalog:\n";
  for (const Book& book : catalog) {
    cout << book.owner << ": " << book.title << endl;
  }
}
// Function to add a new book and owner
void add_book(vector<Book>& catalog) {
  string owner, title;
  cout << "Enter the owner's name: ";
  getline(cin, owner); // Consider using cin.ignore() after to clear input buffer
  cout << "Enter the book title: ";
  getline(cin, title);
  Book new_book;
  new_book.owner = owner;
  new_book.title = title;
  catalog.push_back(new_book);
  cout << title << " has been added to the catalog for " << owner << endl;
}
// Function to append a book to an existing owner (enumeration not used here)
void append_book(vector<Book>& catalog) {
  string owner, title;
  cout << "Enter the owner's name to add a book: ";
  getline(cin, owner);
  bool found = false;
  for (Book& book : catalog) {
    if (book.owner == owner) {
      cout << "Enter the book title: ";
      getline(cin, title);
      book.title += ", " + title; // Append the new book title
      cout << title << " has been added to " << owner << "'s collection.\n";
      found = true;
      break;
    }
  }
  if (!found) {
    cout << "No book found for " << owner << " in the catalog.\n";
  }
}
// Function to remove a book by owner name using iterators (enumeration)
void remove_book(vector<Book>& catalog) {
  string owner;
  cout << "Enter the owner's name to remove their book: ";
  getline(cin, owner);
  // Find the book to remove
  auto it = find_if(catalog.begin(), catalog.end(),
                    [&owner](const Book& book) { return book.owner == owner; });
  // Remove the book if found
  if (it != catalog.end()) {
    catalog.erase(it);
    cout << "Book removed from the catalog.\n";
  } else {
    cout << "No book found for " << owner << " in the catalog.\n";
  }
}
// Function to sort the catalog by owner name (using a lambda expression)
void sort_catalog(vector<Book>& catalog) {
  sort(catalog.begin(), catalog.end(), [](const Book& a, const Book& b) {
    return a.owner < b.owner;
  });
  cout << "The catalog has been sorted by owner name.\n";
}
