After initializing a new **Empty Activity** project with the **Minimum SDK** set to `API 19: Android 4.4 (KitKat)`, follow this guide to properly set up your Glassware app for modern development.

# `AndroidManifest.xml`
At the path `app/manifests/AndroidManifest.xml`, we're going to tweak a couple things. Replace the `<activity></activity>` with what's below:

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

---

# `MainActivity.java`
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

---

# `activity_main.xml`
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

---

# `themes.xml`


# `show_me_a_demo.xml` (new)
We must make a new file at the path `app/res/xml` entitled `show_me_a_demo.xml`, and inside is:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<!-- https://developers.google.com/glass/develop/gdk/reference/com/google/android/glass/app/VoiceTriggers.Command -->  
<trigger command="SHOW_ME_A_DEMO" />
```

---

# Final Steps
To get your code to run on your Glass, you must first navigate to **Run > Edit Configurations** and then at the bottom under **Launch Options**, set the **Launch** parameter to be **Specified Activity** instead of **Default Activity**. Below, select `com.{your name}.{project name}.MainActivity` and then hit **Apply**.

You should be able to build and run now!