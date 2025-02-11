# Nested Navigation in Jetpack Compose

## Introduction

In Jetpack Compose, nested navigation allows for organizing routes into smaller navigation graphs within a parent NavHost. This helps in managing navigation efficiently, especially in large apps with multiple sections. This guide explains how to set up and use nested navigation in a structured and understandable manner.

## Prerequisites

Before implementing nested navigation, ensure you have:
- Jetpack Compose set up in your project.
- The navigation-compose library added to your dependencies.
- Basic understanding of the NavController and navigation concepts in Compose.

### Step 1: Add Dependencies

Ensure the following dependencies are included in your **libs.versions.toml**:

```toml
[versions]
composeNavigation = "2.8.6"

[libraries]
navigation-compose = { module = "androidx.navigation:navigation-compose", version.ref = "composeNavigation" }
```

In your **app-level build.gradle.kts**, apply the plugin and dependencies:

```kotlin
plugins {
    alias(libs.plugins.kotlin.serialization)
}

dependencies {
    implementation(libs.navigation.compose)
}
```

### Step 2: Setting Up the Main Navigation Graph

The `NavHost` is responsible for managing different screens and their routes. We define a `NavController` and set up our navigation structure inside `MyNav`.

```kotlin
@Composable
fun MyNav() {
    val navController = rememberNavController()
    NavHost(navController = navController, startDestination = "home") {
        composable("home") { HomeScreen(navController) }
        navigation(startDestination = "profile", route = "account") {
            composable("profile") { ProfileScreen(navController) }
            composable("settings") { SettingsScreen(navController) }
        }
    }
}
```

### Step 3: Creating Screens

Each screen is defined as a composable function. Below are the implementations of `HomeScreen`, `ProfileScreen`, and `SettingsScreen`.

#### HomeScreen
```kotlin
@Composable
fun HomeScreen(navController: NavController) {
    Column(modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally) {
        Text("Home Screen", fontSize = 24.sp)
        Button(onClick = { navController.navigate("account") }) {
            Text("Go to Account")
        }
    }
}
```

#### ProfileScreen
```kotlin
@Composable
fun ProfileScreen(navController: NavController) {
    Column(modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally) {
        Text("Profile Screen", fontSize = 24.sp)
        Button(onClick = { navController.navigate("settings") }) {
            Text("Go to Settings")
        }
    }
}
```

#### SettingsScreen
```kotlin
@Composable
fun SettingsScreen(navController: NavController) {
    Column(modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally) {
        Text("Settings Screen", fontSize = 24.sp)
        Button(onClick = { navController.popBackStack() }) {
            Text("Back to Profile")
        }
    }
}
```

### Step 4: Understanding Nested Navigation

1. **Navigation Hierarchy**: The `NavHost` defines an overall structure where the `account` route acts as a parent for `profile` and `settings`.
2. **Start Destination**: The `navigation` function specifies `profile` as the first screen inside the `account` route.
3. **Navigating Within Nested Routes**: When clicking a button on `ProfileScreen`, the user is directed to `SettingsScreen`.
4. **Back Navigation**: Using `popBackStack()` ensures the user can navigate back within nested routes.

### Step 5: Handling Deep Links (Optional)

You can use deep links to navigate directly to nested destinations.

```kotlin
composable("profile", deepLinks = listOf(navDeepLink { uriPattern = "myapp://profile" })) {
    ProfileScreen(navController)
}
```

### Conclusion

Nested navigation in Jetpack Compose allows for better organization and navigation structure within large applications. By following the steps outlined, you can implement a scalable navigation system with nested routes while ensuring a smooth user experience.

