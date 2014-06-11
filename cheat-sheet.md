# AEM Cheat Sheet

Some more useful snippets for AEM. Please create an issue if you have any comments or would like to add some more useful snippets etc.

-----------------------

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

* create `css.txt` and `js.txt`
* use `#base=css/` in the first line of these files to define a base path for file inclusion


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
