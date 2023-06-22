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

here we pass data using putExtra function with data key that received activity can grab it from key.    

> MainActivity.kt  

```kt
btnSendData.setOnClickListener {
     val firstName = etFirstName.text.toString(); // get input value from edit text
     val lastName = etLastName.text.toString(); // get input value from edit text
     val country = etContry.text.toString(); // get input value from edit text
     Intent(this, ActivityReceive::class.java).also {
         it.putExtra("EXTRA_FIRST_NAME", firstName); // set value with key name
         it.putExtra("EXTRA_LAST_NAME", firstName);
         it.putExtra("EXTRA_COUNTRY", firstName);
         startActivity(it);
     }
 }
```

show activity that receive data. by using key of value and intent.get[string|int] function can grab data from parent activity.    
> ActivityReceive.kt  

```kt
val firstName = intent.getStringExtra("EXTRA_FIRST_NAME");
val lastName = intent.getStringExtra("EXTRA_LAST_NAME");
val country = intent.getStringExtra("EXTRA_COUNTRY");
// display data from parent in received activity
tvReceivedData.text = "$firstName $lastName from $country";
```


Let's pass the classes between the activities. (data class)
[rclick] on MainActivity folder > [select] "New" > [select] "Kotlin File/Class" > [select] "class" > [input] "Name" as Person     

we are going to pass following data class to child activity

> Persion.kt  

```kt
package com.example.test001

import java.io.Serializable

data class Person (
    val firstName: String,
    val lastName: String,
    val country: String,
        ): Serializable {

}
```


> MainActivity.kt  

```kt
btnSendData.setOnClickListener {
    val firstName = etFirstName.text.toString();
    val lastName = etLastName.text.toString();
    val country = etContry.text.toString();
    val person = Person(firstName, lastName, country)
    Intent(this, ActivityReceive::class.java).also {
        it.putExtra("EXTRA_PERSON", person);

        startActivity(it);
    }
}
```

show activity that receive data. by using key of value and intent.get[string|int] function can grab data from parent activity.    
> ActivityReceive.kt  

```kt
val person = intent.getSerializableExtra("EXTRA_PERSON") as Person;

tvReceivedData.text = person.toString();
btnReturn.setOnClickListener {
    finish();
}
```


### PERMISSIONS

ACCESS_COARSE_LOCATION and ACCESS_BACKGROUND_LOCATION both are not above android version 10. below that work just location permission as documentation.

tow type of permission    
1. less sensitive (access to the internet)
2. more sensitive (access the device location: need user permission)


go to AndroidManifest.xml for init permission and if it more sensitive then permission will ask from user when it use.   

> AndoridManifest.xml  

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    ...
    <uses-permission android:name="android.permission.INTERNET"/> // no user permission
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    // for access location when app is using
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    // for access location when app is in backgroud mode
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION"/>
    // before android Q there was no COARSE and BACKGROUND but only one type of location.
    ...
    <application>
      ...
    </application>

</manifest>  
```   

go to activity_main amd add button for start get permission.  

> MainActivity.kt   

```kt
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

            Log.d("mainActivity", "this is our first log message");

           btnRequest.setOnClickListener {
               requestPermissions();
           }

       }

    // before this need to check whether device is above Android Q or not. otherwise this will crash the app.
    // here we use "Manifest.permission" because it has all permission types as string.
    private fun hasWriteExternalStoragePermission() =
        ActivityCompat.checkSelfPermission(this, Manifest.permission.WRITE_EXTERNAL_STORAGE) == PackageManager.PERMISSION_GRANTED;

    private fun hasLocationForegroundPermission()=
        ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION) == PackageManager.PERMISSION_GRANTED;

    private fun hasLocationBackgroundPermission()=
        ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_BACKGROUND_LOCATION) == PackageManager.PERMISSION_GRANTED;


    private fun requestPermissions(){
        // first have to check already have permission or not.
        var permissionsToRequest = mutableListOf<String>();
        if(!hasWriteExternalStoragePermission()){
            permissionsToRequest.add(Manifest.permission.WRITE_EXTERNAL_STORAGE);
        }
        if(!hasLocationForegroundPermission()){
            permissionsToRequest.add(Manifest.permission.ACCESS_COARSE_LOCATION);
        }
        if(!hasLocationBackgroundPermission()){
            permissionsToRequest.add(Manifest.permission.ACCESS_BACKGROUND_LOCATION);
        }

        // only one request permission function
        if(permissionsToRequest.isNotEmpty()){
            // .toTypedArray() is convert mutable list convert to string array
            ActivityCompat.requestPermissions(this, permissionsToRequest.toTypedArray(), 0);
        }
    }

    // check is user did accept the permission or not
    override fun onRequestPermissionsResult(
        requestCode: Int,
        permissions: Array<out String>,
        grantResults: IntArray
    ) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults)
        if(requestCode == 0 && grantResults.isNotEmpty() ){
            for(i in grantResults.indices){ // loop index of grantResults array
              if(grantResults[i] == PackageManager.PERMISSION_GRANTED){
                  // print only user granted permission
                  Log.d("PermissionRequest", "${permissions[i]} granted.");
              }
            }
        }
    }

}

