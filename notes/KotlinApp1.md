---
tags: [Notebooks/Android]
title: KotlinApp1
created: '2020-06-21T13:09:32.778Z'
modified: '2020-06-21T13:12:51.150Z'
---

# KotlinApp1
- Cách thiết lập view và ViewGroup

__MainActivity.kt__
```kt
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.text.Layout
import android.widget.Button
import android.widget.FrameLayout
import android.widget.TextView
import androidx.constraintlayout.widget.ConstraintLayout

class MainActivity : AppCompatActivity() {

    // Khai báo các view
    lateinit var txtHelloWorld: TextView
    lateinit var btnClickMe: Button
    lateinit var layoutMain: ConstraintLayout
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        // Thiết lập layout
        layoutMain = findViewById(R.id.layoutMain)

        // Tạo view truyền thống - tạo trong file .xml => sử dụng findView để lấy ra view sử dụng
        txtHelloWorld = findViewById(R.id.txtHelloWorld)
        txtHelloWorld.setText("This is first project with Kotlin")

        // Tạo view bằng code: tạo trực tiếp bằng code => load vào view bằng method addView
        btnClickMe = Button(this)
        btnClickMe.setText("Click me")
        layoutMain.addView(btnClickMe) // add button to frameLayout

    }
}
```

__activity_main.xml__
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:id="@+id/layoutMain"
    >

    <TextView
        android:id="@+id/txtHelloWorld"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

