# Setup
1. Put .aar file into your module's **libs** dir
2. Add following lines to **repository** section of your module's build.gradle:
```groovy
    flatDir {
        dirs 'libs'
    }
```
3. Declare following dependencies:
```groovy
    implementation "org.jetbrains.kotlin:kotlin-stdlib:1.3.+"
    implementation 'com.squareup.retrofit2:retrofit:2.4.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.3.0'
    implementation 'com.squareup.retrofit2:converter-scalars:2.2.0'
    implementation 'com.google.android.exoplayer:exoplayer-core:2.9.6'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    implementation 'androidx.appcompat:appcompat:1.0.2'
    implementation (name: 'player-x.y.z', ext: 'aar')
```
Replace ***x.y.z*** with preferred version from [Releases](https://github.com/coub/coub-android-library/releases) page
# Usage
## Using built-in view:
```kotlin
    val coubPlayer = CoubPlayer.Factory.getInstance(context)
    coubPlayer.injectInto(containerView) // player will remove all existing views in container
    coubPlayer.load(coubUrl) // https://coub.com/view/${permalink}
    coubPlayer.setPlayWhenReady(true)
```
## Using your own custom view:
```kotlin
    val coubPlayer = CoubPlayer.Factory.getInstance(context)
    coubPlayer.setOutputTexture(textureView)
    coubPlayer.load(coubUrl) // https://coub.com/view/${permalink}
    coubPlayer.setPlayWhenReady(true)
```
## Receiving playback events
```kotlin
    coubPlayer.addEventListener(object : CoubPlayer.EventListener {
            override fun onError(player: CoubPlayer, error: Throwable?) {
                // do something
            }

            override fun onLoaded(player: CoubPlayer) {
                // do something
            }

            override fun onStarted(player: CoubPlayer) {
                // do something
            }

            override fun onStopped(player: CoubPlayer) {
                // do something
            }
        })
```
## Adjusting volume and restarting
```kotlin
    coubPlayer.volume = newVolume // 0f..1f
    coubPlayer.restart()
```
## Release player when you no longer need it
```kotlin
    coubPlayer.release()
```
