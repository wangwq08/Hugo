---
title: "批量图片生成PDF文档"
date: 2019-08-03T15:50:49+08:00
draft: false
categories: ["图片"]
tags: ["图片","PDF"]
---

## 前言

之前有一个朋友，提出一个需求。希望把微信推文生成PDF文档保存在本地。

## 分析

* 首先查看微信推文的内容，发现每一页推文是一张图片。

* 进一步分析页面代码发现每张图片均有一个地址URL，并且可以访问。

* 每一张图片的地址都相同，并且图片命名均为序号。

* 使用循环，就可以实现批量图片的下载，保存在本地。

* 然后循环读取本地的图片，写入PDF格式文档。

## 实现

**编写一个调用接口的server类**

```java
/**
* @Description: 调用接口的封装方法
* @Author: wangwq
* @CreateDate: 2019/08/04 17:44
*/
public HttpEntity getImgDataByGet(String url, String data) {
    CloseableHttpClient  client = null;
    
    if(client == null) {
        client = new DefaultHttpClient();
        HttpHost proxy = new HttpHost("address", port);  //这里设置代理，如果是外网环境可以不用设置。
        client.getParams().setParameter(ConnRouteParams.DEFAULT_PROXY, proxy);
    }

    try {
        HttpGet get= new HttpGet(url);
        StringEntity stringEntity = new StringEntity("data="+data);
        get.setHeader("Content-Type", "application/javascript;charset=GBK");
        HttpResponse response = client.execute(get);
        HttpEntity httpEntity = response.getEntity();

        if (httpEntity != null) {
            return httpEntity;
        }
    } catch (Exception e) {
        e.printStackTrace();
    }

    return null;
}
```

**编写一个调用接口批量下载图片的controller类**

```java
/**
* @Description: 批量获取图片
* @Author: wangwq
* @CreateDate: 2019/08/04 16:46
*/
@Component
@RestController
@ReaquestMapping(value = "api/")
public class JpgToPdf {
    String url = "https://book.yunzhan365.com/poui/pudn/files/mobile/" ;  //图片的url地址
    String path = "D:/heimage/";   //保存到本地的地址

    private final Logger logger = LoggerFactory.getLogger(this.getClass());  //日志

    /**
    * @Description 调用图片接口获取图片
    * @Author: wangwq
    * @CreateDate: 2019/08/04 16:57
    */
    @GetMapping(value = "getimage")
    public String getImage() throws IOException {
        HttpClient client = new HttpClient(); //new 一个client对象
        logger.info("start load image...");
        
        for (int i = 1; i < 69; i++) {   //for循环调用接口下载图片
            String imgurl = url + i + ".jpg";  //拼接url地址
            HttpEntity httpEntity = client.getImgDataByGet(imgurl, "");  //获取接口返回信息
            byte[] b = EntityUtils.toByteArray(httpEntity);
            FileOutputStream fos = new FileOutputStream(path + i + ".jpg");  //图片输出到本地
            fos.write(b);
            fos.close();
        }
        logger.info("loading end!");
        return "Loading success!";
    }
}
```

**批量读取本地文档输出PDF文档**

```java
/**
* @Description 读取批量图片生成PDF
* @Author: wangwq
* @CreateDate: 2019/08/04 17:13
*/
public static void toPdf(String imageFolderPath, String pdfPath) throws DocumentException {
    try {
        String imagepath = null;
        FileOutputStream fos = new FileOutputStream(pdfPath);  //设置pdf的保存路径
        Document doc = new Document(null,0,0,0,0);
        PDFWriter/getInstance(doc, fos);
        BufferedImage img = null;
        Image image = null;
        File file = new File(imageFolderPath);
        File[] files = files.listFiles();

        doc.setPageSize(new Rectangle(1366, 122400));  //设置pdf宽度和总长度

        for (int i = 1; i < 69; i++) {
            imagepath = imageFolderPath + i + ".jpg";  //拼接每一张图片的地址
            doc.setPageSize(new Rectangle(1366, 1800)); //设置每一页的宽度和高度
            image = Image.getInstance(imagepath); //根据路径读取图片
            doc.open();
            doc.add(image);  //将图片添加到pdf文档中。
        }
        doc.close();  //关闭文档
    } catch (IOException e) {
        e.printStackTrace();
    }
}

```

**编写一个静态主类方法调用测试**

```java
public static void main(String[] args) throws DocumentException {
    long starttime = System.currentTimeMillis();
    
    String imgpath = "D:/heimage/";   //存放图片的地址
    Stirng pdfpath = "D:/heimage/feidao.pdf";  //存放pdf的位置
    toPdf(imgpath,pdfpath);

    long endtime = System.currentTimeMillis();

    int time = (int)((endtime - starttime)/1000);

    System.out.println("The program runs: " + time + "s");
}
```
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=700 height=86 src="//music.163.com/outchain/player?type=2&id=472129311&auto=1&height=66"></iframe>

> 外面的世界，很精彩。外面的世界，很无奈。