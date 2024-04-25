---
title: Accessible footer
description: Use semantic HTML for footer.
date: '2024-4-15'
category: basics
components:
  - footer
  - layout
published: true
successCriteria:
  - '1.3.1'
  - '2.4.1'
level: A
source: https://www.magentaa11y.com/checklist-web/footer/#example-footer
---

This semantic HTML contains all accessibility features by default.

```html
<!-- This link lets people skip content and jump directly to the footer -->
<a href="#example-footer">Skip to example footer</a>

<footer tabindex="-1" id="example-footer">
	<nav aria-label="Site map">
		<ul>
			<li><a href="/">Home</a></li>
			<li><a href="/about/">About</a></li>
			<li><a href="/contact/">Contact</a></li>
		</ul>
	</nav>
	© 2021
</footer>
```

If you can't use semantic HTML give the element a specific attribute to define its role

```html
<div role="contentinfo" tabindex="-1" id="example-footer">&copy; 2021 Site Name</div>
```

The [`role="contentinfo"`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles#roles_defined_on_mdn) role defines a footer, containing identifying information such as copyright information, navigation links, and privacy statements, found on every document within a site. This section is commonly called a footer.
