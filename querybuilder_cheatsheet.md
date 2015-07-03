Query Builder Queries 
=========

### References
* [CQ Queries Demystified](http://itgumby.github.io/blog/2014/10/cq-queries-demystified/)
* [Tuning your JCR Queries for the AEM & Jackrabbit OAK](http://tech.ethomasjoseph.com/2015/03/tuning-your-jcr-queries-for-aem.html)

### Documentation
* [JCR 2.0 Spec - Query](http://www.day.com/specs/jcr/2.0/6_Query.html)
* [Predicate](http://docs.adobe.com/docs/en/cq/5-6-1/javadoc/com/day/cq/search/Predicate.html)
* [PredicateEvaluator](http://docs.adobe.com/docs/en/cq/5-6-1/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)
* [JcrPropertyPredicateEvaluator](http://docs.adobe.com/docs/en/cq/5-6-1/javadoc/com/day/cq/search/eval/JcrPropertyPredicateEvaluator.html)

### Query Builder
* [5.6.1](https://docs.adobe.com/docs/en/cq/5-6-1/dam/customizing_and_extendingcq5dam/query_builder.html)
* [6.1](https://docs.adobe.com/docs/en/aem/6-1/develop/search/querybuilder-api.html)


### Query Builder Samples
* [Operation Exists](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fcq%3Atoolbars%0D%0Aproperty.operation%3Dexists%0D%0A)
* [Operation Like](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dlike%0D%0Aproperty.value%3D%25ac%25)
* [Operation Equals](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dequals%0D%0Aproperty.value%3DContact)
* [Operation UnEquals](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fjcr%3Atitle%0D%0Aproperty.operation%3Dunequals%0D%0Aproperty.value%3DContact)
* [Operation Not Exist](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dcq%3APage%0D%0Aproperty%3Djcr%3Acontent%2Fcq%3Atoolbars%0D%0Aproperty.operation%3Dnot)

* [Special Character Search](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=path%3D%2Fcontent%2Fgeometrixx%0D%0Atype%3Dnt%3Aunstructured%0D%0Aproperty%3Dtext%0D%0Aproperty.operation%3Dlike%0D%0Aproperty.value%3D%25%3Cli%3EThe+whole+is+greater+than+the+part.%3C%2Fli%3E%25)