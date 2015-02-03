# Dispatcher

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
