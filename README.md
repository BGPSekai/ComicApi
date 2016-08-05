# ComicApi
暫定未命名的漫畫 API 參考文件

# Prefix
>api/

## 首頁

URL | 頁面 | 其他 
--- | --- | --- |
 | 首頁 | 
[auth](#Auth) | JWT 認證 |
[comic](#Comic) | 漫畫列表 | 
[tag](#Tag) | 標籤列 | 
[type](#Type) | 分類 |
[search](#Search) | 搜尋 |
[publish](#Publish) | 發布 |
[service](#Service) | 服務 |
[user](#User) | 使用者 |
[comment](#Comment) |留言 |

### <a name="Auth"></a> JWT 認證
URL | 頁面 | 其他 
--- | --- | --- |
/auth | JWT | POST

>`/auth`

類型 | 參數名稱 | 必須
--- | --- | --- |
String | email | ✔
String | password | ✔

>success

```
{
    "token": *token*
}
```

>error

```
{
    "error": "invalid_credentials"
}
```

-----or-----

```
{
    "error": "could_not_create_token"
}
```


### <a name="Comic"></a>Comic 漫畫列表

URL | 頁面 | 其他 
--- | --- | --- |
/comic/{Page} | 所有漫畫 | 
/comic/{ComicName} | 單一漫畫列表 |
/comic/{ComicName}/{ArticleID}/{Page} | 單一章節頁面 | 
/comic/tag/{TagName}/{page} | 顯示某 Tag 所有漫畫 |
/comic/type/{TypeName}/{page} | 顯示某 Tyoe 所有漫畫 |

#### JSON Response
>`/comic/{Page}`

```
{
    "status": Status,
    "comics":[
        {
            "id":  id,
            "comicName": comic_name,
            "comicImg": comic_img,
            "comicSummary": comic_summary,
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
        "comicSummary": comic_summary,
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
>`/comic/tag/{TagName}/{page}`

```
TODO
```

>`/comic/type/{TypeName}/{page}`

```
TODO
```

### <a name="Tag"></a>Tag 標籤列表
URL | 頁面 | 其他 
--- | --- | --- |
/tag | Tag 列表 | 
/tag/{TagName}/{Page} | Tag 相關漫畫 | 

#### JSON Response
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
            "comicSummary": comic_summary,
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

#### JSON Response
> `/tag`

```
{
    "status": Status,
    "tags": [
        {
            "id": id,
            "name": name
        },
        ...
    ]
}
```

### <a name="Search"></a>Search 搜尋
URL | 頁面 | 其他 
--- | --- | --- |
/search | 搜尋頁面 | 
/search/{SearchName}/{Page} | 顯示搜尋結果 |

#### JSON Response
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
### <a name="Service"></a>Service 服務
URL | 頁面 | 其他 
--- | --- | --- |
/service/register | 註冊帳號 | POST
/service/forgot_password | 忘記密碼 | POST

#### JSON Response
>`/service/register`

類型 | 參數名稱 | 必須 
--- | --- | --- |
String | email | ✔
String | password | ✔
String | password_confirmation | ✔
String | name | ✔

>success

```
{
    "status": "success",
    "msg": "Register successful."
}
```

>error

```
{
    "status": "error",
    "msg": *msg[Array]*
}
```

>`/service/forgot_password`

類型 | 參數名稱 | 必須 
--- | --- | --- |
String ︎|︎ email | ✔ 
String | password | ✔

>success

```
{
    "status": "success",
    "token": token
}
```

>error

```
{
    "status": "error",
    "msg": msg
}
```


## 須提供帳號驗證

### <a name="Publish"></a>Publish 發佈漫畫
URL | 頁面 | 其他 
--- | --- | --- |
/publish/ | 發佈 | POST
/publish/chapter/{ComicName}/ | 發佈新章節 | POST

#### JSON Response
>`/publish`

類型 | 參數名稱 | 必須 
--- | --- | --- |
String | comicName | ✔ ︎
File | comicCoverImg | ✔
String | comicSummary | ✔ (最少 30 字)
```
{
    "status": Status
    "info": {
        "id": id,
        "coverImgUrl": cover_img_url
    }
}
```

>`/publish/chapter/{ComicName}/`

類型 | 參數名稱 | 必須 
--- | --- | --- |
Integer | chapter | 
String ︎|︎ ︎︎chapterName | ✔ 
String | authorComment |
File |  chapterCoverImg | ✔
Files |  comicImgs | ✔ Muti

```
{
    "status": Status,
    "msg": msg
}
```

### <a name="User"></a>User 帳號頁面
URL | 頁面 | 其他 
--- | --- | --- |
/user  | 帳號頁面 | 
/user/password/reset | 修改密碼 | PUT
/user/avatar/edit | 修改頭貼 | POST

#### JSON Response
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
`可以考慮使用臉書留言板 (有好有壞) `
URL | 頁面 | 其他 
--- | --- | --- |
/comment/{ComicId} | 顯示某漫所有留言 |
/comment/{ComicId}/{Chapter} | 顯示某漫章節留言  |
/comment/{ComicId}/{Chapter}/add | 添加某漫章節留言 |
/comment/{CommentId}/edit | 修改某漫留言  | PUT
/comment/{CommentId}/delete | 刪除某漫留言 | DELETE

#### JSON Response
>`/comment/{ComicId}`

```
{
    "status": Status,
    comics: [
        "userName": user_name,
        "userId": user_id,

    ]
}
```


```
 TODO
```