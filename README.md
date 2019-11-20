
## sbt-optimize-prod-with-build-env-plugin-example

A working example of using a sbt [AutoPlugin](https://www.scala-sbt.org/1.x/docs/Plugins.html) ([scaladoc](https://www.scala-sbt.org/1.x/api/sbt/AutoPlugin.html)) to provide a build environment to run the Scala compiler's optimizer only for a production build.

See [BuildEnvPlugin.scala](https://github.com/ryanberckmans/sbt-optimize-prod-with-build-env-plugin-example/blob/master/project/BuildEnvPlugin.scala) and the [usage](https://github.com/ryanberckmans/sbt-optimize-prod-with-build-env-plugin-example/blob/master/build.sbt#L24) of `buildEnv` in build.sbt.

### Running it

```
$ sbt run
```

👉 output of `sbt run` includes "[info] Running in build environment: **Development**".

### Running a production build

```
$ ENV=production sbt run
# or
$ sbt -Denv=production run
```

👉 output of `ENV=production sbt run` includes "[info] Running in build environment: **Production**".

## Potential alternative to the plugin approach in this repo

sbt-native-packager [suggests](https://www.scala-sbt.org/sbt-native-packager/recipes/package_configuration.html#sbt-sub-modules) using sbt submodules for staging and production builds. However in their example the staging and production builds depend on the same app build. They add configuration based on staging/production but the app build is unmodified. The example in this repo modifies the app build to include scalac optimizer options for a production build.

## Troubleshooting

* in my personal use of this plugin I found it necessary to include `scalaVersion := "2.12.10"` in my `project/plugins.sbt` so that the build of BuildEnvPlugin.scala was compatible with other plugins used via `addSbtPlugin(...)` in `project/plugins.sbt`.
