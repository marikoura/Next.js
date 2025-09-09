### 🔍 resolve の役割  
#### 「約束を果たしたよ！」を伝える関数  
Promiseの作り方  
```next.js
javascriptconst myPromise = new Promise((resolve, reject) => {
  // 何かの処理をする
  
  // 成功した場合
  resolve('成功したデータ');
  
  // 失敗した場合  
  reject('エラーメッセージ');
});
```

### 🍳 料理の例で理解
料理を作るPromise
```next.js
javascriptfunction cookCurry() {
  return new Promise((resolve, reject) => {
    console.log('カレーを作り始めます...');
    
    setTimeout(() => {
      const success = Math.random() > 0.3; // 70%の確率で成功
      
      if (success) {
        resolve('美味しいカレーができました！'); // 成功を報告
      } else {
        reject('カレーを焦がしてしまいました...'); // 失敗を報告
      }
    }, 3000); // 3秒後に結果が出る
  });
}

// 使用例
try {
  const curry = await cookCurry();
  console.log(curry); // '美味しいカレーができました！'
} catch (error) {
  console.log(error); // 'カレーを焦がしてしまいました...'
}
```

### 📞 電話の約束で例えると
友達との約束
```next.js
javascriptfunction callFriend() {
  return new Promise((resolve, reject) => {
    console.log('友達に電話をかけています...');
    
    setTimeout(() => {
      const answered = Math.random() > 0.5;
      
      if (answered) {
        resolve('友達: こんにちは！元気？'); // 電話に出た
      } else {
        reject('留守電: 後でかけ直してください'); // 電話に出なかった
      }
    }, 2000);
  });
}
```

### 🌐 実際のAPI例
fetch() の内部的な仕組み  
javascript// fetch() は内部的にこんな感じ  
```next.js
function myFetch(url) {
  return new Promise((resolve, reject) => {
    // HTTP リクエストを送信
    const request = new XMLHttpRequest();
    request.open('GET', url);
    
    request.onload = () => {
      if (request.status === 200) {
        resolve(request.response); // 成功！データを渡す
      } else {
        reject(`エラー: ${request.status}`); // 失敗！エラーを渡す
      }
    };
    
    request.onerror = () => {
      reject('ネットワークエラー'); // 通信エラー
    };
    
    request.send();
  });
}
```

### 🎯 resolve と reject の使い分け
resolve（成功時）
```next.js
javascript// データが正常に取得できた
resolve(data);

// ファイルの読み込みが完了
resolve(fileContent);

// 計算が完了
resolve(result);
```

reject（失敗時）
```next.js
javascript// ネットワークエラー
reject('接続できませんでした');

// データが見つからない
reject('データが存在しません');

// 権限がない
reject('アクセス権限がありません');
```

### 🧪 実際に作ってみよう
簡単なタイマーPromise
```next.js
javascriptfunction wait(seconds) {
  return new Promise((resolve) => {
    console.log(`${seconds}秒待ちます...`);
    
    setTimeout(() => {
      resolve(`${seconds}秒経過しました！`);
    }, seconds * 1000);
  });
}

// 使用例
const message = await wait(2);
console.log(message); // '2秒経過しました！'
```
