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

### 获取若干新闻预览信息

**GET** ```/news/<tabIndex>/entry?<count>&<img_most>```

+ count - 请求至多几条新闻标题。返回数量可能不足`count`。

#### Response

```json
{
  "code": 200,
  "data": {
    "count": number,
    “data”: {
      “id”: number,
      "title": string,
      "image_links": string[],
      "detail_url": string,
    }[],
  },
}
```

#### Sample

```shell
curl -XGET "$BASE_URL/news/1/entries?count=3&img_most=3"
```

### 获取新闻详情页数据

**GET** ```/news/details/<newsIndex>```

+ newsIndex - 使用上一条请求返回的`data.data.id`字段

#### Response

```json
{
  "code": 200,
  "data": {
    "count": number,
    "data": {
      "type": "typography" | "image",
      "content": string,
    }[],
  }
}
```

+ 当 `data.type = "typography"`时，`data.content`为原始内容字符串
+ 当 `data.type = "image"` 时，`data.content`为图片URL

#### Sample

```shell
curl -XGET "$BASE_URL/news/details/1"
```

## 图片页 [ /photo ]

### 获取图片预览信息

**GET** ```/photo/entries?<count>```

#### Response

```json
{
  "code": 200,
  "data": {
    "count": number,
    "data": {
      "title": string,
      "image_link": string,
    }[],
  }[],
}
```

#### Sample

```shell
curl -XGET "$BASE_URL/photo/entries?count=5"
```

## 视频页 [ /video ]

### 获取视频预览信息

**GET** ```/video/entries?<count>```

#### Response

```json
{
  "code": 200,
  "data": {
    "count": number,
    "data": {
      "id": number,
      "title": string,
      "author": string,
      "video_link": string,
      "n_good": number,
      "n_comment": number,
    }[],
  }
}
```

#### Sample

```shell
curl -XGET "$BASE_URL/video/entries?count=5"
```