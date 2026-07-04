---
layout: activity
permalink: /Activities/FrontEnd
title: "CS474: Human Computer Interaction - Front End Development with Bootstrap"


info: 
  goals: 
    - To structure a web page with semantic HTML and style it with CSS
    - To build responsive layouts using flexbox, grid, and the Bootstrap framework
    - To apply course design principles (hierarchy, contrast, affordance) and accessibility practices to a real front end
  additional_reading:
    - link: "https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content"
      title: "MDN - Structuring content with HTML"
    - link: "https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics"
      title: "MDN - CSS styling basics"
    - link: "https://getbootstrap.com/docs/5.3/getting-started/introduction/"
      title: "Bootstrap 5.3 Documentation - Introduction"
    - link: "https://css-tricks.com/snippets/css/a-guide-to-flexbox/"
      title: "CSS-Tricks - A Complete Guide to Flexbox"
    - link: "https://css-tricks.com/snippets/css/complete-guide-grid/"
      title: "CSS-Tricks - A Complete Guide to CSS Grid"
    - link: "https://webaim.org/standards/wcag/"
      title: "WebAIM - WCAG 2 Overview"
  models:
    - model: |
        <div align="left">
        Every web page is three cooperating layers: <strong>HTML</strong> provides the structure and <em>meaning</em> of the content, <strong>CSS</strong> provides the presentation, and <strong>JavaScript</strong> provides the behavior.  Consider this fragment of two different implementations of the same visual design:
        <br><br>
        <code>&lt;div class="top"&gt;&lt;div class="big"&gt;Adopt a Pet&lt;/div&gt;&lt;div onclick="go()"&gt;Apply&lt;/div&gt;&lt;/div&gt;</code>
        <br><br>
        <code>&lt;header&gt;&lt;h1&gt;Adopt a Pet&lt;/h1&gt;&lt;button type="button"&gt;Apply&lt;/button&gt;&lt;/header&gt;</code>
        </div>
      title: Semantic Structure as an Affordance
      questions:
        - "Both fragments can be styled to look identical.  What does a screen reader user experience with each?  What does the keyboard <code>Tab</code> key do with each?"
        - "Relate this to Norman's affordances and signifiers: which element names act as signifiers, and to whom - the visual user, the assistive technology, or the next developer?"
        - "Give two more examples of semantic HTML elements and what they 'promise' about their content."
    - model: |
        <div align="left">
        Resize any Bootstrap-based site (for example, the <a href="https://getbootstrap.com/docs/5.3/examples/">Bootstrap Examples gallery</a>) from full-screen desktop down to phone width using your browser's developer tools (F12, then toggle device emulation).
        </div>
      title: Responsive Layout
      questions:
        - "Identify three things that change as the viewport narrows (navigation, columns, image sizes, spacing).  At roughly what widths do they change?"
        - "Why do frameworks define standard 'breakpoints' instead of letting every developer pick their own?"
        - "Who benefits from a mobile-first design process besides phone users?  Consider low-vision users who zoom to 400%."

tags:
  - frontend
  - design
  - accessibility
  
---

Front-end development is where the concepts of this course stop being abstract: every affordance, signifier, hierarchy, and accessibility decision becomes a concrete line of HTML or CSS.  This walkthrough builds up from raw HTML to a polished, accessible landing page with Bootstrap, and ends with a scaffolded exercise you can apply directly to your final project.

## Part 1: HTML Structure Refresher

HTML describes *what things are*, not what they look like.  A minimal, well-structured page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Campus Pet Adoption</title>
</head>
<body>
  <header>
    <nav><!-- site navigation --></nav>
  </header>
  <main>
    <h1>Find your new best friend</h1>
    <section aria-labelledby="pets-heading">
      <h2 id="pets-heading">Available pets</h2>
      <!-- content -->
    </section>
  </main>
  <footer>&copy; 2024 Campus Pet Adoption</footer>
</body>
</html>
```

Key habits to build now:

- **Use semantic elements** (`header`, `nav`, `main`, `section`, `article`, `footer`, `button`, `label`) rather than a page full of `div`s.  Assistive technologies, search engines, and keyboards all rely on these names — semantics are affordances for non-visual users.
- **One `h1` per page**, with heading levels that nest without skipping (`h1` then `h2` then `h3`).  Screen reader users navigate by headings the way sighted users skim.
- **Every image gets `alt` text** describing its function (or `alt=""` if purely decorative).
- **The `viewport` meta tag** is what allows your page to adapt on mobile at all — without it, phones render a zoomed-out desktop page.

## Part 2: CSS and the Box Model

Every element is a rectangular box: **content**, wrapped in **padding**, wrapped in a **border**, wrapped in **margin**.  Most alignment frustration is a box model misunderstanding.

```css
* { box-sizing: border-box; }  /* width now includes padding and border */

