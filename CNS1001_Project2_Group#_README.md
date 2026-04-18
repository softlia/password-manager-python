# CNS1001 Project 2 — Final Programming Project
## README / Final Report

---

## a. Project Title

**🔐 Password Manager — Desktop Credential Management Application**

---

## b. Student Information

| Field | Details |
|-------|---------|
| **Full Name** | Aleisha Fuller (2503042), Anthony Demetrius (2502004), Joshua Tyrrel (2506464), Mikhiel Miller (2506699), Okay-Lia Buchanan (2506017) Paul Duncanson (2506019)  |
| **Course Code** | CNS1001 — Introduction to Programming |
| **Semester / Year** | Semester 2, 2026 |
| **Lecturer** | Wayne Thompson |
| **Due Date** | April 17, 2026 |
| **Submission Date** | April 17, 2026 |

---

## c. Problem Statement

### What problem does this project solve?

The average internet user manages over 100 online accounts across banking, email, social media, shopping, and work platforms. Every security best practice recommends using a **unique, complex password** for each account — but the human memory is simply not built to store dozens of random strings like `aB3!xQ9#mK7`.

As a result, most people fall into one of three unsafe habits:

1. **Reusing the same password** across multiple sites — so one breach exposes everything
2. **Using simple, guessable passwords** like names, birthdays, or common words
3. **Storing passwords unsafely** — in plain text files, sticky notes, browser autofill, or unencrypted spreadsheets

This project solves these problems by providing a **free, offline, fully transparent Password Manager** that generates strong passwords automatically, stores credentials in a structured local file, and lets users retrieve or delete them through a clean graphical interface.

### Why was this project chosen?

This project was chosen because it:
- Solves a real, everyday problem that any computer user can relate to
- Covers a wide range of CNS1001 programming concepts in a single application
- Produces a working, useful tool rather than a toy exercise
- Follows the curriculum taught by Dr. Angela Yu (100 Days of Code, Days 29–30), demonstrating that beginner-level Python is enough to build genuinely practical software

### Who is the intended user?

Any individual who manages multiple online accounts and wants a simple, local, and free way to store and retrieve passwords — particularly students, everyday computer users, and anyone who does not want to pay for a commercial password manager or trust their credentials to a cloud service.

---

## d. Program Description

### What does the program do?

The Password Manager is a **desktop GUI application** built with Python and the `tkinter` library. When launched, it opens a window containing three input fields (Website, Email/Username, Password) and five action buttons. The user can:

- Type a website name and click **Generate** to produce a strong random password instantly
- Click **Add** to save the website, email, and password permanently to a local file
- Type a website name and click **Search** to retrieve previously saved credentials
- Click **Delete** to permanently remove a saved entry after confirmation
- Click **Clear** to reset all fields and start fresh

All data is stored in a `data.json` file on the user's computer. The file is created automatically the first time a credential is saved, and updated on every subsequent save or delete.

### Main Features

| # | Feature | What It Does |
|---|---------|--------------|
| 1 | 🎲 **Password Generator** | Produces a random 12–18 character password with letters, symbols, and digits. Auto-copies to clipboard. |
| 2 | ✅ **Save Credentials** | Validates all fields, asks for confirmation, then writes the record to `data.json`. |
| 3 | 🔍 **Search / Retrieve** | Finds a saved entry by website name and populates the form fields. Copies password to clipboard. |
| 4 | 🗑 **Delete Entry** | Removes a credential record permanently after a yes/no confirmation dialog. |
| 5 | 👁 **Show / Hide Password** | Toggles the password field between masked (•••) and visible text using a checkbox. |
| 6 | 📊 **Live Status Bar** | Displays a live feedback message at the bottom of the window after every action. |
| 7 | 🧹 **Clear / Reset** | Resets all three input fields and the status bar to their default state. |

### Overall Program Flow

