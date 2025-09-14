### 📚 fetchの基本構文
```next.js
fetch(url, options)
第1引数： URL（必須）
第2引数： オプション（任意）
```

### 🔍 パターン別の使い方
1. GET（シンプル）
```next.js
// オプションなし = 自動的にGET
const response = await fetch('/api/tasks');
```

3. GET（明示的）
```next.js
const response = await fetch('/api/tasks', {
  method: 'GET'  // ← 省略可能
});
```

4. POST（データ送信）
```next.js
const response = await fetch('/api/tasks', {
  method: 'POST',                                    // ← HTTPメソッド
  headers: {                                         // ← リクエストヘッダー
    'Content-Type': 'application/json'              // ← JSONを送信することを宣言
  },
  body: JSON.stringify({ title: 'new task' })       // ← 送信するデータ
});
```

5. PUT（更新）
```next.js
const response = await fetch('/api/tasks/123', {
  method: 'PUT',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ completed: true })
});
```

6. DELETE
```next.js
const response = await fetch('/api/tasks/123', {
  method: 'DELETE'
});
```

### 💡 なぜheadersとbodyが必要？
#### headers（Content-Type）:
- サーバーに「JSONデータを送るよ」と伝える
- サーバーが正しく解析できるように

#### body（JSON.stringify）:
- JavaScriptオブジェクト → JSON文字列に変換
- HTTPでは文字列しか送れないため
