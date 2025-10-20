# Password Breach Checker

A web-based tool that checks if a password has been compromised in known data breaches, helping users maintain secure passwords.

Created by [G-Gangalapudi](https://github.com/G-Gangalapudi)

---

## Overview

Password Breach Checker is a client-side web application that verifies whether your password has appeared in known data breaches. By using the Have I Been Pwned API with k-anonymity, this tool protects your privacy while checking billions of compromised passwords.

**Key Feature:** Your actual password never leaves your browser. Only a partial hash is sent to the API, making it impossible for anyone (including the API service) to determine your actual password.

---

## Features

- **Privacy-First Design**: Uses k-anonymity model - only the first 5 characters of your password's SHA-1 hash are sent to the API
- **Client-Side Security**: All hashing happens in your browser - no server-side processing
- **Real-Time Checking**: Queries the Have I Been Pwned API against billions of breached passwords
- **Simple Interface**: Clean, user-friendly web interface
- **No Password Transmission**: Your actual password never leaves your browser
- **Responsive Design**: Works on desktop, tablet, and mobile devices
- **Instant Results**: Get immediate feedback on password security

---

## How It Works

1. You enter a password in the web interface
2. JavaScript creates a SHA-1 hash of your password locally in your browser
3. Only the first 5 characters of the hash are sent to the Have I Been Pwned API via HTTPS
4. The API returns all hash suffixes that match those first 5 characters
5. The tool compares the full hash locally in your browser to determine if your password has been breached
6. You receive immediate visual feedback on whether your password is compromised

This method ensures that:
- Your password is never transmitted over the internet
- The API cannot determine what password you're checking
- The hash cannot be reverse-engineered to reveal your password
- Everything runs securely in your browser

---

## Technologies Used

- **HTML5**: Structure and semantic markup
- **CSS3**: Styling and responsive design
- **JavaScript (ES6+)**: Client-side logic and API integration
- **Crypto API**: SHA-1 hashing (or SubtleCrypto Web API)
- **Fetch API**: Communication with Have I Been Pwned API
- **Docker**: Containerization for easy deployment

---

## Installation & Setup

### Option 1: Run with Docker (Recommended)

```bash
# Pull and run the Docker image
docker run -p 3000:80 razrvfx/password-strength-checker:latest

# Access the application at:
# http://localhost:3000
```

Using a different port:

```bash
docker run -p 8080:80 razrvfx/password-strength-checker:latest
# Now accessible at http://localhost:8080
```

### Option 2: Use Directly (No Installation Required)

Simply open `index.html` in your web browser. The app runs entirely client-side!

### Option 3: Clone and Run Locally

```bash
# Clone the repository
git clone https://github.com/G-Gangalapudi/Password-Breach-Checker.git

# Navigate to the project directory
cd Password-Breach-Checker

# Open index.html in your browser
# On macOS:
open index.html

# On Linux:
xdg-open index.html

# On Windows:
start index.html
```

### Option 4: Run with a Local Server

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (with http-server installed)
npx http-server

# Then open http://localhost:8000 in your browser
```

---

## Usage

1. Open the application in your web browser (or via Docker)
2. Enter the password you want to check in the input field
3. Click the "Check Password" button
4. View the results:
   - **✅**: Password has NOT been found in breaches
   - **❌**: Password HAS been found in breaches (with count)

---

## File Structure

```
Password-Breach-Checker/
├── .github/
│   └── workflows/
│       └── docker-image.yaml    # GitHub Actions CI/CD pipeline
├── Dockerfile                   # Docker configuration
├── index.html                   # Main HTML structure with embedded JavaScript
├── styles.css                   # Styling and layout
└── README.md                    # This file
```

Note: The JavaScript is embedded directly in `index.html` for simplicity and ease of deployment.

---

## Docker Details

### Dockerfile Overview
The Dockerfile:

- Uses NGINX Alpine
- Copies both index.html and styles.css
- Serves on port 80
- Removes default NGINX content

### Automated Builds

The GitHub Actions workflow (`docker-image.yaml`) automatically:

- Builds the Docker image on code changes
- Pushes to Docker Hub
- Tags with latest and git commit SHA

---

## Privacy & Security

### Your Privacy is Protected

- **Client-Side Only**: All processing happens in your browser
- **No Server**: No backend server storing or processing passwords
- **No Password Transmission**: Your password is hashed locally using SHA-1 before any data leaves your browser
- **K-Anonymity Model**: Only the first 5 characters of the hash are sent, protecting your privacy
- **HTTPS Encryption**: All API communication is encrypted
- **No Logging**: The Have I Been Pwned API does not log which hashes are searched

### Technical Details

The tool implements the k-anonymity model as described in Troy Hunt's blog post: [Validating Leaked Passwords with k-Anonymity](https://www.troyhunt.com/ive-just-launched-pwned-passwords-version-2/)

The process:
1. Password → SHA-1 Hash in browser (e.g., `5BAA61E4C9B93F3F0682250B6CF8331B7EE68FD8`)
2. First 5 chars sent to API (e.g., `5BAA6`)
3. API returns all matching suffixes
4. Local comparison in browser determines if full hash matches

---

## Browser Compatibility

This tool works in all modern browsers that support:
- ES6 JavaScript
- Fetch API
- Web Crypto API (or SHA-1 implementation)

Tested on:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Opera 76+

---

## About Data Breaches

Data breaches occur when attackers compromise websites and steal user databases containing passwords. Even secure websites can be breached. Some of the largest breaches include:

- **Collection #1** (2019): 773 million email addresses
- **RockYou** (2009): 32 million passwords
- **LinkedIn** (2012): 117 million accounts
- **Yahoo** (2013-2014): 3 billion accounts

The Have I Been Pwned service aggregates data from hundreds of breaches, tracking over 12 billion compromised accounts.

---

## Best Practices

After checking your password:

✅ **If your password is breached:**
- Change it immediately on all accounts where you've used it
- Never reuse this password again
- Enable two-factor authentication (2FA) wherever possible

✅ **For all passwords:**
- Use long, unique passwords for each account (12+ characters)
- Consider using a password manager
- Use passphrases like "Coffee-Mountain-Purple-42"
- Enable 2FA on all important accounts

---

## Contributing

Contributions are welcome! If you'd like to improve this tool:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and commit: `git commit -m 'Add feature'`
4. Push to the branch: `git push origin feature-name`
5. Submit a Pull Request

### Ideas for Contributions

- Add password strength meter
- Implement dark mode toggle
- Add multiple language support
- Show password breach history/details
- Add password generation tool
- Improve mobile responsiveness
- Add loading animations
- Create browser extension version

---

## Deployment

### Docker Deployment
Your Docker image is available on Docker Hub:

``` bash
docker pull razrvfx/password-breach-checker:latest
docker run -p 3000:3000 razrvfx/password-breach-checker:latest
```

### GitHub Pages (Free Hosting)

1. Go to your repository settings
2. Navigate to "Pages" section
3. Select main branch as source
4. Your site will be live at: `https://g-gangalapudi.github.io/Password-Breach-Checker/`

### Other Hosting Options

- Netlify
- Vercel
- Cloudflare Pages
- Any static hosting service

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## Disclaimer

This tool is provided for educational and security purposes. It helps users verify if their passwords have been compromised in known data breaches. 

- This tool does NOT store, log, or transmit your actual passwords
- All processing happens client-side in your browser
- Always use strong, unique passwords for each account
- This tool cannot guarantee complete security - practice good password hygiene

---

## Acknowledgments

- [Have I Been Pwned](https://haveibeenpwned.com/) - Troy Hunt's excellent breach notification service
- [Pwned Passwords API](https://haveibeenpwned.com/API/v3#PwnedPasswords) - The API that powers this tool

---

## Support

If you find this tool useful, please ⭐ star this repository!

For issues, questions, or suggestions, please open an issue on GitHub.

---

**Stay secure! 🔒**