```
1. User runs: python main.py
        ↓
2. PasswordManager class initialises and builds the GUI window
        ↓
3. Program enters the Tkinter event loop (waiting for user input)
        ↓
4. User fills in fields and clicks a button
        ↓
5. Input is validated — warnings shown if fields are empty or invalid
        ↓
6. Action is executed (generate / save / search / delete / clear)
        ↓
7. data.json is updated if required
        ↓
8. Status bar updates with a confirmation message
        ↓
9. Form resets where appropriate — ready for next entry
```

---

## e. Programming Concepts Used

The following programming concepts from CNS1001 are directly applied in this project:

### Functions
The program uses multiple user-defined functions, each with a single, clear purpose:
- `generate_password()` — builds and returns a random password string
- `load_data()` — reads and returns all saved credentials from `data.json`
- `save_entry(website, email, password)` — adds or updates a record in the file
- `find_entry(website)` — searches for and returns a specific credential record
- `delete_entry(website)` — removes a record from the file
- `_build_ui()`, `_entry()`, `_btn()` — construct the GUI layout
- `_save()`, `_search()`, `_delete()`, `_clear()`, `_fill_password()` — handle button click events

### Loops
- A `for` loop builds the three label widgets from a tuple of strings, reducing repeated code
- `random.choices()` uses iteration internally to select characters from the character pools

### Conditionals
- `if not website or not email or not password:` — validates that all fields are filled before saving
- `if entry:` — checks whether a search result was found before populating fields
- `if DATA_FILE.exists():` — checks whether `data.json` exists before attempting to read it
- `if website in data:` — confirms the key exists before attempting deletion

### Dictionaries
- All credentials are stored as a nested dictionary: `{ "website": { "email": "...", "password": "..." } }`
- `dict.get(key)` is used for safe lookup without raising a `KeyError`
- `del data[key]` removes an entry from the dictionary before rewriting the file

### File Handling
- `open(DATA_FILE, "r")` with `json.load()` reads all saved credentials at startup and on every search
- `open(DATA_FILE, "w")` with `json.dump()` writes the complete updated dictionary after every save or delete
- `pathlib.Path` builds a cross-platform file path anchored to the location of `main.py`

### Input Validation
- `.strip()` removes leading and trailing whitespace from all user inputs
- `.lower()` normalises website names so `GitHub.com` and `github.com` map to the same record
- Empty-string checks (`if not field:`) block all actions if any required input is missing
- `try/except (JSONDecodeError, OSError)` handles corrupt or unreadable data files gracefully

### Object-Oriented Programming
- The `PasswordManager` class inherits from `tk.Tk`, giving it a full GUI window
- `super().__init__()` calls the parent class constructor
- All GUI state and event methods are encapsulated inside the class

---

## f. How to Run the Program

### Requirements

- **Python 3.8 or higher** must be installed
- `tkinter` is included with standard Python on **Windows** and **macOS**
- **Linux users only** — install tkinter separately:

```bash
sudo apt-get install python3-tk
```

### Steps to Run

```bash
# Step 1 — Navigate to the project folder
cd CNS1001_Project2_Group#

# Step 2 — Run the program
python main.py
```

> On some systems, use `python3` instead of `python`.

The application window will open immediately. No login, setup, or configuration is required.

### File Naming (Submission Format)

```
CNS1001_Project2_Group#_project.py
CNS1001_Project2_Group#_README.md
CNS1001_Project2_Group#_requirements.txt
CNS1001_Project2_Group#.zip
```

---

## g. Required Libraries

No external libraries need to be installed. All libraries used are part of the **Python Standard Library** and are available on any Python 3.8+ installation.

| Library | Version | Purpose |
|---------|---------|---------|
| `tkinter` | Built-in | GUI window, widgets, labels, buttons, dialogs, entry fields |
| `json` | Built-in | Reading and writing credentials to `data.json` |
| `random` | Built-in | Generating random passwords (choices, randint, shuffle) |
| `string` | Built-in | Character sets — `ascii_letters` and `digits` |
| `pathlib` | Built-in | Cross-platform file path construction |

**requirements.txt** contents:
```
# No external packages required.
# This project uses only the Python Standard Library.
```

---

## h. Sample Inputs and Outputs

