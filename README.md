# BookBorrower
Midterm Spring Boot Application

Midterm Project Assignment
Project Idea:
Building a Library Management System using Spring Framework with Spring Boot, Spring Data JPA, and Thymeleaf

Overview:
You have been tasked with building a web application that allows librarians to manage books and borrowers using the Spring Framework with Spring Boot, Spring Data JPA, and Thymeleaf. The application should have entity relationships between books and borrowers, and allow CRUD functionality for each entity.

Requirements:
The application should use the Spring Framework with Spring Boot and be built using Maven or Gradle. 

The application should include two entities: Book and Borrower with a many-to-many relationship. 

The Book entity should have the following fields: id, title, author, publisher, and ISBN. 

The Borrower entity should have the following fields: id, name, email, and phone number. 

The application should allow librarians to perform CRUD operations (Create, Read, Update, Delete) on each entity. 

The application should use Thymeleaf as the view template engine. 

The application should use Spring Data JPA to interact with the database. 

The application should use Hibernate as the ORM tool. 

The application should use MySQL or PostgreSQL as the database. 

The application should include appropriate error handling and validation. 

The application should include a user interface that is easy to use and responsive. 

The application should have a search functionality that allows librarians to search for books by title, author, or ISBN. 


----------------------------------------------------------------------------------------------------------------------------------------
# How to build this application:
1) Create spring project with dependencies (And you can see this dependencies in pom.xml file)
2) Create new package "modules" and 2 java files "Book" and "Borrower" inside it 
3) Inside "Book" class in "Book" file, add required fields (instance variables) -> id (Long)/title,author,publisher,ISBN (String) 
Then create Set<Borrower> (with HashSet initializing) and generate two constructors (one with all fields except the id and the set ,and other one empty), getter and setter (with all fields),(@override) equals() and hashCode() (only with id), and (@override toString() (with all fields)
4) Inside "Borrower" class in "Borrower" file, add requirenment fields (instance variables) -> id (Long)/name,email,phone_number (String)
Then create Set<Book> (with HashSet initializing) and generate two constructors (one with all fields except the id and the set ,and other one empty), getter and setter (with all fields), (@override) equals() and hashCode() (only with id), and (@override toString() (with all fields)
5) Add (@Entity) before "Book" class and "Borrower" class to make a relation to the data between them
6) Add (@Id @GeneratedValue) before the id in "Book" and "Borrower" classes 
7) In "Book" class add (@ManyToMany(mappedBy="books")) before the set
8) In "Borrower" class add (@ManyToMany) and (@JoinTable(name = "book_borrower", joinColumns = @JoinColumn(name = "book id"), inverseJoinColumns = @JoinColumn(name = "borrower_id")) before the set
9) Create new package "repositories", and 2 jave interfaces files inside it: "BookRepository" and "BorrowerRepository", and extends this two interfaces from (CrudRepository)
10) Create new package "bootstrap" and new java file "bootstrapData", and implement this class to (CommandLineRunner) function interface, and add (@Component) before the class
11) Inside "bootstrapData" class, call the repositories("BookRepository" and "BorrowerRepository") with private final value, then generate non-empty constructor for the repositories and generate implement "run" method with (@override) 
12) Inside "run" method, add a book and fill the required fields to the Book Set, also add a borrower and fill the required fields to the Borrower Set. Then connect between the sets using add(), getBook(), and getBorrower() methods. After that, save the changes in the repositories by save() method 
13) In "application.properties" file, enabled the h2 console and set the path (/h2) instead of (/h2-console) ,and instead of long url(which you can see it in the terminal), make it (jdbc:h2:mem:test) 
14) Now the request will send to the controller so create new package "controllers" and new java file inside it named "MainController", then assign the class as (@Controller)
15) Inside the "MainController" class, call the repositories and add (@Autowired) 
16) Inside the "MainController" class, create "showBookList" method (with 'model' parameter) and call (books) inside it and bookRepository will give the list of books by using addAttribute() and findAll() methodes, and add (@GetMapping)({"/add"/}) before the method 
17) CRUD : 
 *Create & add : create two methods (1- showBook (add(@GetMapping("/add")) before it, then give parameters:book and model, and finaly return the view "books")
                                     2- addBook (add(@PostMapping("/addBook")) before it, then give parameters:@Valid book and BindingResult, add in the body of the                                         method if there is any error return to "add" again, else save the new book in the repository and return back to "books"))

 *Edit & Update : create two methods (1- showUpdateForm (add (@GetMapping("/edit/{id}")) before it, then give parameters:@PathVariable id and Model, and find the book                                       by id in the repository, if there is no problem it will return to "update" which we will create it in the next method)
                                     2- updateBook (add (@PostMapping("/update/{id}")) before it, then give parameters :@PathVariable id,@Valid Book and BindingResult,                                      then save the changes in bookRepository and return back to "book"))
                                     
 *Delete : create method (deleteBook (add (@GetMapping("/delete/{id}")) before it, then give parameter : @PathVariable id, then add if statenment (if the book have borrower delete the borrower) then delete the book and go back to "books"
                                     
18) Create 3 new html files in "Templates" package : 1- books (call the thymeleaf, give title, create table, generate the rows and columns, set the thymeleaf to                                                            generate the elements from books model)
                                                     2- add (create a fields for each parameter to add new information and add a submit button to save the new book)
                                                     3- update (create a fields for each parameter to update and make edit n the information and add a submit button to                                                      save the new change)
                                                    
19) Do the same steps (16-17-18) for Borrower (just change the methods and files name)
20) Add naviagation bar in "books" and "borrowers" html files to make easier moving betwwen this two pages






----------------------------------------------------------------------------------------------------------------------------------------
# How to run the application :
go to (http://localhost:8080/books) to see the book list and move from navigation bar to see borrower list or by (http://localhost:8080/borrowers)
go to (http://localhost:8080/h2) with URL:(jdbc:h2:mem:test) to see the tables : BOOK, BORROWER, and BOOK_BORROWER
