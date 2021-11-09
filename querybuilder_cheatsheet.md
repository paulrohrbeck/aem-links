Query Builder Cheat Sheet
=========


### Query Builder API
* [6.1](https://docs.adobe.com/docs/en/aem/6-1/develop/search/querybuilder-api.html)
* [5.6.1](https://docs.adobe.com/docs/en/cq/5-6-1/dam/customizing_and_extendingcq5dam/query_builder.html)

### References
* [CQ Queries Demystified](http://itgumby.github.io/blog/2014/10/cq-queries-demystified/)
* [Tuning your JCR Queries for the AEM & Jackrabbit OAK](http://tech.ethomasjoseph.com/2015/03/tuning-your-jcr-queries-for-aem.html)
* [AEM Query Builder : Comprehensive Guide](http://www.aemcq5tutorials.com/tutorials/adobe-aem-cq5-tutorials/aem-query-builder/)
* [Tuning your JCR Queries for the AEM & Jackrabbit OAK](https://ethomasjoseph.com/developerhub/blog/2015/03/tuning-your-jcr-queries-for-aem.html)
* [Hashim Khan - Query Builder](https://hashimkhan.in/aem-adobecq5-code-templates/query-builder/)
* [JCR Score - Similarity](http://lucene.apache.org/core/3_0_3/api/core/org/apache/lucene/search/Similarity.html)
* [Lucene Scoring](http://www.lucenetutorial.com/advanced-topics/scoring.html)
* [Sample Filtering Predicate Evaluator](https://github.com/Adobe-Consulting-Services/acs-aem-samples/blob/master/bundle/src/main/java/com/adobe/acs/samples/search/querybuilder/impl/SampleFilteringPredicateEvaluator.java)
* [CQ5 Querybuilder simplified](http://aemcq5.blogspot.com/2014/11/cq5-querybuilder-simplified.html)

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
* [Query Builder API](https://helpx.adobe.com/au/experience-manager/6-4/sites/developing/using/querybuilder-api.html)

### Query Builder Samples
* [Operation Exists](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fcq%3Atoolbars%0D%0Aproperty.operation%3Dexists%0D%0A)
* [Operation Like](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dlike%0D%0Aproperty.value%3D%25ac%25)
* [Operation Equals](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dequals%0D%0Aproperty.value%3DContact)
* [Operation UnEquals](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dunequals%0D%0Aproperty.value%3DContact)
* [Operation Not Exist](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fcq%3Atoolbars%0D%0Aproperty.operation%3Dnot)
* [Special Character Search](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dnt%3Aunstructured%0D%0Aproperty%3Dtext%0D%0Aproperty.operation%3Dlike%0D%0Aproperty.value%3D%25%3Cli%3EThe+whole+is+greater+than+the+part.%3C%2Fli%3E%25)

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

Full list can be found in the [console](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


### Query Syntax

Following is the list of all available keywords that can be used in a a query

| Keyword                       | Description                                                                           |
|-------------------------------|---------------------------------------------------------------------------------------|
| path                          | This is used to search under a  particular hierarchy only. |
| path.self=true                | If true searches the subtree including the main node given in path,  if false searches the subtree only. |
| path.exact=true               | If true exact path is matched, if false all descendants are included. |
| path.flat=true                | If true searches only the direct children . |
| type                          | It is used for searching for a  particular nodetype only. |
| property                      | This is used to search for a specific property only. |
| property.value                | the property value to search . Mutilple values of a particular property could be given using ```property.N_value=X```, where N is number from 1 to N. |
| property.depth                | The number of additional levels to search under a node. eg. if property.depth=2 then the property is searched under <br>```(@jcr:title = 'foo' or */@jcr:title = 'foo' or */*/@jcr:title = 'foo' )``` |
| property.and                  |  If multiple properties are present , by default an OR operator is applied. If you want an AND ,  you may use property.and=true |
| property.operation            | “equals” for exact match (default), “unequals” for unequality comparison, “like” for using the jcr:like xpath function , “not” for no match , (value param will be ignored) or “exists” for existence match .(value can be true – property must exist). [Example](#check-if-property-exist-in-sub-node) |
| property.operation=exists     | check if property exists |
| property.operation=not        | check if property does not exists |
| property.operation=like       | check if property is like value |
| property.operation=equals     | check if property is equals value |
| property.operation=unequals   | check if property is does not equal value |
| property.operation=equalsIgnoreCase   | check if property equals ignoring case |
| property.operation=unequalsIgnoreCase   | check if property not equals ignoring case |
| fulltext                      | It is used to search terms for fulltext search |
| fulltext.relPath              | the relative path to search in (eg. property or subnode) eg. ```fulltext.relPath=jcr:content``` or ```fulltext.relPath=jcr:content/@cq:tags``` |
| daterange                     | This predicate is used to search a date property range. |
| daterange.property            | Specify a property which is searched. |
| daterange.lowerBound          |  Fix a lower bound eg. 2010-07-25 |
| daterange.lowerOperation      | “>” (default) or “>=” |
| daterange.upperBound          | Fix a lower bound eg. 2013-07-26 |
| daterange.upperOperation      | “<” (default) or “<=” |
| relativedaterange             | It is an extension of daterange which uses relative offsets to server time. It also supports 1s 2m 3h 4d 5w 6M 7y |
| relativedaterange.lowerBound  | Lower bound offset, default=0 |
| relativedaterange.upperBound  | Upper bound Offset . |
| nodename                      | This is used to search exact nodenames for the result set. It allows few wildcards like: ```nodename=text```, will search for any character or no character after text. ```nodename=text?``` will search for any character after text. |
| tagid                         | This predicate is used to search for a particular tag on a page. You may specify the exact tagid of a tag in this predicate |
| tagid.property                | this may be used to specify the path of node where tags are stored. |
| group                         | This predicate is used to create logical conditions in your query. You can create complex conditions using OR & AND operators in different groups.  [Example 1](#group-usage-1) [Example 2](#group-usage-2) |
| group.p.or=true               | treat group options as OR |
| group.p.and=true              | treat group options as AND |
| group.fulltext                | search group using full text |
| orderBy                       | This predicate is used to sort the result sets obtained in the query. e.g. ```orderby=@jcr:score``` or ```orderby=@jcr:content/cq:lastModified``` [Multiple ordering](#multiple-ordering) |
| orderby.sort                  | You may define the sorting way for the search results e.g.  desc for descending and “” for ascending. ```orderby.desc=true```  or ```orderby.sort=desc``` for descending and ```orderby.asc=true``` or ```orderby.sort=asc``` for ascending |
| orderby.desc=true             | sort descending |
| orderby.asc=true              | sort ascending |
| orderby.case=ignore           | support case insensitive |
| orderby=custompredicate       | order using custom predicate, try [Available Predicates](#available-predicates) |
| orderby=path                  | order by path predicate |
| p.hits=full                   | Use this when you want to return all the properties in a node. |
| p.hits=selective              | Use this if you want to return selective properties in search result. |
| p.properties                  | jcr:primaryType Example |
| p.nodedepth                   | Use this when you need properties of a node and its child nodes in the same search result. Use this with ```p.hits=full``` |
| p.facets=true                 | This will be used to Search Facets based search for the assigned Query. If you want to calculate the count of tags which are present in your search result or you want to know how many templates for a particular page are there etc, you may go with Facets based search (Example)[#facets-results] |
| p.offset                      | defines start of index means from which index you want to fetch records from query result. |
| p.limit                       | defines page size. In simple words how many records you want to fetch. |
| p.guesstotal                  | The purpose of p.guessTotal parameter is to return the appropriate number of results that can be shown by combining the minimum viable p.offset and p.limit values. The advantage of using this parameter is improved performance with large result sets. This avoids calculating the full total (e.g calling result.getSize()) and reading the entire result set. (Example)[#guess-total] |
| p.excerpt=true                | return page full text excerpt |

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

Exclude certain paths while searching flat (avoid children) in a path

[http://localhost:4502/bin/querybuilder.json?1_property=%40jcr%3acontent%2fsling%3aresourceType&1_property.value=weretail%2fcomponents%2fstructure%2fpage&group.1_group.p.not=true&group.1_group.path=%2fcontent%2fwe-retail%2flanguage-masters%2fen%2fuser&group.1_group.path.self=true&group.2_group.p.not=true&group.2_group.path=%2fcontent%2fwe-retail%2flanguage-masters%2fen%2fabout-us&group.2_group.path.self=true&path=%2fcontent%2fwe-retail%2flanguage-masters%2fen&path.flat=true](http://localhost:4502/bin/querybuilder.json?1_property=%40jcr%3acontent%2fsling%3aresourceType&1_property.value=weretail%2fcomponents%2fstructure%2fpage&group.1_group.p.not=true&group.1_group.path=%2fcontent%2fwe-retail%2flanguage-masters%2fen%2fuser&group.1_group.path.self=true&group.2_group.p.not=true&group.2_group.path=%2fcontent%2fwe-retail%2flanguage-masters%2fen%2fabout-us&group.2_group.path.self=true&path=%2fcontent%2fwe-retail%2flanguage-masters%2fen&path.flat=true)

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


## Query Sample Fragments

```
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```
### Check property Like value

```
property=propertyName
property.operation=like
property.value=%value%
```

### Check if a property exists:

```
property=propertyName
property.operation=exists
property.value=true
```

### Date ranges:

```
daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

### Show pages that have been modified since they were last published

```
path=/content/geometrixx
property=cq:lastModifiedBy
property.value=reference-adjustment-service
dateComparison.property1=cq:lastModified
dateComparison.property2=cq:lastReplicated
dateComparison.operation=greater
```

### Grab all assets and return the path, title and tags

```
type=dam:Asset
path=/content/dam
p.limit=-1
p.hits=selective
p.properties=jcr:path%20jcr:content/metadata/cq:tags%20jcr:content/metadata/dc:title
```

### Check if property exist in sub node

```
path=/content/dam
nodename=metadata
1_property=tiff:ImageHeight
1_property.value=false
2_property=tiff:ImageWidth
2_property.value=false
1_property.operation=exists
2_property.operation=exists
property.and=true
```

### Multiple Predicates at the same time

```
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Group Usage 1

```
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en
group.2_path=/content/dam/geometrixx
```

Final Xpath query will be created as **(fulltext AND (path=… OR path=…))**

### Group Usage 2

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Final Xpath query will be created as **(fulltext AND ( (path= AND type=) OR (path= AND type=) ))**


### Multiple ordering

```
1_orderby=@cq:tags
2_orderby=@cq:lastModified
3_orderby=nodename
```

### Guess total

```
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby:path
```

### Check if property is not empty string

```
property.value=%_%
```

### Facets results

```
type=cq:Page
orderby=@jcr:score
orderby.sort=desc
1_property=jcr:content/cq:tags
2_property=jcr:content/cq:template
2_property.value=/apps/geometrixx/templates/contentpage
p.facets=true
```

# Facets


## Extract Facets for your search result

```java
Map<String, Facet> facets = result.getFacets();
for (String key : facets.keySet()) {
    Facet facet = facets.get(key);
    if (facet.getContainsHit()) {
        for (Bucket bucket : facet.getBuckets()) {
            long count = bucket.getCount();
            Map<String, String> params = bucket.getPredicate().getParameters();
            for (String k : params.keySet()) {
                out.println("<br>k:"+k);
            }
        }
    }
}
```


# Custom Predicates

Broadly there are 2 kinds of Predicate Evaluators which can be used to create new predicates as per Business need.


## XPath Predicate

This is used to create a Backend XPATH Query using the new custom predicates which can be defined as per need. Many of the inbuilt CQ predicates are XPATH predicates. Notice that in XPATH Predicate Evaluator the overriden method canXpath() should return true while canFilter() should return false.  Use the below code snippet to create Custom Predicates

```java

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

/**
* <code>OriginPredicateEvaluator</code>queries the Livecopy status of a page.

*This property is used to find the Livecopy status of the page.
*origin.value=disconnected gives the XPATH query as jcr:content/@jcr:mixinTypes='cq:LiveSyncCancelled'
*origin.value=locally gives the XPATH query as jcr:content/@jcr:mixinTypes!='cq:LiveSync'
*origin.value=inheritted gives the XPATH query as jcr:content/@jcr:mixinTypes='cq:LiveSync'
*/

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/origin")
public class OriginPredicateEvaluator extends AbstractPredicateEvaluator {
    static final String PE_NAME = "origin";
    static final String JCRCONTENT_JCRMIXIN = "jcr:content/@jcr:mixinTypes";

    static final String PREDICATE_VALUE = "value";
    static final String PREDICATE_LIVESYNCCANC = "'cq:LiveSyncCancelled'";
    static final String PREDICATE_LIVESYNC = "'cq:LiveSync'";

    static final String OP_EQUALS = "=";
    static final String OP_NOT_EQUALS = "!=";

    private static final Logger logger = LoggerFactory.getLogger(OriginPredicateEvaluator.class);

    @Override
    public String getXPathExpression(Predicate predicate, EvaluationContext context) {

        String value = predicate.get(PREDICATE_VALUE);

        StringBuilder sb = new StringBuilder();

        if(value != null){
            if (value.equalsIgnoreCase("inheritted")) {
                sb.append(JCRCONTENT_JCRMIXIN).append(OP_EQUALS);
                sb.append(PREDICATE_LIVESYNC);
            }
            if (value.equalsIgnoreCase("disconnected")) {
                sb.append(JCRCONTENT_JCRMIXIN).append(OP_EQUALS);
                sb.append(PREDICATE_LIVESYNCCANC);
            }
            if (value.equalsIgnoreCase("locally")) {
                sb.append(JCRCONTENT_JCRMIXIN).append(OP_NOT_EQUALS);
                sb.append(PREDICATE_LIVESYNC);
            }
        }

        String xpath = sb.toString();

        logger.debug("**********XPATH*******" + xpath);

        return xpath;
    }

    @Override
    public boolean canXpath(Predicate predicate, EvaluationContext context) {
        return true;
    }

    @Override
    public boolean canFilter(Predicate predicate, EvaluationContext context) {
        return false;
    }
}
```

## Filter Predicate

This predicate is used whenever you want to Filter out some results which are not needed in the end Search Result. Notice that in Filter Predicate Evaluator the overriden method canXpath() should return false while canFilter() should return true.

```java

import javax.jcr.query.Row;

import org.apache.felix.scr.annotations.Component;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.resource.collection.ResourceCollection;

import com.day.cq.search.Predicate;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/samplepredicate")
public class SampleFilterPredicateEvaluator extends AbstractPredicateEvaluator {
    public static final String SAMPLE = "samplepredicate";

    @Override
    public boolean includes(Predicate p, Row row, EvaluationContext context) {
        if (!p.hasNonEmptyValue(SAMPLE)) {
        return true;
        }
        /* Write some code logic here as per the condition:
        Return true for a favourable Condition for keeping the entity in Search Results.
        Return false for an unfavourable Condition for removing the entity from the Search Results.
        */

        return false;
    }
    @Override
    public boolean canXpath(Predicate predicate, EvaluationContext context) {
        return false;
    }

    @Override
    public boolean canFilter(Predicate predicate, EvaluationContext context) {
        return true;
    }

}

```
