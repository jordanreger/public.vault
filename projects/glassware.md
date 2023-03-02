# Introduction
Before we start; if your Glass isn't set up yet, view [this page](/projects/glass). Otherwise, this assumes that your Glass is set up, you have at least a little bit of technical/programming knowledge, and you're ready to go. If you'd like to take a look at the fully set up project or take the app for a spin, check out my [HelloGlass GitHub repository](https://github.com/jordanreger/HelloGlass).

# Getting Started
First, let's initialize a new **Empty Activity** project with the **Minimum SDK** set to `API 19: Android 4.4 (KitKat)`. Wait for a bit for it to get itself set up, and then we're ready to move on. 

# Importing the GDK
To get started, you can [download the *original* GDK](https://github.com/jordanreger/gdk/releases/download/v1.0.0/gdk.jar) from my GitHub. Here's the source if you ever want to take a look: [jordanreger/gdk](https://github.com/jordanreger/gdk). Drag the GDK into the `app/libs` folder (which can be found by switching the tab at the top left from `Android` to `Project`). You will now be able to use the old GDK in whatever version you're using!

# Changes
Below are a few changes we need to make before we're ready to run:

## `AndroidManifest.xml`
At the path `app/manifests/AndroidManifest.xml`, we're going to tweak just a couple things. Replace the `<activity></activity>` with what's below:

```xml
<activity  
    android:name="com.{your name}.{project name}.MainActivity"  
    android:enabled="true"  
    android:exported="true">  
    <intent-filter>
	    <action android:name="com.google.android.glass.action.VOICE_TRIGGER" />  
    </intent-filter>
    <meta-data android:name="com.google.android.glass.VoiceTrigger"
	    android:resource="@xml/show_me_a_demo" />  
</activity>
```

As mentioned [here](https://developers.google.com/glass/develop/gdk/quick-start#:~:text=Theme%3A%20None%20(ADT%20and%20Android%20Studio%20usually%20assign%20a%20theme%20automatically%2C%20even%20if%20you%20specify%20no%20theme%2C%20so%20remove%20the%20android%3Atheme%20property%20from%20your%20manifest%20after%20creating%20a%20project.) on step  to make sure you don't blind yourself, remove the following line inside the first `<application>` tag:

```xml
android:theme="@style/Theme.{project name}"
```

## `MainActivity.java`
At the path `app/java/com.{your name}.{project name}/MainActivity.java`, we need to change the whole file, essentially. Copy and paste the following in, replacing what's there already:

```java
package com.{your name}.{project name};

import android.app.Activity;
import android.os.Bundle;

public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

## `activity_main.xml`
At the path `app/res/layout/activity_main.xml`, we're going to replace everything once again with what's below:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<FrameLayout  
    xmlns:android="http://schemas.android.com/apk/res/android"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent">  
  
    <TextView        android:id="@+id/textView"  
        android:layout_width="match_parent"  
        android:layout_height="match_parent"  
        android:gravity="center"  
        android:text="Hello Glass!" />  
</FrameLayout>
```

## `show_me_a_demo.xml` (new)
We must make a new file at the path `app/res/xml` entitled `show_me_a_demo.xml`, and inside is:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<!-- https://developers.google.com/glass/develop/gdk/reference/com/google/android/glass/app/VoiceTriggers.Command -->  
<trigger command="SHOW_ME_A_DEMO" />
```

# Final Steps
To get your code to run on your Glass, you must first navigate to **Run > Edit Configurations** and then at the bottom under **Launch Options**, set the **Launch** parameter to be **Specified Activity** instead of **Default Activity**. Below, select `com.{your name}.{project name}.MainActivity` and then hit **Apply**.

You should be able to build and run now!

# Conclusion
This is just a simple boilerplate application to get you started with modern Glassware development. If you'd like to chat, [send me an email](mailto:mail@jordanreger.com)!