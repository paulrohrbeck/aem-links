Problems & Solutions
--------------------------

Working document to gather common issues and possible solutions. (AEM 5.6.1 and 6.0)


General Advice:
* check all logs
* restart instance


---
#### Components are not editable in edit mode (editor.html) (AEM 6)
Edit button doesn't show up.

Solutions:
* Unknown

---
#### Maven 'MojoExecutionException' (can have a lot of reasons....)

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