```

### IMPLICIT INTENTS

example when our app need a photo and we dones not create the app user going to take photo for our app.

in following example show how to browse image and browser can be any app that user have on phone.    

```xml
<Button
    android:id="@+id/btnBrowse"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Browse Image"
    android:textAllCaps="true"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent" />

<ImageView
    android:id="@+id/ivImage"
    android:layout_width="270dp"
    android:layout_height="400dp"
    android:scaleType="centerCrop"
    app:layout_constraintBottom_toTopOf="@+id/btnBrowse"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)


        btnBrowse.setOnClickListener {
            if (ContextCompat.checkSelfPermission(this, Manifest.permission.READ_EXTERNAL_STORAGE)
                == PackageManager.PERMISSION_GRANTED
            ) {
                openImageChooser();
            } else {
                openImageChooser();
                // here have to ask permission
                //requestPermissions(arrayOf(Manifest.permission.READ_EXTERNAL_STORAGE), 0)
            }
        }
    }

    private val getContent = registerForActivityResult(ActivityResultContracts.GetContent()) { uri: Uri? ->
        uri?.let {
            ivImage.setImageURI(uri) // set image for layout
        }
    }

    private fun openImageChooser() {
        getContent.launch("image/*") // open only for images
    }
}
```
### TOOLBAR MENUS


[r-click] "res" folder > [select] "New" > [select] "Android Resource Directory" > [select] on "Resource type" dropdown "menu" > [click] "Ok"     

now inside "res" folder "menu" folder appeared

[goto] 'res' folder > [r-click] "menu" folder > [select] "New" > [select] "Menu resource file" > [input] "File name" as "app_bar_menu"  

next create icons for app bar menu (for settings and favorites)    

[goto] "drawable" > [select] "New" > [select] "Image Asset" > [input] "Icon Type" to "Action Bar and Tab Icons" > [input] "Name" any name like "ic_settings" > [select] "Asset Type" to "Clip Art" > [click] "Clip Art" icon and search the icon > [input] "Theme" as you want like "HOLO_DARK"

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    // here add menu list
    // top goes to left side of menu
   <item
       android:id="@+id/miSettings"
       android:title="Settgins" // show as hint
       android:icon="@drawable/ic_settings"
       app:showAsAction="ifRoom"/> // show icon only if enough room
    <item
        android:id="@+id/miAddContanct"
        android:title="Add Contact" // show as hint
        android:icon="@drawable/ic_add_contact"
        app:showAsAction="ifRoom"/> // show icon only if enough room
    <item
        android:id="@+id/miFavorite"
        android:title="Favorite" // show as hint
        android:icon="@drawable/ic_favorite"
        app:showAsAction="always"/> // show icon always
    <item
        android:id="@+id/miFeedback"
        android:title="Feeback" // show as menu title
        app:showAsAction="never"/>  // no icon but as dropdown
    <item
        android:id="@+id/miClose"
        android:title="Close App" // show as menu title
        app:showAsAction="never"/> // no icon but as dropdown
</menu>
```

then have to tell MainActivity.kt that we have menu

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        Log.d("mainActivity", "this is our first log message");
    }

    // for display menu
    override fun onCreateOptionsMenu(menu: Menu?): Boolean {
        menuInflater.inflate(R.menu.app_bar_menu, menu)
        //return super.onCreateOptionsMenu(menu) // can remove default return
        return true
    }

    // for add actions when click display menu items
    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        //return super.onOptionsItemSelected(item) // can remove default return
        when(item.itemId){
            R.id.miAddContanct -> Toast.makeText(this, "You clicked on Add Contact", Toast.LENGTH_SHORT).show()
            R.id.miFavorite -> Toast.makeText(this, "You clicked on Favorites", Toast.LENGTH_SHORT).show()
            R.id.miSettings -> Toast.makeText(this, "You clicked on Settings", Toast.LENGTH_SHORT).show()
            R.id.miClose -> finish()
            R.id.miFeedback -> Toast.makeText(this, "You clicked on Feedback", Toast.LENGTH_SHORT).show()
        }
        return true;
    }
}
```

### ALERT DIALOG

following examples show implement 3 types of Alert dialog
1. yes no
2. singlechoice (radio buttons)   
3. multichoice (checkbox)

```xml  
<Button
    android:id="@+id/btnDialog1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Dialog 1"
    app:layout_constraintBottom_toTopOf="@+id/btnDialog2"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />

<Button
    android:id="@+id/btnDialog2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Dialog 2"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/btnDialog1" />

<Button
    android:id="@+id/btnDialog3"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Dialog 3"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/btnDialog2" />
