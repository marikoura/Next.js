#### 📝元データ:
```next.js
const posts = [
  { topics: ["JavaScript", "学習計画"] },
  { topics: ["TypeScript", "型システム", "実践課題"] },
  { topics: ["TypeScript", "エラーハンドリング", "実装"] },
  { topics: ["Next.js", "React", "フレームワーク"] }
];
```

#### 🖊ステップ1: flatMapで全トピックを1つの配列に
```next.js
posts.flatMap(post => post.topics)

// 結果:
[
  "JavaScript", "学習計画",           // 1つ目の記事から
  "TypeScript", "型システム", "実践課題", // 2つ目の記事から  
  "TypeScript", "エラーハンドリング", "実装", // 3つ目の記事から
  "Next.js", "React", "フレームワーク"  // 4つ目の記事から
]
```

#### 🖊ステップ2: new Setで重複を削除
```next.js
new Set([
  "JavaScript", "学習計画",
  "TypeScript", "型システム", "実践課題",
  "TypeScript", "エラーハンドリング", "実装", // ← TypeScriptが重複
  "Next.js", "React", "フレームワーク"
])

// 結果（Setオブジェクト）:
Set {
  "JavaScript", "学習計画", "TypeScript", 
  "型システム", "実践課題", "エラーハンドリング", 
  "実装", "Next.js", "React", "フレームワーク"
}
```

#### 🖊ステップ3: Array.fromで配列に戻す
```next.js
Array.from(Set {...})

// 最終結果:
[
  "JavaScript", "学習計画", "TypeScript","型システム", "実践課題", "エラーハンドリング", "実装", "Next.js", "React", "フレームワーク"
]
```
