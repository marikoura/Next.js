## response.json() ← クライアント側

`受け取る側の処理`  
**何をするか**: fetchで取得したレスポンスのボディをJSONとして読み取る。JSON文字列 → JavaScriptオブジェクトに変換  
**戻り値**: Promise（非同期処理）  
**使う場面**: APIからデータを取得したとき。fetchの専用メソッド  
**JSON.parse()を内部で実行**

```node.js
const response = await fetch('https://api.example.com/data');
const data = await response.json(); // JSONをJSオブジェクトに変換
console.log(data.name); // オブジェクトとして使える
```

## NextResponse.json() ← サーバー側

`送る側の処理`  
**何をするか**: JavaScriptオブジェクト → JSON文字列に変換してHTTPレスポンスを作成  
**戻り値**: NextResponse オブジェクト  
**使う場面**: Next.jsのAPI Routeでクライアントにデータを返すとき（サーバー側）  
**JSON.stringify() を内部で実行**

```typescript
// オブジェクトをJSON文字列にしてレスポンスを返す
return NextResponse.json({ error: 'エラー' });
```

## JSON.parse()

**何をするか**: JSON文字列 → JavaScriptオブジェクトに変換  
**戻り値**: 変換されたオブジェクト（同期処理）  
**使う場面**: 文字列として保存されたJSONをオブジェクトに戻すとき

```node.js
const jsonString = '{"name": "太郎", "age": 25}';
const obj = JSON.parse(jsonString);
console.log(obj.name); // "太郎"
```

## JSON.stringify()

**何をするか**: JavaScriptオブジェクト → JSON文字列に変換（parseの逆）  
**戻り値**: JSON文字列   
**使う場面**: オブジェクトを保存したりAPIに送信したりするとき

```node.js
const obj = {name: "太郎", age: 25};
const jsonString = JSON.stringify(obj);
console.log(jsonString); // '{"name":"太郎","age":25}'
```
