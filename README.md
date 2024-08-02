Database Project for Biblioteca
The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Tools used: MySQL Workbench

Database description: I created a databese for a library conaining 5 tabels:Autori; Carti; Utlizatori; Imprumuturi; Recenzii.


Database Schema

Table Autori
Primary key: AutorID

Table Carti
Primary key: CarteID
Foreign key: AutorID referring to Autori(AutorID)

Table Utilizatori
Primary key: UtilizatorID

Table Imprumuturi
Primary key: ImprumutID
Foreign key: UtilizatorID referring to Utilizatori(UtilizatorID)
Foreign key: CarteID referring to Carti(CarteID)

Table Recenzii
Primary key: RecenzieID
Foreign key: CarteID referring to Carti(CarteID)
Foreign key: UtilizatorID referring to Utilizatori(UtilizatorID)

You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.
The tables are connected in the following way:

**Carti ** is connected with **Autori ** through a 1:1 relationship which was implemented through Autori.AutorID as a primary key and Carti.AutorID as a foreign key

**Imprumuturi ** is connected with **Utilizatori ** through a 1:1 relationship which was implemented through Utilizatori.UtilizatorID as a primary key and Imprumuturi.UtilizatorID as a foreign key

**Imprumuturi ** is connected with **Carti ** through a 1:1 relationship which was implemented through  Carti.CarteID as a primary key and Imprumuturi.CarteID as a foreign key

**Recenzii ** is connected with **Utilizatori ** through a 1:1 relationship which was implemented through Utilizatori.UtilizatorID as a primary key and Recenzii.UtilizatorID as a foreign key

**Recenzii ** is connected with **Carti** through a 1:1 relationship which was implemented through Carti.CarteID as a primary key and Recenzii.CarteID as a foreign key


Database Queries

DDL (Data Definition Language)
The following instructions were written in the scope of CREATING the structure of the database (CREATE INSTRUCTIONS)

create database biblioteca;
use biblioteca;

CREATE TABLE Autori (
    AutorID INT PRIMARY KEY AUTO_INCREMENT,
    Nume VARCHAR(100) NOT NULL,
    Prenume VARCHAR(100) NOT NULL,
    DataNasterii DATE
);

CREATE TABLE Carti (
    CarteID INT PRIMARY KEY AUTO_INCREMENT,
    Titlu VARCHAR(200) NOT NULL,
    Gen VARCHAR(100),
    AnPublicare YEAR,
    AutorID INT,
    FOREIGN KEY (AutorID) REFERENCES Autori(AutorID)
);

