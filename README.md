# Minimal OMERO client

[![Build Status](https://travis-ci.org/ome/minimal-omero-client.svg)](https://travis-ci.org/ome/minimal-omero-client)

Minimal Maven project for connecting to OMERO using the Java gateway based on
https://github.com/imagej/minimal-ij1-plugin. Thanks to @dscho and @ctrueden for the original example.

## Build

    ./gradlew build

Alternatively if you already have [Gradle](https://gradle.org/) installed:

    gradle build

## Install

    cd build/distributions
    unzip minimal-omero-client-5.5.x.zip

## Run

    ./minimal-omero-client-5.5.x/bin/minimal-omero-client --omero.host=localhost --omero.user=USERNAME --omero.pass=PASSWORD

You can pass additional properties, e.g. to debug SSL issues pass `--IceSSL.Trace.Security=1`.

# Using development CI libraries

You can build against a development version of a library from the OME CI systems

Make the following change to `build.gradle`, changing `version` to the CI version:
```diff
diff --git a/build.gradle b/build.gradle
index f832e8e..206cdd1 100644
--- a/build.gradle
+++ b/build.gradle
@@ -11,6 +11,9 @@ def javaOpts = [
 version '5.5.0'

 repositories {
+    maven {
+        name 'latestci'
+        url 'https://latest-ci.openmicroscopy.org/nexus/repository/maven-internal/'}
     mavenLocal()
     mavenCentral()
     maven {
@@ -22,7 +25,7 @@ repositories {
 }

 dependencies {
-    compile(group: 'org.openmicroscopy', name: 'omero-gateway', version: '5.5.2')
+    compile(group: 'org.openmicroscopy', name: 'omero-gateway', version: '5.5.3-SNAPSHOT')
 }

 startScripts {
```

`gradle build` should pull in the new library.
