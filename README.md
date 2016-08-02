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
    {
        "id":  id,
        "title": title,
        "tag": tag[Array],
        "typeid": typeid,
        "last_update": last_update,
        "all_chapter": all_chapter
    },
    ...
}
```
>`/comic/{ComicName}`

```
{
    "info": {
        "id":  id,
        "title": title,
        "tag": tag[Array],
        "typeid": typeid,
        "last_update": last_update,
        "all_chapter": all_chapter
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
    "image": image_url,
    "next_page": next_page,
    "last_page": last_page,
    "is_end": is_end[bool]
}
```

### <a name="Tag"></a>Tag 標籤列表
URL | 頁面 | 其他 
--- | --- | --- |
/ | Tag 列表 | 
/{TagName}/{Page} | Tag 相關漫畫 | 


### <a name="Type"></a>Type 分類
URL | 頁面 | 其他 
--- | --- | --- |
/tag/ | Type分類表 |
/tag/{Type}/{Page} | 分類相關漫畫 |


### <a name="Search"></a>Search 搜尋
URL | 頁面 | 其他 
--- | --- | --- |
/search/search/ | 搜尋頁面 | 
/search/search/{SearchName}/{Page} | 顯示搜尋結果 |

``主頁提供熱度推薦``

## 須提供身分驗證

### <a name="Publish"></a>Publish 發佈漫畫
URL | 頁面 | 其他 
--- | --- | --- |
/publish/ | 發佈 |
/publish/{ComicName}/ | 發佈新章節 |

### <a name="User"></a>User 帳戶頁面
```
todo
```