CREATE TABLE Utilizatori (
    UtilizatorID INT PRIMARY KEY AUTO_INCREMENT,
    Nume VARCHAR(100) NOT NULL,
    Prenume VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE Imprumuturi (
    ImprumutID INT PRIMARY KEY AUTO_INCREMENT,
    UtilizatorID INT,
    CarteID INT,
    DataImprumut DATE,
    DataReturnare DATE,
    FOREIGN KEY (UtilizatorID) REFERENCES Utilizatori(UtilizatorID),
    FOREIGN KEY (CarteID) REFERENCES Carti(CarteID)
);

CREATE TABLE Recenzii (
    RecenzieID INT PRIMARY KEY AUTO_INCREMENT,
    CarteID INT,
    UtilizatorID INT,
    Rating INT CHECK (Rating BETWEEN 1 AND 5),
    Comentariu TEXT,
    DataRecenzie DATE,
    FOREIGN KEY (CarteID) REFERENCES Carti(CarteID),
    FOREIGN KEY (UtilizatorID) REFERENCES Utilizatori(UtilizatorID)
);

DML (Data Manipulation Language)
In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase.

Below you can find all the insert instructions that were created in the scope of this project:

INSERT INTO Autori (Nume, Prenume, DataNasterii) VALUES
('Rowling', 'J.K.', '1965-07-31'),
('Tolkien', 'J.R.R.', '1892-01-03'),
('Martin', 'George R.R.', '1948-09-20'),
('Austen', 'Jane', '1775-12-16'),
('Shakespeare', 'William', '1564-04-26'),
('Orwell', 'George', '1903-06-25'),
('Hemingway', 'Ernest', '1899-07-21'),
('Fitzgerald', 'F. Scott', '1896-09-24'),
('Dickens', 'Charles', '1812-02-07'),
('Huxley', 'Aldous', '1894-07-26'),
('Verne', 'Jules', '1828-02-08'),
('Dostoevsky', 'Fyodor', '1821-11-11'),
('Kafka', 'Franz', '1883-07-03'),
('Joyce', 'James', '1882-02-02'),
('Poe', 'Edgar Allan', '1809-01-19'),
('Homer', 'S', '800-01-01'),
('Hugo', 'Victor', '1802-02-26'),
('Steinbeck', 'John', '1902-02-27'),
('Christie', 'Agatha', '1890-09-15'),
('King', 'Stephen', '1947-09-21');

INSERT INTO Carti (Titlu, Gen, AnPublicare, AutorID) VALUES
('Harry Potter and the Philosopher\'s Stone', 'Fantasy', 1997, 1),
('Harry Potter and the Chamber of Secrets', 'Fantasy', 1998, 1),
('The Hobbit', 'Fantasy', 1937, 2),
('The Fellowship of the Ring', 'Fantasy', 1954, 2),
('A Game of Thrones', 'Fantasy', 1996, 3),
('A Clash of Kings', 'Fantasy', 1998, 3),
('Pride and Prejudice', 'Romance', 1951, 4),
('1984', 'Dystopian', 1949, 6),
('Animal Farm', 'Satire', 1945, 6),
('The Great Gatsby', 'Tragedy', 1925, 8),
('Brave New World', 'Dystopian', 1932, 10),
('Moby Dick', 'Adventure', 1940, 7),
('War and Peace', 'Historical', 1969, 12),
('The Odyssey', 'Epic', 1920, 16),
('Les Misérables', 'Historical', 1962, 17),
('The Grapes of Wrath', 'Historical', 1939, 18),
('Murder on the Orient Express', 'Mystery', 1934, 19),
('The Shining', 'Horror', 1977, 20),
('It', 'Horror', 1986, 20),
('The Catcher in the Rye', 'Literary', 1951, 14);

INSERT INTO Utilizatori (Nume, Prenume, Email) VALUES
('Popescu', 'Ion', 'ion.popescu@example.com'),
('Ionescu', 'Maria', 'maria.ionescu@example.com'),
('Georgescu', 'Andrei', 'andrei.georgescu@example.com'),
('Dumitrescu', 'Elena', 'elena.dumitrescu@example.com'),
('Mihai', 'Vasile', 'vasile.mihai@example.com'),
('Constantinescu', 'Adriana', 'adriana.constantinescu@example.com'),
('Radu', 'Alexandru', 'alexandru.radu@example.com'),
('Stan', 'Ana', 'ana.stan@example.com'),
('Marin', 'Daniel', 'daniel.marin@example.com'),
('Tudor', 'Cristina', 'cristina.tudor@example.com'),
('Nicolae', 'Gabriel', 'gabriel.nicolae@example.com'),
('Iliescu', 'Simona', 'simona.iliescu@example.com'),
('Barbu', 'Catalin', 'catalin.barbu@example.com'),
('Enache', 'Laura', 'laura.enache@example.com'),
('Serban', 'Mihai', 'mihai.serban@example.com'),
('Nita', 'Raluca', 'raluca.nita@example.com'),
('Dragomir', 'Paul', 'paul.dragomir@example.com'),
('Sandu', 'Oana', 'oana.sandu@example.com'),
('Dobre', 'Cosmin', 'cosmin.dobre@example.com'),
('Gheorghe', 'Irina', 'irina.gheorghe@example.com');

INSERT INTO Imprumuturi (UtilizatorID, CarteID, DataImprumut, DataReturnare) VALUES
(1, 161, '2024-01-15', '2024-02-15'),
(2, 162, '2024-01-20', NULL),
(3, 163, '2024-02-01', '2024-02-21'),
(4, 164, '2024-02-05', '2024-03-01'),
(5, 165, '2024-03-10', '2024-03-25'),
(6, 166, '2024-03-15', NULL),
(7, 167, '2024-04-01', '2024-04-20'),
(8, 168, '2024-04-10', '2024-04-30'),
(9, 169, '2024-05-01', '2024-05-20'),
(10, 170, '2024-05-15', NULL),
(11, 171, '2024-06-01', '2024-06-15'),
(12, 172, '2024-06-10', '2024-06-25'),
(13, 173, '2024-07-01', '2024-07-20'),
(14, 174, '2024-07-10', '2024-07-30'),
(15, 175, '2024-08-01', '2024-08-20'),
(16, 176, '2024-08-10', '2024-08-30'),
(17, 177, '2024-09-01', '2024-09-20'),
(18, 178, '2024-09-10', '2024-09-30'),
(19, 179, '2024-10-01', '2024-10-20'),
(20, 180, '2024-10-10', '2024-10-30');

INSERT INTO Recenzii (CarteID, UtilizatorID, Rating, Comentariu, DataRecenzie) VALUES
(161, 1, 5, 'Amazing book!', '2024-01-25'),
(162, 2, 4, 'Great read, but a bit slow at times.', '2024-01-30'),
(163, 3, 5, 'An absolute classic!', '2024-02-15'),
(164, 4, 5, 'Fantastic!', '2024-02-25'),
(165, 5, 4, 'Really enjoyed it.', '2024-03-20'),
(166, 6, 3, 'Good, but not as good as the first one.', '2024-03-30'),
(167, 7, 5, 'A must-read for everyone.', '2024-04-15'),
(168, 8, 4, 'Thought-provoking.', '2024-04-25'),
(169, 9, 5, 'Could not put it down!', '2024-05-10'),
(170, 10, 3, 'Interesting, but a bit dated.', '2024-05-20'),
(171, 11, 5, 'Incredible storytelling.', '2024-06-05'),
(172, 12, 4, 'Very enjoyable.', '2024-06-15'),
(173, 13, 5, 'A work of genius.', '2024-07-05'),
(174, 14, 5, 'Timeless.', '2024-07-15'),
(175, 15, 4, 'Highly recommend.', '2024-08-05'),
(176, 16, 3, 'Not my cup of tea.', '2024-08-15'),
(177, 17, 5, 'Masterpiece.', '2024-09-05'),
(178, 18, 4, 'Very good.', '2024-09-15'),
(179, 19, 5, 'Outstanding.', '2024-10-05'),
(180, 20, 4, 'Solid read.', '2024-10-15');


DQL (Data Query Language)

In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

SELECT * FROM Carti;

SELECT * FROM Carti WHERE Gen = 'Fantasy';

SELECT * FROM Utilizatori WHERE Nume = 'Ionescu' OR Nume = 'Popescu';

SELECT Utilizatori.Nume, Utilizatori.Prenume, Imprumuturi.DataReturnare
FROM Utilizatori
INNER JOIN Imprumuturi ON Utilizatori.UtilizatorID = Imprumuturi.UtilizatorID
WHERE YEAR(Imprumuturi.DataReturnare) = 2024;

SELECT Gen, COUNT(*) AS NumarCarti FROM Carti GROUP BY Gen;

SELECT Gen, COUNT(*) AS NumarCarti FROM Carti GROUP BY Gen HAVING COUNT(*) > 1;

SELECT Imprumuturi.ImprumutID, Utilizatori.Nume, Utilizatori.Prenume
FROM Imprumuturi
LEFT JOIN Utilizatori ON Imprumuturi.UtilizatorID = Utilizatori.UtilizatorID;

SELECT Carti.Titlu, Imprumuturi.DataImprumut, Imprumuturi.DataReturnare
FROM Carti
RIGHT JOIN Imprumuturi ON Carti.CarteID = Imprumuturi.CarteID;

SELECT * FROM Carti ORDER BY AnPublicare DESC;

SELECT Utilizatori.Nume, Utilizatori.Prenume
FROM Utilizatori
WHERE UtilizatorID IN (
    SELECT Imprumuturi.UtilizatorID
    FROM Imprumuturi
    INNER JOIN Carti ON Imprumuturi.CarteID = Carti.CarteID
    WHERE Carti.AutorID = (SELECT AutorID FROM Autori WHERE Nume = 'Tolkien')
);

SELECT 
    a.Nume AS NumeAutor, 
    a.Prenume AS PrenumeAutor, 
    COUNT(c.CarteID) AS NumărCărți
FROM 
    Autori a
LEFT JOIN 
    Carti c ON a.AutorID = c.AutorID
GROUP BY 
    a.AutorID;
    
    SELECT 
    c.Titlu AS TitluCarte, 
    AVG(r.Rating) AS RatingMediu
FROM 
    Carti c
INNER JOIN 
    Recenzii r ON c.CarteID = r.CarteID
GROUP BY 
    c.CarteID
HAVING 
    AVG(r.Rating) >= 4;
    
