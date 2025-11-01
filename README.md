# -Python-Projects-
Developed a Python tool to analyze password strength. The script uses regular expressions (regex) to validate passwords against security criteria like length, mixed cases, numbers, and special characters, providing immediate feedback. A foundational project in applying Python for cybersecurity.
import tkinter as tk
from tkinter import messagebox
import re

def check_password_strength(password):
    score = 0
    feedback = []

    if len(password) >= 8:
        score += 1
    else:
        feedback.append("- Be at least 8 characters long.")

    if re.search("[A-Z]", password):
        score += 1
    else:
        feedback.append("- Contain at least one uppercase letter.")

    if re.search("[a-z]", password):
        score += 1
    else:
        feedback.append("- Contain at least one lowercase letter.")

    if re.search("[0-9]", password):
        score += 1
    else:
        feedback.append("- Contain at least one number.")

    if re.search("[_@$!%*?&]", password):
        score += 1
    else:
        feedback.append("- Contain at least one special character (_@$!%*?&).")

    if score == 5:
        return "Strong", []
    elif score >= 3:
        return "Medium", feedback
    else:
        return "Weak", feedback

def check_strength_button_click():
    password = password_entry.get()
    strength, feedback = check_password_strength(password)
    
    result_message = f"Password Strength: {strength}\n"
    if feedback:
        result_message += "\nSuggestions to improve your password:\n"
        result_message += "\n".join(feedback)
        
    messagebox.showinfo("Password Strength Result", result_message)


# --- Create the main window ---
window = tk.Tk()
window.title("Password Strength Checker")

# --- Create and place the widgets ---
# Label for the password entry
password_label = tk.Label(window, text="Enter your password:")
password_label.pack(pady=5)

# Entry widget for password input
password_entry = tk.Entry(window, show="*") # show="*" hides the password
password_entry.pack(pady=5, padx=20)

# Button to check the strength
check_button = tk.Button(window, text="Check Strength", command=check_strength_button_click)
check_button.pack(pady=10)

# --- Start the GUI event loop ---
window.mainloop()