.card {
  padding: 1rem;         /* space inside the border */
  border: 1px solid #ccc;
  margin: 1rem 0;        /* space outside the border */
}
```

Two tips that prevent hours of confusion:

- `box-sizing: border-box` (used by Bootstrap and virtually all modern sites) makes `width: 300px` mean the *visible* width, padding and border included.
- Vertical margins between elements *collapse* (they overlap rather than add).  When spacing looks wrong, open the browser dev tools and hover the element — the box model diagram shows exactly where the space comes from.

Use relative units (`rem` for sizes, `%` for widths) rather than fixed pixels wherever you can: they respect the user's browser font-size preference, which is itself an accessibility feature.

## Part 3: Responsive Layout with Flexbox and Grid

Modern CSS gives you two layout tools; you will use both:

- **Flexbox** lays out items in *one dimension* (a row or a column) and excels at distributing and aligning them — navigation bars, toolbars, centering things.

```css
.toolbar {
  display: flex;
  justify-content: space-between;  /* main axis */
  align-items: center;             /* cross axis */
  gap: 1rem;
}
```

- **CSS Grid** lays out items in *two dimensions* — page shells and card galleries.

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 1rem;
}
```

That one `gallery` rule is fully responsive with no media queries: the browser fits as many 240px-minimum columns as the screen allows.  When you *do* need different rules at different sizes, use a media query:

```css
@media (max-width: 768px) {
  .sidebar { display: none; }
}
```

**Design this mobile-first:** write your base styles for small screens, then add `min-width` media queries to take advantage of larger ones.  Constraints first, enhancements second — the same discipline we saw with constrained applications.

## Part 4: Bootstrap

