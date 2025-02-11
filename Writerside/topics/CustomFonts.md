# Adding Custom Fonts in Jetpack Compose

This guide will walk you through the process of adding and using custom fonts in a Jetpack Compose application. By following these steps, you will be able to apply a custom font family across your app’s typography styles.

## Before You Start

Make sure you have the following prerequisites:
- An Android project set up with Jetpack Compose.
- The required `.ttf` font files available for use.

## Step 1: Add Font Files

1. Inside your Android project, navigate to `res`.
2. Create a new folder named `font` (if it doesn’t already exist).
3. Drag and drop your `.ttf` font files into the `res/font` directory.

## Step 2: Define Font Family

In your UI theme package, typically inside `Type.kt`, initialize your font family as follows:

```kotlin
import androidx.compose.ui.text.font.Font
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.text.font.FontWeight

import com.horizondevelopers.news.R

val Poppins = FontFamily(
    fonts = listOf(
        Font(R.font.poppins_regular, FontWeight.Normal),
        Font(R.font.poppins_bold, FontWeight.Bold),
        Font(R.font.poppins_semibold, FontWeight.SemiBold),
    )
)
```

This ensures that different font weights are mapped correctly for use in your app.

## Step 3: Apply Fonts in Typography

Now, integrate the `Poppins` font into your app’s typography styles. This is also done in `Type.kt`:

```kotlin
import androidx.compose.material3.Typography
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.unit.sp

val Typography = Typography(
    displaySmall = TextStyle(
        fontSize = 24.sp,
        fontFamily = Poppins,
        fontWeight = FontWeight.Normal,
        lineHeight = 36.sp,
    ),
    displayMedium = TextStyle(
        fontSize = 32.sp,
        fontFamily = Poppins,
        fontWeight = FontWeight.Normal,
        lineHeight = 48.sp,
    ),
    bodySmall = TextStyle(
        fontSize = 14.sp,
        fontFamily = Poppins,
        fontWeight = FontWeight.Normal,
        lineHeight = 21.sp,
    ),
    bodyMedium = TextStyle(
        fontSize = 16.sp,
        fontFamily = Poppins,
        fontWeight = FontWeight.Normal,
        lineHeight = 24.sp,
    ),
    labelSmall = TextStyle(
        fontSize = 13.sp,
        fontFamily = Poppins,
        fontWeight = FontWeight.Normal,
        lineHeight = 19.sp,
    ),
)
```

## Step 4: Use Custom Fonts in Your UI

Once the typography is set, apply it in your Compose UI elements as follows:

```kotlin
Text(
    text = "Hello, Jetpack Compose!",
    style = Typography.displayMedium
)
```

This ensures that the `Poppins` font is used consistently across your app’s text elements.

## Conclusion

By following these steps, you have successfully integrated and applied a custom font in Jetpack Compose. You can now style your text elements with a unique and professional typography system that aligns with your app's branding.

