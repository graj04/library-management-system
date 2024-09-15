#include <iostream>
#include <string>
#include <vector>
#include <stack>
#include <algorithm>

class Book {
private:
    int id;
    std::string title;
    std::string author;
    bool isIssued;
    std::string studentName;

public:
    // Constructor
    Book(int id, const std::string& title, const std::string& author)
        : id(id), title(title), author(author), isIssued(false), studentName("") {}

    // Getters and Setters
    int getId() const { return id; }
    std::string getTitle() const { return title; }
    std::string getAuthor() const { return author; }
    bool getStatus() const { return isIssued; }
    std::string getStudentName() const { return studentName; }

    void setId(int id) { this->id = id; }
    void setTitle(const std::string& title) { this->title = title; }
    void setAuthor(const std::string& author) { this->author = author; }
    void issueBook(const std::string& studentName) { 
        isIssued = true; 
        this->studentName = studentName;
    }
    void returnBook() { 
        isIssued = false; 
        studentName = ""; 
    }

    // Display details
    void displayDetails() const {
        std::cout << "ID: " << id << "\nTitle: " << title << "\nAuthor: " << author 
                  << "\nStatus: " << (isIssued ? "Issued to " + studentName : "Available") << std::endl;
    }
};

class Library {
private:
    std::vector<Book> books;
    std::stack<Book> issuedBooks;  // For managing issued books

public:
    // Add new book
    void addBook(const Book& book) {
        books.push_back(book);
    }

    // Search for a book by title or ID
    Book* searchBookById(int id) {
        for (auto& book : books) {
            if (book.getId() == id) {
                return &book;
            }
        }
        return nullptr;
    }

    Book* searchBookByTitle(const std::string& title) {
        for (auto& book : books) {
            if (book.getTitle() == title) {
                return &book;
            }
        }
        return nullptr;
    }

    // Issue a book
    void issueBook(int id, const std::string& studentName) {
        Book* book = searchBookById(id);
        if (book && !book->getStatus()) {
            book->issueBook(studentName);
            issuedBooks.push(*book);
            std::cout << "Book issued successfully.\n";
        } else {
            std::cout << "Book not available for issue.\n";
        }
    }

    // Return a book
    void returnBook(int id) {
        Book* book = searchBookById(id);
        if (book && book->getStatus()) {
            book->returnBook();
            issuedBooks.pop();
            std::cout << "Book returned successfully.\n";
        } else {
            std::cout << "Book not found or not issued.\n";
        }
    }

    // List all books
    void listAllBooks() {
        std::sort(books.begin(), books.end(), [](const Book& a, const Book& b) {
            return a.getId() < b.getId();
        });
        for (const auto& book : books) {
            book.displayDetails();
        }
    }

    // Delete a book
    void deleteBook(int id) {
        books.erase(std::remove_if(books.begin(), books.end(), [id](const Book& book) {
            return book.getId() == id;
        }), books.end());
        std::cout << "Book deleted successfully.\n";
    }
};

void displayMenu() {
    std::cout << "Library Management System\n";
    std::cout << "1. Add New Book\n";
    std::cout << "2. Search for a Book\n";
    std::cout << "3. Issue a Book\n";
    std::cout << "4. Return a Book\n";
    std::cout << "5. List All Books\n";
    std::cout << "6. Delete a Book\n";
    std::cout << "7. Exit\n";
    std::cout << "Choose an option: ";
}

int main() {
    Library library;
    int choice, id;
    std::string title, author, studentName;

    while (true) {
        displayMenu();
        std::cin >> choice;

        switch (choice) {
            case 1:
                std::cout << "Enter Book ID: ";
                std::cin >> id;
                std::cin.ignore();
                std::cout << "Enter Book Title: ";
                std::getline(std::cin, title);
                std::cout << "Enter Book Author: ";
                std::getline(std::cin, author);
                library.addBook(Book(id, title, author));
                break;
            case 2:
                std::cout << "Enter Book ID to search: ";
                std::cin >> id;
                if (Book* book = library.searchBookById(id)) {
                    book->displayDetails();
                } else {
                    std::cout << "Book not found.\n";
                }
                break;
            case 3:
                std::cout << "Enter Book ID to issue: ";
                std::cin >> id;
                std::cin.ignore();
                std::cout << "Enter Student Name: ";
                std::getline(std::cin, studentName);
                library.issueBook(id, studentName);
                break;
            case 4:
                std::cout << "Enter Book ID to return: ";
                std::cin >> id;
                library.returnBook(id);
                break;
            case 5:
                library.listAllBooks();
                break;
            case 6:
                std::cout << "Enter Book ID to delete: ";
                std::cin >> id;
                library.deleteBook(id);
                break;
            case 7:
                return 0;
            default:
                std::cout << "Invalid option. Please try again.\n";
        }
    }
}
