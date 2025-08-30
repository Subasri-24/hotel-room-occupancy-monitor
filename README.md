# hotel-room-occupancy-monitor
Developed a database-driven system to monitor and manage hotel room occupancy efficiently. The project focuses on leveraging SQL and MySQL to handle real-time data about room availability, reservations, and guest details.
use hotel;

create TABLE Rooms (
    room_id INT PRIMARY KEY,
    room_number VARCHAR(10) UNIQUE,
    room_type VARCHAR(20), 
    price DECIMAL(10,2),
    status VARCHAR(20) DEFAULT 'Available' 
);

Create TABLE Bookings (
    booking_id INT PRIMARY KEY AUTO_INCREMENT,
    room_id INT,
    guest_name VARCHAR(100),
    check_in DATE,
    check_out DATE,
    booking_status VARCHAR(20) DEFAULT 'Upcoming', 
    FOREIGN KEY (room_id) REFERENCES Rooms(room_id)
);
CREATE TABLE Cleaning_Status (
    cleaning_id INT PRIMARY KEY AUTO_INCREMENT,
    room_id INT,
    last_cleaned DATE,
    status VARCHAR(20) DEFAULT 'Clean', 
    FOREIGN KEY (room_id) REFERENCES Rooms(room_id)
);

SELECT room_number, room_type, price
FROM Rooms
WHERE status = 'Available';

SELECT r.room_number, b.guest_name, b.check_in, b.check_out
FROM Rooms r
JOIN Bookings b ON r.room_id = b.room_id
WHERE r.status = 'Occupied' AND b.booking_status = 'Checked-in';

SELECT r.room_number, c.last_cleaned
FROM Rooms r
JOIN Cleaning_Status c ON r.room_id = c.room_id
WHERE c.status = 'Needs Cleaning';

INSERT INTO Rooms (room_id, room_number, room_type, price, status)
VALUES
(1, '101', 'Single', 1500.00, 'Available'),
(2, '102', 'Double', 2500.00, 'Occupied'),
(3, '103', 'Suite', 5000.00, 'Cleaning'),
(4, '104', 'Single', 1600.00, 'Available'),
(5, '105', 'Double', 2700.00, 'Occupied');

INSERT INTO Bookings (room_id, guest_name, check_in, check_out, booking_status)
VALUES
(2, 'suba', '2025-08-18', '2025-08-22', 'Checked-in'),
(5, 'hari', '2025-08-19', '2025-08-21', 'Checked-in'),
(1, 'madhan', '2025-08-25', '2025-08-28', 'Upcoming'),
(3, 'prem', '2025-08-15', '2025-08-17', 'Checked-out');

INSERT INTO Cleaning_Status (room_id, last_cleaned, status)
VALUES
(1, '2025-08-19', 'Clean'),
(2, '2025-08-18', 'In Progress'),
(3, '2025-08-17', 'Needs Cleaning'),
(4, '2025-08-19', 'Clean'),
(5, '2025-08-18', 'Needs Cleaning'); 
#mysql
#sql
