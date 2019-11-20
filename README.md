
## sbt-optimize-prod-with-build-env-plugin-example

A working example of using a sbt [AutoPlugin](https://www.scala-sbt.org/1.x/docs/Plugins.html) ([doc](https://www.scala-sbt.org/1.x/api/sbt/AutoPlugin.html)) to provide a build environment to run the Scala compiler's optimizer only for a production build.

TODO link to key source files

### Running it

```
$ sbt run
```

👉 output of `sbt run` includes "[info] Running in build environment: *Development*".

### Running a production build

```
$ ENV=production sbt run
# or
$ sbt -Denv=production run
```

👉 output of `ENV=production sbt run` includes "[info] Running in build environment: *Production*".

## Potential alternative to the plugin approach in this repo

sbt-native-packager [suggests](https://www.scala-sbt.org/sbt-native-packager/recipes/package_configuration.html#sbt-sub-modules) using sbt submodules for staging and production builds. However in their example the staging and production builds depend on the same app build. They add configuration based on staging/production but the app build is unmodified. The example in this repo modifies the app build to include scalac optimizer options for a production build.
