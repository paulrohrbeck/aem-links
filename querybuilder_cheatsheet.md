Query Builder Cheat Sheet
=========


### Query Builder API
* [6.1](https://docs.adobe.com/docs/en/aem/6-1/develop/search/querybuilder-api.html)
* [5.6.1](https://docs.adobe.com/docs/en/cq/5-6-1/dam/customizing_and_extendingcq5dam/query_builder.html)

### References
* [CQ Queries Demystified](http://itgumby.github.io/blog/2014/10/cq-queries-demystified/)
* [Tuning your JCR Queries for the AEM & Jackrabbit OAK](http://tech.ethomasjoseph.com/2015/03/tuning-your-jcr-queries-for-aem.html)

### Documentation
* [JCR 2.0 Spec - Query](http://www.day.com/specs/jcr/2.0/6_Query.html)
* [Predicate](http://docs.adobe.com/docs/en/cq/5-6-1/javadoc/com/day/cq/search/Predicate.html)
* [PredicateEvaluator](http://docs.adobe.com/docs/en/cq/5-6-1/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)
* [JcrPropertyPredicateEvaluator](http://docs.adobe.com/docs/en/cq/5-6-1/javadoc/com/day/cq/search/eval/JcrPropertyPredicateEvaluator.html)
* [Implementing a Custom Predicate Evaluator for the Query Builder](https://docs.adobe.com/docs/en/aem/6-1/develop/search/implementing-custom-predicate-evaluator.html)
* [Security CQ Actions](https://docs.adobe.com/docs/en/cq/5-6-1/javadoc/index.html?com/day/cq/security/util/CqActions.html)
* [Creating Adobe CQ OSGi bundles that use the Query Builder API](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)
* [CRX 2.3 Search Features](https://docs.adobe.com/docs/en/crx/2-3/developing/searching_in_crx.html)
* [AEM 5.6.1 Search Features](https://docs.adobe.com/docs/en/cq/5-6-1/core/developing/searching_in_crx.html)
* [Apache Lucene - Query Parser Syntax](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html)

### Query Builder Samples
* [Operation Exists](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fcq%3Atoolbars%0D%0Aproperty.operation%3Dexists%0D%0A)
* [Operation Like](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dlike%0D%0Aproperty.value%3D%25ac%25)
* [Operation Equals](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dequals%0D%0Aproperty.value%3DContact)
* [Operation UnEquals](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dunequals%0D%0Aproperty.value%3DContact)
* [Operation Not Exist](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fcq%3Atoolbars%0D%0Aproperty.operation%3Dnot)
* [Special Character Search](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dnt%3Aunstructured%0D%0Aproperty%3Dtext%0D%0Aproperty.operation%3Dlike%0D%0Aproperty.value%3D%25%3Cli%3EThe+whole+is+greater+than+the+part.%3C%2Fli%3E%25)
<<<<<<< HEAD

### Tools
* [QueryBuilder Debugger](http://localhost:4502/libs/cq/search/content/querydebug.html)
* [Available Predicates](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


### Available Predicates
These are the keywords that can be used in the Query Builder when creating predicate queries:

* relativedaterange
* hasPermission
* nodename
* tagsearch
* property
* rangeproperty
* path
* memberOf
* tagid
* mainasset
* type
* savedquery
* dateComparison
* notexpired
* tag
* language
* similar
* daterange
* fulltext
* boolproperty
* group

### Samples 

GET USER PATH
```bash
curl -s -u admin:admin -X GET "http://localhost:4502/bin/querybuilder.json?path=/home/users&1_property=rep:authorizableId&1_property.value=admin&p.limit=-1" | sed -e 's/^.*"path":"\([^"]*\)".*$/\1/'
```


### Query Builder API Docs

* SOURCE: [Query Builder API](https://docs.adobe.com/docs/en/aem/6-1/develop/search/querybuilder-api.html)

Returning all results

The following query will return ten results (or to be precise a maximum of ten), but inform you of the Number of hits: that are actually available:

[http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby:path](http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby:path)


The same query (with the parameter p.limit=-1) will return all results (this might be a high number depending on your instance):

[http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby:path](http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby:path)

Find jar files and order them, newest first

[http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc](http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc)

Find all pages and order them by last modified

[http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified](http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified)

Find all pages and order them by last modified, but descending

[http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc](http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc)

Fulltext search, ordered by score

[http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc](http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc)

Search for pages tagged with a certain tag

[http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags](http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags)

Search under multiple paths (using groups)

[http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true](http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true)

Search for properties

Here you are searching for all pages of a given template, using the cq:template property:

[http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent](http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent)

This has the drawback that the jcr:content nodes of the pages, not the pages themselves, are returned. To solve this, you can search by relative path:

[http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage](http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage)

Search for multiple properties

When using the property predicate multiple times, you have to add the number prefixes again:

[http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage](http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage)

Search for multiple property values

To avoid big groups when you want to search for multiple values of a property ("A" or "B" or "C"), you can provide multiple values to the property predicate:

[http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events](http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events)

For multi-value properties, you can also require that multiple values match ("A" and "B" and "C"):

[http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar](http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar)


REFINING WHAT IS RETURNED

By default, the QueryBuilder JSON Servlet will return a default set of properties for each node in the search result (e.g. path, name, title, etc.). In order to gain control over which properties are returned, you can do one of the following:

Specify p.hits=full, in which case all properties will be included for each node:

[http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle](http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle)

Use p.hits=selective and specify the properties you want to get in p.properties, separated by a space:

[http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Triangle](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Triangle)

Another thing you can do is include child nodes in the QueryBuilder response. In order to do this you need to specify p.nodedepth=n, where n is the number of levels you want the query to return. Note that, in order for a child node to be returned, it must be specified by the properties selector (p.hits=full). Example:

[http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle](http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle)

MORE PREDICATES

For more predicates, see the [Javadoc for the *PredicateEvaluator classes](https://docs.adobe.com/docs/en/aem/6-1/ref/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). The Javadoc for these classes contains the list of properties that you can use.

The prefix of the class name (for example, "similar" in [SimilarityPredicateEvaluator](https://docs.adobe.com/docs/en/aem/6-1/ref/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) is the principal property of the class. This property is also the name of the predicate to use in the query (in lower case).

For such principal properties, you can shorten the query and use "similar=/content/en" instead of the fully qualified variant "similar.similar=/content/en". The fully qualified form must be used for all non-principal properties of a class.

EXAMPLE QUERY BUILDER API USAGE

```java
String fulltextSearchTerm = "Geometrixx";
               
// create query description as hash map (simplest way, same as form post)
Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
map.put("path", "/content");
map.put("type", "cq:Page");
map.put("group.p.or", "true"); // combine this group with OR
map.put("group.1_fulltext", fulltextSearchTerm);
map.put("group.1_fulltext.relPath", "jcr:content");
map.put("group.2_fulltext", fulltextSearchTerm);
map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

// can be done in map or with Query methods
map.put("p.offset", "0"); // same as query.setStart(0) below
map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below
                 
Query query = builder.createQuery(PredicateGroup.create(map), session);
query.setStart(0);
query.setHitsPerPage(20);
           
SearchResult result = query.getResult();

// paging metadata
int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
long totalMatches = result.getTotalMatches();
long offset = result.getStartIndex();
long numberOfPages = totalMatches / 20;
              
//Place the results in XML to return to client
DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document doc = builder.newDocument();
                           
//Start building the XML to pass back to the AEM client
Element root = doc.createElement( "results" );
doc.appendChild( root );
              
// iterating over the results
for (Hit hit : result.getHits()) {
   String path = hit.getPath();

  //Create a result element
  Element resultel = doc.createElement( "result" );
  root.appendChild( resultel );
                  
  Element pathel = doc.createElement( "path" );
  pathel.appendChild( doc.createTextNode(path ) );
  resultel.appendChild( pathel );
}
```

The same query executed over HTTP using the Query Builder (JSON) Servlet:

[http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20](http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20)


STORING AND LOADING QUERIES

Queries can be stored to the repository so that you can use them later. The QueryBuilder provides the  storeQuery method with the following signature:
```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

When using the QueryBuilder#storeQuery method, the given Query is stored into the repository as a file or as a property according to the createFile argument value. The following example shows how to save a Query to the path /mypath/getfiles as a file:
```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Any previously stored queries can be loaded from the repository by using the QueryBuilder#loadQuery method:
```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

For example, a Query stored to the path /mypath/getfiles can be loaded by the following snippet:
```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## More Examples
[Query Builder Debugger](http://localhost:4502/libs/cq/search/content/querydebug.html)

```
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc

# LIKE
property=propertyName
property.operation=like
property.value=%value%

# check if a property exists:
property=propertyName
property.operation=exists
property.value=true

# set this higher so you can actually see all the results and not just 10
p.limit=1000

# date ranges:
daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=

```


```
Grab all assets and return the path, title and tags:
http://localhost:4502/bin/querybuilder.json?type=dam:Asset&path=/content/dam&p.limit=-1&p.hits=selective&p.properties=jcr:path%20jcr:content/metadata/cq:tags%20jcr:content/metadata/dc:title
```
