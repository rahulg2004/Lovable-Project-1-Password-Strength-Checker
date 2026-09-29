# 🔐 Password Strength Checker

A modern, privacy-focused **Password Strength Checker and Secure Password Generator** built with React, TypeScript, Tailwind CSS, and TanStack Start.

Password Guard Locket analyses passwords directly in the browser and provides a detailed security assessment based on length, character complexity, uniqueness, entropy, predictable patterns, common passwords, dictionary words, and estimated offline crack time.

The application also includes a configurable password generator, masked local password-check history, security recommendations, report export, dark/light mode, responsive design, and animated security visualisations.

> 🔒 **Privacy First:** Password analysis is performed locally in the browser. The application does not send the password to a backend service for analysis.

---

## ✨ Features

### 🔍 Real-Time Password Analysis

Enter or paste a password and receive a live security assessment.

The application checks:

* 📏 Password length
* 🔠 Uppercase characters
* 🔡 Lowercase characters
* 🔢 Numbers
* 🔣 Special characters
* 🔁 Repeated characters and patterns
* 🔢 Sequential characters
* ⌨️ Keyboard patterns
* 🚨 Common passwords
* 📖 Dictionary words
* 🧮 Estimated entropy
* ⏱️ Estimated offline crack time

Password analysis is debounced by 120 ms to avoid unnecessary calculations while typing.

---

## 💪 Password Strength Scoring

Each password receives a score from **0 to 100**.

The score is calculated using five weighted categories:

| Category             | Maximum Score |
| -------------------- | ------------: |
| 📏 Length            |            30 |
| 🧩 Complexity        |            25 |
| 🆕 Uniqueness        |            20 |
| 🧮 Entropy           |            15 |
| 🔍 Pattern Detection |            10 |
| **Total**            |       **100** |

The application maps the final score to six strength levels:

* 🔴 **Very Weak**
* 🟠 **Weak**
* 🟡 **Fair**
* 🟢 **Good**
* 🟩 **Strong**
* 🟢 **Excellent**

Additional score limits are applied when a password is very short or identified as a common password.

---

## 🧠 Password Analysis Engine

The main password-analysis logic is implemented in:

```text
src/utils/password.ts
```

### Entropy Estimation

The application estimates entropy based on the character classes detected in the password:

* Lowercase letters
* Uppercase letters
* Numbers
* Symbols

It also considers the ratio of unique characters to total password length.

The result is displayed in bits and used as one component of the overall strength score.

### Pattern Detection

The application detects several types of predictable patterns.

#### Repeated Characters

Examples:

```text
aaa
111
!!!
```

It also checks for repeated multi-character patterns.

#### Sequential Characters

Examples:

```text
abc
bcd
123
456
```

Both increasing and decreasing sequences are checked.

#### Keyboard Patterns

The application checks common keyboard walks such as:

```text
qwerty
asdf
zxcv
123456
qaz
wsx
```

Both normal and reversed keyboard sequences are considered.

#### Common Password Detection

A built-in list contains commonly used passwords such as:

```text
123456
password
qwerty
admin
welcome
letmein
football
secret
test123
```

The application also checks whether a password contains a common password as a substring.

#### Dictionary Word Detection

The application checks for common dictionary words such as:

```text
password
welcome
summer
winter
money
hello
computer
dragon
football
google
school
coffee
```

---

## 📊 Password Requirements

The interface provides a live checklist containing:

* At least 8 characters
* At least 12 characters recommended
* Uppercase letter
* Lowercase letter
* Number
* Special character
* No repeated patterns
* Not a common password
* No sequential characters

Each requirement dynamically changes between a success and failure state as the password is analysed.

---

## 📈 Password Statistics

The application displays detailed statistics for the current password.

### Character Statistics

* Total length
* Unique characters
* Uppercase count
* Lowercase count
* Number count
* Symbol count

### Security Statistics

* Estimated entropy in bits
* Estimated offline crack time

---

## ⏱️ Estimated Crack Time

The application estimates the time required for an offline attacker to guess a password.

The calculation uses an assumed attack rate of:

```text
10 billion guesses per second
```

The estimated time is calculated from the password's entropy and then presented using readable units such as:

```text
Instantly
Seconds
Minutes
Hours
Days
Months
Years
Centuries
Million years
Beyond a lifetime of the universe
```

> ⚠️ Crack-time estimates are mathematical approximations based on the assumptions used by the application. Real-world attack speeds vary depending on the hashing algorithm, hardware, password-storage practices, rate limits, and other security controls.

---

# ⚙️ Secure Password Generator

Password Guard Locket includes a configurable password generator.

