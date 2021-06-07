AEM Docker ❤
========

Using docker containers for your AEM instance will make you smile. You will be able to run different version of AEM without any conflicts and with ease. There are number of benefits you sure already know.

If you are not using docker you will be doing something else that makes your do things you dont need to considering how far tech has come along.

To use docker download and install Docker Desktop for your OS [https://hub.docker.com/search?offering=community&type=edition](https://hub.docker.com/search?offering=community&type=edition)

One you have done that you can run docker containers on your machine with ease.  

When you have installed docker desktop please ensure you configure following items:
- Set docker to start when you login
- Set amount of memory to use to at least 6GB
- Set amount of CPU's you at least half available
- Update disk space to allow for at least 100GB of space

Everything else you can leave as defaults.

## Running AEM Author using Docker Container with Debugging Enabled

If you would like to start and run new instance of AEM using Docker use the following command:

```bash
docker run --name author \
-e "TZ=Australia/Sydney" \
-e "AEM_JVM_OPTS=-server -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=58242 -Xms1024m -Xmx1024m -XX:MaxDirectMemorySize=256M -XX:+CMSClassUnloadingEnabled -Djava.awt.headless=true -Dorg.apache.felix.http.host=0.0.0.0" \
-p4502:8080 \
-p30303:58242 -d \
-v ~/aemdesign-docker/author/crx-quickstart/repository:/aem/crx-quickstart/repository \
-v ~/aemdesign-docker/author/crx-quickstart/logs:/aem/crx-quickstart/logs \
aemdesign/aem:6.5.0
```

This will start a new instance and will mount internal repository content in a subfolder ```~/aemdesign-docker/author``` of your home directory. 

## Access Author Container logs

If you have configured your logging to output all logs to console you can see all logs using the docker logs command

```bash
docker logs -tf author --since=2019-01-01
``` 

Using since will ensure that you only see logs from specific time

## Accessing Author to play around inside the container

If you find your self wanting to checkout internal container setup you can get bash access using following command

```bash
docker exec -it author bash
```



## Running AEM Publish using Docker Container with Debugging Enabled

```bash
docker run --name aem64-publish \
-e "TZ=Australia/Sydney" \
-e "AEM_JVM_OPTS=-server -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=58242 -Xms1024m -Xmx1024m -XX:MaxDirectMemorySize=256M -XX:+CMSClassUnloadingEnabled -Djava.awt.headless=true -Dorg.apache.felix.http.host=0.0.0.0" \
-e "AEM_RUNMODE=-Dsling.run.modes=publish,crx3,crx3tar,nosamplecontent" \
-p4503:8080 \
-p30304:58242 -d \
-v ~/aemdesign-docker/publish/crx-quickstart/repository:/aem/crx-quickstart/repository \
-v ~/aemdesign-docker/publish/crx-quickstart/logs:/aem/crx-quickstart/logs \
aemdesign/aem:6.5.0
```

## Start AEM 6.4.8.4

This container will run until stopped and will restart when ever you reboot your pc, this is done using `--restart unless-stopped` setting.

```bash
docker run --name author6484 -e "TZ=Australia/Sydney" -e "AEM_RUNMODE=-Dsling.run.modes=author,crx3,crx3tar,forms,localdev" -e "AEM_JVM_OPTS=-server -Xms248m -Xmx2524m -XX:MaxDirectMemorySize=256M -XX:+CMSClassUnloadingEnabled -Djava.awt.headless=true -Dorg.apache.felix.http.host=0.0.0.0 -Xdebug -Xrunjdwp:transport=dt_socket,server=y,address=58242,suspend=n" -p4502:8080 -p30303:58242 --restart unless-stopped -d aemdesign/aem:6.4.8.4
```

:heart: :heart: :heart: