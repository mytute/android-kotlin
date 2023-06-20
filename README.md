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

        /* add 'kotlin-android-extensions' in build.gradle(:app) if not import automatically
        plugins {
            id 'com.android.application'
            id 'kotlin-android'
            id 'kotlin-android-extensions' // add
        }
        */

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

(Ctrl + Alt + Shift + L) for re arrange the code of xml file.

```xml
<TextView
    android:id="@+id/tvCount"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"

    android:text="TextView Samadhi " // change text, can from code
    android:textSize="18sp" // set text size (scale independent pixel )
    android:textColor="@color/purple_200" // set text color from global color.xml file
    //android:textColor="@android:color/purple_200" // use android default colors
    android:textStyle="italic|bold" // set text italic and bold
    android:textAllCaps="true" // set text capital letters
    android:textAligment="center"

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

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
</resources>
```

res> values > colors.xml

### EDITTEXTS

to get edit text
[go] Palette > [select] "Text" > [drag] "Plain Text"    

add constraint as you need

ems mean how many 'M' can fit in EditText-
inputType mean what type data user can input (eg phone, textPassword..) (CTRL + SPACE to show all posible here.)

```xml
<EditText
    android:id="@+id/etTest"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:ems="5"
    android:inputType="number"
    android:hint="33"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

### IMAGEVIEWS

to get Iamge view   
activity_main.xml file <ImageView then enter

to get image for android studio
copy image from computer and go to res>drawable press CTRL+v (marta.png)

add image src to <ImageView .   
android:src="@drawable/marta"     

add scale type    
android:scaleType="center"    // make center but not scale the image
android:scaleType="centerCrop" // make center and only height fit
android:scaleType="centerInside" // make center and only width fit
android:scaleType="fitcenter" // make center and fit width or height(default)
android:scaleType="fitStart" // align image to top
android:scaleType="fitEnd" // align image to bottom
android:scaleType="fitXY" // fit with width and height but proportion destroyed
android:scaleType="metrix" // to make custom


```xml
<ImageView
     android:id="@+id/imageView"
     android:layout_width="match_parent"
     android:layout_height="400dp"
     android:scaleType="centerCrop" // default type is centerCrop
     android:src="@drawable/marta" // marta.png is in drawable folder
 />
```   

let's show image using kotlin code    

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        btnShow.setOnClickListener{
            imageView.setImageResource(R.drawable.marta)
        }
    }
}
```

```xml
<ImageView
    android:id="@+id/imageView"
    android:layout_width="match_parent"
    android:layout_height="400dp"
    android:scaleType="centerCrop"/>

<Button
    android:id="@+id/btnShow"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="View"/>
```

### CHECKBOX AND RADIOBUTTON

```xml
<TextView
    android:id="@+id/tvQuestion"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="What do you want"
    android:textSize="20sp" />

// for radio we have to group by using 'RadioGroup'
<RadioGroup
    android:id="@+id/rgMeat"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:orientation="horizontal" // all radio button align Horizontally
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/tvQuestion">

    <RadioButton
        android:id="@+id/rbBeef"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Beef"
        android:checked="true"/> // checked true at start of the app

    <RadioButton
        android:id="@+id/rbChiken"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Chiken" />

    <RadioButton
        android:id="@+id/rbPork"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Pork" />

</RadioGroup>

<CheckBox
    android:id="@+id/cbCheese"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Cheese"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/rgMeat" />

<CheckBox
    android:id="@+id/cbOnions"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Onions"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/cbCheese" />

<CheckBox
    android:id="@+id/cbSalad"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Salad"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/cbOnions" />

<Button
    android:id="@+id/btnOrder"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Order"
    android:textAllCaps="false"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/cbSalad" />

<TextView
    android:id="@+id/tvOrder"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="26sp"
    app:layout_constraintTop_toBottomOf="@+id/btnOrder"
    tools:layout_editor_absoluteX="8dp" />
```

