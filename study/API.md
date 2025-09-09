```next.js
import { NextRequest, NextResponse } from 'next/server';
```

#### NextRequest とは
```next.js
// ブラウザからのリクエスト情報を扱う道具
function GET(request: NextRequest) {
  // request の中に以下の情報が入っている：
  // - どのURLにアクセスしたか
  // - どんなパラメータ（?tag=TypeScript）が付いているか  
  // - どんなデータを送ってきたか
}
```

#### NextResponse とは
```next.js
// ブラウザに返事を送る道具
return NextResponse.json({
  success: true,
  data: filteredPosts
});
// ↑ これでブラウザに「JSON形式で返事を送る」
```

### 取得の場合
```next.js
export async function GET(request: NextRequest): Promise<NextResponse<ApiResponse<BlogPost[]>>> {
//ApiResponse<BlogPost[]までは全てGETの定型文
```

#### 他のAPIでの例
ユーザー情報API
```next.js
// ユーザー一覧を取得
export async function GET(request: NextRequest): Promise<NextResponse<ApiResponse<User[]>>> {

// ユーザー1人を取得  
export async function GET(request: NextRequest): Promise<NextResponse<ApiResponse<User>>> {
```

商品情報API
```next.js
// 商品一覧を取得
export async function GET(request: NextRequest): Promise<NextResponse<ApiResponse<Product[]>>> {

// 商品1つを取得
export async function GET(request: NextRequest): Promise<NextResponse<ApiResponse<Product>>> {
```

### 作成・更新の場合
```next.js
export async function POST(request: NextRequest): Promise<NextResponse<ApiResponse<データ型>>> {
```

### GET用テンプレート
```next.js
export async function GET(request: NextRequest): Promise<NextResponse<ApiResponse<データ型>>> {
  try {
    // 処理を書く
    return NextResponse.json({
      success: true,
      data: 結果
    });
  } catch (error) {
    return NextResponse.json({
      success: false,
      error: 'エラーメッセージ'
    }, { status: 500 });
  }
}
```

