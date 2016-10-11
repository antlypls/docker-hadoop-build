docker-hadoop-build
===================

> This is a fork of https://github.com/sequenceiq/docker-hadoop-build repository

## Build Apache Hadoop
Often when we use Apache Hadoop and would like to make a custom build (stock or forked) you'll have to
rebuild the whole Hadoop, native libs, etc ... which takes 30+ minutes, and carries lots of dependencies
(libraries, protobuf, etc - at a given version).

This Docker image contains the build process of Hadoop 2.7.3 nativelibs.

## Build the image
```
docker build -t antlypls/hadoop-nativelibs .
```

## Release libs to bintray

Steps needed:
- Copy the tarred libs from docker container
- Create a new version on bintray
- Upload the tarred libs to bintray

```
docker run --rm  antlypls/hadoop-nativelibs > hadoop-native-64-2.7.3.tar
curl -Lo /tmp/bintray-functions j.mp/bintray-functions && . /tmp/bintray-functions
bint-upload-with-version antlypls antlypls-bin hadoop-native-64bit 2.7.3 hadoop-native-64-2.7.3.tar
```
*Note: you will need to set your `BINTRAY_KEY` and `BINTRAY_USER` as environment variables*

## TODO

create a Makefile to fully automate the release
