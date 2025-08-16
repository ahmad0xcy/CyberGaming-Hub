# 🎮 CyberGaming Hub - CTF Challenge

A modern, dark-themed gaming website with an **intentional Cross-Site Scripting (XSS) vulnerability** designed for Capture The Flag (CTF) security challenges.

## 🌟 Features

- **Modern Gaming Theme**: Dark, attractive design with neon accents and smooth animations
- **Responsive Design**: Works on desktop and mobile devices
- **Interactive Elements**: Search functionality, comment system, leaderboards, and tournaments
- **High-Quality UI**: Gaming-inspired color palette with purple, blue, and green neon accents
- **CTF Challenge**: Intentional XSS vulnerability for security testing

## 🚨 CTF Challenge: XSS Vulnerability

### Vulnerability Type
**Cross-Site Scripting (XSS)** - The website has an intentionally flawed input filter that can be bypassed using encoded or obfuscated payloads.

### Vulnerability Locations
1. **Search Functionality** (`/search` endpoint)
2. **Comment System** (`/comment` endpoint)

### How the Vulnerability Works
The server-side filter only strips obvious `<script>` tags but fails to handle:
- HTML entity encoding (e.g., `&lt;script&gt;`)
- URL encoding (e.g., `%3Cscript%3E`)
- Unicode encoding (e.g., `&#60;script&#62;`)
- Mixed encoding techniques

### Example Payloads That Bypass the Filter
```html
<!-- HTML Entity Encoding -->
&lt;script&gt;alert('XSS')&lt;/script&gt;

<!-- URL Encoding -->
%3Cscript%3Ealert('XSS')%3C/script%3E

<!-- Unicode Encoding -->
&#60;script&#62;alert('XSS')&#60;/script&#62;

<!-- Mixed Encoding -->
&lt;img src=x onerror=alert('XSS')&gt;
```

### Exploitation Steps
1. **Search Vector**: Go to the search section and enter an encoded XSS payload
2. **Comment Vector**: Go to the community section and post a comment with an encoded XSS payload
3. **Execution**: The payload will execute when the content is displayed in the browser

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.7 or higher
- pip (Python package installer)

### Quick Start
1. **Clone or download** the project files to your local machine
2. **Open a terminal/command prompt** in the project directory
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
4. **Run the application**:
   ```bash
   python app.py
   ```
5. **Open your browser** and navigate to `http://localhost:5000`

### Alternative Setup (if you don't have pip)
```bash
# Install Flask directly
python -m pip install Flask

# Run the application
python app.py
```

## 📁 Project Structure

```
CyberGaming-Hub/
├── app.py                 # Main Flask application with XSS vulnerability
├── requirements.txt       # Python dependencies
├── README.md             # This file
├── templates/
│   └── index.html        # Main HTML template
└── static/
    ├── css/
    │   └── style.css     # Gaming theme stylesheet
    └── js/
        └── script.js     # Frontend functionality and XSS demo
```

## 🔍 Testing the Vulnerability

### Method 1: Search Functionality
1. Navigate to the search section on the website
2. Enter one of the encoded payloads above
3. Submit the search
4. The XSS payload should execute in the search results

### Method 2: Comment System
1. Go to the community section
2. Fill in a username
3. Enter an encoded XSS payload in the comment field
4. Submit the comment
5. The payload should execute when the comment is displayed

### Browser Console
Open your browser's developer console (F12) to see detailed information about the vulnerability and helpful hints for the CTF challenge.

## 🎯 CTF Challenge Objectives

**Primary Goal**: Successfully execute an XSS payload on the website

**Challenge Levels**:
- **Beginner**: Execute a simple alert using HTML entity encoding
- **Intermediate**: Use URL encoding or Unicode encoding
- **Advanced**: Create a payload that steals user data or performs more complex attacks
- **Expert**: Chain multiple encoding techniques or use DOM-based XSS

**Learning Outcomes**:
- Understanding how input filters can be bypassed
- Recognizing the importance of proper input sanitization
- Learning about different encoding techniques used in XSS attacks
- Practicing real-world security testing scenarios

## 🛡️ Security Notes

⚠️ **IMPORTANT**: This application is intentionally vulnerable and should **NEVER** be deployed in a production environment or exposed to the internet.

**For CTF Use Only**:
- Run only on localhost or isolated networks
- Use only for educational purposes
- Do not use with real user data
- Ensure proper network isolation during testing

## 🎨 Design Features

- **Dark Theme**: Professional gaming aesthetic with dark backgrounds
- **Neon Accents**: Cyan, magenta, and green neon highlights
- **Modern Typography**: Orbitron (headings) and Rajdhani (body text) fonts
- **Smooth Animations**: Floating elements, gradient shifts, and hover effects
- **Responsive Layout**: Adapts to different screen sizes
- **Interactive Elements**: Hover effects, smooth scrolling, and dynamic content

## 🚀 Customization

### Modifying the Vulnerability
To make the challenge easier or harder, edit the `flawed_xss_filter()` function in `app.py`:

```python
def flawed_xss_filter(user_input):
    # Make it easier: Remove the filter entirely
    # return user_input
    
    # Make it harder: Add more sophisticated filtering
    # filtered = re.sub(r'<[^>]*>', '', user_input)
    
    # Current: Basic filter that can be bypassed
    filtered = re.sub(r'<script[^>]*>.*?</script>', '', user_input, flags=re.IGNORECASE | re.DOTALL)
    return filtered
```

### Changing the Theme
Modify `static/css/style.css` to change colors, fonts, or overall appearance.

### Adding New Features
Extend the Flask application in `app.py` to add new vulnerable endpoints or modify existing ones.

## 📚 Learning Resources

- **OWASP XSS Prevention**: https://owasp.org/www-project-cheat-sheets/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
- **XSS Filter Evasion**: https://owasp.org/www-community/attacks/xss/
- **Flask Security**: https://flask-security.readthedocs.io/

## 🤝 Contributing

This is a CTF challenge project. If you find ways to improve the vulnerability or add new challenges, feel free to contribute!

## 📄 License

This project is created for educational purposes and CTF challenges. Use responsibly and only in controlled, isolated environments.

---

**Happy Hacking! 🎯🔓**

*Remember: This is a learning tool. Always practice security testing in safe, controlled environments.*
