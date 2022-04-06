
# Rapport

 I denna uppgift har jag ändrat appens namn i filen string.xml.

 För att tillåta appen att använda internet så implementerades kod som gjorde detta möjligt i filen AndroidManifest.xml;
 ```
    <uses-permission android:name="android.permission.INTERNET" />
 ```

Följdaktligen skapade jag en Webview-variabel i filen "content_main.xml" och tilldelade den ett ID;
```
   <WebView
        android:id="@+id/my_webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

I koden nedan så deklarerar jag först en variabel av typen "Webview" i filen MainActivity.java.
För att koppla en aktivitet till komponenten så används "findViewById" där jag sätter till att vara idet som jag gav min Webview-element.
```
public class MainActivity extends AppCompatActivity {
    WebView myWebView;
    ...
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ...
        myWebView = findViewById(R.id.my_webview);
        myWebView.getSettings().setJavaScriptEnabled(true);
        myWebView.setWebViewClient(new WebViewClient());
```

Jag skapade en html-sida under en ny map (assets -> about.html) och skapade två funktioner (i MainActivity.java) som gör så att två olika hemsidor öppnas när den funktionen kallas på.
```
    public void showExternalWebPage(){
        myWebView.loadUrl("https://www.his.se/");
    }
    public void showInternalWebPage(){
        myWebView.loadUrl("file:///android_asset/about.html");
    }
```
Beroende på vilken menyalternativ användaren har tryckt på så kommer denna funktion validera vilken funktion som ska starta (som ses i koden ovan).
```
public boolean onOptionsItemSelected(MenuItem item) {
    int id = item.getItemId();
    if (id == R.id.action_external_web) {
        Log.d("==>","Will display external web page");
        showExternalWebPage();
        return true;
    }
    if (id == R.id.action_internal_web) {
        Log.d("==>","Will display internal web page");
        showInternalWebPage();
        return true;
    }
```
Skärmbilder från den externa hemsidan och den interna.
Externa hemsidan:
![](external.png)
Intern hemsida:
![](internal.png)

