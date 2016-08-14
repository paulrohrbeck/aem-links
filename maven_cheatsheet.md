Maven Cheat Sheet
=========
### Common commands

* `mvn clean package` - check if maven is able to build package
* `mvn clean install -PautoInstallPackage` - install package to defined AEM instance

### Init new project

```
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.2 -DarchetypeRepository=adobe-public-releases
```

### Maven settings
Add to `~/.m2/settings.xml`:

```xml
 <profiles>
    <profile>
      <id>adobe-public</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>        
        <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
        <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
        <releaseRepository-URL>http://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
      </properties>
      <repositories>
        <repository>
          <id>adobe-public-releases</id>
          <name>Adobe Basel Public Repository</name>
          <url>http://repo.adobe.com/nexus/content/groups/public</url>
          <releases>
            <enabled>true</enabled>
            <updatePolicy>never</updatePolicy>
          </releases>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>adobe-public-releases</id>
          <name>Adobe Basel Public Repository</name>
          <url>http://repo.adobe.com/nexus/content/groups/public</url>
          <releases>
            <enabled>true</enabled>
            <updatePolicy>never</updatePolicy>
          </releases>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
        </pluginRepository>
      </pluginRepositories>
    </profile>
  </profiles>
  <activeProfiles>
    <activeProfile>adobe-public</activeProfile>
  </activeProfiles>
```  
