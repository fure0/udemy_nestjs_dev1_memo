## @Request() req: ExpressRequest & { user: RequestUser }

## 型定義の分析

### @Request()
- 役割: NestJSでHTTPリクエストオブジェクトを注入するデコレーター
- 結果: req変数に全体のリクエスト情報が格納される

### ExpressRequest & { user: RequestUser }
- 型: TypeScriptのインターセクション型 (交差型)
- 意味: Expressの基本Request型 + ユーザー情報が追加されたカスタム型


## 各型の意味

### ExpressRequest
- Express.jsの基本リクエストオブジェクト型
- ヘッダー、クエリ、ボディ、クッキーなどHTTPリクエストの全ての情報を含む

### { user: RequestUser }
- JWT認証後に追加されるユーザー情報
- req.userにユーザーデータが保存される

## 全体構造の理解

### RequestUser型:
```typescript
{
  id: string;        // ユーザー固有ID
  name: string;      // ユーザー名  
  status: UserStatus; // ユーザーステータス
}
```

### 最終的なreqオブジェクト:
```typescript
{
  // Express基本プロパティ
  headers: {...},
  body: {...},
  query: {...},
  params: {...},
  
  // JWT認証後に追加されるユーザー情報
  user: {
    id: "user-uuid-here",
    name: "ユーザー名",
    status: "ACTIVE"
  }
}
```