Train Ticket Booking System

A simple C language console-based project for CSE115L that allows users to book, view, search, cancel, and save train tickets.
Built by ByteCrew (Oli, Yamin, Zoheb).

---

📌 Features

* Book New Ticket:
  Enter passenger details, train info, travel date, and automatically get assigned a **PNR** and **seat number**.

* See All Tickets:
  Displays all booked tickets in a clean list.

* Find Ticket by PNR:
  Searches and displays a ticket using the unique PNR number.

* Cancel Ticket:
  Deletes any ticket using PNR and shifts remaining tickets properly.

* Save Data to File:
  Saves all tickets into **tickets_data.bin** using binary file handling.

* Load Saved Data Automatically:
  Loads previous data when the program starts.

---

🛠️ Project Structure

The code is divided among team members:

| Member    | Contribution                                                            |
| --------- | ----------------------------------------------------------------------- |
| Oli       | Main menu, booking system, struct definitions, initialization functions |
| Yamin     | View all tickets, find ticket functionality                             |
| Zoheb     | Cancel ticket, save & load file handling                                |

---

⚙️ How It Works

When the program starts:

* It loads saved data using `loadData()`
* Displays a menu with 6 options
* Executes user-selected operations
* On exit, automatically saves all data

---

📂 File Used

The system uses one file for persistence:

```
tickets_data.bin
```

This file stores:

* Total tickets
* Current PNR counter
* All ticket data (Passenger struct)

---

📸 Sample Output

Main Menu

```
------------ MENU -------------
1. Book new ticket
2. See all tickets
3. Find ticket
4. Cancel ticket
5. Save
6. Exit
-------------------------------
```

Ticket Booking Example

```
--- BOOK TICKET ---
Passenger name: Jack
Age: 23
Train name: MRT001
Train number: 182828
Travel date (dd/mm/yyyy): 9/12/25

SUCCESS! Ticket booked!
Your PNR: 1000
Your seat: 1
```

Save Confirmation

```
Saved!
```

---

🧠 Technologies Used

* C Programming
* File Handling (Binary I/O)
* Structs
* Arrays
* Basic Input/Output and Menu Systems

---

🚀 How to Run

1. Compile using GCC:

   ```
   gcc main.c -o train
   ```

2. Run the executable:

   ```
   ./train
   ```

3. Use menu options to book, cancel, or view tickets.

---

👥 Team ByteCrew

* Oli
* Yamin
* Zoheb

