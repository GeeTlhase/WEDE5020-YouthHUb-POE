# YouthTech Skills Hub

A multi-page website for a fictional South African non-profit digital skills organisation, built as part of an IIE Web Development assignment.

## Live Site

> _(Deploy URL to be added here after deployment)_

## GitHub Repository

> _(Repository URL to be added here)_

---

## Project Structure

```
/
├── index.html          — Home page
├── about.html          — About Us
├── programme.html      — Programmes listing
├── resources.html      — Digital library & blog
├── register.html       — Application form
├── donate.html         — Donation form
├── contact.html        — Contact / general message form (NEW – Part 3)
├── enquiry.html        — Enquiry form with cost/availability response (NEW – Part 3)
├── styles.css          — Main stylesheet
├── robots.txt          — SEO: search engine crawler instructions (NEW – Part 3)
├── sitemap.xml         — SEO: site map for search engines (NEW – Part 3)
└── images/             — Team photos and other images
```

---

## Changelog

All changes made during Part 3 are recorded below. Entries list the file changed, what was done, and why.

---

### Part 3 — Enhancing Functionality and SEO

---

#### Bug fixes from Part 2 feedback

**index.html**
- **Fix:** Corrected malformed `<link>` tag. Original code read `<linkrel=about"` (missing space and opening quote), which is invalid HTML. Corrected to `<link rel="alternate" href="about.html">`.
- **Fix:** Removed the redundant `<link rel="programmes">`, `<link rel="resources">`, `<link rel="register">`, and `<link rel="donate">` tags which used non-standard `rel` attribute values. These served no functional or SEO purpose.

**about.html**
- **Fix:** Removed a CSS-style block comment (`/*The team and their roles on the project*/`) that had been placed directly inside the HTML `<body>` within the `<section id="team">` element. CSS comments in HTML body are not valid and render as visible text in some browsers. Replaced with a proper HTML comment (`<!-- Team members and their roles on the project -->`).

---

#### 1. SEO enhancements (applied to all pages)

**index.html, about.html, programme.html, resources.html, register.html, donate.html, contact.html, enquiry.html**
- **Added** `<meta name="description">` to every page with a unique, descriptive summary (under 160 characters) relevant to that page's content. Meta descriptions improve click-through rates from search engine results pages.
- **Added** `<meta name="keywords">` to every page with relevant keyword phrases matching the page topic.
- **Added** `<meta name="robots" content="index, follow">` to all pages to explicitly instruct search engine crawlers to index the pages and follow links.
- **Added** Contact and Enquiry links to the navigation bar and footer across all pages to improve internal linking and crawlability.

**robots.txt** _(new file)_
- Created `robots.txt` in the root directory to instruct search engine crawlers. Allows all crawlers to index all pages and references the sitemap URL.

**sitemap.xml** _(new file)_
- Created `sitemap.xml` listing all eight pages with their `<loc>`, `<lastmod>`, `<changefreq>`, and `<priority>` values. This helps search engines discover and understand the structure of the site.

---

#### 2. JavaScript — Interactive elements

**styles.css**
- Added CSS for all new interactive components introduced in Part 3: accordion buttons and panels, filter bars, lightbox overlay, modal overlay, fade-in animation (`fade-in` / `visible` classes), form validation error states (`field-error`, `invalid`, `valid`), form success messages, and dynamic blog post grid.

**programme.html**
- **Accordion:** Replaced the flat list of `<article class="course">` elements with interactive accordion buttons. Each course heading is a button; clicking it opens/closes the course panel with a smooth `max-height` CSS transition. Only one panel is open at a time. The open button changes colour and the `+` icon rotates to `×`.
- **Filter bar:** Added a live text search input and a level dropdown (Beginner / Intermediate) above the accordion. As the user types or changes the dropdown, courses are instantly shown or hidden using `data-name` and `data-level` attributes on each button. A "No courses match your search." message appears when no results are found.
- **Fade-in on scroll:** Applied `IntersectionObserver` to all `section` and `article` elements so they fade up into view as the user scrolls down the page.

