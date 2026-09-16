# HE Bundle Size Chart Builder

A single-page tool for combining Historical Emporium size charts (Shopify metaobject HTML) into one chart for bundle listings.

## Host on GitHub Pages

1. Create a repo (e.g. `he-size-charts`) and add `index.html` to the root.
2. Repo **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main` / `(root)`.
3. The tool will be live at `https://<your-org>.github.io/he-size-charts/` within a minute or two.

No build step, no dependencies. You can also just open `index.html` locally in a browser.

## How to use

1. **Paste** each piece's full size chart snippet (table + inlined sizing guide) into its own box. Add more boxes for 3+ piece bundles. Name each piece (Jacket, Trousers…).
2. **Combine** — choose a layout:
   - **Auto** — merges by size when the pieces share size labels, otherwise stacks.
   - **Merge by size** — one table: `Size | jacket columns | trouser columns`. Size labels are normalized (XXL = 2XL = 2X, Large = L). Sizes missing from a piece show “—”.
   - **Stack** — one table, each piece gets its own titled section; narrower charts are widened to match.
   - **Separate tables** — each chart kept as its own table, one after the other.
   Duplicate note rows and duplicate sizing guides (e.g. the mens guide in both charts) are removed.
3. **Edit & copy** — click into the preview to edit any cell. The toolbar moves/adds/duplicates/deletes rows and columns, switches a row between normal / header / subheading styling, and adds note rows. You can also edit the HTML directly; both views stay in sync. **Copy HTML** and paste into the metaobject.

## Notes

- Preview styling is copied from the live theme’s `sizecharts.css`, the Bootstrap `visible-xs` / `hidden-xs` rules, and the product-page Size Guide modal. Toggle **Desktop / Mobile** to check both guide variants. If the theme’s size chart CSS changes, update the `SITE_CSS` block near the top of the script.
- **Broken HTML protection.** Pasted sizing guides are run through the browser’s HTML parser before combining, so stray closing tags (e.g. an extra `</div>`, which closes the theme’s size-chart modal and breaks the product page) are removed and unclosed tags are closed. Guide elements that reuse an id (like a second `#mens_guide`) are dropped. The final HTML is checked on every change. If it has unbalanced tags or duplicate ids, a red panel lists them with line numbers, **Copy** and **Download** are disabled, and **Fix automatically** repairs it. The preview can look fine even when the HTML is broken, so trust the panel over the preview.
- Charts with a side image column (`rowspan`, e.g. hats) can’t be merged by size; they fall back to stacking automatically.
- Drafts are saved in your browser’s local storage. Nothing is sent anywhere.