### Sample 1 — Generating and Saving a Password

**Step 1:** Enter website and email, click Generate

```
Website  : netflix.com
Email    : student@gmail.com
Password : (click Generate)
```

**Generated password (example):** `mK9!bQ3#xT7`

**Status bar:** `✅ Password generated & copied to clipboard!`

**Step 2:** Click Add → Confirm dialog

**Result in data.json:**
```json
{
    "netflix.com": {
        "email": "student@gmail.com",
        "password": "mK9!bQ3#xT7"
    }
}
```

**Status bar:** `✅ Entry saved for 'netflix.com'.`

---

### Sample 2 — Searching a Saved Entry

**Input:** Type `netflix.com` in the Website field → click Search

**Output:** Email field fills with `student@gmail.com`; Password field fills with `mK9!bQ3#xT7`

**Status bar:** `🔍 Found 'netflix.com' — password copied to clipboard!`

---

### Sample 3 — Searching a Non-Existent Entry

**Input:** Type `unknownsite.com` → click Search

**Output:** Pop-up dialog — *"No entry found for 'unknownsite.com'."*

**Status bar:** `❌ No entry for 'unknownsite.com'.`

---

### Sample 4 — Attempting to Save with an Empty Field

**Input:** Leave Website blank; fill Email and Password → click Add

**Output:** Warning dialog — *"Please fill in all fields before saving."*

No data is written. Form remains unchanged.

---

### Sample 5 — Deleting an Entry

**Input:** Type `netflix.com` → click Delete → click Yes in confirmation dialog

**Output:** Entry removed from `data.json`; form cleared.

**Status bar:** `🗑 Entry for 'netflix.com' deleted.`

---

## i. Manual Testing / Validation

All test cases were performed manually by running the program and entering the specified inputs, then observing and recording the actual outputs.

| # | Test Case Description | Input | Expected Output | Actual Output | Pass / Fail |
|---|----------------------|-------|-----------------|---------------|-------------|
| 1 | Generate password with empty fields | Click Generate (no input) | Password generated and placed in field; auto-copied to clipboard; status bar updates | Password generated, field filled, clipboard updated, status updated | ✅ Pass |
| 2 | Save a valid entry | Website: `amazon.com`, Email: `test@mail.com`, Password: `abc!123` → click Add → Confirm | Entry written to `data.json`; fields cleared; status bar confirms | Entry saved to file, form reset, status: `✅ Entry saved for 'amazon.com'.` | ✅ Pass |
| 3 | Save entry with empty Website field | Website: *(blank)*, Email: `test@mail.com`, Password: `abc!123` → click Add | Warning dialog shown; save blocked; no file write | Dialog: *"Please fill in all fields before saving."* No file change. | ✅ Pass |
| 4 | Save entry with empty Password field | Website: `amazon.com`, Email: `test@mail.com`, Password: *(blank)* → click Add | Warning dialog shown; save blocked | Dialog appeared, save blocked | ✅ Pass |
| 5 | Search for an existing entry | Website: `amazon.com` → click Search | Fields populated with saved email and password; clipboard updated | Email and password fields filled; status: `🔍 Found 'amazon.com'...` | ✅ Pass |
| 6 | Search for a non-existent entry | Website: `fakesite.xyz` → click Search | Info dialog: "No entry found"; fields unchanged | Dialog appeared, no field change, status: `❌ No entry for 'fakesite.xyz'.` | ✅ Pass |
| 7 | Search with empty Website field | Website: *(blank)* → click Search | Warning dialog: "Please enter a website to search." | Warning dialog appeared, search blocked | ✅ Pass |
| 8 | Delete an existing entry | Website: `amazon.com` → click Delete → Yes | Entry removed from `data.json`; form cleared; status confirms | Entry deleted, form cleared, status: `🗑 Entry for 'amazon.com' deleted.` | ✅ Pass |
| 9 | Delete with empty Website field | Website: *(blank)* → click Delete | Warning dialog: "Please enter a website to delete." | Warning dialog appeared, delete blocked | ✅ Pass |
| 10 | Show / Hide password toggle | Type password → tick Show checkbox | Password text becomes visible; untick re-masks with bullets | Toggle worked correctly in both directions | ✅ Pass |
| 11 | Clear form | Fill all fields → click Clear | All fields emptied; password re-masked; status resets to "Ready." | Form fully reset, checkbox unticked, status: `Ready.` | ✅ Pass |
| 12 | Case-insensitive website key | Save as `GITHUB.COM`; search as `github.com` | Same entry found (normalised to lowercase) | Entry retrieved correctly | ✅ Pass |

