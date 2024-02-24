# json-server-auth Fake API

## 參考說明


## 安裝方式

```js
npm install

npm start

// 成功訊息
// json-server-auth is running at http://localhost:3033 ~
```

## PORT 設定

```js
//server.js:1
const PORT: {port}
```

## Token 時效性
```
為 1 小時有效，過期顯示 "jwt expired"，需重新 POST /login/ 取得
```

## 預設 API 說明

<h3 id="Member">會員</h3>

#### 註冊

```js
-POST /signup/

// Request
{
    "email" : 必填，[唯一值],
    "password": 必填,
    // ... 其他可自訂欄位
}

// Responese
{
    "accessToken": Bearer Token,
    "user": {
        "email": email,
        // ... 若有其他欄位一並回傳
        "id": 系統產生 id，之後的 userId
    }
}
```

#### 登入

```js
-POST /login/

// Request
{
    "email" : 必填，唯一值,
    "password": 必填,
}

// Responese
{
    "accessToken": [Bearer Token],
    "user": {
        "email": email,
        "id": 系統產生 id，之後的 userId
    }
}
```

#### 修改會員資料

```js
-PATCH /users/{userId}
Header Authorization: Bearer [Token]

// Request
{
    // 欲修改欄位....
    "name": "new Name"
}

// Responese
 {
    "email": email,
    "password": password,
    "id": userId
    // ... 其他自定義欄位
}
```

#### 刪除會員資料 (無法恢復)

```js
-DELETE /users/{userId}
Header Authorization: Bearer {Token}

// Responese
{}
```

####

---

<h3 id="Dishes">菜餚</h3>

#### 菜餚全部列表

```js
-GET /api/dishes/all

// Responese
[
    {
        "id": "1",
        "title": "蔥爆牛肉",
        "engTitle": "Stir-fried Beef with Scallions",
        "healthLevel": 4.5,
        "starchPortion": 0,
        "proteinPortion": 0.25,
        "vegetablePortion": 0.5,
        "img": "https://res.cloudinary.com/dfvtounam/image/upload/v1707714590/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2_2024-02-12_130924_mbdgp0.png",
        "noBgImg": ""
    },
    {
        "id": "2",
        "title": "紅燒獅子頭",
        "engTitle": "Braised Lion's Head (pork balls)",
        "healthLevel": 4.5,
        "starchPortion": 0,
        "proteinPortion": 0.25,
        "vegetablePortion": 0.5,
        "img": "https://res.cloudinary.com/dfvtounam/image/upload/v1707714590/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2_2024-02-12_130924_mbdgp0.png",
        "noBgImg": ""
    },
    // ....
]

```


#### 新增菜餚

```js
-POST /api/admin/dishes/
Header Authorization: Bearer {Token}

// Request
{
    "title": "中文菜名",
    "engTitle": "英文菜名",
    "category": "主食類 | 配菜類 | 主菜類",
    "healthLevel": "number (1~5，0.5為間隔)",
    "starchPortion": "0.25 | 0.33 | 0.5 | 0.66 | 0.75 | 1 | ...",
    "proteinPortion": "0.25 | 0.33 | 0.5 | 0.66 | 0.75 | 1 | ...",
    "vegetablePortion": "0.25 | 0.33 | 0.5 | 0.66 | 0.75 | 1 | ...",
    "img": "url",
    "noBgImg": "url (僅有主菜類需要此屬性)"
    // ... 可自訂義欄位
}

// Response
{
    "success": true,
    "message": {
        "title": title,
        "engTitle": engTitle,
        "category": category,
        "healthLevel": healthLevel,
        "starchPortion": starchPortion,
        "proteinPortion": proteinPortion,
        "vegetablePortion": vegetablePortion,
        "img": img,
        "noBgImg": noBgImg
        // ... 可自訂義欄位
        "id": 自動生成 | 時間戳記
    }
}
```

#### 修改菜餚

```js
-PATCH /api/admin/dishes/{dishId}
Header Authorization: Bearer {Token}

// Request
{
    "title": title,
    "engTitle": engTitle,
    "category": category,
    "healthLevel": healthLevel,
    "starchPortion": starchPortion,
    "proteinPortion": proteinPortion,
    "vegetablePortion": vegetablePortion,
    "img": img,
    "noBgImg": noBgImg
}

// Response
{
    "title": title,
    "engTitle": engTitle,
    "category": category,
    "healthLevel": healthLevel,
    "starchPortion": starchPortion,
    "proteinPortion": proteinPortion,
    "vegetablePortion": vegetablePortion,
    "img": img,
    "noBgImg": noBgImg
    // ... 可自訂義欄位
    "id": 系統自動產生
}
```

#### 刪除菜餚

```js
-DELETE /api/admin/dishes/{dishId}
Header Authorization: Bearer {Token}

// Response
{
    "success": true,
    "message": {}
}
```

####
