# Prototype Mode

This repository is only for disposable, clickable UI prototypes used in stakeholder discussions.

## Primary objective

Produce the requested screens with the minimum possible code, context exploration, tool calls, and explanation.

## Technology

* Use plain HTML, CSS, and minimal vanilla JavaScript.
* Do not use React, TypeScript, npm, build tools, frameworks, component libraries, databases, APIs, authentication, routing libraries, or servers.
* The prototype must run by opening `index.html` directly in a browser.
* Keep all code in the respective module wise `.html` files, unless the user explicitly requests otherwise.
* Use inline CSS and JavaScript.
* Use placeholders, static sample data, and CSS shapes instead of external assets whenever practical.

## Interaction requirements

* Make requested buttons, tabs, menus, dialogs, and navigation paths clickable.
* Simulate state locally in JavaScript.
* Navigation may show and hide sections in the same HTML file.
* Only implement the interactions explicitly requested.
* Do not implement production functionality.

## Working rules

* Do not inspect unrelated files.
* Do not search the web.
* Do not install packages.
* Do not run broad tests, linters, accessibility audits, or production checks.
* Do not refactor working code unless necessary for the requested change.
* Do not create plans, documentation, tests, or architecture notes.
* Do not add features or screens that were not requested.
* Do not recreate the entire file when a small edit is sufficient.
* Preserve existing prototype behavior unless the request changes it.
* Make reasonable visual assumptions instead of asking questions.
* Stop as soon as the requested interaction works.

## Visual standard

Aim for a credible discussion prototype, not production polish:

* clear hierarchy
* consistent spacing
* legible typography
* recognizable controls
* approximate desktop layout
* lightweight responsive behavior only when requested

## Response format

After editing, respond with no more than three bullets:

* files changed
* interactions implemented
* how to open the prototype

Do not provide a detailed explanation unless requested.

Keep all prototype code in index.html.

Use:
- Inline CSS inside <style>
- Inline JavaScript inside <script>

Do not create additional files unless explicitly requested.


When modifying the prototype, edit only the affected section.
Do not rewrite the entire index.html unless explicitly requested.