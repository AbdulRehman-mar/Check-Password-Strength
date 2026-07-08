# Password Strength Assessment — Three Methods

A CEH lab exploring three different ways to assess password strength: using Cracklib on Kali Linux, a Python GUI-terminal script in Visual Studio Code (Windows), and a Python script run directly in the Kali Linux terminal.

**Author:** Abdur Rahman Akhtar
**Registration No:** 94012
**Batch No:** 056
**Course:** Cyber Security
**Institute:** PNY Trainings

📄 Full report: [`project_1_password_strength_checker.docx`](./project_1_password_strength_checker.docx) · [PDF](./project_1_password_strength_checker.pdf)

---

## 📌 Objective
Assess and evaluate password strength using three different approaches, and identify weak passwords that may be vulnerable to password attacks.

## 🧭 Three Methods Covered
1. **Cracklib** (Kali Linux utility)
2. **Python in Visual Studio Code** (Windows)
3. **Python script in Kali Linux terminal**

---

## 1️⃣ Cracklib (Kali Linux)

**Requirements:** Kali Linux, Cracklib Runtime package, terminal access, min 4 GB RAM.

**Commands:**
```bash
sudo apt update
sudo apt install cracklib-runtime -y
cracklib-check
# Then enter a password to check its strength, e.g.:
Hello613@

# Or check a specific password directly:
echo "Password123" | cracklib-check
```

**Procedure:** Open terminal → update repo → install Cracklib → run `cracklib-check` → enter test passwords → observe and classify output as weak/strong.

**Observations:**
| Password | Cracklib Result |
|---|---|
| password123 | Based on a dictionary word |
| admin123 | Based on a dictionary word |
| Welcome2026 | OK |
| Abdul@2026 | OK |
| A9#kL2@xP7!mQ4$z | OK |

**Result:** Cracklib successfully flagged dictionary-based and predictable passwords as weak, while accepting passwords with sufficient length and complexity.

---

## 2️⃣ Python in Visual Studio Code (Windows)

**Requirements:** Windows 10/11, VS Code, Python 3.x, Python extension, `re` module.

**Program logic** — a password is checked for:
- Minimum 8 characters
- At least one digit
- At least one uppercase letter
- At least one lowercase letter
- At least one special character

**Procedure:** Install Python 3 and VS Code → create `password_checker.py` → paste code → run from the VS Code terminal → test with different passwords.

**Sample Results:**
| Password | Result |
|---|---|
| password | Weak |
| Password1 | Medium |
| Password1@ | Strong |
| Admin123 | Medium |
| Admin123@ | Strong |

---

## 3️⃣ Python in Kali Linux Terminal

**Requirements:** Kali Linux, Python 3, Nano editor, terminal.

**Program code** (`password_checker.py`):
```python
# password strength checker
import re

# password strength check conditions:
# min 8 chars, digit, uppercase, lowercase, special char
def check_password_strength(password):
    """
    Function to check the strength of a password.
    """
    if len(password) < 8:
        return "Weak: Password must be at least 8 characters long."
    if not any(char.isdigit() for char in password):
        return "Weak: Password must include at least one number."
    if not any(char.isupper() for char in password):
        return "Weak: Password must include at least one uppercase letter."
    if not any(char.islower() for char in password):
        return "Weak: Password must include at least one lowercase letter."
    if not re.search(r'[!@#$%^&*(),.?":{}|<>]', password):
        return "Medium: Add special characters to make your password stronger."
    return "Strong: Your password is secure!"

def password_checker():
    """
    Main function to take user input and check password strength.
    """
    print("Welcome to the Password Strength Checker!")
    while True:
        password = input("\nEnter your password (or type 'exit' to quit): ")
        if password.lower() == "exit":
            print("Thank you for using the Password Strength Checker! Goodbye!")
            break
        result = check_password_strength(password)
        print(result)

# Run the password checker
if __name__ == "__main__":
    password_checker()
```

**Commands used:**
```bash
nano password_checker.py     # create file, paste code
# Save & exit: Ctrl+O → Enter → Ctrl+X
python3 password_checker.py  # run program
```

**Sample Output:**
```
Enter your password (or type 'exit' to quit): password
Weak: Password must include at least one number.

Enter your password (or type 'exit' to quit): Password1
Medium: Add special characters to make your password stronger.

Enter your password (or type 'exit' to quit): Password1@
Strong: Your password is secure!
```

---

## ✅ Overall Conclusion
Across all three approaches — Cracklib, Python in VS Code, and Python in the Kali terminal — weak passwords based on dictionary words or lacking complexity were consistently flagged, while passwords combining length, uppercase/lowercase letters, digits, and special characters were rated strong. The labs demonstrate the importance of enforcing multi-factor password complexity rules to defend against password attacks.

## 🛠️ Skills Demonstrated
- Linux package management and Cracklib usage
- Python scripting for security validation (regex, conditionals, loops)
- Cross-platform development (Windows/VS Code and Kali Linux/Nano)
- Password policy design and evaluation
