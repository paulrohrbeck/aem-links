Problems & Solutions
--------------------------

Working document to gather common issues and solutions. (AEM 5.6.1 and 6.0)



---
#### Components are not editable in edit mode (editor.html/). Edit button doesn't show up.  (AEM 6)

Solutions:
* Restart instance?

---
#### Maven Mojo Exception (can have a lot of reasons....)

Solutions:
* Build Content packages before Core packages (?)

---

#### Component does not show up in component list (AEM 6)

Solutions:
* missing or malformed '_cq_editConfig.xml' file
* Component is '.hidden'
* Component is not allowed for current page / parsys / etc.

---

#### Console shows 404 for component that's not there anymore (AEM 6)
Solutions:
* clear local storage in browser since it might have old references to it if it was deleted in a different tab
