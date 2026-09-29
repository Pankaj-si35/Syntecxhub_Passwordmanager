# Syntecxhub_Passwordmanager
A secure local password manager built with Python using AES-GCM encryption and PBKDF2-HMAC-SHA256 for protected credential storage
# 🔐 Secure Password Manager

A local, command-line password manager built with Python that securely stores user credentials using modern cryptographic techniques.

The project demonstrates practical implementation of **password-based key derivation, AES-GCM authenticated encryption, secure local storage, credential management, and authentication failure handling**.

---

## 📌 Project Overview

The **Secure Password Manager** is an educational cybersecurity project designed to provide a secure method for storing and managing credentials locally.

Instead of storing passwords in plain text, the application encrypts the password vault before writing it to disk.

The encryption key is derived from the user's master password using **PBKDF2-HMAC-SHA256** with a randomly generated salt.

The vault data is then protected using **AES-256-GCM authenticated encryption**.

### Security Flow

```text
                 Master Password
                        │
                        ▼
              PBKDF2-HMAC-SHA256
                        │
                 Random Salt
                        │
                        ▼
                 256-bit Key
                        │
                        ▼
                  AES-256-GCM
                        │
                        ▼
              Encrypted Vault
                        │
                        ▼
                  vault.json
🎯 Objectives
The main objectives of this project are:
Understand secure password storage concepts
Implement symmetric encryption
Understand AES-GCM authenticated encryption
Implement PBKDF2-based key derivation
Avoid storing the master password directly
Store credentials in encrypted form
Implement secure local credential management
Handle incorrect authentication attempts
Practice Python cryptography and secure coding principles
✨ Features
🔑 Master Password Protection
Uses a master password to unlock the password vault.
The master password is not stored directly.
A cryptographic key is derived from the master password.
🔒 AES-GCM Encryption
Uses AES-GCM for authenticated encryption.
Provides confidentiality and integrity protection.
A random nonce is generated for each encryption operation.
🧂 Random Salt
A cryptographically secure random salt is generated when creating the vault.
The salt is stored with the encrypted vault because it does not need to remain secret.
🛡️ PBKDF2 Key Derivation
The project uses:
PBKDF2-HMAC-SHA256
with:
Key Length: 256 bits
Iterations: 600000
This makes direct brute-force attacks against the master password more computationally expensive.
➕ Add Credentials
Users can store:
Service/Website
Username/Email
Password
🔎 Search Credentials
Credentials can be searched by service/website name.
📋 List Credentials
The application can display the stored services and usernames without requiring users to inspect the encrypted storage manually.
🗑️ Delete Credentials
Stored credentials can be removed from the vault.
🚫 Wrong Password Detection
An incorrect master password results in a failed decryption attempt and access is denied.
💾 Local Encrypted Storage
All vault data is stored locally in:
vault.json
The sensitive vault contents are encrypted before being written to disk.
🛠️ Technologies Used
Technology
Purpose
Python 3
Application development
Cryptography
Cryptographic operations
AES-GCM
Authenticated encryption
PBKDF2-HMAC-SHA256
Password-based key derivation
JSON
Local vault storage
Base64
Binary data representation
Git & GitHub
Version control and project hosting
Kali Linux
Development and security testing environment
📂 Project Structure
SyntexHub_Password_Manager/
│
├── main.py
├── vault.json
├── requirements.txt
├── README.md
└── venv/
File Description
File/Directory
Description
main.py
Main password manager application
vault.json
Encrypted local password vault
requirements.txt
Python dependencies
README.md
Project documentation
venv/
Python virtual environment
⚠️ The venv/ directory should normally not be uploaded to GitHub. Use a .gitignore file for it.
🚀 Installation
1. Clone the Repository
git clone https://github.com/YOUR_USERNAME/SyntexHub_Password_Manager.git
Move into the project directory:
cd SyntexHub_Password_Manager
2. Create a Virtual Environment
python3 -m venv venv
Activate the virtual environment:
Linux / Kali Linux
source venv/bin/activate
3. Install Dependencies
pip install -r requirements.txt
▶️ Usage
Start the application:
python3 main.py
🔐 First Run
On the first run, the application asks the user to create a master password.
Example:
=== Create New Vault ===

Create master password:
Confirm master password:
The application validates the password and creates an encrypted vault.
➕ Adding a Credential
Select:
1. Add Credential
Example:
Service/Website: Test-Gmail
Username/Email: test@example.com
Password: TestPass@123
The credential is then encrypted and stored in the local vault.
🔎 Searching Credentials
Select:
2. Search Credential
Example:
Search service: Gmail
The application displays the matching credential after successful authentication.
📋 Listing Credentials
Select:
3. List Credentials
Example output:
=== Stored Services ===

1. Test-Gmail - test@example.com
🗑️ Deleting Credentials
Select:
4. Delete Credential
Then select the credential number to remove it.
Example:
Enter credential number to delete: 1
🚪 Exit
Select:
5. Exit
🔐 Security Architecture
The application follows this basic security architecture:
                 User
                  │
                  ▼
           Master Password
                  │
                  ▼
        ┌───────────────────┐
        │ PBKDF2-HMAC-SHA256│
        └───────────────────┘
                  │
             Random Salt
                  │
                  ▼
            256-bit Key
                  │
                  ▼
        ┌───────────────────┐
        │     AES-256-GCM   │
        └───────────────────┘
                  │
                  ▼
           Encrypted Data
                  │
                  ▼
             vault.json
🧠 Cryptographic Concepts
PBKDF2
PBKDF2 is used to derive a cryptographic key from the master password.
The project uses:
Algorithm: PBKDF2-HMAC-SHA256
Iterations: 600000
Derived Key Length: 32 bytes
Salt: 16 bytes
The derived key is used for AES encryption.
AES-GCM
AES-GCM provides authenticated encryption.
It provides:
Confidentiality
Protects stored credentials from being read without the encryption key.
Integrity
Helps detect unauthorized modification of encrypted data.
Authentication
The GCM authentication tag allows the application to detect invalid or modified ciphertext during decryption.
Random Nonce
A new random 12-byte nonce is generated for each encryption operation.
Nonce → AES-GCM → Ciphertext
The nonce is stored with the encrypted data because it is not a secret value.
🧪 Security Testing
The following tests were performed:
Test 1 — Correct Master Password
Expected result:
Vault unlocked successfully
Test 2 — Incorrect Master Password
Example:
Enter master password: wrongpassword
Expected result:
Invalid master password or corrupted vault.
Test 3 — Encrypted Storage Verification
Inspecting:
cat vault.json
should not reveal stored passwords in plain text.
The vault contains encoded encrypted data such as:
{
    "salt": "...",
    "nonce": "...",
    "data": "..."
}
Test 4 — Credential Management
The application was tested for:
Add
Search
List
Delete
credential operations.
🛡️ Security Considerations
This project follows several secure coding principles:
Passwords are not intentionally stored as plain text in the vault.
The master password is not stored directly.
A random salt is used for key derivation.
PBKDF2 is used to derive the encryption key.
AES-GCM provides authenticated encryption.
Random nonces are generated for encryption.
Vault data is stored locally.
Incorrect master passwords result in failed decryption.
⚠️ Limitations
This project is designed primarily for educational and cybersecurity learning purposes.
It should not currently be considered a production-grade password manager.
Potential improvements include:
Secure memory handling
Automatic vault locking
Password strength analysis
Clipboard timeout
Password generator
Login attempt throttling
Secure deletion
OS keychain integration
Multi-user support
Hardware-backed key storage
Automated security testing
GUI interface
Encrypted backup functionality
🔮 Future Improvements
Planned improvements may include:
Password Generator
        ↓
Password Strength Checker
        ↓
Automatic Vault Lock
        ↓
Clipboard Protection
        ↓
Secure Backup
        ↓
OS Keychain Integration
        ↓
GUI Application
📸 Project Screenshots
Screenshots demonstrating the following functionality can be added to this section:
1. Project Setup
Python environment and project structure
2. Vault Creation
Master password creation
3. Add Credential
Adding a test credential
4. Search Credential
Searching stored credentials
5. Encrypted Vault
vault.json showing encrypted data
6. Authentication Failure
Incorrect master password rejection
📚 Learning Outcomes
Through this project, the following concepts were practiced:
Python programming
File handling
JSON data management
Exception handling
Password-based authentication
Cryptographic key derivation
AES encryption
Authenticated encryption
Secure local storage
Secure coding practices
Cybersecurity fundamentals
Git and GitHub workflow
🎓 Internship Project
Project: Password Manager
Internship/Organization: SyntexHub
Domain: Cybersecurity / Secure Coding
Project Type: Local Security Application
⚠️ Disclaimer
This project was developed for educational and cybersecurity learning purposes.
Do not use this implementation as a replacement for a professionally audited password manager for storing highly sensitive production credentials.
Always use dummy/test credentials while demonstrating or testing this project.
