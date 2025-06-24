# Why HTML Edits Don't Persist in the Email Template Editor

If you modify the HTML code directly within a Salesforce Email Template, please note that **those changes will not be reflected in the Creative Mail editor interface**.

To ensure your edits persist and display correctly within the Editor:

* **All changes must be made through the Creative Mail editor.**

While it is technically possible to alter the HTML manually, such changes:

* Will not be recognized by the editor
* Will **not display** during subsequent edits
* Will be **overwritten** the next time the template is saved via the editor.

This behavior occurs because Creative Mail stores the visual design data separately from the HTML template. That design data is only updated through the editor itself.
