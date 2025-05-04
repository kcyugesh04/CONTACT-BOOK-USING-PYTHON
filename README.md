## NAME:YUGESH K C
## REG NO:111923AI01118
## DEPARTMENT:B.TECH (AI&DS)

# TASK 5-CONTACT-BOOK-USING-PYTHON
```
import sqlite3

# Connect to SQLite database
conn = sqlite3.connect("contacts.db")
cursor = conn.cursor()

# Create table
cursor.execute("""
CREATE TABLE IF NOT EXISTS contacts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    store_name TEXT NOT NULL,
    phone TEXT NOT NULL,
    email TEXT,
    address TEXT
)
""")
conn.commit()

# Add new contact
def add_contact():
    store = input("Store Name: ")
    phone = input("Phone Number: ")
    email = input("Email (optional): ")
    address = input("Address (optional): ")
    cursor.execute("INSERT INTO contacts (store_name, phone, email, address) VALUES (?, ?, ?, ?)",
                   (store, phone, email, address))
    conn.commit()
    print("Contact added successfully!\n")

# View all contacts
def view_contacts():
    cursor.execute("SELECT * FROM contacts")
    results = cursor.fetchall()
    print("\n--- Contact List ---")
    for row in results:
        print(f"ID: {row[0]}, Store: {row[1]}, Phone: {row[2]}, Email: {row[3]}, Address: {row[4]}")
    print()

# Search for a contact
def search_contact():
    query = input("Enter name or phone number to search: ")
    cursor.execute("SELECT * FROM contacts WHERE store_name LIKE ? OR phone LIKE ?", (f'%{query}%', f'%{query}%'))
    results = cursor.fetchall()
    if results:
        print("\n--- Search Results ---")
        for row in results:
            print(f"ID: {row[0]}, Store: {row[1]}, Phone: {row[2]}, Email: {row[3]}, Address: {row[4]}")
    else:
        print("No matching contacts found.\n")

# Update a contact
def update_contact():
    contact_id = input("Enter Contact ID to update: ")
    cursor.execute("SELECT * FROM contacts WHERE id=?", (contact_id,))
    contact = cursor.fetchone()
    if contact:
        print("Leave blank to keep current value.")
        store = input(f"New Store Name ({contact[1]}): ") or contact[1]
        phone = input(f"New Phone ({contact[2]}): ") or contact[2]
        email = input(f"New Email ({contact[3]}): ") or contact[3]
        address = input(f"New Address ({contact[4]}): ") or contact[4]
        cursor.execute("UPDATE contacts SET store_name=?, phone=?, email=?, address=? WHERE id=?",
                       (store, phone, email, address, contact_id))
        conn.commit()
        print("Contact updated.\n")
    else:
        print("Contact not found.\n")

# Delete a contact
def delete_contact():
    contact_id = input("Enter Contact ID to delete: ")
    cursor.execute("SELECT * FROM contacts WHERE id=?", (contact_id,))
    if cursor.fetchone():
        cursor.execute("DELETE FROM contacts WHERE id=?", (contact_id,))
        conn.commit()
        print("Contact deleted.\n")
    else:
        print("Contact not found.\n")

# Menu
def main():
    while True:
        print("========== Contact Manager ==========")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")
        choice = input("Enter your choice (1-6): ")

        if choice == '1':
            add_contact()
        elif choice == '2':
            view_contacts()
        elif choice == '3':
            search_contact()
        elif choice == '4':
            update_contact()
        elif choice == '5':
            delete_contact()
        elif choice == '6':
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Try again.\n")

# Start the program
if __name__ == "__main__":
    main()

```
## OUTPUT:
![Screenshot 2025-05-04 133939](https://github.com/user-attachments/assets/74ac6a23-8c4a-4ff1-956b-b4b7ac4e922f)
![Screenshot 2025-05-04 134022](https://github.com/user-attachments/assets/24db01f2-bbc0-4b0b-bb04-1724b2fabed3)
![Screenshot 2025-05-04 134042](https://github.com/user-attachments/assets/c8abfc06-da6e-4688-8128-bdaa648bae88)


## RESULT:
The code has been executed successfully.