### Generator Controls

Users can configure:

* 📏 Password length
* 🔠 Uppercase letters
* 🔡 Lowercase letters
* 🔢 Numbers
* 🔣 Symbols
* 🚫 Exclude ambiguous characters
* 📖 Easy-to-read mode

### Password Length

The generator supports lengths from:

```text
8 to 64 characters
```

The default configuration generates a 20-character password using:

```text
Uppercase
Lowercase
Numbers
Symbols
```

with ambiguous characters excluded.

### Randomness

The generator uses the browser's:

```javascript
crypto.getRandomValues()
```

when available instead of relying exclusively on `Math.random()`.

This provides a stronger source of randomness for password generation in supported browsers.

### Generate and Analyse

Generated passwords can immediately be passed into the password analyser using:

```text
Generate strong password & analyse it
```

This allows users to generate a password and then inspect its score, entropy, requirements, and estimated crack time.

---

# 🔐 Privacy Architecture

Privacy is a central design goal of the application.

### Client-Side Password Analysis

The password analysis functions execute in the browser.

The project does not contain a database, authentication system, password API, or external password-analysis service.

The application therefore does not need to transmit passwords to a remote analysis server.

### Password History

Recent checks are stored locally using:

```text
localStorage
```

However, the application stores a **masked representation** rather than the original password.

For example:

```text
my••••••••rd
```

The history is limited to the five most recent unique masked entries.

### Exported Reports

The application can export a text report containing:

* Score
* Strength level
* Password length
* Character statistics
* Entropy
* Estimated crack time
* Security suggestions

The actual password is explicitly excluded from the exported report.

### Clipboard

Password copying is performed only when the user explicitly presses the copy button.

The application uses the browser Clipboard API when available.

---

# 🌓 Dark and Light Mode

The interface supports:

* ☀️ Light mode
* 🌙 Dark mode

The selected theme is persisted using browser `localStorage`.

If no saved preference exists, the application checks the user's system colour preference using:

```javascript
prefers-color-scheme
```

---

# 🎨 User Interface

The application uses a modern glassmorphism-inspired interface.

### Design Features

* 🪟 Glass-effect cards
* 🌈 Gradient background effects
* 🔵 Rounded UI elements
* ✨ Smooth animations
* 📊 Animated progress indicators
* ⭕ Circular security score
* 🌓 Dark/light theme
* 📱 Responsive layouts
* 🎯 Clear visual hierarchy
* 🔤 Dedicated display, sans-serif, and monospace typography

The design system is implemented primarily through Tailwind CSS and custom CSS variables.

---

# 🎬 Animations

Animations are implemented using the `motion` library.

Animated elements include:

* Glass card entrance animations
* Strength progress bars
* Circular score indicator
* Entropy meter
* Requirement state transitions
* Feedback messages
* Theme icon transitions
* Background floating effects
* Interactive button states

The stylesheet also includes support for:

```text
prefers-reduced-motion
```

to reduce animation for users who request reduced motion.

---

# ♿ Accessibility

The application includes several accessibility-oriented features:

* Semantic HTML elements
* Accessible form labels
* ARIA labels
* ARIA live regions
* Screen-reader descriptions
* Keyboard-accessible controls
* Visible focus indicators
* Progress-bar accessibility attributes
* Accessible show/hide password controls
* Reduced-motion support

For example, the password strength meter exposes its current score through a `progressbar` role and ARIA attributes.

---

# 🕘 Recent Password Checks

The application maintains a small local history of recently analysed passwords.

History entries include:

```text
Masked password
Strength level
Score
Timestamp
```

Only the masked representation is displayed.

The history is intentionally limited to five entries.

---

# 📄 Export Security Report

Users can export a `.txt` report containing the current analysis.

Example structure:

```text
Password Strength Report

Generated: [date and time]

Score: 82/100 (Strong)
Length: 16
Unique characters: 15
Uppercase / lowercase / numbers / symbols: 3 / 7 / 3 / 3
Entropy: 61.4 bits
Estimated crack time: ...

Suggestions:
- ...

Note: the password itself is never included in this report.
```

This allows users to save or share analysis results without exposing the password itself through the generated report.

---

# 💡 Security Education

The application includes built-in security guidance covering topics such as:

### Never Reuse Passwords

A compromised password can put multiple accounts at risk when the same credential is reused.

### Use a Password Manager

Password managers can generate and store long, unique credentials.

### Enable MFA

Multi-factor authentication adds another authentication factor beyond the password.

### Avoid Personal Information

Personal information can make passwords easier to predict.

### Prefer Random Passphrases

