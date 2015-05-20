Problems & Solutions
--------------------------

Working document to gather common issues and possible solutions. (AEM 5.6.1 and 6.0)
Please let me know if you have explanations for any of these issues.

General Advice:
* check all logs (make sure to check them on the correct instancce if there's more than one)
* restart/reload/update bundle
* restart instance
* delete /var/classes and /var/clientlibs

---
#### Components are not editable in edit mode (editor.html) (AEM 6)
Edit button doesn't show up.

Solutions:
* the only thing that helped for me is re-install the instance.. (bug?)

---
#### Maven 'MojoExecutionException'
(Pretty generic error that can have a lot of reasons...)

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

#### Favicon scrambled/broken

Never really found out why this happened..
Solution for now: Use favicon from DAM instead of /etc or upload to CRXDE directly.

---

#### Changes don't show up in JCR/CRX

Vault might not have pushed your changes to CRX. Make sure there is no XML errors in any of the files you're building. (Example: & -> &amp;)

---

#### cannot render resource SyntheticResource

org.apache.sling.servlets.get.impl.DefaultGetServlet No renderer for extension html, cannot render resource SyntheticResource

Resource/Component doesn't exist. Check resource path.

---

#### Only a type can be imported. ... resolves to a package

org.apache.sling.servlets.resolver.internal.SlingServletResolver Calling the error handler resulted in an error
java.lang.Error: Unresolved compilation problems: 
	Only a type can be imported. com.adobe.acs.commons.errorpagehandler.ErrorPageHandlerService resolves to a package
	ErrorPageHandlerService cannot be resolved to a type
	ErrorPageHandlerService cannot be resolved to a type

* Make sure bundle is active
* Make sure bundle actually exports this class/service

---

#### Image doesn't show up on Dispatcher

- Check: Does it show up on Author/Publish?
- Check: Is there Redirects set on the Dispatcher?

#### ClassNotFoundException

- Maven dependency included?

---

#### Dispatcher ignores "Content-disposition" header

- set header directly on Dispatcher and/or CDN
- use Varnish? (see [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0CB4QFjAA&url=http%3A%2F%2Fwww.netcentric.biz%2Fblog%2F2014%2F10%2Fcache-is-king--the-life-beyond-the-adobe-dispatcher.html&ei=qpz7VI3JHMjpoATk1oCACg&usg=AFQjCNEeE2lTGNVMVdTPBzcEcXMkQ55NXQ&sig2=nx5sJHSyYDcIujvkRKdQUQ))

---

#### Cannot read property 'length' of undefined (Client context not showing)
campaigns.length seems to be 0

- check that campaigns is actually part of your client context configuration
- any personalization components included that shouldn't be there? hit "Target" by accident?


---

#### AntiSamy warning
"com.adobe.granite.xss.impl.HtmlToHtmlContentContext AntiSamy warning: The a tag contained an attribute that we could not process. The adhocenable attribute has been filtered out, but the tag is still in place. The value of the attribute was "false"."

- Depending on which attribute it's complaining about, you might want to see where it's coming from.
- If it should be allowed, like target="_blank", simply add it to your AntiSamy config (/libs/cq/xssprotection/config.xml, copied to /apps of course)


---

#### editor.html throws 404
Whenever you try to edit a page and enter the /editor.html/path/to/page.html it throws a 404 error.

- I'm still not sure how/shy this happened but for some reason there was a folder node "editor.html" under "/libs/wcm/core/content" that prevented the actual "editor" node from loading.

---

#### Taglibs don't resolve
....JasperException: The absolute uri: http://abc.com/taglibs cannot be resolved in either web.xml or the jar files deployed with this application

- does taglib bundle exist and is active?


---

#### Sitekick: all 'Page' operations greyed out (can't edit page properties etc.)

- Check console, see if AEM can read the "....permissions.json?path=...". If it's a 404, call that page and see what it returns. For me, a "jcr:content" node was missing.
 
