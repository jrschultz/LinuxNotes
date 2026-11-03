# 🖨️ Weasy Print Tutorial

This is for rendering .PDF files from Markdown using WeasyPrint instead of Latex. This process uses CSS for the .PDF styling.

## Write the markdown file as per usual. It doesn't require any yaml blocks. The page header is adjusted in the css file as desired. 

## 🌻 The CSS for Formating for Sermon Manuscripts

Save this code as **sermon-styles.css** and place the file in the directory with the files to render.

```css
/* V1.0 November 2, 2026
/* ==========================================================================
1. PAGE CONFIGURATION & GEOMETRY
   ========================================================================== */

@page {
  /* Set standard US Letter portrait page size with margins */
  size: letter portrait;
  margin: 0.75in;

  /* Running Header: Simple page number placed in the top-right */
  @top-right {
    content: "Proper 24A | Nov 8, 2026 | MT 25:1-13 | p. " counter(page);
    font-family: "Merriweather";
    font-size: 11pt;
    color: #000000;
  }
}

/* ==========================================================================
2. PAGE BREAK & LAYOUT CONTROLS
   ========================================================================== */

/* Force a new page before specific elements like main chapters */
.chapter-title {
  page-break-before: always;
  break-before: page;
}

/* Prevent paragraph or element fragmentation across pages */
h1, h2, h3, h4, .keep-together {
  page-break-inside: avoid;
  break-inside: avoid;
}

/* Prevent tables and lists from splitting awkwardly */
table, ul, ol {
  break-inside: avoid;
}

/* ==========================================================================
3. TYPOGRAPHY & ELEMENTS
   ========================================================================== */

body {
  font-family: "Merriweather";
  font-size: 16pt;
  line-height: 1.2;
  color: #000000;
}

h1 {
  font-size: 26pt;
  color: #1a365d;
  margin-bottom: 20px;
}

h2 {
  font-size: 18pt;
  color: #2b6cb0;
  margin-top: 30px;
  border-bottom: 1px solid #e2e8f0;
  padding-bottom: 5px;
}

p {
  margin-bottom: 15px;
  text-align: justify;
}

/* ==========================================================================
4. DATA TABLES (With repeating headers across pages)
   ========================================================================== */

table {
  width: 100%;
  border-collapse: collapse;
  margin: 25px 0;
}

/* Ensures the header row duplicates at the top of a new page if split */
thead {
  display: table-header-group;
}

th {
  background-color: #2b6cb0;
  color: #ffffff;
  font-weight: bold;
  text-align: left;
  padding: 10px;
  font-size: 10pt;
}

td {
  padding: 10px;
  border-bottom: 1px solid #e2e8f0;
  font-size: 10pt;
}

tr:nth-child(even) {
  background-color: #f7fafc;
}

/* ==========================================================================
5. COVER PAGE COMPONENT
   ========================================================================== */

.cover {
  background-color: #1a365d;
  color: #ffffff;
  width: 100%;
  height: 100%;
  padding: 60mm 20mm 20mm 20mm;
  box-sizing: border-box;
}

.cover h1 {
  color: #ffffff;
  font-size: 38pt;
  margin-bottom: 10px;
}

.cover .subtitle {
  font-size: 18pt;
  color: #90cdf4;
}
```

## 💻 Terminal Rendering Command

**Markdown to PDF:**

```bash
20261108-Proper27A.md --pdf-engine=weasyprint -c sermon-styles.css -o 20261108-Proper27A.pdf
```

**Markdown to HTML:**

```bash
20261108-Proper27A.md --pdf-engine=weasyprint -c sermon-styles.css -o 20261108-Proper27A.html
```

## 🛒 Dependencies 

I just installed ```pandoc``` and ```weasyprint``` from the repos. It worked fine on OpenSUSE without extra config.