```

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        Log.d("mainActivity", "this is our first log message");

        // YES OR NOT Dialog box
        // build a alert message
        val addContactDialog = AlertDialog.Builder(this)
            .setTitle("Add contact")
            .setMessage("Do you want to add Mr. Poop to your contacts list? ")
            .setIcon(R.drawable.ic_add_contact)
            .setPositiveButton("Yes"){ dialogInterface, i -> // jere
                Toast.makeText(this,"you add Mr. Poop to contact list", Toast.LENGTH_SHORT).show();
            }
            .setNegativeButton("No"){ dialogInterface, i ->
                Toast.makeText(this,"you didn't add Mr. Poop to contact list", Toast.LENGTH_SHORT).show();
            }.create() // .create() function make create from builder

        btnDialog1.setOnClickListener {
            addContactDialog.show()
        }

        // Radio button Dialog box (singlechoice dialog)
        // for this have to create array to define different options
        val options = arrayOf<String>("Firat Item", "Second Item", "Third Item");
        val singleChoiceDialog = AlertDialog.Builder(this)
            .setTitle("Choose on of these options")
            .setSingleChoiceItems(options, 0){dialogInterface,i-> // @params (optionlist, default check index)
                Toast.makeText(this,"you clicked on ${options[i]}", Toast.LENGTH_SHORT).show();
            }
            .setPositiveButton("Accept"){ dialogInterface, i -> // jere
                Toast.makeText(this,"you accepted the singleChoiceDialog", Toast.LENGTH_SHORT).show();
            }
            .setNegativeButton("Decline"){ dialogInterface, i ->
                Toast.makeText(this,"you decline singlechoiceDailog", Toast.LENGTH_SHORT).show();
            }.create() // .create() function make create from builder

        btnDialog2.setOnClickListener {
            singleChoiceDialog.show()
        }

        // checkbox Dialog box (multichoice dialog)
        // for this have to create array to define different options
        //val options = arrayOf<String>("Firat Item", "Second Item", "Third Item");
        val multiChoiceDialog = AlertDialog.Builder(this)
            .setTitle("Choose on of these options")
            .setMultiChoiceItems(options, booleanArrayOf(false, false, false)){ dialogInterface, i, b-> // @params (optionlist, default check index)
                if(b){
                    Toast.makeText(this,"you checked on ${options[i]}", Toast.LENGTH_SHORT).show();
                }else{
                    Toast.makeText(this,"you unchecked on ${options[i]}", Toast.LENGTH_SHORT).show();
                }

            }
            .setPositiveButton("Accept"){ dialogInterface, i -> // jere
                Toast.makeText(this,"you accepted the multiChoiceDialog", Toast.LENGTH_SHORT).show();
            }
            .setNegativeButton("Decline"){ dialogInterface, i ->
                Toast.makeText(this,"you decline multiChoiceDialog", Toast.LENGTH_SHORT).show();
            }.create() // .create() function make create from builder

        btnDialog3.setOnClickListener {
            multiChoiceDialog.show()
        }
    }
}
```

### SPINNER

when we have list to select we can use SPINNER instead of radio-buttons/checkbox. it is simple select view.

here for the options instead of string array we can use string xml for escape boilerplate code.

[go] "res" > [click] "values" > [click] "string.xml"  

> string.xml    

```xml
<resources>
    <string name="app_name">test001</string>
    <string-array name="months">
        <item>January</item>
        <item>February</item>
        <item>March</item>
        <item>April</item>
        <item>May</item>
        <item>June</item>
        <item>July</item>
        <item>August</item>
        <item>September</item>
        <item>October</item>
        <item>November</item>
        <item>December</item>
    </string-array>
</resources>
```

[go] "activity_main.xml" and create spinner   

> activity_main.xml    

```xml
<Spinner
    android:id="@+id/spMonths"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:entries="@array/months" // only for get values form string.xml
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.5"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintVertical_bias="0.5" />
```

let's see how to detect currently selected items.   
example show options from string.xml and runtime    

> MainActivity.kt

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
    Log.d("mainActivity", "this is our first log message");

    /* //////////////////////////////////////////////////////////////////
                      SET ITEMS ON RUNTIME

     //////////////////////////////////////////////////////////////// */

    // crate options list for spinner
    val customList = listOf<String>("First", "Second", "Third", "Fourth");
    // spinner is a view for that we need create adapter that list to spinner list
    val adapter = ArrayAdapter<String>(this, androidx.appcompat.R.layout.support_simple_spinner_dropdown_item, customList);
    spMonths.adapter = adapter;


    /* //////////////////////////////////////////////////////////////////
                    SET ITEMS FROM STRING.XML

    //////////////////////////////////////////////////////////////// */

    // we have to write class for onItemClickListener
    // press Ctrl+I for get override functions
    spMonths.onItemSelectedListener = object : AdapterView.OnItemSelectedListener {
        // change the params name for more understanding
        override fun onItemSelected(adapterView: AdapterView<*>?, view: View?, position: Int, id: Long) {
            // here we can't pass this because of inside anonymous class
          Toast.makeText(this@MainActivity, "You Selected ${adapterView?.getItemAtPosition(position).toString()}", Toast.LENGTH_LONG).show()
        }
        override fun onNothingSelected(adapterView: AdapterView<*>?) {
        }
    }

}
```

Now let's see how to set option in runtime    

### RECYCLERVIEW 
