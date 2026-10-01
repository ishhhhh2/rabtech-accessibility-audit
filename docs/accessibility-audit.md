# RabTech Academy — Accessibility & Architecture Audit

## Website

https://rabtechacademy.in/

## Audit Date

20 September 2026

## Audit Scope

This audit reviewed the RabTech Academy website for:

- Accessibility issues
- Keyboard accessibility
- Semantic HTML and heading structure
- Images and alternative text
- ARIA usage
- Page structure and landmarks
- Frontend architecture
- API usage
- JavaScript behavior

## Tools Used

- Chrome DevTools
- Lighthouse
- Elements panel
- Network panel
- Console

---

# 1. Accessibility Findings

## Finding 1 — Insufficient Color Contrast

**Severity:** Accessibility issue

### Evidence

Lighthouse Accessibility reported:

> Background and foreground colors do not have a sufficient contrast ratio.

The Lighthouse Accessibility score was **95**.

Examples of affected content included text such as:

- `10K+`
- `7.5K+`
- `SPECIALIZED TECHNICAL DISCIPLINES`

### Impact

Low-contrast text can make content difficult to read, particularly for users with low vision or color-vision difficulties.

### Recommendation

Review the affected foreground/background color combinations and adjust them to meet WCAG contrast requirements.

### Evidence Screenshot

`screenshots/accessibility-01-color-contrast.png`

---


## Finding 2 — Non-Sequential Heading Hierarchy

**Severity:** Accessibility issue

### Evidence

Lighthouse reported:

> Heading elements are not in a sequentially-descending order.

Manual inspection showed an `h2` heading followed by:

```html
<h4>A structured project desk</h4>

Impact:
A non-sequential heading structure can make the page structure harder to understand for users who navigate content using headings, including screen-reader users.
Recommendation:
Use heading levels in a logical hierarchy, such as H2 → H3 → H4, where appropriate.
Evidence Screenshot:
screenshots/architecture-02-heading-hierarchy.png

# 2. Architecture Findings

### Finding 3 — Program Catalog Appears Maintained in Frontend JavaScript

**Type:** Architecture / Maintainability

**Evidence:**  
The frontend JavaScript file `education-site.js` contains a `programs` data structure with program information, including Artificial Intelligence & ML and Full Stack Web Development.

During the Network → Fetch/XHR investigation, no dedicated programs, courses, or internships API request was observed.

**Impact:**  
Maintaining program catalog information directly in frontend JavaScript means content changes may require modifying and redeploying frontend code instead of updating centralized application data.

**Recommendation:**  
Consider moving program/catalog data to a backend API or content/data layer if the catalog is expected to change frequently.

**Evidence Screenshots:**  
`screenshots/architecture-03-hardcoded-programs.png`  
`screenshots/architecture-03-no-program-api.png`

### Finding 4 — Promotion API Over-Fetches Data for Banner Use

**Type:** Architecture / Performance

**Evidence:**  
The banner code in `education-site.js` requests:

```javascript
fetch(`${publicApiBase()}/api/public/promotions`)

The frontend then searches the returned promotions for the banner promotion:
data.promotions.find((item) => item.displayType === 'banner')
The application also uses a filtered promotion endpoint:
/api/public/promotions?displayType=popup
This shows that promotion data can be filtered by display type.
Impact:
The banner use case requests the full promotions collection even though it only needs the banner promotion. As the number of promotions increases, this can result in unnecessary data being transferred and processed by the client.
Recommendation:
Use a filtered request for the banner use case, such as:
/api/public/promotions?displayType=banner

if supported by the backend.
Evidence Screenshot:
screenshots/architecture-04-promotion-overfetch.png

# 3. Checks Performed With No Issue Found

The following checks were also performed during the audit:

- Keyboard-only navigation
- Visible keyboard focus indicators
- Logical keyboard focus order
- FAQ keyboard interaction
- Focus trap behavior
- Interactive controls being keyboard accessible
- Interactive controls having understandable purpose and state
- HTML5 landmarks such as `main`, `header`, `nav`, and `footer`
- Image alternative text
- ARIA attributes and roles
- Heading elements containing content
- JavaScript console errors
- Network/API requests
- FAQ API response
- Cloudflare Insights script

No additional confirmed accessibility or architecture issue was identified from these checks.

# 4. Lighthouse Accessibility Result

**Accessibility Score:** 95/100

Lighthouse identified two accessibility failures:

1. Insufficient color contrast
2. Non-sequential heading hierarchy

Other Lighthouse accessibility checks were either passed or marked as not applicable.

# 5. Conclusion

The audit identified four evidence-based findings across accessibility and frontend architecture.

The accessibility findings concern color contrast and heading structure.

The architecture findings concern frontend program data maintenance and promotion API data usage.

Additional manual checks were performed to avoid reporting unsupported or speculative issues.