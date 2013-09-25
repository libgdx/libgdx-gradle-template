libgdx-gradle-template
======================

Gradle template for libgdx projects that works on the CLI, Eclipse and Intellij IDEA. This tempate will eventually
replace the libgdx Setup-UI currently in use. To get started **[Download the template](https://github.com/libgdx/libgdx-gradle-template/archive/master.zip)**
or fork and clone this repository.

### A word about Gradle
[Gradle](http://www.gradle.org/) is a nifty build and dependency managment system. A build system allows you to easily
compile and package (potentially different versions of) your project. A dependency management system allows
you to declaratively specify 3rd party libraries, which the dependency management system will
pull in automatically for you. No need to put Jar files or native libraries in your project tree.

You do not need to install Gradle manually, this template uses the [Gradle wrapper](http://www.gradle.org/docs/current/userguide/gradle_wrapper.html)
which takes care of that for you transparently. The first time you invoke gradle on the command line,
the Gradle wrapper will automatically download and install Gradle into your home directory.

To use this template you do not need to know Gradle necessarily, pretty much everything is taken 
care of for you.

### A word about Source Control
The contents of this repository are everything you need to commit to your source control repository.
Do not commit Eclipse or IntelliJ Idea projec files, especially if other people are working on the
same project. Instead, everyone just downloads this IDE-unaware project, then uses Gradle to generate
local IDE project files.

Also make sure to commit the gradlew, gradlew.bat files and the gradle/ folder. This way, nobody needs
to manually install Gradle on their system.

### Project Structure
This template has the following structure (ignoring some directores and files in the Android project for brevity).

    build.gradle                 <- main Gradle build file, add dependencies here
    settings.gradle              <- definition of the sub-modules for core, desktop, Android
    
    core/                        <- Core project
       build.gradle              <- Gradle build file for core project, no need to touch this
       src/                      <- All your game's source code goes here!
       
    desktop/                     <- Desktop project
       build.gradle              <- Gradle build file for desktop project, no need to touch this
       src/                      <- the desktop project's source code, contains launcher class
       
    android/                     <- Android project
       AndroidManifest.xml       <- Android specific configuration
       build.gradle              <- Gradle build file for Android project, DON'T EVER TOUCH THIS!
       assets/                   <- contains all your graphics, audio, etc. files, shared with desktop
       res/                      <- contains icons of your app and other resources
       src/                      <- the Android project's source code, contains launcher class

### Command Line Usage
Before you can do anything, you need to set the ANDROID_HOME environment variable to point
to your Android SDK's root folder. On Windows you can do this on the command line

    set ANDROID_HOME=C:/Path/To/Your/Android/Sdk
    
On Linux and Mac OS X you can do this in the shell

    export ANDROID_HOME=/Path/To/Your/Android/Sdk
    
Both commands will set the ANDROID_HOME enviroment variable for the duration of your shell session. You 
should set this environment variable permanently on your system. Please consult the internet for instructions.

Once you have ANDROID_HOME set, you can continue with using Gradle. On windows, you use 
the gradlew.bat files, which you can invoke like this:

    gradlew clean
    
On Linux or Mac OS X you invoke gradle like this:

    ./gradlew clean
    
Note the leading dot slash on Unix like systems. In both cases, the clean task will remove all 
build files, e.g. class files previously generated.

#### Running the desktop project
To run the desktop project issue this gradle command:

    ./gradlew desktop:run
    
#### Packaging the desktop project
To create a ZIP distribution including shell scripts to start your app, issue this gradle command:

    ./gradlew desktop:distZip
    
This will create a ZIP file in the folder desktop/build/distributions, ready to be send to testers.
    
#### Running the Android project
To run the Android project, issues this gradle command:

    ./gradlew android:installDebug
   
This will compile the APK for Android, and install it on a connected device. You will have to
start the app manually on the device.

#### Packaging the Android project
The android:installDebug task will create an unsigned debug APK of your app, which you can find
in the android/build/apk/ folder. If you want to build a signed APK for release on the Google 
Play Store, please consult the [Android Gradle plugin documentation](http://tools.android.com/tech-docs/new-build-system/user-guide)

### Eclipse Usage
You can let Gradle generate Eclipse projects for your application easily:

    ./gradlew eclipse
    
Once Gradle is done, **delete the .project file in the root directory of the project**. This is a 
little glitch that will get resolved shorty.

Now you can import the projects into Eclipse

  1. File -> Import ... -> General -> Existing projects into Workspace
  2. Click 'Browse', select the root folder of the project. You should see the core, android and desktop project.
  3. Make sure the three projects are checked, then click 'OK'

#### Running/Debugging in Eclipse
To run/debug the desktop project: 
  1. Right click the desktop project in the package viewer
  2. Select either 'Run As' or 'Debug As'
  3. Select 'Java Application'
  
To run/debug the Android project:
  1. Right click the Android project in the package viewer
  2. Select either 'Run As' or 'Debug As'
  3. Select 'Android Application'
  
### Intellij Idea Usage
You can let Gradle generate Intellij Idea project for your application easily:

    ./gradlew idea
    
Once Gradle is done, you can open the projects in Intellij Idea:

  1. File -> Open
  2. Select the .ipr file in the root of the project, Click 'OK'
  
You'll need to set the Android SDK on the Android module before continuing:

  1. File -> Project Structure ...
  2. Select 'modules' in the left side panel
  3. Select the 'android' module in the modules panel
  4. Set 'Module SDK' to the Android SDK you configured for IntelliJ Idea
  
#### Running/Debugging in Intellij Idea
To run/debug the desktop project, first create a run configuration:

  1. Run -> Edit Configurations
  2. Click the plus ('+') in the top left corner, select 'Application'
  3. Set the Name of the configuration, e.g. 'Desktop'
  4. Set the Main Class to 'DesktopLauncher', by clicking on the button on the left of the field
  5. Set the Working Directory to $root/android/assets, by clicking on the button on the left of the field
  6. Set 'Use classpath of module' to 'desktop'
  7. Click 'OK'
  
To run/debug the desktop project, just select the run configuration you just created
and then either click the green play button, or the green play button with the bug.

To run/debug the Android project, first create a run configuration:

  1. Run -> Edit Configurations
  2. Click the plus ('+') in the top left corner, select 'Android Application'
  3. Set the Name of the configuration, e.g. 'Android'
  4. Set 'Module' to 'Android'
  7. Click 'OK'
  
To run/debug the desktop project, just select the run configuration you just created
and then either click the green play button, or the green play button with the bug.

### Dependency Management
One of the benefits of Gradle and similar systems like Maven or Ivy, is that integrating
third party dependencies in your project is really simple. It also has the benfit that
your project file tree doesn't contain any JAR files or other 3rd party resources, keeping
things clean and tidy. Every time your or a team mate invoke a Gradle task, the 
dependencies of your project will get checked and updated if necessary.

How and where do you specify dependencies?

TBD see build.gradle in root for now
