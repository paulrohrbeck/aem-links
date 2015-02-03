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
* the only thing that helped for me is re-install the instance.. (bug?)

---
#### Maven 'MojoExecutionException' (can have a lot of reasons....)

1. "Installation on http://localhost:4502/apps/abc/install failed, cause: Installation failed" --> 'install' folder doesn't exist yet so the jars can't be pushed to the instance. Create folder manually in CRXDE Lite.

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

---

### Favicon scrambled/broken

Never really found out why this happened..
Solution for now: Use favicon from DAM instead of /etc.

---

### Changes don't show up in JCR/CRX
Make sure there is no XML errors in any of the files you're building. (Example: & -> &amp;)

---

### cannot render resource SyntheticResource

org.apache.sling.servlets.get.impl.DefaultGetServlet No renderer for extension html, cannot render resource SyntheticResource

Resource/Component doesn't exist. Check resource path.

---

### Only a type can be imported. ... resolves to a package

org.apache.sling.servlets.resolver.internal.SlingServletResolver Calling the error handler resulted in an error
java.lang.Error: Unresolved compilation problems: 
	Only a type can be imported. com.adobe.acs.commons.errorpagehandler.ErrorPageHandlerService resolves to a package
	ErrorPageHandlerService cannot be resolved to a type
	ErrorPageHandlerService cannot be resolved to a type

* Make sure bundle is active
* Make sure bundle actually exports this class/service

---

### Image doesn't show up on Dispatcher

- Check: Does it show up on Author/Publish?
- Check: Is there Redirects set on the Dispatcher?
