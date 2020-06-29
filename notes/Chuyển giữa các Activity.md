---
attachments: [Clipboard_2020-06-21-20-18-09.png]
favorited: true
tags: [Notebooks/Android]
title: Chuyển giữa các Activity
created: '2020-06-21T13:13:10.245Z'
modified: '2020-06-21T14:27:28.558Z'
---

# 2. Chuyển giữa các Activity
- Mỗi khi ta muốn thực hiện nhảy qua một activity nào đó => ta dùng <mark>intent</mark>
![](@attachment/Clipboard_2020-06-21-20-18-09.png)

<details close>
<summary>Kịch bản 1: Mở một activity khác</summary>
<markdown>
- Step 1. MainActivity: tạo một intent để chuyển sang second activity
- Step 2. SecondActivity: activity thứ 2

```kt
public void onClick(View view) {
    Log.e(Tag, "Goto new screen");
    // Tạo một intent
    Intent intentGotoNewScreen = new Intent(MainActivity.this, SecondActivity.class);
    startActivity(intentGotoNewScreen);
}
```
</markdown>
</details>

<details close>
<summary>Kịch bản 2: Truyền dữ liệu từ MainActivity sang SecondActivity</summary>
<markdown>
```kt
@Override
public void onClick(View view) {
    Log.e(Tag, "Goto new screen");
    // Tạo một intent
    Intent intentGotoNewScreen = new Intent(MainActivity.this, SecondActivity.class);

    // Gửi đi dữ liệu tới activity second theo key-value
    intentGotoNewScreen.putExtra("key1", "value1");
    intentGotoNewScreen.putExtra("key2", "value2");

    // start Activity 2
    startActivity(intentGotoNewScreen);
}
```

```kt
// Dữ liệu được bọc trong lớp bundle khi chuyển giữa các activity
Bundle extraInfomation = getIntent().getExtras();

// lấy ra theo keyword
String key1 = extraInfomation.getString("key1");
String key2 =  extraInfomation.getString("key2");

Log.e(Tag, key1);
Log.e(Tag, key2);
```

</markdown>
</details>

<details open>
<summary>Kịch bản 3: Nhận thông tin ngược lại</summary>
<markdown>
- Đóng một Activity
  - Cách 1: close khi mà ta ấn nút back trên điện thoại => tương đương gọi tới method <mark>this.finish()</mark>
  - Cách 2: gọi trực tiếp method <mark>this.finish()</mark>
```kt
// class MainActivity.java

public void onClick(View view) {
    Log.e(Tag, "Goto new screen");
    // Tạo một intent
    // Activity thứ 2 được coi là sub-activity
    Intent intentGotoNewScreen = new Intent(MainActivity.this, SecondActivity.class);

    int REQUEST_CODE = 9;
    // khởi động activity số 2 và yêu cầu trả về dữ liệu REQUEST_CODE
    startActivityForResult(intentGotoNewScreen, REQUEST_CODE);
}


// ....
// Override lại method để lấy kết quả trả về từ Activity 2
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (resultCode == RESULT_OK && requestCode == 9) {
        if (data.hasExtra("returnKey1")) {
            Toast.makeText(this, data.getExtras().getString("returnKey1"),
                    Toast.LENGTH_SHORT).show();
        }
    }
}
```

```kt
// SecondActivity.java

// Override lại method finish() để xử lý khi close lại activity
@Override
public void finish() {
    // Tạo một intent mang dữ liệu để trả về cho activity cha
    Intent data = new Intent();
    data.putExtra("returnKey1", "Swinging on a star. ");
    data.putExtra("returnKey2", "You could be better then you are. ");
    setResult(RESULT_OK, data);
    super.finish();
}
```
</markdown>
</details>

