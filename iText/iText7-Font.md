# iText 7 Font


> 传统意义上，每个阅读器应该识这14种字体，这14种字体也是标准的Type 1字体。每个阅读器不能使用与声明字体一样的字体，但是会使用和声明字体看起来完全一样的字体。
> - 四种Helvetica字体(normal,bold,oblique和bold-oblique，也就是普通，加粗，斜体和加粗斜体), 
> - 四种Times-Roman字体(normal,bold,italic和bold-italic,italic也是斜体，和oblique的区别就是：italic是斜体字，对于没有斜体的字体应该使用oblique属性来实现倾斜的文字效果)，
> - 四种Courier字体(normal,bold,oblique和bold-oblique)，
> - Symbol符号以及Zapfdingbats(这个暂时不知道怎么翻译，先放着，估计是专门的术语吧)。



### 导入字体

- 方法一：使用Windows系统字体（TrueType）
```java
PdfFont yaHei = PdfFontFactory.createFont("c://windows//fonts//msyh.ttc,0", PdfEncodings.IDENTITY_H,false); //微软雅黑
```
- 方法二：使用iText自带字体
```java
PdfFont song = PdfFontFactory.createFont("STSongStd-Light", "UniGB-UCS2-H", true);//华文宋体
```
- 方法三：使用资源字体（classPath）
```java
PdfFont font = PdfFontFactory.createFont("src/main/resources/PingFang-SC-Regular.ttf", PdfEncodings.IDENTITY_H, false);//苹方字体
```
- 方法四：IO流加载资源字体（classPath）
```java
InputStream inputStream = ItextPDFExportUtil.class.getResourceAsStream("/simfang.ttf");
PdfFont font = PdfFontFactory.createFont(IOUtils.toByteArray(inputStream), PdfEncodings.IDENTITY_H, false);
```



## Error

- 错误：Font 'C:\WINDOWS\FONTS\msyh.ttc' with 'Identity-H' is not recognized

解决方案：
```java
PdfFont yaHei = PdfFontFactory.createFont("c://windows//fonts//msyh.ttc,0", PdfEncodings.IDENTITY_H,false); //微软雅黑
```
在字体路径的后面加了一个“,0”解决了，虽然不知道为什么，但是猜测这个是字体组有关，因为雅黑有三种，常规、加粗、极细






## Resource 
- https://www.cnblogs.com/albertay/p/6610667.html