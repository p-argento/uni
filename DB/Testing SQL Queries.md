On https://onecompiler.com/mysql/427ufrn4q

```mysql
-- create
CREATE TABLE Students (
  Sid INTEGER PRIMARY KEY,
  Name TEXT,
  Surname TEXT
);

CREATE TABLE Teachers (
  Tid INTEGER PRIMARY KEY,
  Name TEXT,
  Surname TEXT
);

CREATE TABLE Exams (
  Eid INTEGER PRIMARY KEY,
  Date TEXT,
  Year TEXT,
  Subject TEXT,
  Grade INTEGER,
  Sid INTEGER,
  FOREIGN KEY (Sid) REFERENCES Students(Sid),
  Tid INTEGER,
  FOREIGN KEY (Tid) REFERENCES Teachers(Tid)
);

-- insert
INSERT INTO Students VALUES (0001, 'Mario', 'Rossi');
INSERT INTO Students VALUES (0002, 'Guido', 'Guidi');
INSERT INTO Students VALUES (0003, 'Maria', 'Bianchi');

INSERT INTO Teachers VALUES (1001, 'Giorgio', 'Ghelli');
INSERT INTO Teachers VALUES (1002, 'Riccardo', 'Guidotti');
INSERT INTO Teachers VALUES (1003, 'Salvatore', 'Ruggieri');

INSERT INTO Exams VALUES (11,'0303' ,'2024' ,'DB',30, 0001,1001);
INSERT INTO Exams VALUES (11,'0303' ,'2024' ,'DM',28, 0001,1001);
INSERT INTO Exams VALUES (11,'0303' ,'2024' ,'ST',27, 0001,1001);

-- fetch 
SELECT * FROM Exams;


```

