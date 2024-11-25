# hospital-management
--patient table
CREATE TABLE Patient (
    P_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Gender VARCHAR(10),
    Age INT,
    DOB DATE,
    Mob_No VARCHAR(15)
);

INSERT INTO Patient VALUES 
(101, 'Alice Johnson', 'Female', 30, '1994-01-05', '1234567890'),
(102, 'Bob Smith', 'Male', 40, '1984-03-15', '0987654321'),
(103, 'Cathy Brown', 'Female', 29, '1995-07-20', '2233445566'),
(104, 'David Wilson', 'Male', 52, '1971-12-01', '3344556677'),
(105, 'Eva Adams', 'Female', 60, '1963-02-25', '4455667788'),
(106, 'Frank White', 'Male', 45, '1978-09-10', '5566778899'),
(107, 'Grace Taylor', 'Female', 38, '1985-11-30', '6677889900'),
(108, 'Henry Johnson', 'Male', 24, '1999-06-12', '7788990011'),
(109, 'Ivy Lee', 'Female', 50, '1973-05-18', '8899001122'),
(110, 'Jack Harris', 'Male', 30, '1994-04-23', '9900112233');

-- 2. Doctor Table
CREATE TABLE Doctor (
    D_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Mob_No VARCHAR(15),
    Address VARCHAR(100),
    E_ID INT,
    State VARCHAR(50),
    City VARCHAR(50),
    Pin_No VARCHAR(10),
    Dept VARCHAR(50),
    Qualification VARCHAR(50)
);

INSERT INTO Doctor VALUES 
(201, 'Dr. John Doe', '1234567890', '123 Main St', 101, 'TX', 'Houston', '77001', 'Cardiology', 'MD'),
(202, 'Dr. Jane Smith', '0987654321', '456 Elm St', 102, 'FL', 'Miami', '33101', 'Neurology', 'MD'),
(203, 'Dr. Steve White', '2233445566', '789 Pine St', 103, 'CA', 'Los Angeles', '90001', 'Orthopedics', 'DO'),
(204, 'Dr. Anna Green', '3344556677', '321 Oak St', 104, 'IL', 'Chicago', '60601', 'Dermatology', 'MD'),
(205, 'Dr. Paul Blue', '4455667788', '654 Maple St', 105, 'NY', 'New York', '10001', 'Oncology', 'MD'),
(206, 'Dr. Susan Grey', '5566778899', '987 Cedar St', 106, 'MA', 'Boston', '02101', 'Psychiatry', 'MD'),
(207, 'Dr. Richard Red', '6677889900', '123 Birch St', 107, 'GA', 'Atlanta', '30301', 'Surgery', 'DO'),
(208, 'Dr. Emily Yellow', '7788990011', '456 Spruce St', 108, 'NV', 'Las Vegas', '89101', 'Pediatrics', 'MD'),
(209, 'Dr. Peter Orange', '8899001122', '789 Walnut St', 109, 'OH', 'Columbus', '43201', 'Radiology', 'MD'),
(210, 'Dr. Linda Pink', '9900112233', '321 Cherry St', 110, 'WA', 'Seattle', '98101', 'Pathology', 'DO');

-- 3. Nurse Table
CREATE TABLE Nurse (
    N_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    State VARCHAR(50),
    City VARCHAR(50),
    Pin_No VARCHAR(10),
    Qualification VARCHAR(50)
);

INSERT INTO Nurse VALUES
(301, 'Nurse Emma Brown', 'TX', 'Houston', '77001', 'BSN'),
(302, 'Nurse Daniel Grey', 'FL', 'Miami', '33101', 'RN'),
(303, 'Nurse Olivia Green', 'NY', 'New York', '10001', 'LPN'),
(304, 'Nurse Noah White', 'CA', 'Los Angeles', '90001', 'RN'),
(305, 'Nurse Ava Black', 'IL', 'Chicago', '60601', 'BSN'),
(306, 'Nurse Liam Blue', 'GA', 'Atlanta', '30301', 'LPN'),
(307, 'Nurse Sophia Violet', 'NV', 'Las Vegas', '89101', 'RN'),
(308, 'Nurse Lucas Red', 'MA', 'Boston', '02101', 'BSN'),
(309, 'Nurse Mia Orange', 'FL', 'Miami', '33101', 'LPN'),
(310, 'Nurse Mason Grey', 'TX', 'Houston', '77001', 'RN');

-- 4. Rooms Table
CREATE TABLE Rooms (
    R_ID INT PRIMARY KEY,
    Type VARCHAR(50),
    Capacity INT,
    Availability BOOLEAN
);

INSERT INTO Rooms VALUES 
(1, 'Private', 1, TRUE),
(2, 'Semi-private', 2, TRUE),
(3, 'General', 4, FALSE),
(4, 'ICU', 1, TRUE),
(5, 'Pediatrics', 2, TRUE),
(6, 'Maternity', 2, TRUE),
(7, 'Surgical', 1, FALSE),
(8, 'Recovery', 2, TRUE),
(9, 'Isolation', 1, TRUE),
(10, 'Emergency', 4, TRUE);

-- 5. Records Table
CREATE TABLE Records (
    Record_No INT PRIMARY KEY,
    App_No INT,
    P_ID INT,
    R_ID INT,
    FOREIGN KEY (P_ID) REFERENCES Patient(P_ID),
    FOREIGN KEY (R_ID) REFERENCES Rooms(R_ID)
);

INSERT INTO Records VALUES 
(1, 1001, 101, 1),
(2, 1002, 102, 2),
(3, 1003, 103, 3),
(4, 1004, 104, 4),
(5, 1005, 105, 5),
(6, 1006, 106, 6),
(7, 1007, 107, 7),
(8, 1008, 108, 8),
(9, 1009, 109, 9),
(10, 1010, 110, 10);

-- 6. Bills Table
CREATE TABLE Bills (
    B_ID INT PRIMARY KEY,
    P_ID INT,
    Amount DECIMAL(10, 2),
    FOREIGN KEY (P_ID) REFERENCES Patient(P_ID)
);

INSERT INTO Bills VALUES 
(1, 101, 150.00),
(2, 102, 200.00),
(3, 103, 120.00),
(4, 104, 300.00),
(5, 105, 250.00),
(6, 106, 180.00),
(7, 107, 220.00),
(8, 108, 300.00),
(9, 109, 160.00),
(10, 110, 130.00);

-- 7. Test Report Table
CREATE TABLE Test_Report (
    Test_ID INT PRIMARY KEY,
    P_ID INT,
    R_ID INT,
    Result VARCHAR(50),
    Test_Type VARCHAR(50),
    FOREIGN KEY (P_ID) REFERENCES Patient(P_ID),
    FOREIGN KEY (R_ID) REFERENCES Rooms(R_ID)
);

INSERT INTO Test_Report VALUES 
(1, 101, 1, 'Negative', 'Blood Test'),
(2, 102, 2, 'Positive', 'X-Ray'),
(3, 103, 3, 'Normal', 'MRI'),
(4, 104, 4, 'Abnormal', 'CT Scan'),
(5, 105, 5, 'Negative', 'Ultrasound'),
(6, 106, 6, 'Positive', 'Biopsy'),
(7, 107, 7, 'Normal', 'Blood Test'),
(8, 108, 8, 'Negative', 'X-Ray'),
(9, 109, 9, 'Positive', 'MRI'),
(10, 110, 10, 'Abnormal', 'CT Scan');




