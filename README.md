## WebViewGTK — Mobile WebView for Android

**WebViewGTK** is a lightweight browser rendering component built on top of **WebKitGTK** that brings a full‑featured WebView to Android devices. It lets you embed modern web content in native Android apps.

---

### Features  

- **Modern WebKit rendering** – utilizes the latest WebKitGTK (GTK 4) engine, supporting HTML5, CSS3, JavaScript, and WebAssembly. 
- **Touch & gesture support** – native handling of scroll, pinch‑zoom, long‑press, and other mobile gestures.  
- **Secure sandbox** – runs in a separate process with restricted permissions, mirroring the security model of Android WebView.   
- **Lightweight** – minimal overhead compared to the default Android WebView, ideal for low‑end devices.  

---

## Getting Started
### Either download the APK from the release section or follow this guide for building.

#### Prerequisites  

| Requirement | Version |
|-------------|---------|
| Android SDK | 25 (or newer) |
| CMake       | 3.22+ |
| WebKitGTK   | 2.44+ (GTK 4) |
| Java/Kotlin | 11+ |

#### Installation  

1. **Add the Maven repository** to your project’s `build.gradle`:

   ```groovy
   repositories {
       mavenCentral()
       // optional: your own repo if you host the package
   }
   ```

2. **Declare the dependency**:

   ```groovy
   dependencies {
       implementation "com.todcubed:webviewgtk:1.0.0"
   }
   ```

3. **Sync the project** and let Gradle download the native libraries.  
4. **Load the WebView** in your activity/fragment:

   ```kotlin
   import com.todcubed.webviewgtk.WebViewGTK

   class MainActivity : AppCompatActivity() {
       private lateinit var webView: WebViewGTK

       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           webView = WebViewGTK(this)
           setContentView(webView)

           webView.settings.apply {
               javaScriptEnabled = true
               domStorageEnabled = true
           }

           webView.loadUrl("https://duckduckgo.com")
       }
   }
   ```

---

### API Overview  

| Class / Interface | Description |
|-------------------|-------------|
| **WebViewGTK** | Main view class that extends `android.view.View`. Handles rendering, navigation, and lifecycle. |
| **WebSettings** | Configuration object (similar to Android’s `WebSettings`) to enable JavaScript, control caching, etc. |
| **WebViewClient** | Callback interface for page‑load events, errors, SSL handling, and URL overrides. |
| **WebChromeClient** | Provides UI‑related callbacks (progress, title, JavaScript dialogs, file chooser). |
| **JsBridge** | Simple bridge for exposing Kotlin/Java objects to JavaScript (`addJavascriptInterface`). |

#### Common usage pattern  

```kotlin
val webView = WebViewGTK(this).apply {
    webViewClient = object : WebViewClient() {
        override fun onPageFinished(view: WebViewGTK, url: String) {
            Log.d("WebViewGTK", "Loaded: $url")
        }
    }
    webChromeClient = object : WebChromeClient() {
        override fun onProgressChanged(view: WebViewGTK, newProgress: Int) {
            progressBar.progress = newProgress
        }
    }
    settings.javaScriptEnabled = true
}
```

---

### Building from Source  

```bash
# Clone the repo
git clone https://github.com/todcubed/WebViewGTK.git
cd WebViewGTK

# Install build dependencies (Ubuntu example)
sudo apt-get install -y build-essential cmake libgtk-4-dev libwebkit2gtk-4.1-dev ndk-build

# Build the native library
./gradlew :webviewgtk:assembleRelease
```

The generated AAR will be located under `webviewgtk/build/outputs/aar/`.

---

### Contributing  

1. Fork the repository.  
2. Create a feature branch (`git checkout -b feat/your-feature`).  
3. Write tests for new functionality.  
4. Submit a pull request with a clear description and changelog entry.  

All contributions are welcome, especially improvements to performance, Android version compatibility, and documentation.

---

### License  

See the `LICENSE` file for details.

---

### Contact me

Feel free to contact me on Telegram (I may take some time to reply, take my word, I'll surely do)

[Click Here](https://t.me/todcubed)