Long combinations of unrelated words can provide a practical alternative to short predictable passwords.

### Change Compromised Credentials

Credentials should be changed when a service reports that they have been compromised.

---

# 🏗️ Project Architecture

The application follows a modular React architecture.

```text
User Input
    │
    ▼
PasswordInput
    │
    ▼
Debounced Password Value
    │
    ▼
calculateStrength()
    │
    ├── validatePassword()
    ├── getPasswordStats()
    ├── estimateEntropy()
    ├── hasRepeatedCharacters()
    ├── hasSequentialCharacters()
    ├── hasKeyboardPattern()
    ├── isCommonPassword()
    └── containsDictionaryWord()
    │
    ▼
StrengthResult
    │
    ├── Strength Meter
    ├── Security Score
    ├── Requirements
    ├── Suggestions
    ├── Statistics
    ├── Entropy
    └── Crack-Time Estimate
```

The password generator follows a separate flow:

```text
Generator Options
       │
       ▼
generatePassword()
       │
       ▼
Cryptographically Random Selection
       │
       ▼
Generated Password
       │
       ▼
Password Analyzer
```

---

# 📁 Project Structure

```text
Password-Guard-Locket/
│
├── public/
│   ├── favicon.ico
│   └── robots.txt
│
├── src/
│   │
│   ├── components/
│   │   ├── GlassCard.tsx
│   │   ├── PasswordGenerator.tsx
│   │   ├── PasswordHistory.tsx
│   │   ├── PasswordInput.tsx
│   │   ├── PasswordStats.tsx
│   │   ├── RequirementsList.tsx
│   │   ├── ScoreRing.tsx
│   │   ├── SecurityTips.tsx
│   │   ├── StrengthMeter.tsx
│   │   ├── Suggestions.tsx
│   │   ├── ThemeToggle.tsx
│   │   ├── strength-colors.ts
│   │   │
│   │   └── ui/
│   │       └── Reusable Radix UI components
│   │
│   ├── data/
│   │   └── password-data.ts
│   │
│   ├── hooks/
│   │   ├── use-debounced-value.ts
│   │   ├── use-mobile.tsx
│   │   └── use-theme.ts
│   │
│   ├── lib/
│   │   ├── error-capture.ts
│   │   ├── error-page.ts
│   │   ├── lovable-error-reporting.ts
│   │   └── utils.ts
│   │
│   ├── routes/
│   │   ├── __root.tsx
│   │   ├── index.tsx
│   │   └── README.md
│   │
│   ├── types/
│   │   └── password.ts
│   │
│   ├── utils/
│   │   └── password.ts
│   │
│   ├── router.tsx
│   ├── routeTree.gen.ts
│   ├── server.ts
│   ├── start.ts
│   └── styles.css
│
├── .gitignore
├── bun.lock
├── bunfig.toml
├── components.json
├── eslint.config.js
├── package.json
├── prettier.config
├── tsconfig.json
└── vite.config.ts
```

---

# 🛠️ Technologies Used

### Frontend

* ⚛️ React 19
* 🔷 TypeScript
* 🎨 Tailwind CSS 4
* ⚡ Vite
* 🧭 TanStack Router
* 🚀 TanStack Start

### UI & Components

* 🧩 Radix UI
* 🎨 Tailwind CSS
* 🎬 Motion
* 🖼️ Lucide React

### Forms & Validation

* React Hook Form
* Zod
* Hook Form Resolvers

### Data & Utilities

* TanStack React Query
* date-fns
* clsx
* tailwind-merge

### Development Tools

* ESLint
* Prettier
* TypeScript
* Bun lockfile
* Vite

---

# ⚡ Installation

## 1. Clone the Repository

```bash
git clone https://github.com/rahulg2004/Lovable-Project-1-Password-Guard-Locket.git
```

## 2. Navigate to the Project

```bash
cd Lovable-Project-1-Password-Guard-Locket
```

## 3. Install Dependencies

Using npm:

```bash
npm install
```

Or using Bun:

```bash
bun install
```

---

# 🚀 Run the Development Server

Using npm:

```bash
npm run dev
```

Or using Bun:

```bash
bun run dev
```

The application will be available through the local Vite development server.

---

# 🏭 Production Build

Create a production build with:

```bash
npm run build
```

For a development-mode build:

```bash
npm run build:dev
```

Preview the production build with:

```bash
npm run preview
```

---

# 🧹 Code Quality

Run ESLint:

```bash
npm run lint
```

Format the project:

```bash
npm run format
```

The project uses strict TypeScript configuration and reusable React components to maintain a structured codebase.

---

