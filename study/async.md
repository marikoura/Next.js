## async/await とは？
### async:
async キーワードは、関数が非同期であることを示します。  
async が付いた関数は、必ず Promise を返します。もし関数が明示的な Promise を返さなくても、TypeScriptは自動的にそれを Promise でラップします。
### await:
await キーワードは、async 関数の中でのみ使用できます。  
Promise の完了を待ちます。つまり、Promise が resolve または reject されるのを待ってから次の行に進みます。  
await は、Promise が成功した場合にその結果を返します。失敗した場合にはエラーをスローします。

## async関数の引数について
### 引数なし
```next.js
// 決まったURLを取得する関数

const fetchPosts = async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  return response.json();
};
```

### 引数あり
```typescript
// userIdによって取得するデータが変わる関数
//引数なしだと、いつも同じユーザーしか取得できない

const getUserAndPosts = async (userId: number) => {
  const response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`); //userId:3 → ユーザー3の情報
  return response.json();
};
```
