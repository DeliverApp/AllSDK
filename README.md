# Using DeliverApp Android SDK via Maven Central

This guide explains how to add our Android library, hosted on GitHub Packages, to your Android project.

## Step 1: Add the Maven Central Repository to `settings.gradle.kts`

To access the DeliverApp library, add the Maven repository to your `settings.gradle.kts` file:

```kotlin
// settings.gradle.kts

dependencyResolutionManagement {
    repositories {
        ...
        mavenCentral()
        ...
    }
}
```

## Step 2: Add the Library Dependency (depending your pricing plan)

```kotlin
// build.gradle.kts

dependencies {
    ...
    implementation("io.deliverapp:all-sdk:0.10.0")
    ...
}
```

You can add all our Github dependencies whatever your pricing plan but the SDK won't work if your apiKey is not registered for the service.
Add the dependency with full knowledge of the facts.

## Step 3: How to use it

Deliver Android SDK provide an unique initialize method you could use in your Android Application.
First, Find your apiKey (Application ID) on https://store.deliverapp.io/settings/apps.

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