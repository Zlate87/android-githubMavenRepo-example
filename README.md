# Android example for using github repo as maven repo
This is a an example to illustrate how one can setup a maven repository using github (poor man's maven repo) and use it for Android projects. To do so the [wagon-git](https://github.com/synergian/wagon-git) plugin is used. This example contains:
* One maven repo for releases.
* One maven repo for snapshots.
* An Android library that can deploy it's aar artifact to the maven repo.
* An Android application that has dependency to the libraries aar and gets it from the maven repo.

To deploy to the maven repo use the following command from the library:

```
./gradlew clean build uploadArchives
```

##Notes
Some things worth mentioning are:
* The repos are just a standard git branches. There is no need to create them manually, the wagon-git plugin will create them automatically once there is something to deploy.
* If the version name do not end with -SNAPHOT it will go to the [releases](https://github.com/Zlate87/android-githubMavenRepo-example/tree/releases) repo, if it ends with -SNAPSHOT it will go into the [snapshots](https://github.com/Zlate87/android-githubMavenRepo-example/tree/snapshots) repo.
* Once you deploy a release version, if you try to deploy it again, the old version will **not** be overridden.
* When you deploy a snapshot version, it also gets timestamp at the end, so you can have multiple artifacts from the same version.
* It is OK (and I would say better) to have a separate git repositories for the maven repos, library, application. For this example I choose to have one, just for simplicity.
   
##Troubleshooting
If you get an error like this:
```
The authenticity of host 'github.com (192.30.253.113)' can't be established.
```
The plugin that is doing the deployment need an SSH key to work, and you probably do not have one setup properly on the machine from which you are trying to deploy. For more information on how to do this, go [here](https://help.github.com/articles/generating-an-ssh-key/).

##Credits
http://jeroenmols.com/blog/2016/02/05/wagongit/

