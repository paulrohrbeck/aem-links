Sling Curl Command 
=========

### References
* [Manipulating Content - The SlingPostServlet (servlets.post)](http://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)
* [How to find out CURL command for any CQ operation?](http://aemtips.blogspot.com.au/2013/05/how-to-find-out-curl-command-for-any-cq.html)
* [Some of the COMMON CURL commands to work with AEM](http://aemtips.blogspot.com.au/2013/05/some-of-common-curl-commands-to-work.html)
* [sergeimuller](https://gist.github.com/sergeimuller/2916697)
* [bkondepudi](https://balawcm.wordpress.com/2013/02/13/curl-it-out-adobe-cq5-curl-commands-and-usage/)
* [AEM / CQ5 Curl Commands](http://sergeimuller.com/aem-cq5-curl-commands/)
* [Useful Curl Commands](http://cq-ops.tumblr.com/post/19017053665/useful-curl-commands)


### NOTES

USE --form-string instead of -F


### Common Curl's



Clear Audit

curl -u admin:admin -F":operation=delete" http://localhost:4502/var/audit/com.day.cq.replication

curl -u admin:admin -F":operation=delete" http://localhost:4502/var/audit/com.day.cq.wcm.core.page

GC

curl -u admin:admin -X POST --data "delete=true&delay=2" http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository/op/runDataStoreGarbageCollection/java.lang.Boolean

Upload DAM Image via WebDav

curl -u admin:admin -X PUT -T /Users/maxbarrass/Desktop/GearBumper.jpg http://localhost:4502/crx/repository/crx.default/content/dam/sitesmart/GearBumper1.jpg

curl -u admin:admin -X POST -T /Users/maxbarrass/Desktop/GearBumper.jpg http://localhost:4502/crx/repository/crx.default/content/dam/sitesmart/GearBumper2.jpg

Update DAM ASSET

curl -u admin:admin -Fdc:title="some title" -Fdc:description="some content" http://localhost:4502/content/dam/import/documents/2001/02/13/00003709-source.pdf/jcr%3Acontent/metadata

Update Title

curl -u admin:admin -Fjcr:title="Test" http://localhost:4502/content/geometrixx-outdoors/en/jcr%3Acontent | grep 'id="Message"' | sed 's/.*<div id="Message">\([^<]*\)<.*/\1/' 




