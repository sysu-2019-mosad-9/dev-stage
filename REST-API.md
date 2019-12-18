# REST API DOC [ /api/v1 ]

**Global Base URL** ```http://localhost:8000/api/v1```

在运行 curl 例子前请在shell环境中设置变量`$BASE_URL`:
```shell
export BASE_URL=localhost:8000/api/v1
```

或者人眼替换`$BASE_URL`

## 应用首页 [ /base ]

---

### 获取Tab标签名

**GET** ```/news/tabs```

#### Response

```json
{
  "code": 200,
  "data": {
    "len": number,
    "names": string[],
  },
}
```

#### Sample
```shell
curl -XGET "$BASE_URL/news/tabs"
```
---

### 获取若干新闻标题

**GET** ```/news/<tabIndex>/titles?<count>```

+ count - 请求至多几条新闻标题。返回数量可能不足`count`。

#### Response

```json
{
  "code": 200,
  "data": {
    "count": number,
    "titles": string[],
  },
}
```

  + count - 实际返回多少条标题。

#### Sample

```shell
curl -XGET "$BASE_URL/news/1/titles?count=3"
```
---

### 获取若干新闻预览图URL

**GET** ```/news/<tabIndex>/images?<count>&<most>```

+ count - 请求至多几条新闻的预览图。返回数量可能不足`count`。
+ most - 每条新闻至多返回多少张预览图。

#### Response

```json
{
  "code": 200,
  "data": {
    "count": number,
    "payload": {
      "each": number,
      "urls": string[],
    }[],
  }
}
```

#### Sample

```shell
curl -XGET "$BASE_URL/news/1/images?count=2&most=3"
```

```json
{
   "payload" : [
      {
         "each" : 3,
         "urls" : [
            "https://zh.moegirl.org/File:215%E6%BB%A1%E7%A0%B4.png",
            "https://img.moegirl.org/common/thumb/2/2b/Liangyishi_houqi_A.jpg/300px-Liangyishi_houqi_A.jpg",
            "https://img.moegirl.org/common/thumb/2/2b/Liangyishi_houqi_A.jpg/300px-Liangyishi_houqi_A.jpg"
         ]
      },
      {
         "each" : 2,
         "urls" : [
            "https://img.moegirl.org/common/thumb/2/2b/Liangyishi_houqi_A.jpg/300px-Liangyishi_houqi_A.jpg",
            "https://img.moegirl.org/common/thumb/2/2b/Liangyishi_houqi_A.jpg/300px-Liangyishi_houqi_A.jpg",
         ]
      }
   ],
   "count" : 2
}

```

## 图片页 [ /photo ]

## 视频页 [ /video ]