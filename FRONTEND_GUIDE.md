# Frontend Guide — PawConnect / PawNest

## 1. Purpose

This document explains the frontend of the PawConnect pet adoption management project. It is intended for a beginner developer or teammate who needs to understand, test, and maintain the user interface.

The frontend is built with:
- **HTML** — page structure and content
- **CSS** — layout, colours, spacing, and responsive styling
- **JavaScript** — interactive behaviour
- **Chart.js** — charts, where used

The backend and database are separate layers. The frontend should communicate with the backend rather than connecting directly to MySQL.

## 2. Main frontend responsibilities

The frontend helps users:
- Browse pets and view pet details.
- Read adoption and shelter information.
- Register or log in, where those pages are available.
- View adoption application status.
- Navigate between pages using menus, buttons, and links.
- Understand information through clear labels, messages, and charts.

Only describe a feature as implemented if it is present and working in the current project version.

## 3. Typical page structure

A page commonly contains these parts:

1. **Header / navigation** — project name and links to other pages.
2. **Main content** — pet cards, forms, tables, or information.
3. **Feedback area** — success, validation, or error messages.
4. **Footer** — supporting links or project information.

Example HTML structure:

```html
<header class="site-header">
  <h1>PawConnect</h1>
  <nav aria-label="Main navigation">
    <a href="index.html">Home</a>
    <a href="pets.html">Browse Pets</a>
    <a href="login.html">Login</a>
  </nav>
</header>

<main>
  <section class="page-intro">
    <h2>Find a pet to adopt</h2>
    <p>Explore pet profiles and adoption information.</p>
  </section>
</main>

<footer>
  <p>&copy; PawConnect</p>
</footer>
```

This is a teaching example. Adjust filenames and links to match the actual repository.

## 4. Suggested frontend folder organisation

Keep the existing repository structure if the project already has one. If the team needs a cleaner structure, a possible arrangement is:

```text
project/
├── templates/          # HTML templates, if using Flask
├── static/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   └── images/
├── docs/
│   └── FRONTEND_GUIDE.md
└── README.md
```

In a Flask project, HTML templates are commonly stored in `templates/` and static CSS, JavaScript, and images in `static/`. Do not move existing files without checking how the application references them.

## 5. Styling with CSS

Use reusable classes instead of repeating inline styles.

```css
.pet-card {
  padding: 1rem;
  border: 1px solid #d8dee4;
  border-radius: 12px;
  background: #ffffff;
}

.pet-card h3 {
  margin-top: 0;
}

.button {
  display: inline-block;
  padding: 0.65rem 1rem;
  border-radius: 8px;
  text-decoration: none;
  cursor: pointer;
}

@media (max-width: 600px) {
  .pet-card {
    padding: 0.75rem;
  }
}
```

Before adding new CSS, search the project for an existing class that already performs the same job.

## 6. JavaScript and dynamic content

HTML that is written directly into a page is static. Dynamic content is generated or updated using JavaScript or server-rendered backend data.

Example: changing a heading with JavaScript:

```html
<h2 id="page-title">Shelter and Adoption Hub</h2>

<script>
  const title = document.getElementById("page-title");
  if (title) {
    title.textContent = "PawConnect — Shelter and Adoption Hub";
  }
</script>
```

If a heading still displays an old name, check:
- Whether you edited the file that the application actually serves.
- Whether another HTML template contains the same heading.
- Whether JavaScript changes the heading after the page loads.
- Whether the browser is showing a cached version.
- Whether a different server or project folder is running.

Prefer editing the original source of the text rather than adding a second script that overwrites it.

## 7. Forms and validation

Forms should have visible labels, appropriate input types, and helpful validation messages.

```html
<form id="contact-form">
  <label for="email">Email address</label>
  <input id="email" name="email" type="email" required>
  <button type="submit">Submit</button>
  <p id="form-message" role="status"></p>
</form>
```

Client-side validation improves usability, but it is not a replacement for backend validation. The server must validate all submitted values again.

## 8. Accessibility basics

- Give every form field a visible label.
- Use meaningful link and button text.
- Add alternative text to informative images.
- Keep heading levels in a logical order.
- Make sure text has sufficient contrast.
- Do not use colour alone to communicate errors or status.
- Ensure interactive elements can be used with a keyboard.
- Use status messages that assistive technologies can identify.

## 9. Frontend testing checklist

Test each page after changes.

- [ ] Page opens without a 404 error.
- [ ] Project name and page headings are correct.
- [ ] Navigation links open the intended pages.
- [ ] Images load correctly.
- [ ] Buttons and forms respond as expected.
- [ ] Required-field and invalid-input messages are understandable.
- [ ] Empty or missing data is handled gracefully.
- [ ] Layout remains usable on a narrow/mobile screen.
- [ ] Browser developer tools show no new JavaScript errors.
- [ ] Backend errors are shown clearly without exposing passwords, SQL, or sensitive configuration.

For a team testing record, note the page, test input, expected result, actual result, status, and screenshot path.

## 10. Safe Git workflow

Before committing:
1. Run `git status` to see which files changed.
2. Open the document and check that it contains no passwords, API keys, database credentials, or personal data.
3. Stage only the intended file.
4. Commit with a clear message.

Example commands:

```bash
git status
git add docs/FRONTEND_GUIDE.md
git commit -m "docs: add frontend guide"
git push
```

If the `docs` folder does not exist, create it first. If your repository uses another documentation folder, save the file there and update the `git add` path accordingly.

## 11. Contribution note

This guide documents general frontend practices and examples. Confirm all page names, routes, and implemented features against the current code before treating them as project-specific facts. Update this document when the frontend structure or behaviour changes.
