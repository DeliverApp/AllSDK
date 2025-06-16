# Using DeliverApp Android SDK via GitHub Packages

This guide explains how to add our Android library, hosted on GitHub Packages, to your Android project.

## Step 1: Add the GitHub Packages Repository to `settings.gradle.kts`

To access the DeliverApp library from GitHub Packages, add the Maven repository to your `settings.gradle.kts` file:

```kotlin
// settings.gradle.kts

pluginManagement {
    repositories {
        maven {
            url = uri("https://maven.pkg.github.com/DeliverApp/AllSDK")
            credentials {
                username =System.getenv("GITHUB_USERNAME") ?: ""
                password = System.getenv("GITHUB_TOKEN") ?: ""
            }
        }
        gradlePluginPortal()
        mavenCentral()
    }
}
```

## Step 2: Use Environment Variable for GitHub Username and Token

GitHub Packages use Personal access tokens to download package unless the repository is public.
If you already has a token with **read:packages** privilege, you can use it.
If not, you could set a new token by visit https://github.com/settings/tokens.
Finally, if you really don't want to create your own token, Deliver offers you a token you can use.
Be careful, it expires every 90 days.

### MacOS / Linux
```bash
export GITHUB_USERNAME=your_username
export GITHUB_TOKEN=your_access_token
```
or 
```bash
export GITHUB_USERNAME=DeliverApp
export GITHUB_TOKEN=`Ask contact@deliverapp.io for the token` // expire every 90 days, ask for faster regeneration
```

### Windows
```bash
set GITHUB_USERNAME=your_username
set GITHUB_TOKEN=your_access_token
```
or
```bash
set GITHUB_USERNAME=DeliverApp
set GITHUB_TOKEN=`Ask contact@deliverapp.io for the token`  // expire every 90 days, ask for faster regeneration
```

## Step 3: Add the Library Dependency (depending your pricing plan)

```kotlin
// build.gradle.kts

dependencies {
    implementation("deliver.io:all-sdk:latest")
}
```

You can add all our Github dependencies whatever your pricing plan but the SDK won't work if your apiKey is not registered for the service.
Add the dependency with full knowledge of the facts.

## Step 4: How to use it

Deliver Android SDK provide two initialize methods you could use in your Android Application.
First, Find your apiKey (Application ID) on https://store.deliverapp.io/settings/apps.

# Using DeliverApp Android SDK via manual installation

## Step 1: Download aar file

On Github packages :
https://github.com/DeliverApp/AllSDK/packages/2489644

And put it in libs folder for exemple.

## Step 2: Add the Library Dependency (depending your pricing plan)

Don't forget to add all dependencies needed by our SDK.

```kotlin
// build.gradle.kts

dependencies {
    implementation(fileTree(mapOf("dir" to "../libs", "include" to listOf("*.aar"))))
    implementation("androidx.core:core-ktx:1.16.0")
    implementation("androidx.appcompat:appcompat:1.7.0")
    implementation("com.google.android.material:material:1.12.0")
    implementation("com.squareup.retrofit2:retrofit:2.11.0")
    implementation("com.squareup.retrofit2:converter-moshi:2.11.0")
    implementation("com.squareup.okhttp3:logging-interceptor:4.12.0")
    implementation("com.squareup.okhttp3:okhttp:4.12.0")
    implementation("com.squareup.moshi:moshi-kotlin:1.15.1")
    implementation("androidx.camera:camera-camera2:1.4.2")
    implementation("androidx.camera:camera-lifecycle:1.4.2")
    implementation("androidx.camera:camera-view:1.4.2")
    implementation("com.google.mlkit:barcode-scanning:17.3.0")
    implementation("io.coil-kt:coil:2.7.0")
    implementation(platform("androidx.compose:compose-bom:2025.04.01"))
    implementation("androidx.compose.runtime:runtime-livedata:1.8.0")
    implementation("androidx.lifecycle:lifecycle-runtime-compose:2.8.7")
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.8.7")
    implementation("io.insert-koin:koin-androidx-compose:3.5.6")
    implementation("io.insert-koin:koin-androidx-compose-navigation:3.5.6")
    implementation("com.jakewharton.timber:timber:5.0.1")
}
```

# Initialization

You can just init the SDK with your app apiKey.

```kotlin
// Application.kt

DeliverAllSDK.init(this, "APP_API_KEY")
```

If youd do so this way, you will have access to all the marvelous features SDK offers except Network remote debugging.
To unlock this one, you have to use our okhttp3 interceptor.

```kotlin
your_okhttp3_builder.addNetworkInterceptor(DeliverHTTPInterceptor()).build()
```

# And that's it ! Start using magic

Thank you for choosing Deliver !