# Jetpack Compose Navigation Guide

## Introduction
Navigation in Jetpack Compose allows developers to move between different screens in an app using a `NavController`. This guide provides a step-by-step explanation of setting up and using Compose Navigation with detailed comments and explanations.

---

## Prerequisites
Before implementing navigation, ensure that:
- You have Jetpack Compose set up in your Android project.
- The necessary dependencies are added to your project.
- You understand the basics of Jetpack Compose.

---

## Step 1: Add Dependencies

Add the required dependencies in your `libs.versions.toml` file:

```toml
[versions]
composeNavigation = "2.8.6"
serialization = "1.6.3"

[libraries]
navigation-compose = { module = "androidx.navigation:navigation-compose", version.ref = "composeNavigation"}
kotlinx-serialization-json = { module = "org.jetbrains.kotlinx:kotlinx-serialization-json", version.ref = "serialization" }

[plugins]
kotlin-serialization = { id = "org.jetbrains.kotlin.plugin.serialization", version.ref = "kotlin" }
```

In `app/build.gradle.kts`, apply the plugin:

```kotlin
plugins {
    alias(libs.plugins.kotlin.serialization)
}
```

And add the dependencies:

```kotlin
dependencies {
    // Navigation
    implementation(libs.navigation.compose)
    implementation(libs.kotlinx.serialization.json)
}
```

---

## Step 2: Set Up Navigation in MainActivity

Modify `MainActivity.kt` to initialize navigation:

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            NewNavigation {
                MyNav()
            }
        }
    }
}
```

This initializes the navigation when the app starts.

---

## Step 3: Creating Navigation Controller (NavController)

The `NavController` is the core of Jetpack Compose navigation. It helps manage the app’s navigation stack, keeping track of destinations and arguments.

### How `NavController` Works:
- It allows navigating between screens.
- It maintains a back stack of destinations.
- It enables passing arguments between destinations.

Create `MyNav.kt` and set up the `NavController`:

```kotlin
@Composable
fun MyNav() {
    val navController = rememberNavController() // Initialize NavController

    // NavHost manages the navigation stack and defines destinations
    NavHost(
        navController = navController, 
        startDestination = Home // Define the starting screen
    ) {
        composable<Home> {
            HomeScreen(navController) // Navigate to HomeScreen
        }

        composable<Detail> {
            val args = it.toRoute<Detail>() // Extract arguments
            DetailScreen(name = args.name, age = args.age)
        }
    }
}
```

### Explanation: {id="explanation_1"}
- `rememberNavController()` initializes a navigation controller that keeps track of the current screen.
- `NavHost()` defines the navigation graph, specifying the screens and their navigation paths.
- `composable<Home>` and `composable<Detail>` define the two screens.
- `it.toRoute<Detail>()` extracts arguments passed from the previous screen.

---

## Step 4: Define Navigation Destinations

We define two destinations: `Home` (starting screen) and `Detail` (screen with arguments).

```kotlin
@Serializable
object Home // Represents the Home screen

@Serializable
data class Detail(
    val name: String?,
    val age: Int
) // Represents the Detail screen with arguments
```

---

## Step 5: Implement Screens

### HomeScreen (Navigation with Arguments)

```kotlin
@Composable
fun HomeScreen(navController: NavController) {
    Column(
        Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(text = "Home Screen", fontSize = 32.sp)
        Spacer(modifier = Modifier.height(16.dp))
        Button(onClick = {
            navController.navigate(Detail(name = "Andre", age = 25))
        }) {
            Text(text = "Go to Detail")
        }
    }
}
```

### Explanation: {id="explanation_3"}
- Displays a text and a button.
- When the button is clicked, it navigates to `DetailScreen` passing arguments (`name` and `age`).

---

### DetailScreen (Receiving Arguments)

```kotlin
@Composable
fun DetailScreen(name: String?, age: Int) {
    Box(modifier = Modifier.fillMaxSize(), contentAlignment = Alignment.Center) {
        Text(text = "Detail Screen \n\n name $name age $age", fontSize = 32.sp)
    }
}
```

### Explanation: {id="explanation_2"}
- Displays the received arguments (`name` and `age`).
- Extracts the passed arguments from `MyNav`.

---

## Summary

1. **Add Dependencies:** Ensure `navigation-compose` and `kotlinx-serialization-json` are included.
2. **Initialize `NavController`:** Use `rememberNavController()` inside `MyNav`.
3. **Set Up Navigation Graph:** Use `NavHost()` to define the navigation flow.
4. **Define Screens:** Use `composable<T>` for each screen and handle arguments.
5. **Navigate with Arguments:** Use `navController.navigate(Detail(name, age))`.

This guide provides a structured approach to implementing navigation in Jetpack Compose, ensuring clarity and usability. 🚀

