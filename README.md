# AndroidSplashScreenDemo
It’s not uncommon these days for apps to have a splash screen when you first open the app. In fact, the splash screen is useful in a technical way too because, for apps that have long loading times, splash screen can cover that awkward second of white screen of loading, and make the user experience a little better than it is.

Implementing the splash screen is actually extremely easy. The idea is that you start by setting the loading screen as your main Activity, and as soon as the loading screen finishes, you redirect to your original “main activity” that you want. The splash screen should in theory load instantly, and thus act as a loading screen for your app.

You want to first declar a splash screen on your resource file and in your Manifest:

```xml
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    </style>

    <style name="SplashTheme" parent="Theme.AppCompat.NoActionBar">
        <item name="android:windowBackground">@drawable/back_ground_splash</item>
    </style>

</resources>
```

In your drawable resource folder, you should make the corresponding file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:drawable="@android:color/white"/>

    <item>
        <bitmap
            android:gravity="center"
            android:src="@drawable/ic_action_name"/>
    </item>
</layer-list>
```

Of course, you can customize this to your liking.  Please note that for bitmaps, vector image source will not work, so be sure to add your own image source.  After this, just add it to your Application Manifest:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="yiminghan.splashscreendemo">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
        </activity>

        <activity android:name=".SplashActivity"
            android:theme="@style/SplashTheme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

Remember to set **android:theme="@style/SplashTheme"** for the splash activity
Finally, in your SplashActivity, just set it to redirect to your main activity:

```kotlin
public class SplashActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Intent intent = new Intent(this, MainActivity.class);
        startActivity(intent);
        finish();
    }
}
```




