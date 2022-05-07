# introduction to Android


to create new Project
[click] "File" > [select] "New" > [select] "Empty Activity" > [input] "Name" & [select] "Language"


### ANDROID STUDIO ROUNDTRIP

to select Android Mode (only view files which we are dealing with)    
go to left-top corner of files palate and select "Android"

AndoridManifest.xml
AndoridManifest.xml includes basic configuration of app (permission, icon, components etc).
This file will automatically generate when we are create app on Android studio.

MainActivity.kt  
Java > com > <your projct name> > MainActivity.kt  
This file is the main entry point our android app

res(resources) folder
"drawable" >
"layout" >
"mipmap" > set app display icon on mobile
"values" >
         "colors.xml"  crate themes colors value  
         "strings.xml"  set global strings / useful when change app language       
         "styles.xml"    
"Gradle Scripts"
         "build.gradle"
         "build.gradle(Module.app)"   change app target version/ app version / add dependencies(3rd party)

### ACTIVITIES AND LIFECYCLE        

```kotlin

package com.example.tute001

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {

    // on create lifecycle
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState) // call the supper class
        setContentView(R.layout.activity_main) // R = resource > "layout" folder > activity_main.xml link
    }

   // onPause lifecycle
    override fun onPause() {
        super.onPause()
        println("start onPause")
    }
}

```       

### SOLVING EVERY ERROR IN ANDROID STUDIO

```kotlin

package com.example.tute001

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // in logcat you can select "Debug" mode to filter log messages
        // you can filter log tag using searchbar
        Log.d("tag of the log here","This is first log message")
    }

}

```  

### LAYOUT BASICS AND LINEAR LAYOUT

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--create LinearLayout-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"  // flex direction vertical
    android:padding="16dp" // add padding
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent" // get parent width
        android:layout_height="wrap_content" // get space the component need
        android:orientation="horizontal"> // flex direction horizontal

        <EditText // text input
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:hint="First Name" // input placeholder
            android:layout_weight="1" // ratio of horizontal weight  
            />

        <EditText
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:hint="Last Name"
            android:layout_weight="1"
            />

    </LinearLayout>

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Birth Day"

        />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:hint="Country"
            android:layout_weight="1"
            />

        <Button // button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Apply" // add text to button
            />

    </LinearLayout>




</LinearLayout>
```

### CONSTRAINT LAYOUT BASICS

ConstraintLayout better than LinearLayout. Because LinearLayout have to use more than one time.    
So It will create more calculation set create on screen.

### CHAINS AND GUIDELINES

to align elements
[select] elements > [click] top "Align" button > [click] "Vertically" or "Horizontally"

to align elements with baseline
[select] element > [right-click && select] "Show Baseline" > [Drag] element1 baseline to element2 baseline

to distribute elements
[select] elements > [right-click] > [select] Chains > [click] "Create Horizontal Chain" or "Create Vertical Chain"

to fill remaining width
[select] one element > [change] "layout_width" from "wrap_content" to "0dp"

to constraint with GUIDELINES(invisible on prod)
[right-click && select] "Helpers" > [click] any GUIDELINE that need > [click && drag] GUIDELINE position >
[drag] constraint element to GUIDELINE

### BUTTONS

to rename in layout id in xml (activity.xml) file
[press] Fn+Shift+F6 > [input] new name

```kotlin

package com.example.tute001
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import android.widget.Button
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // java method , but in kotlin we can direct access the widgets using it's id
        // val btnApply = findViewById<Button>(R.id.btnApply)

        // set event listener for "apply" buttton
        btnApply.setOnClickListener{
            val firstName = etFirstName.editableText.toString();
            val lastName = etLastName.editableText.toString();
            val bithDay = etBirthDay.editableText.toString();
            val contryName = etCountryName.editableText.toString();

            Log.d("MainActivity", "Input $firstName $lastName $bithDay $contryName ")
        }
    }
}

```

### TEXTVIEWS

```xml
<TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"

    android:text="TextView Samadhi laksahan fsdfd sdfdsf fsdfsf sdfsdf sdfsf"
    android:textSize="18sp" // set text size
    android:textColor="@color/colorAccent" // set text color from global color.xml file
    android:textStyle="italic|bold" // set text italic and bold
    android:textAllCaps="true" // set text capital letters

    android:ellipsize="end" // add "..." at the end if more text
    android:lines="2" // set max text line for 2

    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

change TextView value    

```kotlin
   tvCount.text = "Let's change the text"
```

### EDITTEXTS

to get edit text
[go] Palette > [select] "Text" > [drag] "Plain Text"
