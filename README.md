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
  
 2) 
