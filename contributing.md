# How to contribute

## Setting up the working environment

In order to be able to contribute to the plugin you need to:

+ install java jdk. Version is java6 or java7 or java8.
+ checkout and build the IntelliJ IDEA Community source code. Version is idea/139.144
(so you can have access to the platform internals in debugging and understanding what goes wrong)
+ checkout out and build a recent version of [Google Go](http://golang.org). Version is go1.3
+ checkout and setup the plugin sources

### Checking out the IntellJ IDEA Platform sources.

We start with cloning the idea git repository and checking out the revision
used to build IDEA 14:

```bash
    git clone git@github.com:JetBrains/intellij-community.git idea
    cd idea
    git checkout idea/139.144
    # and we build it using ant
    ant
```

The build will take around 5 to 20 minutes (depending on the machine) and at the
end it should put the build artifacts into `out/artifacts` folder.

    $ ls -al out/artifacts/
    total 728672
    drwxr-xr-x   7 mtoader  staff        238 Jun  1 22:34 .
    drwxr-xr-x   8 mtoader  staff        272 Jun  1 22:25 ..
    drwxr-xr-x  10 mtoader  staff        340 Jun  1 22:34 core
    -rw-r--r--   1 mtoader  staff  112106975 Jun  1 22:34 ideaIC-139.SNAPSHOT.mac.zip
    -rw-r--r--   1 mtoader  staff  110192607 Jun  1 22:34 ideaIC-139.SNAPSHOT.tar.gz
    -rw-r--r--   1 mtoader  staff  110468031 Jun  1 22:34 ideaIC-139.SNAPSHOT.win.zip
    -rw-r--r--   1 mtoader  staff   40308058 Jun  1 22:34 sources.zip

Use the artifact from your target OS to run the built version of IDEA.

### Checking out and building Google Go 1.3

While we support Go from 1.0 to 1.3.3, we prefer to work with the latest release
installed from sources by following the page source installation page from here:
<http://golang.org/doc/install/source>.

This will work even with a binary installation (as a result of following the
<http://golang.org/doc/install> page).

### Checking out the plugin sources

If you are on the contributors list:

    git clone git@github.com:go-lang-plugin-org/go-lang-idea-plugin.git

If you are not then fork the repository using the github web interface and do a
clone of your fork on the local machine.

### Building and running the unit tests

In order to build the sources you need to download an IDEA Community version,
open the project and add the built IDEA artifact as a Idea SDK for the plugin.
It's also helpful to add the idea sources to the IDEA SDK as it helps
tremendously with debugging.

The steps:

* Download the IDEA Community (or you can use your licensed IDEA Ultimate copy)
from here: <http://www.jetbrains.com/idea/>.
* Open the copy of google-go-lang-idea-plugin repository (that was previously
checked out) with it (the default project module config should work with a
recent IDEA 14 version).
* Open the Project Settings (Command + ; on Mac or File -> Project Settings on
other platforms), go to the SDKs entry, click the `+` (and select IntelliJ IDEA
Plugin SDK). 
* If it says you need a Java SDK first. You should add a java SDK with the same
version that you used for build idea. If you use mac,you should check follow path:
```
/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/
/Library/Java/JavaVirtualMachines/jdk1.8.0_25.jdk/Contents/
```
* After setup java SDK. go to the SDKs entry, click the `+` (and select IntelliJ IDEA
Plugin SDK) navigate to the unzipped location of the IDEA build that you
created before. It will recognize a new IDEA Plugin SDK with the name
`IDEA IC-139.SNAPSHOT`. After that you should add the IDEA sources to it by
selecting the SDK, going to the `Sourcepath` tab, clicking `+` in the lower
panel and navigating to the checkout out sources of IDEA. Press add, let it
inspect the folders for sources and add all the found sources to the SDK.
* Go to the Project entry and make sure that the Project SDK is set to selected
SDK.
* Wait until the source files of the SDK are indexed.

Now you can use the run configurations provided by the plugin source code to
run and play:

+ `Execute Slave IDEA with plugin` will spawn a new IDEA with the latest version
of the plugin enabled.
+ `ro.redeul.google.go in google-go-language` will run all the test cases available
in the project. Please make sure that all the test cases pass before committing anything
 (or making a pull request).

### Profit

Now you can play, add functionality and commit or make pull requests.
That's it. Enjoy your play time.


### Notice on run test cases
* If you see a lot of java.io.FileNotFoundException when run test cases and those test cases
are passed in Travis CI, you may need to try [#923](https://github.com/go-lang-plugin-org/go-lang-idea-plugin/issues/923). Please look at the location: /Users/xxx/Library/Caches/IntelliJIdea14/plugins-sandbox/test and remove the test folder from there. This usually happens when you change the directory structure in one of the tests. The testing idea will not update it's caches properly.
