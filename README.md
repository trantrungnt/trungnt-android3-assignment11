# trungnt-android3-assignment11

##Yêu cầu
+ [Đọc RSS của VnExpress bằng Android](http://vnexpress.net/rss/tin-moi-nhat.rss) 
+ Hoàn thiện bài Asyc Task Read RSS 
+ Load ảnh lên Recycle View (có sử dụng thư viện load ảnh Picaso hoặc thư viện nào đó, đọc đường dẫn từ Link ảnh đọc được trong link RSS)

![BTVN Asyc Task Read RSS](http://i477.photobucket.com/albums/rr132/trungepu/AsyncTask-ReadRSS_zpsnfoobfpr.jpg)

##Demo code
+ [HIển thị danh sách Tin trong RSS, hiển thị ảnh đai diện của Bài viết dùng thư viện Picasso](https://youtu.be/XtxtWJ6mO7k)

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
+ Phương thức doInBackground của AsyncTaskXMLParrse có nhiệm vụ tải file rss (thường phương thức này xử lý những công việc nặng)
```
private class DownloadXmlTask extends AsyncTask<String, Void, String> {
        @Override
        protected String doInBackground(String... urls) {
            try {
                return loadXmlFromNetwork(urls[0]);
            } catch (IOException e) {
                return getResources().getString(R.string.connection_error);
            } catch (XmlPullParserException e) {
                return getResources().getString(R.string.xml_error);
            }
        }

        @Override
        protected void onPostExecute(String result) {
            recyclerView.setAdapter(new SimpleItemRecyclerViewAdapter(items));
        }
    }

    // Uploads XML from stackoverflow.com, parses it, and combines it with
// HTML markup. Returns HTML string.
    private String loadXmlFromNetwork(String urlString) throws XmlPullParserException, IOException {
        InputStream stream = null;
        // Instantiate the parser
        VnExpressXmlParser vnExpressXmlParser = new VnExpressXmlParser();
        String title = null;
        String url = null;
        String summary = null;
        Calendar rightNow = Calendar.getInstance();
        DateFormat formatter = new SimpleDateFormat("MMM dd h:mmaa");

        try {
            stream = downloadUrl(urlString);
            items = vnExpressXmlParser.parse(stream);
            // Makes sure that the InputStream is closed after the app is
            // finished using it.
        } finally {
            if (stream != null) {
                stream.close();
            }
        }

        return null;
    }

    // Given a string representation of a URL, sets up a connection and gets
// an input stream.
    private InputStream downloadUrl(String urlString) throws IOException {
        URL url = new URL(urlString);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setReadTimeout(10000 /* milliseconds */);
        conn.setConnectTimeout(15000 /* milliseconds */);
        conn.setRequestMethod("GET");
        conn.setDoInput(true);
        // Starts the query
        conn.connect();
        return conn.getInputStream();
    }
}
```

##Tham khảo
+ [XML Parse in Android](https://developer.android.com/intl/zh-tw/training/basics/network-ops/xml.html)
+ [Thư viện Picasso](http://square.github.io/picasso/)
+ [WebView in Android](http://www.mkyong.com/android/android-webview-example/)
+ [WebView](http://developer.android.com/intl/zh-tw/guide/webapps/webview.html)

##Môi trường phát triển
+ Bộ công cụ Android Studio 2.1
+ Máy ảo Genymotion dùng api 21

