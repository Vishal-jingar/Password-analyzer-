#  Password Strength Analyzer & Custom Wordlist Generator

This is a beginner-friendly Python tool that helps you:

1. Check how strong a password is using real-world crack time estimates.
2. Generate a simple wordlist based on personal information (like name, pet, and year) — useful for learning how attackers guess passwords.

---

##  Features

-  Password strength scoring (0 to 4)
-  Estimated crack time
-  Security suggestions
-  Custom wordlist creation using:
  - Name
  - Pet name
  - Year of birth
-  Wordlist saved to `.txt` file

---

## 🛠 Tools & Technologies

- Python 3
- [zxcvbn](https://github.com/dropbox/zxcvbn) (password strength library)


## How to Run

1. **Clone the repo** or download the script:
   ```bash
   git clone https://github.com/Vishal-jingar/Password tool.py
   cd password-tool

The main script you can copy pste in your pyhton.

##
import itertools
from zxcvbn import zxcvbn
import re

def analyze_password_strength():
    print("\n Password Strength Analyzer")
    password = input("Enter a password to check: ")
    result = zxcvbn(password)
    
    print("\n Score (0=Weak, 4=Strong):", result['score'])
    print(" Estimated Crack Time:", result['crack_times_display']['offline_fast_hashing_1e10_per_second'])
    print(" Feedback:")
    for tip in result['feedback']['suggestions']:
        print("   -", tip)
hasattr
def generate_custom_wordlist():
    print("\n Custom Wordlist Generator")
    name = input("Enter your name: ")
    pet = input("Enter your pet's name: ")
    birth_year = input("Enter your birth year: ")

    base_words = [name, pet, birth_year]
    patterns = []

    # Basic combinations
    for word in base_words:
        patterns.append(word)
        patterns.append(word + "123")
        patterns.append(word + "@" + birth_year)
    
    # Combine all 2-word combinations
    for combo in itertools.permutations(base_words, 2):
        patterns.append("".join(combo))

    # Add leetspeak replacements
    leet = {'a': '@', 'e': '3', 'i': '1', 'o': '0', 's': '$'}
    final_list = []
    for word in patterns:
        variants = [word]
        for letter, sub in leet.items():
            variants += [re.sub(letter, sub, word, flags=re.IGNORECASE)]
        final_list += list(set(variants))

    final_list = list(set(final_list))  # remove duplicates

    with open("custom_wordlist.txt", "w") as f:
        for item in final_list:
            f.write(item + "\n")

    print(f"\n Wordlist saved as 'custom_wordlist.txt' with {len(final_list)} entries.")

def main():
    print(" PASSWORD TOOL MENU")
    print("1. Analyze Password Strength")
    print("2. Generate Custom Wordlist")
    choice = input("Enter your choice (1 or 2): ")

    if choice == "1":
        analyze_password_strength()
    elif choice == "2":
        generate_custom_wordlist()
    else:
        print("Invalid choice.")

if __name__ == "__main__":
    main()

---
