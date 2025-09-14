## 🤔 Promiseオブジェクトとは  
Promise は「未来のある時点で結果が手に入る」という約束を表すオブジェクト
普通の処理（同期処理）
```next.js
const result = 5 + 3;  // すぐに結果が出る
console.log(result);   // 8
```

時間のかかる処理（非同期処理）
```next.js
javascriptconst promise = fetch('/api/posts');  // すぐには結果が出ない
console.log(promise);  // Promise { <pending> }  ← これがPromiseオブジェクト
```

#### 🕐 Promise: 3つの状態がある
```next.js
// 1. pending（処理中）
const promise = fetch('/api/posts');
console.log(promise);  // Promise { <pending> }

// 2. fulfilled（成功）
// データが取得できた状態

// 3. rejected（失敗）  
// エラーが発生した状態
```

#### 🎁 Promise の中身を取り出す方法
1. await を使う方法
```next.js
// ❌ Promise オブジェクトのまま
const promise = fetch('/api/posts');
console.log(promise);  // Promise { <pending> }

// ✅ await で中身を取り出す
const response = await fetch('/api/posts');
const data = await response.json();
console.log(data);     // 実際のデータ
```

2. .then() を使う方法
```next.js
fetch('/api/posts')
  .then(response => response.json())
  .then(data => {
    console.log(data);  // 実際のデータ
  });
```

#### 🏪 日常生活の例
レストランでの注文
```next.js
// 注文する（非同期処理の開始）
const orderPromise = restaurant.order('カレーライス');
console.log(orderPromise);  // Promise { <pending> } "調理中..."

// 完成を待つ（await）
const curry = await orderPromise;
console.log(curry);  // "できたてのカレーライス"
```

#### 🌐 なぜ request.json() がPromise？
JSONの解析は時間がかかる
```next.js
// リクエストボディが大きい場合、解析に時間がかかる
const body = request.json();  // Promise オブジェクト（解析中...）

// awaitで解析完了を待つ
const body = await request.json();  // 解析されたデータ
```

🎯 つまり  
Promise = 「今すぐじゃないけど、後で結果をくれる約束」
```next.js
// Promise を返す関数
function cookRice() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('ご飯が炊けました！');
    }, 3000);  // 3秒後に完成
  });
}

// await で待つ
const rice = await cookRice();  // 3秒待ってから結果を取得
console.log(rice);  // 'ご飯が炊けました！'
```

### 別の書き方
```typescript
const fetchWithRetry = async (url: string, retries = 3) => {
  for (let i = 0; i < retries; i++) {
    try {
      const response = await fetch(url);
      if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
      }
      return await response.json();
    } catch (error) {
      console.log(`試行 ${i + 1} 失敗:`, error);
      if (i === retries - 1) throw error; // 最後の試行(i=2. retries-1は2)でエラー。エラーが投げられるとその時点で離脱
      await new Promise(resolve => setTimeout(resolve, 1000)); // エラーにならない場合1秒待機
    }
  }
};
```
流れ
1回目失敗（i = 0）:
- エラーキャッチ
- 「試行 1 失敗」をログ出力
- i === 2？ → No（まだ最後じゃない）
- 1秒待機してからもう一度

2回目失敗（i = 1）:
- エラーキャッチ
- 「試行 2 失敗」をログ出力
- i === 2？ → No（まだ最後じゃない）
- 1秒待機してからもう一度

3回目失敗（i = 2）:
- エラーキャッチ
- 「試行 3 失敗」をログ出力
- i === 2？ → Yes（最後の試行）
- エラーを投げて諦める（1秒待機しない）


## 🤔Promise.allの仕組み

普通のやり方（順番に実行）
```typescript
// 1秒待って、さらに1秒待つ = 合計2秒
const userResponse = await fetch('/users/1');     // 1秒かかる
const postsResponse = await fetch('/posts?userId=1'); // 1秒かかる
```

Promise.allのやり方（同時実行）
```node.js
// 同時にスタートして、両方終わるまで待つ = 1秒
const [userResponse, postsResponse] = await Promise.all([
  fetch('/users/1'),        // 1秒かかる（同時にスタート）
  fetch('/posts?userId=1')  // 1秒かかる（同時にスタート）
]);
```


### Promise.allの書き方パターン
```node.js
// パターン1: 結果を配列で受け取る
const [result1, result2] = await Promise.all([
  fetch('/api/1'),
  fetch('/api/2')
]);
```

```node.js
// パターン2: 結果を変数に分けて受け取る  
const responses = await Promise.all([
  fetch('/users/1'),
  fetch('/posts?userId=1')
]);
const userResponse = responses[0];
const postsResponse = responses[1];
```
