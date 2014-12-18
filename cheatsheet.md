# AEM Cheat Sheet

Some more useful snippets for AEM. Please create an issue if you have any comments or would like to add some more useful snippets etc.

-----------------------

## General

### Debugging

* Remove `#cf/` - Don’t want to see/wait for the content-finder while refereshing pages, just remove #cf/ in your url.
* `?debug=layout` - Shows you all details of the components used on your page
* `?debugConsole=true` - Runs Firebug Lite inside your browser
* `?wcmmode=(edit|preview|design|disabled)` - This parameter sets your WcmMode in the specified mode, makes testing for a particular WcmMode easier .
* `?debugClientLibs=true` - Writes out all Clientlib categories as separate files (check your HTML-source).
* `CTRL+SHIFT+U` - In combination with ?debugClientLibs=true will show you timing information of your page

[(_Source_)](http://experiencedelivers.adobe.com/cemblog/en/experiencedelivers/2012/03/cq_developer_tricks.html)


### Clientlibs

* create folder `clientlibs` with these properties (`.content.xml`):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root
    xmlns:cq="http://www.day.com/jcr/cq/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:ClientLibraryFolder"
    dependencies=""
    categories=""
    embed=""/>
```

* `categories` will be the identifier to this clientlib
* create `css.txt` and `js.txt`
* use `#base=css/` in the first line of these files to define a base path for file inclusion
* inlude clientlib with this in your jsp files: `<cq:includeClientLib categories="" />`

[(Source)](http://blogs.adobe.com/mtg/2011/11/building-components-in-adobe-cq-5-part-1-a-tutorial-on-clientlibs-using-jquery-ui.html)

### Link Checker

```
<a x-cq-linkchecker="valid" ...
<a x-cq-linkchecker="skip" ...
```

[(Source)](http://tostring.me/206/how-to-disable-adobe-cq-link-checker/)

### Font embedding

If you want to include (*.woff, *.eot, etc.), make sure to include them from a folder that is defined as a `sling:Folder`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root 
    xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    xmlns:rep="internal"
    jcr:primaryType="sling:Folder"/>
```

## Component Development

### Dialogs

```xml
<jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    cq:emptyText="Defines text that is displayed when no visual content is present."
    jcr:primaryType="cq:EditConfig">
        <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"/>    
</jcr:root>
```

* actions: (text:<some text> | - | edit | delete | insert | copymove)
* dialogMode: (floating | inline | auto)
* layout: (rollover | editbar | auto)

(See here for more details on the [EditConfig](http://dev.day.com/docs/en/cq/current/developing/components.html#Configuring with cq:EditConfig Properties) and [listener](http://dev.day.com/docs/en/cq/current/developing/components.html#cq:listeners) properties.)

-----------------------

## Querybuilder

```
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc

property=
property.operation=like
property.value=
```

(more to come...)

[(Source)](http://dev.day.com/docs/en/cq/current/dam/customizing_and_extendingcq5dam/query_builder.html)

-----------------------

### Install AEM

```
java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.0.0.jar
```

```
crx-quickstart/bin/(stop | start | status | quickstart)
```


### Install AEM with different run modes

Installation run modes (not changeable): author, publish, samplecontent, nosamplecontent

```
cq-<instance-type>-p<port-number>.jar
cq-publish-p4503.jar
```

Additional run modes:

1. crx-quickstart/conf/sling.properties: ```sling.run.modes=author```
2. ```java -jar cq-56-p4545.jar -r dev```
3. System property: ```-Dsling.run.modes=publish,prod```

### Troubleshooting

Possible memory leaks? ```-XX:+HeapDumpOnOutOfMemoryError```

Start in debug mode: [help article](http://helpx.adobe.com/experience-manager/kb/CQ5HowToSetupRemoteDebuggingWithEclipse.html)

```
-agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n

Example:
java -Xmx512m -agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n -jar cq-author-4502.jar

OR:

crx-quickstart/bin/start -d --debug-port 8000
```

### Vault

```
Checkout:
vlt --credentials admin:admin co http://localhost:4502/crx/-/etc/designs ~/Desktop/

Export code from JCR:
vlt export -v http://localhost:4502/crx /content/forms forms

Import code to JCR:
vlt -v import http://localhost:4502/crx . /

See modified files:
vlt st

See  changes:
vlt diff text.jsp

Commit  changes:
vlt ci test.jsp

```

### David's Model

1. Data First, Structure Later. Maybe.
2. Drive the content hierarchy, don't let it happen.
3. Workspaces are for clone(), merge() and update().
4. Beware of Same Name Siblings.
5. References considered harmful.
6. Files are Files are Files.
7. ID's are evil.

[(Source)](http://wiki.apache.org/jackrabbit/DavidsModel)
