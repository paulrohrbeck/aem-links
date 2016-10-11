AEM Cheat Sheet
========

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
How to disable the link checker for specific links:
```
<a x-cq-linkchecker="valid" ...
<a x-cq-linkchecker="skip" ...
```

[(Source)](http://tostring.me/206/how-to-disable-adobe-cq-link-checker/)

## Templates

### Availability
Order of evaluation:

1. cq:allowedTemplates
2. allowedPaths (deprecated)
3. allowedParents
4. allowedChildren

[(Source)](http://docs.adobe.com/docs/en/cq/current/developing/templates.html#Template Availability)

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

[(More info)](https://helpx.adobe.com/experience-manager/kb/RunModeSetUp.html)

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

##### filter.xml Modes
There are three Mode available:

1. replace: Normal behavior. Existing content is replaced completly by the imported content, i.e. is overridden or deleted accordingly.
2. merge: Existing content is not modified, i.e. only new content is added and none is deleted or modified
3. update: Existing content is only updated but never deleted

(via [wemblog](http://www.wemblog.com/2012/04/how-to-change-package-install-behavior.html))

### David's Model

1. Data First, Structure Later. Maybe.
2. Drive the content hierarchy, don't let it happen.
3. Workspaces are for clone(), merge() and update().
4. Beware of Same Name Siblings.
5. References considered harmful.
6. Files are Files are Files.
7. ID's are evil.

[(Source)](http://wiki.apache.org/jackrabbit/DavidsModel)

### Sling URL to Script resolution

GET Request: [...]/print.a4.html (Resource type of this resource is is "sling\sample")

Matches in order:

1. print/a4.html.jsp
2. print/a4.jsp (matches more selectors, html extension is implied)
3. print.html.jsp
4. print.jsp
5. html.jsp
6. sample.jsp
7. GET.jsp

Wrong:
a4.html.jsp - does not include the first selector (print)
a4/print.html.jsp - wrong order of selectors

([Source](http://sling.apache.org/documentation/the-sling-engine/url-to-script-resolution.html), also see [here] (http://svn.apache.org/repos/asf/sling/trunk/bundles/servlets/resolver/src/test/java/org/apache/sling/servlets/resolver/internal/helper/ScriptSelectionTest.java) for some example tests)

### Dialog settings

```
sling:hideProperties (String or String[])
Specifies the property, or list of properties, to hide.
The wildcard * hides all.

sling:hideResource (Boolean)
Indicates whether the resources should be completely hidden, including its children.

sling:hideChildren (String or String[])
Contains the child node, or list of child nodes, to hide. The properties of the node will be maintained.
The wildcard * hides all.

sling:orderBefore (String)
Contains the name of the sibling node that the current node should be positioned in front of.

```

([Source](https://docs.adobe.com/docs/en/aem/6-1/develop/platform/sling-resource-merger.html))

```
cq:showOnCreate="{Boolean}true"
Page property to be available in the create view (e.g. Create Page wizard)

cq:hideOnEdit
Page property to be available in the edit view (e.g. View/Edit) Properties option)

renderReadOnly="{Boolean}true"
If this is not set it will show the form fields even if the author is not in edit mode.
```

([Source](https://docs.adobe.com/docs/en/aem/6-1/develop/extending/customizing-page-properties/page-properties-views.html))

```
allowBulkEdit="{Boolean}true"
```

([Source](https://docs.adobe.com/docs/en/aem/6-1/develop/extending/customizing-page-properties/bulk-editing.html))
