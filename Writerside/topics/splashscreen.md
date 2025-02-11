# Splash Screen Setup in a Kotlin Android App

A How-to article is an action-oriented type of document. It explains how to implement a splash screen in a Kotlin Android application using the official Android Splash Screen API. By following this guide, you will successfully integrate a modern splash screen into your app.

> **Highlight important information**
>
> You can change the element to *tip* or *warning* by renaming the style attribute below.
>
{style="note"}

## Before you start

Make sure that:
- You have a working Kotlin Android project.
- You have updated your dependencies to support the latest AndroidX Core SplashScreen API.

## How to Add a Splash Screen

### 1. Add Dependency

Include the **Splash Screen API** dependency in `build.gradle.kts (Module: app)`:

```kotlin
dependencies {
    implementation(libs.androidx.core.splashscreen)
}
```

### 2. Add Splash Assets

Place your splash screen image (`ic_splash.xml` or `.png`) in the **res/drawable** directory.

### 3. Create a Splash Theme

Create a new **res/values/splash/splash.xml** file and define the splash screen theme:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="App.Starting.Theme" parent="Theme.SplashScreen">
        <item name="windowSplashScreenBackground">#FFFF</item>
        <item name="windowSplashScreenAnimatedIcon">@drawable/ic_splash</item>
        <item name="postSplashScreenTheme">@style/Theme.News</item>
    </style>
</resources>
```

### 4. Add a Night Mode Splash Theme

To support dark mode, create a **res/values/splash/splash.xml** file and define the night theme:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="App.Starting.Theme" parent="Theme.SplashScreen">
        <item name="windowSplashScreenBackground">#1C1E21</item>
        <item name="windowSplashScreenAnimatedIcon">@drawable/ic_splash</item>
        <item name="postSplashScreenTheme">@style/Theme.News</item>
    </style>
</resources>
```

### 5. Apply Theme in AndroidManifest.xml

Update `AndroidManifest.xml` to use the splash theme in the `<application>` and `<activity>` tags:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:theme="@style/App.Starting.Theme"
        tools:targetApi="31">
        
        <activity
            android:theme="@style/App.Starting.Theme">
        </activity>
    </application>
</manifest>
```

### 6. Implement Splash Screen in MainActivity.kt

Modify your `MainActivity.kt` to handle the splash screen transition:

```kotlin
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.core.splashscreen.SplashScreen.Companion.installSplashScreen

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        // Install Splash Screen
        installSplashScreen()
        
        setContent {
            MyAppTheme {
                // Your app's main content goes here
            }
        }
    }
}
```

### 7. Sync and Run the Project

Run the following command to build your project:

```bash
./gradlew build
```

## 🎉 Done!
Your splash screen is now successfully implemented with both light and dark mode support following the official Android API. 🚀

