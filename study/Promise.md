## 🤔 Promiseオブジェクトとは  
「後で結果をくれる約束手形」のようなもの  
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

## Promise.allの仕組み

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
