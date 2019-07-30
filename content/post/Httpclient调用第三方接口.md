---
title: "Httpclient调用第三方接口"
date: 2019-07-30T14:07:09+08:00
draft: false
categories: ["HttpClient"]
tags: ["HttpClient", "接口调用"]
---

## 关于接口调用

由于现在的开发模式是前后端分离开发，且趋向于接口开发，微服务。在与第三方合作的过程中，往往是通过接口调用。这里就涉及到如何调用他人的接口问题。

本文主要介绍了，如何调用第三方接口，传输JSON格式数据。

## 主要使用依赖

```gradle
compile('org.apache.httpcomponents:httpclient');
```

## service

```java
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;

public class HttpClient {
    private CloseableHttpClient client;

    public String sendDataByPost(String url, String data) {
        
        Interger statusCode = -1;
        if(client == null) {
            client = new DefaultHttpClient();
        }

        try {
            HttpPost post = new HttpPost(url);
            StringEntity stringEntity = new StringEntity(data, "utf-8");
            post.setEntity(stringEntity);
            post.setHeader("Content-Type", "application/json");
            HttpResponse response = client.execute(post);
            HttpEntity httpEntity = response.getEntity();
            if(httpEntity != null) {
                String responsemessage = EntityUtils.toString(httpEntity, "utf-8");
                return responsemessage;
            }
        } catch (Exception e) {
            return e.toString();
        }
        return null;
    }
}
```

## Controller 调用

```java
public String sendData(String url, String data) {
    
    // 注意，需要把Json数据转换为String,否则会报错，无法识别
    // ObjectMapper mapper = new ObjectMapper();
    // String data = mapper.writeValueAsString(listData);
    HttpClient httpClient = new HttpClient();
    String response = httpClient.sendDataByPost(url,data);
    return response;
}
```

> 温馨的光景不过借出，到期拿回吗？





