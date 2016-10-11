Dispatcher Cheat Sheet
==========

* Docs: http://docs.adobe.com/docs/en/dispatcher.html
* FAQ: http://helpx.adobe.com/experience-manager/using/dispatcher-faq.html
* Download: https://www.adobeaemcloud.com/content/companies/public/adobe/dispatcher/dispatcher.html

### Snippets
```
# serve stale content if no remote server is available (502, 503, 504). (/cache section)
/serveStaleOnError "1"

# disable query selector (@see http://crxdelight.com/2012/02/01/3-important-things-you-forgot-to-configure-on-your-cq-instance/)
/0080 { /type "deny" /glob "GET *.query*" }
 
# disable feed selector 
/0081 { /type "deny" /glob "GET *.feed*" }

```

See [Configuration Docs](http://docs.adobe.com/docs/en/dispatcher/disp-config.html) for more info.

```
# in JSP/Sightly:
# http://helpx.adobe.com/experience-manager/kb/DispatcherNoCache.html)
getResponse().setHeader("Dispatcher", "no-cache");
```

### Permission Sensitive Caching

Authorization checker: before a page in the cache is delivered, a HEAD request is sent to the URL specified in 'url' with the query string '?uri=<page>'. If the response status is 200 (OK), the page is returned from the cache. Otherwise, the request is forwarded to the render and its response returned.

```
/auth_checker
  {
  # request is sent to this URL with '?uri=<page>' appended
  /url "/bin/permissioncheck.html"
       
  # only the requested pages matching the filter section below are checked,
  # all other pages get delivered unchecked
  /filter
    {
    /0000
      {
      /glob "*"
      /type "deny"
      }
    /0001
      {
      /glob "*.html"
      /type "allow"
      }
    }
  # any header line returned from the auth_checker's HEAD request matching
  # the section below will be returned as well
  /headers
    {
    /0000
      {
      /glob "*"
      /type "deny"
      }
    /0001
      {
      /glob "Set-Cookie:*"
      /type "allow"
      }
    }
  }
```

And the Java Servlet that does the checking:
```java
package com.abc.servlet;


import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Property;

import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Session;

@Component(metatype=false)
@Service
public class AuthcheckerServlet extends SlingSafeMethodsServlet {

    @Property(value="/bin/permissioncheck")
    static final String SERVLET_PATH="sling.servlet.paths";

    private Logger logger = LoggerFactory.getLogger(this.getClass());

    public void doHead(SlingHttpServletRequest request, SlingHttpServletResponse response) {
        try{
            //retrieve the requested URL
            String uri = request.getParameter("uri");
            //obtain the session from the request
            Session session = request.getResourceResolver().adaptTo(javax.jcr.Session.class);
            //perform the permissions check
            try {
                session.checkPermission(uri, Session.ACTION_READ);
                logger.info("authchecker says OK");
                response.setStatus(SlingHttpServletResponse.SC_OK);
            } catch(Exception e) {
                logger.info("authchecker says READ access DENIED!");
                response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            }
        }catch(Exception e){
            logger.error("authchecker servlet exception: " + e.getMessage());
        }
    }
}
```

See this [help article](https://helpx.adobe.com/experience-manager/kb/PSCachingDelivery.html)