**resources.html**
- **Dynamic blog loading:** Replaced static blog HTML with a JavaScript-driven rendering system. Blog post data is stored in a JS array (`allPosts`). Posts are rendered four at a time via a "Load More Posts" button, which appends the next four to the container without a page reload.
- **Blog search + category filter:** Added a text search input and a category dropdown above the blog posts. Filtering re-runs the render from the beginning against the filtered subset.
- **Digital library filter:** Added a text search and resource-type dropdown above the library grid. Items are shown/hidden in real time as the user types or selects a type.
- **Lightbox:** Added a full-screen lightbox overlay. Any image with the class `lightbox-trigger` will open in the lightbox when clicked. The overlay can be closed with the × button, clicking outside the image, or pressing `Escape`.
- **Fade-in on scroll:** Applied to all `section` elements.

**about.html, index.html**
- **Fade-in on scroll:** Applied `IntersectionObserver` to `section`, `article`, and `blockquote` elements to create a smooth entrance animation as the user scrolls.

---

#### 3. JavaScript — Form validation and AJAX-style submission

**register.html**
- **Client-side validation:** Added JavaScript validation for all required fields: first name and last name (minimum 2 characters), South African ID number (exactly 13 digits), date of birth (age must be 18–35), province, email address (regex), phone number (10–15 digits), programme selection, intake date, learning mode, and education level.
- **Live (blur) validation:** Each field is validated on `blur` (when the user leaves the field), showing or hiding an inline error message immediately below the field.
- **Error display:** Invalid fields receive a red border and box shadow (`input.invalid`); valid fields receive a green border (`input.valid`). Error messages appear in `<span class="field-error">` elements.
- **AJAX-style submission:** On submit, all fields are re-validated. If valid, the submit button shows "Submitting…" and is disabled. After 1.2 seconds (simulating a server round-trip), the form is cleared, a green success message is revealed, and the button is re-enabled. No full page reload occurs.
- **Login form validation:** The existing student login form also has email and password validation added.

**donate.html**
- **Conditional field display:** The recurring frequency fieldset is hidden by default and shown only when the "Recurring Monthly Donation" radio is selected. The custom amount input is shown only when "Other Amount" is chosen.
- **Client-side validation:** Validates that a donation amount is selected, that the custom amount is at least R 10 if selected, that first name, last name, and email are valid, and that the POPIA consent checkbox is ticked.
- **AJAX-style submission:** Same simulated-submit pattern as register.html — button text changes, then a success message appears after 1.2 seconds.

---

#### 4. New pages

**enquiry.html** _(new file)_
- Created a full enquiry page with a validated multi-section form covering: personal details (name, email, phone, organisation), enquiry type (programme, corporate, volunteer, sponsor, other), programme selection and group size (shown conditionally for programme/corporate types), a free-text message, preferred contact method, and POPIA consent.
- **JavaScript validation:** All required fields validated on blur and on submit, with inline error messages.
- **Conditional fields:** The programme fieldset is hidden by default and displayed only when "Programme Enrolment" or "Corporate / Group Training" is selected as the enquiry type.
- **Response modal:** On successful submission (AJAX-style, 1-second delay), a modal dialog appears with a tailored response based on the enquiry type. For programme enquiries, it shows the selected programme's cost, duration, next intake, and available spaces. For corporate enquiries, it calculates the total cost and applies a group discount (10% for 5+, 15% for 10+). Volunteer and sponsor responses include relevant details about commitment and pricing. The modal can be closed with the × button, clicking the backdrop, or pressing `Escape`.
- **Character counter** on the message textarea.
- **Fade-in** animations applied to all sections and fieldsets.

**contact.html** _(new file)_
- Created a general contact page with contact details for four departments (General, Admissions, Partnerships, Finance) and a validated contact form.
- The form collects: first name, last name, email, optional phone, message type (dropdown), subject, full message, recipient selection (which department email address to send to), and POPIA consent.
- **JavaScript validation:** All required fields validated on blur and on submit. Optional phone is validated only if a value is entered.
- **Mailto compilation:** On successful validation, the form does NOT submit to a server. Instead, the full message is compiled into a `mailto:` URL with the recipient address, a prefixed subject line, and a formatted message body (including sender name, email, phone, and message type). An email preview table appears below the form showing exactly what will be sent. A clearly labelled "Open in Email Client & Send" button opens the user's default email client with the message pre-filled. The user reviews it in their own email client and clicks Send.
- **Character counter** on the message textarea (2000 character limit).
- **Fade-in** animations applied to all sections, fieldsets, and articles.
