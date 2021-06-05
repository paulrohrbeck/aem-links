Sling Curl Command Cheat Sheet
=========

### References
* [Manipulating Content - The SlingPostServlet (servlets.post)](http://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)
* [How to find out CURL command for any CQ operation?](http://aemtips.blogspot.com.au/2013/05/how-to-find-out-curl-command-for-any-cq.html)
* [Some of the COMMON CURL commands to work with AEM](http://aemtips.blogspot.com.au/2013/05/some-of-common-curl-commands-to-work.html)
* [sergeimuller](https://gist.github.com/sergeimuller/2916697)
* [bkondepudi](https://balawcm.wordpress.com/2013/02/13/curl-it-out-adobe-cq5-curl-commands-and-usage/)
* [AEM / CQ5 Curl Commands](http://sergeimuller.com/aem-cq5-curl-commands/)
* [Useful Curl Commands](http://cq-ops.tumblr.com/post/19017053665/useful-curl-commands)
* [CRX 2.3 - Working with Packages](https://docs.adobe.com/docs/en/crx/2-3/how_to/package_manager.html)
* [CQ5 curl commands](https://gist.github.com/sergeimuller/2916697)
* [Culr It Out](http://balawcm.wordpress.com/2013/02/13/curl-it-out-adobe-cq5-curl-commands-and-usage/)

### NOTES

* When using curl to insert UTF-8 content instead of -F use:
```
--form-string
```
Example:
```bash
curl -X POST -u "admin:admin" -F"_charset_=utf-8" --form-string "text-ja=サーバーへの接続に問題が発生しました。数分待ってから再度お試しください。" \
    http://localhost:4502/content/site/jcr:content/par
```

* Since version 1.0.6 of the Sling Security bundle, you will get Forbidden when accessing endpoint, without valid user agent or without CSRF token, to fix add some header to your curl :
```bash
AEM_SCHEME=http \
AEM_HOST=localhost \
AEM_PORT=4502 \
AEM_LOGIN=admin:admin \
CURL=$(which curl) \
REFERER=${AEM_SCHEME}://${AEM_HOST}:${AEM_PORT} \
SERVICE_TOKEN=/libs/granite/csrf/token.json \
AEM_TOKEN="$(${CURL} -s -H User-Agent:curl -H Referer:${REFERER} -u ${AEM_LOGIN} ${REFERER}${SERVICE_TOKEN}  | sed -e 's/[{"token":}]/''/g')"  \
${CURL} -H User-Agent:curl -H Referer:${REFERER} -u ${AEM_LOGIN} -H CSRF-Token:${AEM_TOKEN} -X POST ${REFERER}/content/jcr:content -F jcr:primaryType=nt:unstructured -F jcr:title=Test
```

you can check valid User-Agent headers here:
```
http://localhost:4502/system/console/configMgr/com.day.cq.wcm.foundation.impl.HTTPAuthHandler
```

you can check valid CSRF User-Agent headers here:
```
http://localhost:4502/system/console/configMgr/com.adobe.granite.csrf.impl.CSRFFilter
```

alternative is to set allow empty and 'allow.hosts.regexp':
```
http://localhost:4502/system/console/configMgr/org.apache.sling.security.impl.ReferrerFilter
```



* The following CQ curl commands assumes a admin:admin username and password.

* For Windows/Powershell users: use two "" when doing a -F cURL command.
```
Example: -F"":operation=delete""
```
* Quotes around name of package (or name of zip file, or jar) should be included.

CSRF Request in Scripts
========
Here is how to add CSRF to your scripts
```bash
AEM_SCHEME=http
AEM_HOST=localhost
AEM_PORT=4502
AEM_LOGIN=admin:admin
REFERER=${AEM_SCHEME}://${AEM_HOST}:${AEM_PORT}
SERVICE_URL=/libs/granite/security/post/authorizables
SERVICE_TOKEN=/libs/granite/csrf/token.json

AEM_TOKEN="$(curl -s -H User-Agent:curl -H Referer:${REFERER} -u ${AEM_LOGIN} ${REFERER}${SERVICE_TOKEN}  | sed -e 's/[{"token":}]/''/g')"

echo "CSRF Token: ${AEM_TOKEN}"

HEADERS=" -u ${AEM_LOGIN} -H User-Agent:curl -H CSRF-Token:${AEM_TOKEN} -H Referer:${REFERER}"

echo "Headers: $HEADERS"

curl ${HEADERS} -FcreateGroup= -FauthorizableId=testGroup1 ${REFERER}${SERVICE_URL}
```

### Common Curl's


Clear Audit
```bash
curl -u admin:admin -F":operation=delete" http://localhost:4502/var/audit/com.day.cq.replication

curl -u admin:admin -F":operation=delete" http://localhost:4502/var/audit/com.day.cq.wcm.core.page
```


Upload DAM Image via WebDav
```bash
curl -u admin:admin -X PUT -T /Users/maxbarrass/Desktop/GearBumper.jpg http://localhost:4502/crx/repository/crx.default/content/dam/sitesmart/GearBumper1.jpg

curl -u admin:admin -X POST -T /Users/maxbarrass/Desktop/GearBumper.jpg http://localhost:4502/crx/repository/crx.default/content/dam/sitesmart/GearBumper2.jpg
```

Update DAM ASSET
```bash
curl -u admin:admin -Fdc:title="some title" -Fdc:description="some content" http://localhost:4502/content/dam/import/documents/2001/02/13/00003709-source.pdf/jcr%3Acontent/metadata
```


Encrypt a String
```bash
curl -u admin:admin --header "Referer:http://localhost:4502" -F"datum=password" http://localhost:4502/system/console/crypto/.json
```

Disabled Dam Workflow
```bash
curl -u admin:admin -X POST 'http://127.0.0.1:4502/libs/cq/workflow/launcher' --data '_charset_=utf-8&edit=%2Fetc%2Fworkflow%2Flauncher%2Fconfig%2Fupdate_asset_create&%3Astatus=browser&eventType=1&nodetype=nt%3Afile&glob=%2Fcontent%2Fdam(%2F.*%2F)renditions%2Foriginal&condition=&workflow=%2Fetc%2Fworkflow%2Fmodels%2Fdam%2Fupdate_asset%2Fjcr%3Acontent%2Fmodel&description=&enabled=false&excludeList=&runModes=author'
```
Enable Dam workflow
```bash
curl -u admin:admin -X POST 'http://127.0.0.1:4502/libs/cq/workflow/launcher' --data '_charset_=utf-8&edit=%2Fetc%2Fworkflow%2Flauncher%2Fconfig%2Fupdate_asset_create&%3Astatus=browser&eventType=1&nodetype=nt%3Afile&glob=%2Fcontent%2Fdam(%2F.*%2F)renditions%2Foriginal&condition=&workflow=%2Fetc%2Fworkflow%2Fmodels%2Fdam%2Fupdate_asset%2Fjcr%3Acontent%2Fmodel&description=&enabled=true&excludeList=&runModes=author'
```


### Content Management


Create a folder in /apps called myFolder:
```bash
curl -u admin:admin -Fjcr:primaryType=sling:Folder http://localhost:4502/content/dam/myFolder
```

Copy the folder /content/dam/geometrixx/icons/ (and its contents) to /content/dam/myFolder
```bash
curl -u admin:admin -F:operation=copy -F:dest=/content/dam/myFolder/ http://localhost:4502/content/dam/geometrixx/icons/
```

Update Title Attribute
```bash
curl -u admin:admin -Fjcr:title="Test" http://localhost:4502/content/geometrixx-outdoors/en/jcr%3Acontent | grep 'id="Message"' | sed 's/.*<div id="Message">\([^<]*\)<.*/\1/'
```

Move Content
```bash
curl -u admin:admin \
--header "Referer:http://localhost:4502/" \
-F":diff=>/apps/test1/test2 : /apps/test2/test2" \
http://localhost:4502/crx/server/crx.default/jcr%3aroot
```


Activate Page
```bash
curl -u admin:admin -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

Deactivate Page
```bash
curl -u admin:admin -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```


Tree Activation
```bash
curl -u admin:admin -F cmd=activate -F ignoredeactivated=true -F onlymodified=true \
    -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

Lock page
```bash
curl -u admin:admin -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" \
http://localhost:4502/bin/wcmcommand
```


Unlock page
```bash
curl -u admin:admin -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" \
http://localhost:4502/bin/wcmcommand
```

Copy page
```bash
curl -u admin:admin -F:operation=copy -F:dest=/path/to/destination http://localhost:4502/path/to/source
```


### Bundle Management


Uninstall a bundle (use http://localhost:4502/system/console/bundles to access the Apache Felix web console)
```bash
curl -u admin:admin -daction=uninstall http://localhost:4502/system/console/bundles/name-of-bundle
```

Install a bundle
```bash
curl -u admin:admin -F action=install -F bundlestartlevel=20 -F bundlefile=@name-of-jar.jar http://localhost:4502/system/console/bundles
```

Build a bundle
```bash
curl -u admin:admin -F"bundleHome=/apps/centrica/bundles/name of bundle" \
-F descriptor=/apps/centrica/bundles/com.centrica.cq.wcm.core-bundle/name_of_bundle.bnd \
http://localhost:4502/libs/crxde/build
```

Stop a bundle
```bash
curl -u admin:admin http://localhost:4502/system/console/bundles/org.apache.sling.scripting.jsp \
-F action=stop
```

Start a bundle
```bash
curl -u admin:admin http://localhost:4502/system/console/bundles/org.apache.sling.scripting.jsp \
-F action=start
```
Delete a node (hierarchy) - (this will delete any directory / node / site)
```bash
curl -u admin:admin -X DELETE http://localhost:4502/path/to/node/jcr:content/nodeName
```

Get Bundle Config
```bash
curl -u admin:admin http://localhost:4502/system/console/bundles/org.apache.jackrabbit.oak-core.json
```



### Package Management

List Commands
```bash
 curl -u admin:admin  http://localhost:4502/crx/packmgr/service.jsp?cmd=help
```

Check If Package Exist
```bash
curl -u admin:admin -s -I -w %{http_code} http://localhost:4502/etc/packages/package/group/path/name_of_package.zip
```

List Packages
```bash
#XML
curl -u admin:admin http://localhost:4502/crx/packmgr/service.jsp?cmd=ls
#JSON
curl -u admin:admin http://localhost:4502/crx/packmgr/list.jsp
```

Upload a package AND install
```bash
curl -u admin:admin -F file=@"name of zip file" -F name="name of package" \
    -F force=true -F install=true http://localhost:4502/crx/packmgr/service.jsp
```

Upload a package DO NOT install
```bash
curl -u admin:admin -F file=@"name of zip file" -F name="name of package" \
    -F force=true -F install=false http://localhost:4502/crx/packmgr/service.jsp
```

Rebuild an existing package in CQ
```bash
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/name_of_package.zip?cmd=build
```

Download (the package)
```bash
curl -u admin:admin http://localhost:4502/etc/packages/export/name_of_package.zip > name_of_package.zip
```

Upload a new package
```bash
curl -u admin:admin -F package=@"name_of_package.zip" http://localhost:4502/crx/packmgr/service/.json/?cmd=upload
```

Install an existing package
```bash
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/export/name-of-package?cmd=install
```

Delete Package
```bash
curl -u admin:admin -X POST -F cmd=delete http://localhost:4502/crx/packmgr/service/script.html/etc/packages/package-group/package-name.zip
```






### JCR Node Management:

Delete a node (hierarchy) – (this will delete any directory / node / site)
```bash
curl -X DELETE http://localhost:4502/path/to/node/jcr:content/nodeName -u admin:admin
```

Create or add a JCR node:
```bash
curl -u admin:admin -F"_charset_=utf-8" -F":nameHint=node" -F"jcr:primaryType=nt:unstructured" -F"sling:resourceType=project-A/components/abc-definition" -F"nodeReferenceName=ref-name1" -F"jcr:createdBy=bala" -F"jcr:lastModifiedBy=bala"http://localhost:4502/content/geometrixx/en_GB/products/jcr:content/abc/
```

Create or add a JCR node along with some properties:
```bash
curl -u admin:admin -F"_charset_=utf-8" -F":nameHint=var" -F"jcr:primaryType=nt:unstructured" -F"key=key1" -F"value=key1-value"http://localhost:4502/content/geometrixx/en_GB/products/jcr:content/abc/variables/
```

### CQ Replication Commands:
Tree Activation
```bash
curl -u admin:admin -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixxhttp://localhost:4502/etc/replication/treeactivation.html
```

Clear Queue Jobs
```
AEM_SCHEME=http; \
AEM_HOST=localhost; \
AEM_PORT=4502; \
AEM_LOGIN=admin:admin; \
CURL=$(which curl); \
REFERER="${AEM_SCHEME}://${AEM_HOST}:${AEM_PORT}"; \
TOKEN_SERVICE="/libs/granite/csrf/token.json"; \
SERVICE_URL="/etc/replication/agents.author/publish/jcr:content.queue.json"; \
SERVICE_CONTENT="cmd=clear&agent=publish"; \
AEM_TOKEN=$( ${CURL} -v -s -H User-Agent:curl -H Referer:${REFERER} -u "${AEM_LOGIN}" ${REFERER}${TOKEN_SERVICE} | sed -e 's/[{"token":}]/''/g' ); \
echo AEM_TOKEN=$AEM_TOKEN; \
AEM_COMMAND=$( ${CURL} -v -H User-Agent:curl -H Referer:${REFERER} -u "${AEM_LOGIN}" -H "CSRF-Token:${AEM_TOKEN}" --data ${SERVICE_CONTENT} -X POST ${REFERER}${SERVICE_URL} ); \
echo AEM_COMMAND=$AEM_COMMAND
```

### User & Group Administration
Get User Info:
```bash
curl -u admin:admin http://localhost:4502/libs/granite/security/balakondepudi.json
```

Create User:
```bash
curl -u admin:admin -FcreateUser= -FauthorizableId=testuser -Frep:password=abc123 http://localhost:4502/libs/granite/security/post/authorizables
```

Create Group:
```bash
curl -u admin:admin -FcreateGroup= -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

Create user with Profile:
```bash
curl -u admin:admin -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

Set a Profile Property on an Existing User:
```bash
curl -u admin:admin -Fprofile/age=29 http://localhost:4502/home/users/t/testuser1.rw.html
```

Create a User as a Member of a Group:
```bash
curl -u admin:admin -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

Add a User to a Group:
```bash
curl -u admin:admin -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

Add multiple Users to a Group:
```bash
curl -u admin:admin -FaddMembers=testuser1 -FaddMembers=testuser2 http://localhost:4502/home/groups/t/testGroup.rw.html
```

Remove a User from a Group:
```bash
curl -u admin:admin -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

Set a User’s Group Memberships:
```bash
curl -u admin:admin -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

Delete user and Group:
```bash
curl -u admin:admin -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
curl -u admin:admin -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

Change a user password:
```bash
curl -u testuser:OLD_PWD -F rep:password="NEW_PWD" http://localhost:4502/home/users/t/testuser.rw.html

curl -u admin:admin -F rep:password="test" http://localhost:4502/home/users/a/alister@geometrixx.com
```

Group Permissions
```bash
curl -u admin:admin http://localhost:4502/.cqactions.tidy.json?_dc=1403662520751&anode=%2Fhome%2Fgroups%2Fa%2Fadministrators&path=%2Fhome%2Fgroups%2Fa%2Fadministrators&predicate=useradmin&depth=1&authorizableId=admin
```

Get User Info
```bash
curl -s -u admin:admin -X GET "http://localhost:4502/bin/querybuilder.json?path=/home/users&1_property=rep:authorizableId&1_property.value=admin&p.limit=-1"
```

Get User Path
```bash
curl -s -u admin:admin -X GET "http://localhost:4502/bin/querybuilder.json?path=/home/users&1_property=rep:authorizableId&1_property.value=admin&p.limit=-1" | sed -e 's/^.*"path":"\([^"]*\)".*$/\1/'
```


### Backup Commands:
Online Backup:
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=<PATH-TO-BACKUP>/12-feb-2013.zip
```
Online backup with delay in milli seconds:
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/a/BackupDelay?value=<TIME-IN-MILISECOND&gt;

curl -u admin:admin --data "delay=TIME-IN-MILISECONDS&force=false&target=01-dec-2012.zip" http://localhost:4502/libs/granite/backup/content/admin/backups/
```
How to stop a running online backup:
```bash
curl -u admin:admin http://localhost:4502/libs/granite/backup/content/admin/backups.cancel.html
```
Link to track online progress:
```bash
http://localhost:4502/libs/granite/backup/content/admin.html
```
To Cancel the backup
```bash
curl -u admin:admin -X POST http://localhost:4502/libs/granite/backup/content/admin/backups.cancel.html
```


### Datastore GC:

Start Datastore Garbage Collection:
```bash
curl -u admin:admin -X POST \
http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/runDataStoreGarbageCollection/java.lang.Boolean
```

Start Datastore Garbage Collection Delayed:
```bash
curl -u admin:admin -X POST --data "delete=true&delay=2" \
http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository/op/runDataStoreGarbageCollection/java.lang.Boolean
```

Tar Optimization:
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startTarOptimization/
```

Flush Dispatcher Cache:
```bash
curl -H "CQ-Action: Flush" -H "CQ-Handle: /content/geometrixx/en/products" -H "CQ-Path:/content/geometrixx/en/products" \
-H "Content-Length: 0" -H "Content-Type: application/octet-stream" \
http://dispatcher-server-hostname:port/dispatcher/invalidate.cache
```

BINARY GARBAGE COLLECTION
```bash
curl -u admin:admin -X POST --data 'markOnly=false' \
'http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D14%2Cname%3D%22repository+manager%22%2Ctype%3D%22RepositoryManagement%22/op/startDataStoreGC/boolean'
```
GARBAGE COLLECTION FOR A SHARED DATA STORE
```bash
curl -u admin:admin -X POST --data 'markOnly=true' \
    'http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D14%2Cname%3D%22repository+manager%22%2Ctype%3D%22RepositoryManagement%22/op/startDataStoreGC/boolean'
```

CURL Command to Run AEM 6 TarMK Consistency Check
```bash
curl -u admin:admin -X POST --data "workspace=crx.default&path=%2F&traversal=on&fixinconsistencies=on&log=off&datastoreconsistency=on" http://localhost:4502/system/console/repositorycheck
```


### LDAP CURL


List Orphaned Users
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite.ldap:host=<ldaphost>,port=<ldapport>,type=Tools/op/listOrphanedUsers/
```
Sync All Users
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite.ldap:host=<ldaphost>,port=<ldapport>,type=Tools/op/syncAllUsers/
```
Sync User
```bash
curl -u admin:admin -X POST --data "user=<cn=user001,ou=users,dc=day,dc=com> http://localhost:4502/system/console/jmx/com.adobe.granite.ldap:host=<ldaphost>,port=<ldapport>,type=Tools/op/syncUser/java.lang.String"
```
Sync User List
Ex:-  To sync 2 users user007 & user008 on my localhost
```bash
curl -u admin:admin -X POST --data userlist=%5B%22cn%3Duser007%2Cou%3Dusers%2Cdc%3Dday%2Cdc%3Dcom%22%2C%22cn%3Duser008%2Cou%3Dusers%2Cdc%3Dday%2Cdc%3Dcom%22%5D http://localhost:4502/system/console/jmx/com.adobe.granite.ldap%3Ahost%3Dlocalhost%2Cport%3D389%2Ctype%3DTools/op/syncUserList/%5BLjava.lang.String%3B
```
Purge Users
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite.ldap:host=<ldaphost>,port=<ldapport>,type=Tools/op/purgeUsers/
```
Sync Users
```bash
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite.ldap:host=<ldaphost>,port=<ldapport>,type=Tools/op/syncUsers/
```

### Query Builder

Find "all” page references for a given image/asset in a jcr path. The below command will return in JSON format:
```bash
curl -s -u admin:admin -X GET \
http://localhost:4502/bin/querybuilder.json?path=/content/my-site&1_property=fileReference&1_property.value=/content/dam/my-site/image.jpg&p.limit=-1
```
*Note: -1 in the p.limit will return all page references else prints only 10.

You can also specify the required number of page references; something like below which will return only 20 page references:
```bash
curl -s -u admin:admin -X GEThttp://localhost:4502/bin/querybuilder.json?path=/content/my-site&1_property=fileReference&1_property.value=/content/dam/my-site/image.jpg&p.limit=20
```
To find all pending Jobs
```bash
curl -s -u admin:admin http://localhost:4502/bin/querybuilder.json?&path=/var/eventing/jobs&type=slingevent:Job&p.limit=-1&fulltext=/com/day/cq/replication/job&fulltext.relPath=@slingevent:topic&property.and=true&property=slingevent:finished&property.operation=not&orderby=slingevent:created&orderby.sort=asc&#8221;
```

To find all Blocking Jobs
```bash
curl -s -u admin:admin http://localhost:4502/bin/querybuilder.json?path=/var/eventing/jobs/anon&type=slingevent:Job&rangeproperty.property=event.job.retrycount&rangeproperty.lowerBound=1&#8243;
```

Clear JSP Cache
```bash
curl -s -u admin:admin -H User-Agent:curl -X POST http://localhost:4502/system/console/slingjsp
```

### System Console
download logs without viewing them in console
```bash
curl -s -u admin:admin -X POST http://localhost:4502/system/console/status-slinglogs/configuration-status.zip
```

### Restart AEM
```bash
curl -u admin:admin -d "shutdown_type=Restart" http://localhost:4502/system/console/vmstat
```

### Enable CRX/De / WebDav
enable wedav

```bash
curl -u admin:admin -H User-Agent:curl -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" -F"../../jcr:primaryType=sling:Folder" -F"../jcr:primaryType=sling:Folder" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

or 

```bash
curl -u admin:admin -H User-Agent:curl -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" -F"../../jcr:primaryType=sling:Folder" -F"../jcr:primaryType=sling:Folder" http://localhost:4502/apps/system/config/org.apache.sling.jcr.webdav.impl.servlets.SimpleWebDavServlet
```

disable wedav
```bash
curl -u admin:admin -H User-Agent:curl -X DELETE http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

or

```bash
curl -u admin:admin -H User-Agent:curl -X DELETE http://localhost:4502/apps/system/config/org.apache.sling.jcr.webdav.impl.servlets.SimpleWebDavServlet
```


### Enable Query Debug Log
create Query Debug log file
```bash
curl -u admin:admin -H User-Agent:curl -F "jcr:primaryType=sling:OsgiConfig" -F "org.apache.sling.commons.log.names@TypeHint=String[]" -F "org.apache.sling.commons.log.names=com.day.cq.search" -F "org.apache.sling.commons.log.names=org.apache.jackrabbit.oak.plugins.index" -F "org.apache.sling.commons.log.names=org.apache.jackrabbit.oak.query" -F "org.apache.sling.commons.log.file=logs/query.log" -F "org.apache.sling.commons.log.level=info" -F "org.apache.sling.commons.log.additiv=false" http://localhost:4502/apps/system/config/org.apache.sling.commons.log.LogManager.factory.config-query.config
```

remove Query Debug log file
```bash
curl -u admin:admin -H User-Agent:curl -F":operation=delete" http://localhost:4502/apps/system/config/org.apache.sling.commons.log.LogManager.factory.config-query.config
```

count Session Statistics on your instance
```bash
curl -u admin:admin http://localhost:4502/system/console/jmx | grep -o SessionStat | wc -l
```


count Admin Session Statistics on your instance
```bash
curl -u admin:admin http://192.168.27.2:4502/system/console/jmx | grep -o "&quot;admin@session" | wc -l
```

Start workflow

```bash
curl -u admin:admin -H User-Agent:curl -F "payload=/content/aemdesign-showcase/en/component/lists/page-list" -F "payloadType=JCR_PATH" -F "workflowTitle=CurlTitle" -F "startComment=CurlComment" -F"model=/var/workflow/models/test1" http://192.168.27.2:4502/etc/workflow/instances
```

## Workflow Launchers

### Disable Workflow Launchers

```bash
curl -u admin:admin -H User-Agent:curl -F "action=stop" http://localhost:4502/system/console/bundles/com.adobe.granite.workflow.core
```

#### Enable Workflow Launchers

```bash
curl -u admin:admin -H User-Agent:curl -F "action=start" http://localhost:4502/system/console/bundles/com.adobe.granite.workflow.core
```
