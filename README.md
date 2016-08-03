# ComicApi
暫定未命名的漫畫 API 參考文件

## 首頁

URL | 頁面 | 其他 
--- | --- | --- |
/ | 首頁 | 
[comic](#Comic) | 漫畫列表 | 
[tag](#Tag) | 標籤列 | 
[type](#Type) | 分類 |
[search](#Search) | 搜尋 |
[publish](#Publish) | 發布 |
[user](#User) | 使用者 |
[comment](#Comment) |留言 |

### <a name="Comic"></a>Comic 漫畫列表

URL | 頁面 | 其他 
--- | --- | --- |
/{Page} | 所有漫畫 | 
/comic/{ComicName} | 單一漫畫列表 |
/comic/{ComicName}/{ArticleID}/{Page} | 單一章節頁面 | 


#### JSON Response
>`/{Page}`

```
{
    "status": Status,
    "comics":[
        {
            "id":  id,
            "comicName": comic_name,
            "comicImg": comic_img,
            "tag": tag[Array],
            "typeId": type_id,
            "createUser": create_user,
            "lastUpdate": last_update,
            "allChapter": all_chapter,
            "create_time": create_time
        },
        ...
    ]
}
```
>`/comic/{ComicName}`

```
{
    "status": Status,
    "comic": {
       "id":  id,
        "comicName": comic_name,
        "comicImg": comic_img,
        "tag": tag[Array],
        "typeId": type_id,
        "createUser": create_user,
        "lastUpdate": last_update,
        "allChapter": all_chapter,
        "create_time": create_time
    },
    chapter: [
        {
            "article_id": article_id,
            "title": title,
            "all_page": page,
        },
        ...
    ]
}
```
>`/comic/{ComicName}/{ArticleID}/{Page}`

```
{
    "status": Status,
    "image": image_url,
    "next_page": next_page,
    "last_page": last_page,
    "is_end": is_end[bool]
}
```

### <a name="Tag"></a>Tag 標籤列表
URL | 頁面 | 其他 
--- | --- | --- |
/tag | Tag 列表 | 
/tag/{TagName}/{Page} | Tag 相關漫畫 | 

>`/tag`

```
{
    "status": Status,
    "tags": [
        {
            "tagId": tag_id,
            "tagName": tag_name,
        },
        ...
    ]
}
```
>`/tag/{TagName}/{Page}`

```
{
    "status": Status,
    "tag": {
            "tagId": tag_id,
            "tagName": tag_name,
    },
    "comics":[
        {
            "comicName": comic_name,
            "comicImg": comic_img,
            "tag": tag[Array],
            "typeId": type_id,
            "createUser": create_user,
            "lastUpdate": last_update,
            "allChapter": all_chapter,
            "create_time": create_time
        },
        ...
    ]
}
```

### <a name="Type"></a>Type 分類
URL | 頁面 | 其他 
--- | --- | --- |
/tag/ | Type分類表 |
/tag/{Type}/{Page} | 分類相關漫畫 |


### <a name="Search"></a>Search 搜尋
URL | 頁面 | 其他 
--- | --- | --- |
/search | 搜尋頁面 | 
/search/{SearchName}/{Page} | 顯示搜尋結果 |

> `/search`

`主頁提供熱度推薦，共10筆`

```
{
    "status": Status,
    comics: [
        {
            "comicName": comic_name,
            "comicImg": comic_img,
            "tag": tag[Array],
            "typeId": type_id,
            "lastUpdate": last_update,
            "allChapter": all_chapter,
            "create_time": create_time
        },
        ...(9)
    ]
}
```
> `/search/{SearchName}/{Page}`

```
    同主頁資料 (每頁15筆)
```

## 須提供帳號驗證

### <a name="Publish"></a>Publish 發佈漫畫
URL | 頁面 | 其他 
--- | --- | --- |
/publish/ | 發佈 | POST
/publish/{ComicName}/ | 發佈新章節 | POST

>`/publish`

類型 | 參數名稱 | 必須 
--- | --- | --- |
comicName | | ✔ ︎
```
```

### <a name="User"></a>User 帳號頁面
URL | 頁面 | 其他 
--- | --- | --- |
/user  | 帳號頁面 | 
/user/password/reset | 修改密碼 | PUT
/user/avatar/edit | 修改頭貼 | POST

>`/user`

```
{
    "status": Status,
    "profile": {
        "uid": uid,
        "name": user_name,
        "acountName": user_account,
        "avatar": user_avatar,
        "level": user_level
    }
}
```
>`/user/psword/reset`

```
{
    "status": Status,
    "msg": msg
}
```
>`/user/avatar/edit`

```
{
    "status": Status,
    "msg": msg
}
```

### <a name="Comment"></a>Comment 留言
URL | 頁面 | 其他 
--- | --- | --- |
