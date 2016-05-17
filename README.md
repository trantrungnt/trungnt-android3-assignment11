# trungnt-android3-assignment11

##Yêu cầu
+ [Đọc RSS của VnExpress bằng Android](http://vnexpress.net/rss/tin-moi-nhat.rss) 
+ Hoàn thiện bài Asyc Task Read RSS 
+ Load ảnh lên Recycle View (có sử dụng thư viện load ảnh Picaso hoặc thư viện nào đó, đọc đường dẫn từ Link ảnh đọc được trong link RSS)

![BTVN Asyc Task Read RSS](http://i477.photobucket.com/albums/rr132/trungepu/AsyncTask-ReadRSS_zpsnfoobfpr.jpg)

<<<<<<< HEAD
##Demo code
+ [HIển thị danh sách Tin trong RSS, hiển thị ảnh đai diện của Bài viết dùng thư viện Picasso](https://youtu.be/XtxtWJ6mO7k)
=======
##Chú ý khi code
+ Cắt chuỗi có chứa thẻ HTML: để lấy link ảnh, ta dùng phương thức indexOf để lấy vị trí cắt, sau đó ta dùng thư viện Picasso để load ảnh từ URL của ảnh vừa lấy được để hiển thị ảnh trong ImageView: holder.image 
```
//tim link anh jpg va cat chuoi, sau do load anh jpg voi thu vien Picasso
  int startDescription = description.indexOf("src=\"http://");
  int endDescription = description.indexOf(".jpg");
  final String urlImage = description.substring(startDescription + 5, endDescription + 4);
  Picasso.with(holder.image.getContext()).load(urlImage).into(holder.image);
```

+ Để dùng được thư viện Picasso trong project, ta điền dòng này trong file build.gradle (Module: app) và sync về để cài thư viện trong Project
```
   compile 'com.squareup.picasso:picasso:2.5.2'
```
>>>>>>> origin/master

##Tham khảo
+ [XML Parse in Android](https://developer.android.com/intl/zh-tw/training/basics/network-ops/xml.html)
+ [Thư viện Picasso](http://square.github.io/picasso/)
+ [WebView in Android](http://www.mkyong.com/android/android-webview-example/)
+ [WebView](http://developer.android.com/intl/zh-tw/guide/webapps/webview.html)

##Môi trường phát triển
+ Bộ công cụ Android Studio 2.1
+ Máy ảo Genymotion dùng api 21

