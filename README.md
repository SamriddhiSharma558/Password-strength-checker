# Password-strength-checker
python

```python

import streamlit as st
import re

st.set_page_config(page_title="Password Strength Checker", page_icon="🔐")

st.title("🔐 Password Strength Checker")
st.write("Check the strength of your password.")

password = st.text_input("Enter Password", type="password")

if password:

    length = len(password) >= 8
    uppercase = bool(re.search(r"[A-Z]", password))
    lowercase = bool(re.search(r"[a-z]", password))
    number = bool(re.search(r"[0-9]", password))
    special = bool(re.search(r"[^A-Za-z0-9]", password))

    checks = {
        "At least 8 characters": length,
        "Uppercase letter": uppercase,
        "Lowercase letter": lowercase,
        "Number": number,
        "Special character": special
    }

    score = sum(checks.values())

    if score <= 2:
        strength = "Weak"
    elif score <= 4:
        strength = "Moderate"
    else:
        strength = "Strong"

    st.subheader("Password Analysis")

    st.write("Password Score:", score, "/5")
    st.write("Password Strength:", strength)

    st.progress(score / 5)

    if strength == "Weak":
        st.error("Your password is weak!")
    elif strength == "Moderate":
        st.warning("Your password is moderate.")
    else:
        st.success("Your password is strong!")

    st.subheader("Password Checklist")

    for name, result in checks.items():
        if result:
            st.write("✅", name)
        else:
            st.write("❌", name)

    st.subheader("Suggestions")

    if not length:
        st.write("- Use at least 8 characters.")

    if not uppercase:
        st.write("- Add an uppercase letter.")

    if not lowercase:
        st.write("- Add a lowercase letter.")

    if not number:
        st.write("- Add a number.")

    if not special:
        st.write("- Add a special character.")

    if score == 5:
        st.success("All password criteria are satisfied!")

else:
    st.info("Please enter a password to check its strength.")
```
