
# Database Design for Online Bookstore

# Team Members and Their Roles : 

1: Harsh Kirtibhai Patel (8972238) (Database Design and Schema Creation)

2: Rahi Patel(8975566) (DDL/DML Scripts)

3: Mohammed Shadab Uddin (8975367) (SQL Queries)

4: Iqbal singh(8331548) (TypeScript Interface)


## Authors Table

```sql
CREATE TABLE Authors (
    AuthorID SERIAL PRIMARY KEY,
    Name VARCHAR(100),
    Bio TEXT
);
```

## Customers Table

```sql
CREATE TABLE Customers (
    CustomerID SERIAL PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100) UNIQUE,
    TotalSpent DECIMAL(10, 2)
);
```

## Publishers Table

```sql
CREATE TABLE Publishers (
    PublisherID SERIAL PRIMARY KEY,
    Name VARCHAR(100)
);
```

## Genres Table

```sql
CREATE TABLE Genres (
    GenreID SERIAL PRIMARY KEY,
    Name VARCHAR(50)
);
```

## Books Table

```sql
CREATE TABLE Books (
    BookID SERIAL PRIMARY KEY,
    Title VARCHAR(100),
    AuthorID INT REFERENCES Authors(AuthorID),
    PublisherID INT REFERENCES Publishers(PublisherID),
    GenreID INT REFERENCES Genres(GenreID),
    PublishedDate DATE,
    Rating DECIMAL(3, 2)
);
```

## Reviews Table

```sql
CREATE TABLE Reviews (
    ReviewID SERIAL PRIMARY KEY,
    BookID INT REFERENCES Books(BookID),
    CustomerID INT REFERENCES Customers(CustomerID),
    ReviewText TEXT,
    Rating INT,
    ReviewDate DATE
);
```

## Sales Table

```sql
CREATE TABLE Sales (
    SaleID SERIAL PRIMARY KEY,
    BookID INT REFERENCES Books(BookID),
    CustomerID INT REFERENCES Customers(CustomerID),
    SaleDate DATE,
    Price DECIMAL(10, 2)
);
```

## Sample Data Insertion

### Authors Table

```sql
INSERT INTO Authors (Name, Bio) VALUES 
('J.K. Rowling', 'British author, best known for the Harry Potter series'),
('George R.R. Martin', 'American novelist and short story writer, best known for A Song of Ice and Fire series');
```

### Customers Table

```sql
INSERT INTO Customers (Name, Email, TotalSpent) VALUES 
('Harsh Patel', 'harsh@example.com', 200.00),
('shadd', 'shad@example.com', 150.00);
```

### Publishers Table

```sql
INSERT INTO Publishers (Name) VALUES 
('Bloomsbury'),
('Bantam Books');
```

### Genres Table

```sql
INSERT INTO Genres (Name) VALUES 
('Fantasy'),
('Science Fiction');
```

### Books Table

```sql
INSERT INTO Books (Title, AuthorID, PublisherID, GenreID, PublishedDate, Rating) VALUES 
('Harry Potter and the Philosopher''s Stone', 1, 1, 1, '1997-06-26', 4.8),
('A Game of Thrones', 2, 2, 1, '1996-08-06', 4.7);
```

### Reviews Table

```sql
INSERT INTO Reviews (BookID, CustomerID, ReviewText, Rating, ReviewDate) VALUES 
(1, 1, 'Amazing book!', 5, '2024-01-01'),
(2, 2, 'Very interesting', 4, '2024-01-02');
```

### Sales Table

```sql
INSERT INTO Sales (BookID, CustomerID, SaleDate, Price) VALUES 
(1, 1, '2023-06-30', 20.00),
(2, 2, '2023-07-01', 15.00);
```

## CRUD Operations

### Create

```sql
INSERT INTO Books (Title, AuthorID, PublisherID, GenreID, PublishedDate, Rating) 
VALUES ('New Book', 1, 1, 1, '2024-01-01', 4.0);
```

### Read

```sql
SELECT * FROM Books;
```

### Update

```sql
UPDATE Books 
SET Rating = 4.5 
WHERE BookID = 1;
```

### Delete

```sql
DELETE FROM Books 
WHERE BookID = 3;
```

## Queries

### Power Writers

```sql

SELECT Authors.Name, COUNT(Books.BookID) AS BookCount
FROM Authors
JOIN Books ON Authors.AuthorID = Books.AuthorID
WHERE Books.GenreID = 1 AND Books.PublishedDate >= (CURRENT_DATE - INTERVAL '3 YEARS')
GROUP BY Authors.Name
HAVING COUNT(Books.BookID) > 3;
```

### Loyal Customers

```sql

SELECT Customers.Name, Customers.TotalSpent
FROM Customers
WHERE Customers.TotalSpent > 100;
```

### Well-Reviewed Books

```sql
SELECT Books.Title, Books.Rating
FROM Books
WHERE Books.Rating > (SELECT AVG(Rating) FROM Books);
```

### Most Popular Genre by Sales

```sql
SELECT Genres.Name, COUNT(Sales.SaleID) AS SalesCount
FROM Sales
JOIN Books ON Sales.BookID = Books.BookID
JOIN Genres ON Books.GenreID = Genres.GenreID
GROUP BY Genres.Name
ORDER BY SalesCount DESC
LIMIT 1;
```

### 10 Most Recent Reviews

```sql
SELECT Customers.Name, Reviews.ReviewText, Reviews.ReviewDate
FROM Reviews
JOIN Customers ON Reviews.CustomerID = Customers.CustomerID
ORDER BY Reviews.ReviewDate DESC
LIMIT 10;
```

## TypeScript Interface

```typescript
interface Book {
    BookID: number;
    Title: string;
    AuthorID: number;
    PublisherID: number;
    GenreID: number;
    PublishedDate: string; 
    Rating: number;
}


function updateBookRating(bookID: number, newRating: number): void {
    
    console.log(`Updating book ID ${bookID} with new rating ${newRating}`);
}


const book: Book = {
    BookID: 1,
    Title: "Harry Potter and the Philosopher's Stone",
    AuthorID: 1,
    PublisherID: 1,
    GenreID: 1,
    PublishedDate: "1997-06-26",
    Rating: 4.8
};

updateBookRating(book.BookID, 4.5);
```

# Github links: 

1. HarshPatel777

2. Rahipatel11

3. shady-afkk

4. isingh1548

5. https://github.com/HarshPatel777/DatabaseMidterm