```kt
btnOrder.setOnClickListener{
    val checkedMeatRadioButtonId = rgMeat.checkedRadioButtonId;
    val meat = findViewById<RadioButton>(checkedMeatRadioButtonId);
    val cheese: Boolean = cbCheese.isChecked;
    val onions: Boolean  = cbOnions.isChecked;
    val salad: Boolean  = cbSalad.isChecked;

    val orderString:String = "You ordered a burgar with \n"+
            "${meat.text}" +
            (if(cheese) "\nCheese" else "") +
            (if(onions) "\nOnions" else "") +
            (if(salad) "\nSalad" else "")
    tvOrder.text = orderString;
}
```

### TOASTS AND CONTEXT

```kotlin
btnToast.setOnClickListener{
     //Toast.makeText(this,"HI this is toast", Toast.LENGTH_LONG).show();
     Toast.makeText(applicationContext,"HI this is toast", Toast.LENGTH_LONG).show();
 }
```

to create custom toast message    
go res>layout>rclick > New > layout resource file > give name as "custom_toast" >
give Root element as a "androidx.constraintlayout.widget.ConstraintLayout" > click OK  

to crate new Icon for toast  
go res > drawable > rclick > New > Image Asset > [select] "Icon Type" to "Action Bar and Tab Icons" >
[input] Name for icon "ic_notification" > [select] "Asset Type" to "Clip Art" > [click] "Clip Art" button >
[search] 'notification' icon > [select] "Theme" to "HOLO_LIGHT"


> custom_toast.xml   
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/clToast" // add id to access from MainActivity file
    android:layout_width="wrap_content" // only need content size
    android:layout_height="wrap_content" //  only need content size
    android:background="@android:color/holo_green_light" // add backgroud to activity
    android:padding="16dp"> // add margin

    <ImageView
        android:id="@+id/ic_notification"
        android:layout_width="100dp" // add icon size
        android:layout_height="100dp" // add icon size
        android:src="@drawable/ic_notification" // add create icon with name
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="This is custom toast"
        android:textSize="20sp" // add font size
        app:layout_constraintBottom_toBottomOf="@+id/ic_notification"
        app:layout_constraintStart_toEndOf="@+id/ic_notification"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

> MainActivity.kt file    

```kt
btnToast.setOnClickListener{
    Toast(this).apply {
        duration = Toast.LENGTH_LONG;
        // ctToast > custom xml
        view = layoutInflater.inflate(R.layout.custom_toast, clToast)
        show()
    }
}
}
```

### INTENTS AND STARTING ACTIVITIES

first see by scratch

create layout
go > res > layout > [rclick & select] New > [select] layout resource file > [input] "Name" activity_second > [input] "Root element" androidx...ConstrainLayout > [click] "Ok"  
create activity  
go > java>  .. > [rclick] "New" > [select] "kotlin File/Class" > [input] class name like SecondActivity this will create empty class and we have to do with inheritance  



> activity_second

```xml
<TextView
    android:id="@+id/tvActivity"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Welcome to Second Activity"
    android:textSize="25sp"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />

<Button
    android:id="@+id/btnBack"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Back"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/tvActivity" />
```

> SecondActivity   

```kt
class SecondActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        btnBack.setOnClickListener{
            finish(); // stop activity
        }
    }
}
```

```xml
<Button
    android:id="@+id/btnOpenActivity"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Open Activity"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

> MainActivity   

```kt
btnOpenActivity.setOnClickListener{
    // start second activity with intent
    Intent(this, SecondActivity::class.java).also {
        startActivity(it)
    }
}
```

> AndroidManifest.xml   

```xml
<application
    ...
    <activity android:name=".SecondActivity"></activity> // + add
    <activity
        android:name=".MainActivity"
        android:exported="true">
         ...
    </activity>
</application>
```

Let's see shorter way to do it.

go to folder where have "MainActivity"> [rclick] "New" > [select] Activity > [select] "Empty Activity" > [input] "Activity Name" ThirdActivity > [checked] "Generate Layout File"


### PASSING DATA BETWEEN ACTIVITIES
