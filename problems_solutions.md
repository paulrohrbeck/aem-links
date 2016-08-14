Problems & Solutions
==========

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
* Component does not have a dialog or cq:editConfig (must have at least one of these), or the dialog.xml/_cq_editConfig.xml is malformed
* Component is '.hidden'
* Component is not allowed for current page / parsys / etc.
* The design's "components" list is malformed (missing commas "," between components, has whitespace in it, etc)
* There is no cq:designPath set on the site's root page (e.g. /content/mysite) or the page isn't able to inherit this property from the root page (e.g. because it's nested in a folder)

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
* Try deleting /var/classes/* to force recompilation 

---

#### Image doesn't show up on Dispatcher

- Check: Does it show up on Author/Publish?
- Check: Is there Redirects set on the Dispatcher?

---

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
- is the client context (cq/personalization/components/clientcontext) compoentn properly included?

---

#### AntiSamy warning
"com.adobe.granite.xss.impl.HtmlToHtmlContentContext AntiSamy warning: The a tag contained an attribute that we could not process. The adhocenable attribute has been filtered out, but the tag is still in place. The value of the attribute was "false"."

- Depending on which attribute it's complaining about, you might want to see where it's coming from.
- If it should be allowed, like target="_blank", simply add it to your AntiSamy config (/libs/cq/xssprotection/config.xml, copied to /apps of course)

---

#### editor.html throws 404
Whenever you try to edit a page and enter the /editor.html/path/to/page.html it throws a 404 error.

- For me there was a folder node "editor.html" under "/libs/wcm/core/content" that prevented the actual "editor" node from loading.
- As far as I can see the reason for this is: when you don't have a campaign selected but click "+" it creates this fake node because it doesn't know where to save the new experience. Bug?

---

#### Taglibs don't resolve
....JasperException: The absolute uri: http://abc.com/taglibs cannot be resolved in either web.xml or the jar files deployed with this application

- does taglib bundle exist and is active?

---

#### Sitekick: all 'Page' operations greyed out (can't edit page properties etc.)

- Check console, see if AEM can read the "....permissions.json?path=...". If it's a 404, call that page and see what it returns. For me, a "jcr:content" node was missing.
 
---

#### Ajax Post Servlet returns 302 for some form values

- This was a weird one, I'm not sure what exactly went on but whenever I put in a real email address bla@bla.com, it would return a "302 Found" instead of the normal "200 OK" when ajax posting to my servlet. It was fixed when I took out ":formid" and ":formstart"

---

#### Posting (eg. via Postman) to servlet returns 403 Forbidden

- make sure you added authentication headers if needed
- Either check "Allow Empty" in "Apache Sling Referrer Filter" OSGi config or set a proper referrer header in Postman

---

#### Targeted component: simulation doesn't work but selecting the campaign and experience in the client context works

- This happened for me when I was just trying to test some segments on the Geometrixx site. Turns out they have to be under their respective site (ie. '/etc/segmentation/geometrixx-outdoors'), I had them under another folder. They showed up when I created the experiences but then the connection wasn't made properly.

---

#### Maven build: Peer not authenticated

- Adobe's Maven repository seems to have issues some times, try a different source :)
- check that the artifact actually exists by navigating to it in your browser

---

#### IntelliJ doesn't resolve any imports

Some approaches:
- "mvn eclipse:eclipse"
- On the project, do "Maven" > "Reimport"
- "File" > "Invalidate Caches / Restart"

---

#### Unresolved constraint in bundle ... osgi.wiring.package (version conflict)

- does dependency exist in OSGi container? If not, try embedding it.
- try moving up/down the dependecies that have conflicts

---

#### j_security_check returns 403 / User login does not work / Error in logs: org.apache.sling.auth.core.impl.SlingAuthenticator handleSecurity: AuthenticationHandler did not block request; access denied

- In our case a 301 redirect messed with the headers so the auth headers didn't make it through.

---

#### GenericArtifactHandler Error while parsing ....xml / org.xml.sax.SAXException

For me one of the items in my dialog was simply missing "jcr:primaryType="nt:unstructured" but stepping through each field to make sure it can be parsed properly definitely helps.

---

#### Cookie does not show up
Cookie does not show up even when it looks correct in the response headers.
Possible solutions:
- Add Cookie to "Adobe Granite Opt-Out Service" [OSGi config](https://docs.adobe.com/docs/en/aem/6-1/develop/platform/cookie-optout.html)
- Don't set "Domain" in Cookie
- setSecure(true) set on http traffic

---

#### Can't add pages to translation project / translation project gets created with 0 pages

For me the problem was that I had a comment at the beginning of this config file: `/etc/workflow/models/translation/translation_rules.xml`
Apparently AEM can't handle it and fails without error. Make sure to put any comments inside the `<nodelist>`.
