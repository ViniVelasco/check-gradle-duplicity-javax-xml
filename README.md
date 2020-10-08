As many other questions and answers related this topic suggests, the error is related to a duplicity with java.xml import. By default, on Java 11, java.xml is part of the JDK libraries, and is added in the modulepath.

Check the dependencies of your graddle, at least one of then is also adding a transitive dependence to java.xml but in the classpath (unnamed module),thus it is present twice.

Locate the dependency that is adding it, and try adding something similar to this on you gradle (in my case the duplicity was due to Apache Tika library):

compile ('org.apache.tika:tika-parsers:1.22') {
    exclude (group: 'xml-apis')
}