# 🔑 Important Functions

The main password-security functionality is contained in:

```text
src/utils/password.ts
```

Important functions include:

```typescript
calculateStrength()
```

Calculates the overall password score and returns the complete analysis.

```typescript
estimateEntropy()
```

Estimates password entropy.

```typescript
estimateCrackTime()
```

Converts estimated entropy into a human-readable crack-time estimate.

```typescript
getPasswordStats()
```

Calculates password character statistics.

```typescript
validatePassword()
```

Checks the password against the application's security requirements.

```typescript
hasRepeatedCharacters()
```

Detects repeated characters and repeated patterns.

```typescript
hasSequentialCharacters()
```

Detects sequential characters.

```typescript
hasKeyboardPattern()
```

Detects common keyboard walks.

```typescript
isCommonPassword()
```

Checks against the built-in common-password dataset.

```typescript
containsDictionaryWord()
```

Checks for common dictionary words.

```typescript
generatePassword()
```

Generates a configurable random password.

---

# 🔒 Security Considerations

Password Guard Locket is designed as a **local password-analysis tool**, not as a password-storage system.

Important considerations:

* Password analysis happens locally in the browser.
* No password database is implemented.
* No remote password-analysis API is used.
* Recent history stores masked passwords rather than plaintext passwords.
* Exported reports do not contain the original password.
* Theme preferences are stored locally.
* Clipboard access occurs only when the user requests copying.
* The generator uses `crypto.getRandomValues()` where supported.

### Important Limitation

The application's entropy and crack-time calculations are educational estimates rather than a replacement for professional password-auditing systems such as dedicated password-strength libraries, breach databases, or password managers.

The built-in common-password and dictionary datasets are also intentionally limited and should not be interpreted as a complete compromised-password database.

---

# 📱 Responsive Design

The interface adapts to different screen sizes using responsive Tailwind CSS layouts.

The main dashboard uses a responsive grid that changes from a multi-column desktop layout to a mobile-friendly single-column layout.

The generator controls, statistics, requirements, security tips, and analysis cards also adapt to smaller screens.

---

# 🎯 Learning Outcomes

This project provided practical experience in:

* ⚛️ React component development
* 🔷 TypeScript interfaces and type-safe programming
* 🧠 Algorithm design
* 🔐 Password-security concepts
* 🧮 Entropy estimation
* 📊 Weighted scoring systems
* 🔍 Pattern detection
* 🎲 Secure random password generation
* 💾 Browser local storage
* 📋 Clipboard API
* 🎨 Tailwind CSS
* 🧩 Reusable UI components
* 🎬 Motion-based animations
* ♿ Web accessibility
* 📱 Responsive web design
* 🧭 TanStack routing
* ⚡ Vite development
* 🧹 ESLint and Prettier
* 🏗️ Modular project architecture

---

# 🔮 Future Enhancements

Potential future improvements include:

* 🔎 Integration with a trusted breach-checking service using privacy-preserving methods
* 🧠 More comprehensive password dictionaries
* 📚 Larger compromised-password datasets
* 🔐 Passphrase generation
* 🧪 Automated unit tests for password-analysis algorithms
* 📊 Historical strength charts
* 📱 Progressive Web App support
* 🌐 Improved offline support
* 🔑 Password-manager integration
* 🧮 More sophisticated entropy estimation
* ⚙️ Custom scoring profiles
* 📋 Additional export formats
* 🔒 Optional encrypted local history

---

# 📸 Screenshots

Add screenshots of the application here:

```text
screenshots/
├── dashboard.png
├── password-analysis.png
├── password-generator.png
├── security-score.png
└── dark-mode.png
```

Example:

```markdown
![Password Guard Locket Dashboard](screenshots/dashboard.png)
```

---

# 🌐 Live Demo

🔗 **Live Application:**
https://password-guard-locket.lovable.app

---

# 💻 Repository

🔗 **GitHub:**
https://github.com/rahulg2004/Lovable-Project-1-Password-Guard-Locket

---

# 👨‍💻 Author

**Rahul Gupta**

B.Sc. (Hons) Computer Science | University of Delhi

GitHub:
https://github.com/rahulg2004

LinkedIn:
https://linkedin.com/in/rg-rr2004

---

# 📄 License

This project is intended for educational and portfolio purposes.

If you plan to distribute or reuse the project commercially, add an appropriate open-source licence such as MIT after confirming the licensing requirements of the project's dependencies and any third-party assets.

---

## 💜 Built with Lovable

This project was initially developed using **Lovable** and is maintained as a React + TypeScript codebase.

The project can be continued locally using the standard development commands described above.
