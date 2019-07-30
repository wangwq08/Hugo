---
title: "Json数据类型转换"
date: 2019-07-30T08:29:59+08:00
draft: false
categories: ["Json"]
tags: ["Json","数据类型"]
---

## Json数据类型介绍

> [JSON](http://www.json.org/json-zh.html)(JavaScript Object Notation)是一种轻量级的数据交换格式。易于人阅读和编写。同时易于机器解析和生成。它是基于JavaScript Programming Language, Standard ECMA-263 3rd
Edition - December 1999的一个子集。JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C, C++, C#, JAVA, Java）。这些特性使JSON成为理想的数据交换语言。

## JSON与JS对象的关系

**JSON是JS对象的字符串表示法，它使用文本表示一个JS对象的信息，本质是一个字符串**

```JS
var obj = {a: "hello", b: "world"};  //这是一个对象，注意键名也是可以使用引号包裹
var json = '{"a": "hello", "b": "world"}';  //这是一个JSON字符串，本质上是一个字符串
```

## JSON数据类型的转换

现在的开发模式基本是采用前后端分离开发，这就涉及到数据传输的问题。多数数据传输的接口均使用Json格式。因此了解JSON格式数据转换，尤为重要。

第一次使用JSON格式的数据时候，就是在数据转换上走了很多弯路。现根据网络资源及实践经验整理如下常用的转换。

**主要使用包 fasterxml.jackson**

```java
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.JavaType;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.io.IOException;
import java.util.List;

public class JsonUtils {

    //定义Jackson对象
    private static final ObjectMapper MAPPER = new ObjectMapper();

    //将对象转换为Json字符串
    public static String ObjectToJson(Object data) {
        try {
            String string = MAPPER.writeValueAsString(data);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        return null;
    }

    //将json字符串转换为对象
    public static <T> T jsonToPojo(String jsonData, Class<T> beanType) {
        try {
            T t = MAPPER.readValue(jsonData, beanType);
            return t;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }

    //将json字符串对象转换成pojo对象list
    public static <T> List<T> jsonToList(String jsonData, Class<T> beantype) {
        JavaType javaType = MAPPER.getTypeFactory().constructParametricType(List.class, beantype);
        try {
            List<T> list = MAPPER.readValue(jsonData, javaType);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
}

```





