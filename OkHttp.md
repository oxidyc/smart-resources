# OkHttp - 轻量的Java网络请求框架

## Introduce
An HTTP & HTTP/2 client for Android and Java applications.

OkHttp supports Android 5.0+(API level 21+) and Java 8+

Home：http://square.github.io/okhttp/ 或 https://github.com/square/okhttp
## Download
- Maven
```xml
<dependency>
  <groupId>com.squareup.okhttp3</groupId>
  <artifactId>okhttp</artifactId>
  <version>3.12.1</version>
</dependency>
```
- Gradle
```gradle
implementation("com.squareup.okhttp3:okhttp:3.12.1")
```

## Examples
- Get a URL
```java
OkHttpClient client = new OkHttpClient();

String run(String url) throws IOException {
  Request request = new Request.Builder()
      .url(url)
      .build();

  try (Response response = client.newCall(request).execute()) {
    return response.body().string();
  }
}
```
- Post to a server
```java
public static final MediaType JSON
    = MediaType.get("application/json; charset=utf-8");

OkHttpClient client = new OkHttpClient();

String post(String url, String json) throws IOException {
  RequestBody body = RequestBody.create(JSON, json);
  Request request = new Request.Builder()
      .url(url)
      .post(body)
      .build();
  try (Response response = client.newCall(request).execute()) {
    return response.body().string();
  }
}
```