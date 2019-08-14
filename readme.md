

# react native firebase crashlytics



### Manual installation


##### iOS

1. Set up Crashlytics in the Firebase console.
- Click Crashlytics in the left-hand nav panel of the Firebase console.
- If your Firebase project has multiple apps registered in it, select the app you just added from the dropdown next to Crashlytics in the top bar of the console.
- Click Set up Crashlytics.
- Select This app is new to Crashlytics (it doesn't have any version of the SDK).

2. In iOS, in the project install pods  
(1) pod 'Firebase/Analytics’  (2) pod 'Crashlytics', '~> 3.13.2' 

3. Initialize Crashlytics
 - Open your project in Xcode, then select its project file in the Navigator.
 -  Select your main build target from the Select a project or target dropdown.
 - Open the target's Build Phases tab.
 - Click + Add a new build phase, then select New Run Script Phase.
 - Add "${PODS_ROOT}/Fabric/run" line to the Type a script text box:
 - Xcode 10 only: Add your app's built Info.plist location to the Build Phase's Input Files field: 
   Add this line $(SRCROOT)/$(BUILT_PRODUCTS_DIR)/$(INFOPLIST_PATH)
 - After you add the SDK to your app, Crashlytics automatically gets to work listening for and collecting crash reports.
4. Open edit scheme Go to Run -> Arguments -> Arguments Passed On Launch add this line FIRDebugEnabled.
5. Build the project and run.
6. For check force crash in iOS write below code in app delegate.m file
  -   #import <Fabric/Fabric.h>
	 #import <Crashlytics/Crashlytics.h>
	 @import Firebase;
 - Add [[Crashlytics sharedInstance] crash]; in didFinishLaunchingWithOptions method.
7. Open firebasebase console crashlytics option dashboard and show crash logs.



##### Android

1. Set up Crashlytics in the Firebase console

- Click Crashlytics in the left-hand nav panel of the Firebase console.
- If your Firebase project has multiple apps registered in it, select the app you just added from the dropdown next to Crashlytics in the top bar of the console.
- Click Set up Crashlytics.
- Select This app is new to Crashlytics (it doesn't have any version of the SDK).

2. Add the Crashlytics SDK
- In your project-level build.gradle, update your google-services to version 3.1.2 or later, then add the Crashlytics repositories and dependency:

buildscript {
    repositories {
        // Add the following repositories:
        google()  // Google's Maven repository

        maven {
           url 'https://maven.fabric.io/public'
        }
    }

    dependencies {
        // ...
        // Check for v3.1.2 or higher
        classpath 'com.google.gms:google-services:4.3.0'  // Google Services plugin

        // Add dependency
        classpath 'io.fabric.tools:gradle:1.31.0'  // Crashlytics plugin
 
    }
}
allprojects {
    // ...

    repositories {
       // Check that you have the following line (if not, add it):
       google()  // Google's Maven repository
       // ...
    }
}

- In your app-level build.gradle, update your firebase-core to version v11.4.2 or later, then add the Crashlytics dependencies:

apply plugin: 'com.android.application'
apply plugin: 'io.fabric'

dependencies {
    // ...

    // Check for v11.4.2 or higher
    implementation 'com.google.firebase:firebase-core:17.0.1'

    // (Recommended) Add Analytics
    implementation 'com.google.firebase:firebase-analytics:17.0.1'

    // Add dependency
    implementation 'com.crashlytics.sdk.android:crashlytics:2.10.1'
}

- (Optional for apps using NDK) If your app uses Android native libraries, you can configure Crashlytics to report crashes from your NDK libraries. For more instructions, see Get Android NDK crash reports.
After you add the SDK to your app, Crashlytics automatically gets to work listening for and collecting crash reports.

3. Initialize Crashlytics

- For Android apps, a hook in the AndroidManifest.xml file automatically initializes the Firebase SDK.

4.Build or run your project

5. Force a crash to test your implementation
- You don't have to wait for a crash to know that Crashlytics is working. You can add a button to your app's MainActivity to force a crash:

Button crashButton = new Button(this);
crashButton.setText("Crash!");
crashButton.setOnClickListener(new View.OnClickListener() {
    public void onClick(View view) {
        Crashlytics.getInstance().crash(); // Force a crash
    }
});

addContentView(crashButton, new ViewGroup.LayoutParams(
        ViewGroup.LayoutParams.MATCH_PARENT,
        ViewGroup.LayoutParams.WRAP_CONTENT));

- When testing, reopen your app after pressing the button to crash it to make sure Crashlytics has a chance to report the crash. The report should appear in the Firebase console within five minutes.

##### Windows


1. Open terminal with your main project path and do following:
 - yarn add react-native-firebase or npm install --save react-native-firebase.
 - add react-native link