[Bootstrap](https://getbootstrap.com/) packages these layout tools, plus a library of tested components, behind consistent class names.  You get professional defaults, a responsive grid, and components with keyboard and screen reader behavior already implemented.  Add it to a page with two lines (from the [introduction docs](https://getbootstrap.com/docs/5.3/getting-started/introduction/)):

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

### The Grid System

Bootstrap's grid is a 12-column flexbox layout.  You choose how many of the 12 columns each element spans *at each breakpoint* (`sm` ≥576px, `md` ≥768px, `lg` ≥992px, `xl` ≥1200px):

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-8">Main content</div>
    <div class="col-12 col-md-4">Sidebar</div>
  </div>
</div>
```

Read `col-12 col-md-8` as: "full width on phones; 8 of 12 columns from the `md` breakpoint up."  The sidebar stacks below the content on phones and sits beside it on tablets and desktops — responsive behavior with zero CSS written.

### Common Components

A few components you will use constantly (each linked to its documentation, which includes copy-pasteable examples):

- **[Navbar](https://getbootstrap.com/docs/5.3/components/navbar/)** — a responsive navigation header that collapses into a "hamburger" toggle on small screens.
- **[Cards](https://getbootstrap.com/docs/5.3/components/card/)** — the workhorse container for a pet, a product, a post: image, title, text, action button.
- **[Forms](https://getbootstrap.com/docs/5.3/forms/overview/)** — styled inputs with built-in validation states; note that every example pairs an `<input>` with a `<label for=...>`, which is an accessibility requirement, not decoration.
- **[Buttons](https://getbootstrap.com/docs/5.3/components/buttons/)** — `btn btn-primary` for the main action, `btn-outline-secondary` for lesser ones; the visual weight *is* the hierarchy signal.
- **[Modals](https://getbootstrap.com/docs/5.3/components/modal/)** — dialog overlays that trap keyboard focus correctly (hard to get right by hand); use them sparingly, since they interrupt the user's flow.
- **[Alerts](https://getbootstrap.com/docs/5.3/components/alerts/)** — feedback messages; remember Norman's principle that every action deserves timely feedback.

### Utility Classes

Utilities are single-purpose classes that replace one-off CSS: spacing (`mt-3` = margin-top level 3, `p-4`, `gap-2`), layout (`d-flex`, `justify-content-between`, `align-items-center`), text (`text-center`, `fw-bold`, `text-muted`), and color (`bg-light`, `text-danger`).  A centered, spaced toolbar with no custom stylesheet:

```html
<div class="d-flex justify-content-between align-items-center p-3 bg-light">
  <span class="fw-bold">Campus Pet Adoption</span>
  <button class="btn btn-primary">Apply to Adopt</button>
</div>
```

One caution: color utilities like `text-danger` convey meaning *only* to sighted users who can perceive that color.  Pair color with text or an icon ("Error: ..." rather than red text alone).

## Part 5: Applying Course Concepts

A framework gives you components; it cannot give you a *design*.  This is where the rest of the course comes in.

### Design Principles in the Front End

| Principle | Front-end application |
|---|---|
| Visual hierarchy | One `h1`; heading sizes descend with importance; primary action is the largest, highest-contrast button on the page |
| Contrast | Text meets WCAG AA (4.5:1 normal text, 3:1 large text); check with the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) |
| Affordance and signifiers | Links look like links, buttons look like buttons; interactive elements have hover, focus, and active states; never remove focus outlines without replacing them |
| Consistency (Jakob's Law) | Navigation at the top, logo links home, destructive actions ask for confirmation — match the conventions users bring from every other site |
| Feedback | Form submission shows success or specific, polite error messages next to the offending field (see the Designing Better Error Messages reading from earlier in the course) |
| Constraint | Disable or hide actions that are not currently valid; use `input type="date"` and similar constrained controls instead of free text where possible |

### Accessibility in the Front End

Semantic HTML from Part 1 does most of the work; the rest is deliberate:

1. **Keyboard access:** every interactive element reachable and operable with `Tab`/`Enter`/`Space`, in a sensible order.  Test by unplugging your mouse.
2. **Labels:** every form control has a `<label>`; icon-only buttons get `aria-label="..."`.
3. **ARIA, sparingly:** the [first rule of ARIA](https://www.w3.org/TR/using-aria/#rule1) is to prefer a native HTML element over adding ARIA roles to a `div`.  Use ARIA to fill genuine gaps (`aria-expanded` on a custom disclosure, `role="alert"` for dynamic status messages) — Bootstrap's components already include most of what they need.
4. **Don't rely on color alone,** and honor user preferences (`prefers-reduced-motion`) for animation.
5. **Audit it:** run the [WAVE tool](https://wave.webaim.org/) from our accessibility activity on every page you build.  Zero errors is the floor, not the ceiling.

## Try It: Build an Accessible Landing Page

Build a one-page site for a fictional service (a campus pet adoption center, a study-group finder, a food pantry — or a mock landing page for your final project).  Work in a plain `index.html` file, or start from the [Bootstrap examples](https://getbootstrap.com/docs/5.3/examples/) gallery.

Scaffolded steps — get each working before moving on:

1. **Skeleton (HTML only).**  Semantic structure: `header` with `nav`, `main` with an `h1` hero section, a features/cards `section`, a signup `form` in its own `section`, and a `footer`.  Validate your headings nest properly.
2. **Bootstrap layout.**  Add the Bootstrap CDN links.  Make the hero a `container` with a `row`; make three feature cards that are stacked on phones and three-across on desktop (`col-12 col-md-4`).
3. **Navbar and form.**  Add a collapsing navbar and a signup form (name, email, one `select`) with proper `label`s and a clear primary `btn btn-primary` submit button.
4. **Design pass.**  Apply the design principles table above: check your visual hierarchy, verify all color contrast with the WebAIM checker, and confirm hover/focus states are visible.
5. **Accessibility pass.**  Complete the checklist below, then run WAVE and fix every error it reports.
6. **Stretch goals.**  Add a modal ("Adoption application received!") triggered by the form; add a `prefers-color-scheme` dark mode; replace the card gallery with the pure CSS grid `auto-fill` technique from Part 3 and compare.

**Accessibility checklist (adapted from WCAG via WebAIM):**

- [ ] Page has a descriptive `<title>` and `lang` attribute
- [ ] Exactly one `h1`; heading levels do not skip
- [ ] All images have appropriate `alt` text
- [ ] All form inputs have associated `<label>`s
- [ ] All text meets AA contrast (4.5:1; 3:1 for large text)
- [ ] Every feature is usable with keyboard only, and focus is always visible
- [ ] Color is never the only carrier of meaning
- [ ] Page is readable and usable at 200% zoom and at phone width
- [ ] WAVE reports zero errors

When you finish, trade laptops with a neighbor and complete each other's checklists — a two-person heuristic evaluation, just like the stakeholder testing you will document in your final project design report.
