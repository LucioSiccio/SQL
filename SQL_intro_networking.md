CREATE TABLE devices (
    id INT AUTO_INCREMENT PRIMARY KEY,        -- Device ID (auto increments)
    device_name VARCHAR(100),                  -- Name of the device
    ip_address VARCHAR(15) UNIQUE,             -- IP address (unique for each device)
    device_type VARCHAR(50),                   -- Type of device (e.g., Router, Switch, Server)
    status VARCHAR(20)                         -- Status (Active, Inactive)
);

INSERT INTO devices (device_name, ip_address, device_type, status)
VALUES 
('Router1', '192.168.1.1', 'Router', 'Active'),
('Switch1', '192.168.1.2', 'Switch', 'Active'),
('Server1', '192.168.1.3', 'Server', 'Inactive');

SELECT * FROM devices;

UPDATE devices
SET status = 'Active'
WHERE device_name = 'Server1';

DELETE FROM devices
WHERE device_name = 'Switch1';

SELECT COUNT(*) AS total_active_devices FROM devices WHERE status = 'Active';

SELECT device_type, COUNT(*) AS total FROM devices
GROUP BY device_type;

SELECT * FROM devices
WHERE status = 'Active' AND device_type = 'Router';

CREATE TABLE logs (
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    device_id INT,
    event VARCHAR(255),
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (device_id) REFERENCES devices(id)
);

INSERT INTO logs (device_id, event)
VALUES 
(1, 'Router1 activated'),
(2, 'Switch1 connected'),
(3, 'Server1 down');

SELECT devices.device_name, logs.event, logs.timestamp
FROM devices
JOIN logs ON devices.id = logs.device_id;