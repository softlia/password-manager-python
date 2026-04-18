# 🔐 Password Manager

> A clean, offline desktop credential manager built with Python & Tkinter.  
> Inspired by **Dr. Angela Yu's 100 Days of Code** — Days 29 & 30.

---

## 📋 Table of Contents

- [Problem Statement](#-problem-statement)
- [Program Description](#-program-description)
- [Main Features](#-main-features)
- [Programming Concepts Used](#-programming-concepts-used)
- [Project Structure](#-project-structure)
- [How to Run](#-how-to-run)
- [Required Libraries](#-required-libraries)
- [Sample Inputs & Outputs](#-sample-inputs--outputs)
- [Manual Testing](#-manual-testing--validation)
- [Challenges & Lessons Learned](#-challenges--lessons-learned)
- [AI Assistance Disclosure](#-ai-assistance-disclosure)

---

## ❓ Problem Statement

The average internet user manages **100+ online accounts**, each ideally protected by a unique, strong password. In practice, most people reuse simple passwords or store them in unsafe locations (sticky notes, plain text files, spreadsheets) because remembering dozens of complex passwords is not realistic.

This project solves that problem by providing a **free, offline, local password manager** that:
- Generates strong random passwords automatically
- Stores credentials safely in a structured local file
- Lets users retrieve or delete entries in seconds
- Requires no internet connection, no subscription, and no third-party account

**Intended users:** Students, everyday computer users, and anyone who wants a transparent, code-readable credential store they fully own and control.

---

## 💻 Program Description

The Password Manager is a **single-file desktop application** written in Python using the `tkinter` GUI library. It presents a window with three input fields (Website, Email/Username, Password) and five action buttons (Generate, Search, Add, Delete, Clear).

All credentials are stored persistently in a local `data.json` file using a dictionary structure keyed by website name. The program reads this file on every lookup and rewrites it on every save or delete, keeping data always consistent.

**Overall program flow:**

```
Launch → Build GUI → Enter Event Loop
    ↓
User fills fields → Clicks action button
    ↓
Validate input → Execute action (generate / save / search / delete / clear)
    ↓
Update data.json → Update status bar → Reset form
```

---

## ✨ Main Features

| # | Feature | Description |
|---|---------|-------------|
| 1 | 🎲 **Password Generator** | Generates a 12–18 character password using random letters, symbols, and digits. Auto-copies to clipboard. |
| 2 | ✅ **Save Credentials** | Saves website, email, and password to `data.json` after a confirmation dialog. |
| 3 | 🔍 **Search / Retrieve** | Looks up a saved website entry and populates the fields. Auto-copies password to clipboard. |
| 4 | 🗑 **Delete Entry** | Removes a saved record after a yes/no confirmation to prevent accidents. |
| 5 | 👁 **Show / Hide Password** | Toggles between masked (•••) and plain-text display using a checkbox. |
| 6 | 📊 **Live Status Bar** | Shows feedback after every action at the bottom of the window — no interrupting pop-ups. |
| 7 | 🧹 **Clear / Reset** | Wipes all fields and resets the form to its default ready state in one click. |

---

## 🧠 Programming Concepts Used

| Concept | How It Is Applied |
|---------|-------------------|
| **Variables & Constants** | Colour codes, character sets, and the data file path stored as module-level constants |
| **Functions** | `generate_password()`, `load_data()`, `save_entry()`, `find_entry()`, `delete_entry()` |
| **OOP / Classes** | `PasswordManager` class inherits from `tk.Tk`; methods handle all GUI events |
| **Conditionals** | Input validation, empty-field checks, not-found handling in search and delete |
| **Loops** | `for` loop builds label widgets; `random.choices()` uses iteration internally |
| **Dictionaries** | `data.json` loaded as a dict; credentials stored as nested key-value pairs |
| **File Handling** | `json.load()` / `json.dump()` read and write `data.json` on every operation |
| **Exception Handling** | `try/except` catches `JSONDecodeError` and `OSError` when reading the data file |
| **Random Module** | `random.choices()`, `random.randint()`, `random.shuffle()` for password generation |
| **String Module** | `string.ascii_letters`, `string.digits` provide character pools |
| **Input Validation** | `.strip()`, `.lower()`, and empty-string checks sanitise all user input |
| **f-Strings** | Status messages use f-string interpolation for dynamic feedback text |
| **pathlib** | `Path(__file__).parent / "data.json"` builds a cross-platform file path |
| **Lambda Functions** | Hover-effect bindings use `lambda` to capture button colour at creation time |

---

## 📁 Project Structure

```
password_manager/
├── main.py            ← Full application (GUI + logic, ~220 lines)
├── data.json          ← Auto-created on first save (gitignored)
├── requirements.txt   ← No third-party packages needed
├── .gitignore         ← Excludes data.json and __pycache__
└── README.md          ← This file
```

---

## 🚀 How to Run

### Prerequisites

- Python **3.8 or higher**
- `tkinter` is included with standard Python on **Windows** and **macOS**

> **Linux users only:**
> ```bash
> sudo apt-get install python3-tk
> ```

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/password-manager.git

# 2. Enter the project folder
cd password-manager

# 3. Run the application
python main.py
```

No `pip install` required — the project uses only the Python Standard Library.

---

## 📦 Required Libraries

All libraries used are part of the **Python Standard Library**. No external installation is needed.

| Library | Purpose |
|---------|---------|
| `tkinter` | GUI window, widgets, layout, dialogs |
| `json` | Read and write credential records to disk |
| `random` | Generate random passwords |
| `string` | Provide character sets (letters, digits) |
| `pathlib` | Cross-platform file path construction |

---

## 🖥 Sample Inputs & Outputs

### Saving a credential

**Input:**
```
Website  : github.com
Email    : student@email.com
Password : xT7!mQ2#kL9
```

**Output (data.json):**
```json
{
    "github.com": {
        "email": "student@email.com",
        "password": "xT7!mQ2#kL9"
    }
}
```

**Status bar:** `✅ Entry saved for 'github.com'.`

---

### Searching a credential

**Input:** `github.com` in the Website field → click Search

**Output:** Email and password fields populated; password copied to clipboard.

**Status bar:** `🔍 Found 'github.com' — password copied to clipboard!`

---

### Generating a password

**Input:** Click Generate (no typing required)

**Sample output:** `aB3!xQ9#mK7`  *(varies each time)*

**Status bar:** `✅ Password generated & copied to clipboard!`

---

### Invalid input — empty fields

**Input:** Click Add with Website field empty

**Output:** Warning dialog — *"Please fill in all fields before saving."*

---

## 🧪 Manual Testing / Validation

| # | Test Case | Input | Expected Output | Actual Output | Result |
|---|-----------|-------|-----------------|---------------|--------|
| 1 | Generate password | Click Generate with empty fields | Password appears in field; copied to clipboard; status bar updates | Password generated, field filled, clipboard updated, status updated | ✅ Pass |
| 2 | Save valid entry | Website: `amazon.com`, Email: `test@mail.com`, Password: `abc123!` → click Add → confirm | Entry saved to `data.json`; fields cleared; status bar confirms save | Entry written to file, form reset, status updated | ✅ Pass |
| 3 | Save with empty field | Website empty, Email and Password filled → click Add | Warning dialog: "Please fill in all fields before saving." | Warning dialog appeared, save blocked | ✅ Pass |
| 4 | Search existing entry | Website: `amazon.com` → click Search | Email and password fields filled; password copied to clipboard | Fields populated, clipboard updated, status bar updated | ✅ Pass |
| 5 | Search non-existent entry | Website: `unknownsite.com` → click Search | Info dialog: "No entry found for 'unknownsite.com'." | Info dialog shown, fields unchanged | ✅ Pass |
| 6 | Delete existing entry | Website: `amazon.com` → click Delete → confirm Yes | Entry removed from `data.json`; fields cleared; status confirms deletion | Entry deleted from file, form reset, status updated | ✅ Pass |
| 7 | Delete with empty field | Website empty → click Delete | Warning dialog: "Please enter a website to delete." | Warning dialog appeared, delete blocked | ✅ Pass |
| 8 | Show / Hide password | Enter password → tick Show checkbox | Password text becomes visible; untick re-masks it | Toggled correctly in both directions | ✅ Pass |

---

## 🧗 Challenges & Lessons Learned

### Challenge 1 — Cross-platform file paths
Using hardcoded strings like `"data.json"` works locally but can break when the working directory changes. Switching to `pathlib.Path(__file__).parent / "data.json"` resolved this by always anchoring the file path relative to `main.py` — a pattern that works identically on Windows, macOS, and Linux.

### Challenge 2 — Keeping JSON consistent
Early versions overwrote `data.json` without first loading existing data, which erased previous entries. The fix — always calling `load_data()` before writing, merging the new record into the full dictionary, then rewriting — made the storage layer reliable.

### Challenge 3 — GUI state management
Keeping the show/hide checkbox, the Entry mask, and the status bar all in sync required careful ordering of widget updates inside each action method. Using `tk.BooleanVar` and `tk.StringVar` as the single sources of truth for UI state was the key insight.

**Lessons learned:**
- Event-driven programming requires thinking in terms of *what triggered this* rather than *what runs next*
- Defensive validation (checking inputs before every operation) saves significant debugging time
- A simple flat-file store (JSON) is entirely sufficient for single-user desktop applications

---

## 🤖 AI Assistance Disclosure

AI tools (Claude by Anthropic) were used during this project in the following ways:

| Usage | Details |
|-------|---------|
| **Code structure guidance** | Asked for suggestions on how to structure a tkinter class that inherits from `tk.Tk` |
| **Debugging hints** | Used AI to identify why `data.json` was being overwritten on each save |
| **Syntax clarification** | Clarified usage of `random.choices()` vs `random.choice()` |
| **Documentation assistance** | README structure and section content reviewed and refined with AI support |

All code was written, read, tested, and understood by the student. AI was not used to generate the complete solution — it served as a reference tool similar to documentation or Stack Overflow.

---

## 📄 License

MIT — free to use, modify, and distribute for educational purposes.
