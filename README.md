# MavenUpload
Maven and Bintray upload plugin for Gradle allows you to upload your modules at remote repositories.

**Usage**

1) Add this lines to your project root (not module!) `build.gradle` file to the `dependencies` section:

		classpath 'com.android.tools.build:gradle:3.2.1'
		classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.1'
		classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1'

Your final `build.gradle` file should look something like this:
  
	buildscript {
		
		repositories {
			
			google ()
			jcenter ()
			
		}
		
		dependencies {
			
			classpath 'com.android.tools.build:gradle:3.2.1'
			classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.1'
			classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1'
			
		}
		
	}
	
	allprojects {
		
		repositories {
			
			google ()
			jcenter ()
			
		}
		
	}
	
	task clean (type: Delete) {
		delete rootProject.buildDir
	}
	
	subprojects {
		
		tasks.withType (Javadoc).all {
			enabled = false
		}
		
	}
  
  
 2) Add this lines to your module `build.gradle` file **after** `android` section (if it's Android module):
 
 		apply from: 'https://raw.githubusercontent.com/acuna-public/MavenUpload/master/bintray.gradle'
		apply from: 'https://raw.githubusercontent.com/acuna-public/MavenUpload/master/publish.gradle'
		
So final `build.gradle` should look like this:

    apply plugin: 'com.android.library'
    
    android {
      
      compileSdkVersion 27
      
      defaultConfig {
        // ...
      }
      
      buildTypes {
        // ...
      }
      
    }
    
    apply from: 'https://raw.githubusercontent.com/acuna-public/MavenUpload/master/bintray.gradle'
    apply from: 'https://raw.githubusercontent.com/acuna-public/MavenUpload/master/publish.gradle'
    
    dependencies {
      // ...
    }

3) Add and edit this lines at your project `gradle.properties` file:

		libraryName = MyLibrary
		versionName = 1.0
		libraryDescription = MyLibrary is the greatest library in the world
		siteUrl = https://github.com/vasyapupkin/MyLibrary
		gitUrl = https://github.com/vasyapupkin/MyLibrary.git
		issuesUrl = https://github.com/vasyapupkin/MyLibrary/issues
		publishedGroupId = com.yoursite
		artifactId = mylibrary
		bintrayRepo = BintrayRepoName
		developerId = vasyapupkin
		developerName = Vasya Pupkin
		developerEmail = vasya@pupkin.com
		licenseName = General Public License, Version 3.0
		licenseUrl = https://www.gnu.org/licenses/gpl-3.0.txt
		libraryLicenses = GPL-3.0
		publicDownloadNumbers = false
		
3.1) You can change your module `versionName` in `defaultConfig` section of your module `build.gradle` file to `project.property ('versionName')` as follows to get it from `gradle.properties` automatically:

    defaultConfig {
      
      minSdkVersion 14
      versionName project.property ('versionName')
      
    }
   
	4) 
