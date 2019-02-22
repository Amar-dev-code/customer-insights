---
uid: developers/downloads/android-java
title: Get Started with Android (mobile)
---
# Getting started - Android (Java) 
 
This tutorial will help you start sending signals in five minutes. Get the signal sender, get a token, then start sending. 
 
## Prerequisites 
- Android Studio 
- Minimum Android API Level: 16 (Jelly Bean)  
- [API Token](./api-token)

## Integrate the signal sender into your project 
a. Open your project. If you don't have one, create a new project with Empty Activity in Android Studio.

b. Open the app level `build.gradle` file (`app/build.gradle`) and add the following lines after apply plugin to include the dependencies for project:
```
dependencies { 
    def appCenterSdkVersion = '1.11.0' 
    implementation "com.microsoft.appcenter:appcenter-analytics:${appCenterSdkVersion}" 
} 
```
c. Gradle Sync.

d. Open your app's main activity class and import: 
```
import com.microsoft.appcenter.AppCenter; 
import com.microsoft.appcenter.analytics.Analytics; 
```

e. Start the sender (it's only required to start it once): 
```
// The first parameter is the application context, this examples assumes it is called from an Activity. 
AppCenter.start(getApplication(), "target={Your-API-Token}", Analytics.class); 
```

f. Create a signal : 
```
// Do a simple trackEvent call. 
Analytics.trackEvent("my_simple_event_name"); 
 
// Track an event with properties of various types. 
EventProperties properties = new EventProperties(); 
properties.set("Name", "Ashley Smith"); 
properties.set("School", "Bellevue High School"); 
properties.set("Grade", 11); 
properties.set("Gpa", 3.82); 
properties.set("Birthday", new Date(800320249)); 
properties.set("Suspended", false); 
Analytics.trackEvent("StudentInformation", properties); 
```

The following types are supported for event properties: 
- String 
- Date 
- double 
- long 
- boolean
