# oops-projact-details
**Introduction

The Library Management System is a C++ based software project developed using Object-Oriented Programming (OOP) concepts. The main purpose of this project is to manage the activities of a library in a simple, efficient, and organized way.

The system allows the librarian to add and display books, search for books, issue and return books, and maintain student/member records. It reduces manual work and makes the process of managing library records easier and faster.

This project demonstrates important OOP concepts such as classes, objects, encapsulation, constructors, inheritance, polymorphism, function overloading, and function overriding. C++ is used to develop the system because it provides strong support for object-oriented programming.

The Library Management System is useful for understanding how programming concepts can be applied to a real-world problem. It can also be extended in the future by adding features such as file handling, fine calculation, login authentication, due-date management, and database connectivity.

*code
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// ==================== BOOK CLASS ====================
class Book
{
private:
    int id;
    string title;
    string author;
    bool issued;

public:
    // Constructor
    Book(int bookId, string bookTitle, string bookAuthor)
    {
        id = bookId;
        title = bookTitle;
        author = bookAuthor;
        issued = false;
    }

    // Getters
    int getId()
    {
        return id;
    }

    string getTitle()
    {
        return title;
    }

    bool isIssued()
    {
        return issued;
    }

    // Issue book
    void issueBook()
    {
        issued = true;
    }

    // Return book
    void returnBook()
    {
        issued = false;
    }

    // Display book details
    void display()
    {
        cout << "\nBook ID     : " << id;
        cout << "\nTitle       : " << title;
        cout << "\nAuthor      : " << author;
        cout << "\nStatus      : ";

        if (issued)
            cout << "Issued";
        else
            cout << "Available";

        cout << "\n-----------------------------";
    }
};


// ==================== MEMBER CLASS ====================
class Member
{
protected:
    int memberId;
    string name;

public:
    // Constructor
    Member(int id, string memberName)
    {
        memberId = id;
        name = memberName;
    }

    virtual void display()
    {
        cout << "\nMember ID   : " << memberId;
        cout << "\nName        : " << name;
    }

    int getMemberId()
    {
        return memberId;
    }
};


// ==================== STUDENT CLASS ====================
class Student : public Member
{
private:
    string course;

public:
    // Constructor
    Student(int id, string studentName, string studentCourse)
        : Member(id, studentName)
    {
        course = studentCourse;
    }

    // Function overriding
    void display() override
    {
        cout << "\nMember ID   : " << memberId;
        cout << "\nName        : " << name;
        cout << "\nCourse      : " << course;
    }
};


// ==================== LIBRARY CLASS ====================
class Library
{
private:
    vector<Book> books;
    vector<Student> students;

public:

    // Add a book
    void addBook()
    {
        int id;
        string title, author;

        cout << "\nEnter Book ID: ";
        cin >> id;

        cin.ignore();

        cout << "Enter Book Title: ";
        getline(cin, title);

        cout << "Enter Author Name: ";
        getline(cin, author);

        books.push_back(Book(id, title, author));

        cout << "\nBook added successfully!\n";
    }


    // Display all books
    void displayBooks()
    {
        if (books.empty())
        {
            cout << "\nNo books available.\n";
            return;
        }

        cout << "\n========== ALL BOOKS ==========\n";

        for (int i = 0; i < books.size(); i++)
        {
            books[i].display();
        }
    }


    // Search book by ID
    void searchBook(int id)
    {
        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].getId() == id)
            {
                cout << "\nBook found!";
                books[i].display();
                return;
            }
        }

        cout << "\nBook not found.\n";
    }


    // Search book by title
    void searchBook(string title)
    {
        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].getTitle() == title)
            {
                cout << "\nBook found!";
                books[i].display();
                return;
            }
        }

        cout << "\nBook not found.\n";
    }


    // Issue a book
    void issueBook()
    {
        int id;

        cout << "\nEnter Book ID: ";
        cin >> id;

        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].getId() == id)
            {
                if (books[i].isIssued())
                {
                    cout << "\nBook is already issued.\n";
                }
                else
                {
                    books[i].issueBook();
                    cout << "\nBook issued successfully!\n";
                }

                return;
            }
        }

        cout << "\nBook not found.\n";
    }


    // Return a book
    void returnBook()
    {
        int id;

        cout << "\nEnter Book ID: ";
        cin >> id;

        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].getId() == id)
            {
                if (!books[i].isIssued())
                {
                    cout << "\nBook is already available.\n";
                }
                else
                {
                    books[i].returnBook();
                    cout << "\nBook returned successfully!\n";
                }

                return;
            }
        }

        cout << "\nBook not found.\n";
    }


    // Add student
    void addStudent()
    {
        int id;
        string name, course;

        cout << "\nEnter Student ID: ";
        cin >> id;

        cin.ignore();

        cout << "Enter Student Name: ";
        getline(cin, name);

        cout << "Enter Course: ";
        getline(cin, course);

        students.push_back(Student(id, name, course));

        cout << "\nStudent added successfully!\n";
    }


    // Display students
    void displayStudents()
    {
        if (students.empty())
        {
            cout << "\nNo students registered.\n";
            return;
        }

        cout << "\n========== STUDENT LIST ==========\n";

        for (int i = 0; i < students.size(); i++)
        {
            students[i].display();
            cout << "\n-----------------------------";
        }
    }
};


// ==================== MAIN FUNCTION ====================
int main()
{
    Library library;
    int choice;

    do
    {
        cout << "\n\n====================================";
        cout << "\n       LIBRARY MANAGEMENT SYSTEM";
        cout << "\n====================================";

        cout << "\n1. Add Book";
        cout << "\n2. Display Books";
        cout << "\n3. Search Book by ID";
        cout << "\n4. Search Book by Title";
        cout << "\n5. Issue Book";
        cout << "\n6. Return Book";
        cout << "\n7. Add Student";
        cout << "\n8. Display Students";
        cout << "\n9. Exit";

        cout << "\n\nEnter your choice: ";
        cin >> choice;

        if (choice == 1)
        {
            library.addBook();
        }
        else if (choice == 2)
        {
            library.displayBooks();
        }
        else if (choice == 3)
        {
            int id;

            cout << "\nEnter Book ID: ";
            cin >> id;

            library.searchBook(id);
        }
        else if (choice == 4)
        {
            string title;

            cin.ignore();

            cout << "\nEnter Book Title: ";
            getline(cin, title);

            library.searchBook(title);
        }
        else if (choice == 5)
        {
            library.issueBook();
        }
        else if (choice == 6)
        {
            library.returnBook();
        }
        else if (choice == 7)
        {
            library.addStudent();
        }
        else if (choice == 8)
        {
            library.displayStudents();
        }
        else if (choice == 9)
        {
            cout << "\nThank you for using Library Management System!\n";
        }
        else
        {
            cout << "\nInvalid choice! Please try again.\n";
        }

    } while (choice != 9);

    return 0;
}