---

## j. Challenges and Lessons Learned

### Challenge 1 — JSON File Overwriting Previous Data

**Problem:** In an early version of the program, clicking Add would call `json.dump()` with only the new record, completely erasing all previously saved passwords.

**How it was handled:** The fix was to always call `load_data()` first — reading the entire existing dictionary into memory — then adding the new entry to that dictionary before writing the whole thing back. This merge-then-write pattern ensures no data is ever lost.

**Lesson learned:** When working with file-based storage, you must always read before you write if you want to preserve existing data. Overwriting blindly is a common but serious bug in file I/O.

---

### Challenge 2 — Cross-Platform File Paths

**Problem:** Using a plain string like `"data.json"` worked when the program was run from its own folder, but failed when run from a different working directory — Python looked for the file in the wrong place.

**How it was handled:** Replacing the string with `Path(__file__).parent / "data.json"` anchors the file path to the location of `main.py` itself, regardless of where the user runs the program from. This works identically on Windows, macOS, and Linux.

**Lesson learned:** Always use `pathlib.Path` (or `os.path`) for file paths in real applications. Hardcoded relative strings are fragile and environment-dependent.

---

### Challenge 3 — Keeping the GUI and Data in Sync

**Problem:** After actions like Save or Delete, the form fields, the show/hide checkbox, the password mask, and the status bar all needed to update consistently. Early versions had mismatches — for example, the checkbox was ticked but the password was still masked.

**How it was handled:** All state reset was centralised in a single `_clear()` method that is called after every successful write or delete. Using `tk.BooleanVar` and `tk.StringVar` as single sources of truth for checkbox and status bar state made synchronisation straightforward.

**Lesson learned:** In GUI programming, having a single method responsible for resetting state is far more reliable than scattering widget updates across multiple places. Centralisation prevents inconsistencies.

---

### Overall Lessons from the Project

- **Planning matters** — Sketching the function structure before writing code made the implementation faster and cleaner
- **Defensive programming** — Checking inputs before every operation (validation) prevents most runtime errors
- **OOP is practical** — Grouping related functions and variables inside a class made the GUI code significantly easier to read and maintain than a procedural approach
- **Simple tools are powerful** — The Python Standard Library alone — `tkinter`, `json`, `random`, `pathlib` — is sufficient to build a complete, useful desktop application without any external dependencies

---

## 🤖 AI Assistance Disclosure

AI tools were used during this project in accordance with the CNS1001 Academic Integrity Policy.

| AI Tool Used | Type of Use | How the Response Was Validated |
|---|---|---|
| Claude (Anthropic) | Syntax clarification — asked how `random.choices()` differs from `random.choice()` | Verified by reading the Python documentation and testing both functions manually |
| Claude (Anthropic) | Debugging hint — asked why `data.json` was being overwritten instead of updated | Understood the merge-then-write fix and implemented it independently after the explanation |
| Claude (Anthropic) | Concept explanation — asked about how `tk.BooleanVar` links to a Checkbutton widget | Tested the behaviour in isolation before integrating into the main application |
| Claude (Anthropic) | Documentation review — README structure and section completeness reviewed | All content was written by the student; AI checked for missing sections against the rubric |

> All submitted code was written, read line-by-line, and tested by the student.  
> AI was used only as a reference and debugging aid — not to generate the complete solution.  
> The final code and all explanations reflect the student's own understanding.

---

*CNS1001 — Introduction to Programming | University of Technology, Jamaica | Semester 2, 2026*
