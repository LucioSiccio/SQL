# SQL for Networking: A Step-by-Step Demonstration

# ## Introduction In this demonstration, we will cover how to use SQL for managing data in a network context. We will simulate the process of creating and managing a **devices table** for a network, which includes routers, switches, and servers. This tutorial will guide you through the process of creating the database, inserting data, querying, and performing advanced operations like updating records, aggregating data, and joining tables.

We will use **DB-Fiddle** as our SQL playground to run the commands and visualize the results.
---

CREATE TABLE devices ( 
  id INT AUTO_INCREMENT PRIMARY KEY, -- Device ID (auto increments) 
  device_name VARCHAR(100), -- Name of the device 
  ip_address VARCHAR(15) UNIQUE, -- IP address (unique for each device) 
  device_type VARCHAR(50), - Type of device (e.g., Router, Switch, Server) 
  status VARCHAR(20) -- Status (Active, Inactive) );

- **id**: A primary key that uniquely identifies each device (auto-increments).
- **device_name**: Name of the device (e.g., "Router1").
- **ip_address**: IP address of the device (unique).
- **device_type**: Type of device (Router, Switch, Server).
- **status**: Current status of the device (e.g., Active, Inactive).

Run this query in **DB-Fiddle** to create the table.

---

## Step 2: Insert Data into the Table

Now, let’s insert some sample data representing devices in the network. This data will help us simulate devices like routers, switches, and servers.

sql

INSERT INTO devices (device_name, ip_address, device_type, status)
VALUES 
('Router1', '192.168.1.1', 'Router', 'Active'),
('Switch1', '192.168.1.2', 'Switch', 'Active'),
('Server1', '192.168.1.3', 'Server', 'Inactive');

### Explanation:

- We’re inserting three rows into the `devices` table with different device types and statuses.

Run this query in **DB-Fiddle** to populate the `devices` table with data.

## Step 3: Query Data from the Table

To verify that our data is correctly inserted, we’ll query the table to view the records.

sql

Copy code

`SELECT * FROM devices;`

### Explanation:

- **`SELECT *`** retrieves all columns from the `devices` table.

After running this query, you should see the list of devices with their names, IP addresses, types, and statuses.

---

## Step 4: Update Data in the Table

Suppose the status of `Server1` changes to **Active** after it comes back online. Here’s how we can update it:

sql

Copy code

`UPDATE devices SET status = 'Active' WHERE device_name = 'Server1';`

### Explanation:

- **`UPDATE`** modifies the status of `Server1` from "Inactive" to "Active".

Run this query to update the status of `Server1`. Then, run `SELECT * FROM devices;` again to confirm the change.

---

## Step 5: Delete Data from the Table

Now, let's say `Switch1` is no longer part of the network and should be removed from the database. We can delete it with the following query:

sql

Copy code

`DELETE FROM devices WHERE device_name = 'Switch1';`

### Explanation:

- **`DELETE`** removes the record for `Switch1` from the table.

Run this query and then verify that `Switch1` is removed by running `SELECT * FROM devices;`.

---

## Step 6: Aggregate Functions (COUNT, SUM, AVG)

Let's count how many devices are currently **Active**.

sql

Copy code

`SELECT COUNT(*) AS total_active_devices FROM devices WHERE status = 'Active';`

### Explanation:

- **`COUNT(*)`** counts the number of devices where the status is "Active".

Run this query to see how many devices are currently active in your network.

---

## Step 7: Grouping Data (GROUP BY)

We can group the devices by their **device type** (Router, Switch, Server) to see how many of each type we have.

sql

Copy code

`SELECT device_type, COUNT(*) AS total FROM devices GROUP BY device_type;`

### Explanation:

- **`GROUP BY`** groups the devices by their `device_type`, and **`COUNT(*)`** counts the total number of devices of each type.

Run this query to see the breakdown of devices by type.

---

## Step 8: Filtering Results (WHERE, LIKE, AND, OR)

Let’s filter the devices to only show **Active Routers**.

sql

Copy code

`SELECT * FROM devices WHERE status = 'Active' AND device_type = 'Router';`

### Explanation:

- **`WHERE`** filters the results to show only active routers.

Run this query to see only the active routers in your network.

---

## Step 9: Joins (Combining Data from Multiple Tables)

In a real-world network, you might also have event logs for devices. Let’s simulate a scenario where we join the `devices` table with a `logs` table to track events for each device.

### Step 9.1: Create the Logs Table

sql

Copy code

`CREATE TABLE logs (     log_id INT AUTO_INCREMENT PRIMARY KEY,     device_id INT,     event VARCHAR(255),     timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,     FOREIGN KEY (device_id) REFERENCES devices(id) );`

### Step 9.2: Insert Data into the Logs Table

sql

Copy code

`INSERT INTO logs (device_id, event) VALUES  (1, 'Router1 activated'), (2, 'Switch1 connected'), (3, 'Server1 down');`

### Step 9.3: Perform a JOIN to Combine Data

sql

Copy code

`SELECT devices.device_name, logs.event, logs.timestamp FROM devices JOIN logs ON devices.id = logs.device_id;`

### Explanation:

- **`JOIN`** combines the `devices` and `logs` tables based on their **foreign key relationship** (device `id`).
- **`logs.event`** and **`logs.timestamp`** are shown alongside the device name.

Run this query to see which devices triggered specific events and when.

## Conclusion

By following this demonstration, we’ve walked through essential SQL operations in the context of networking. This includes creating tables, inserting and querying data, performing updates, deletions, and aggregations, and combining data from multiple tables using joins.

---

## Final Notes

Feel free to modify this file by adding your own network-related SQL examples or expanding the sections on aggregations, constraints, and user management as needed for your specific use case.
