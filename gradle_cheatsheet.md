Gradle Cheat Sheet
=========

### Links

* [Gradle AEM Plugin](https://github.com/Cognifide/gradle-aem-plugin) (documentation)
* [Gradle AEM Multi](https://github.com/Cognifide/gradle-aem-multi) (multi-module project archetype)
* [Gradle AEM Single](https://github.com/Cognifide/gradle-aem-single) (single-module project archetype)

### Common commands

* `sh gradlew :build` - check if Gradle is able to build package
* `sh gradlew :aemDeploy` - install package to defined AEM instance(s)

### Init new project

Multi-module:

```bash
git clone git@github.com:Cognifide/gradle-aem-multi.git && cd gradle-aem-multi && gradlew fork
```

Single-module:

```bash
git clone git@github.com:Cognifide/gradle-aem-single.git && cd gradle-aem-single && gradlew fork
```

### Project setup

To create user-specific settings file, enter forked project directory and run command:

```bash
sh gradlew props
```

To create local development environment run command:

```bash
sh gradlew aemSetup
```