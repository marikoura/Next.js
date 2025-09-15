## useRouterとは
Webページ間のナビゲーションを助けてくれるツール  
現在表示しているページの情報を取得したり（URL、パス名、クエリパラメータなど）、新しいページへ遷移したりする
```next.js
import { useRouter } from "next/navigation";

function MyComponent() {
  const router = useRouter();

  // ページ移動
  const handleLogin = () => {
    router.push('/dashboard'); // /dashboardに移動・履歴を残す
  };

　// ページ移動
  const replace = () => {
    router.replace('/home'); // /homeに移動・履歴を残さない
  };

  // 履歴の前に戻る
  const goBack = () => {
    router.back();
  };

  // 履歴の次に進む
  const goForward = () => {
　　 router.forward();
  };

  // リロード
  const refresh = () => {
    router.refresh();
  };

  // 使用例
  return (
    <div>
      <button onClick={handleLogin}>ダッシュボードへ</button>
      <button onClick={goBack}>戻る</button>
    </div>
  );
}
```
車の例え話にすると、useRouterはあなたが運転している車のナビゲーションシステムのようなもの。  
目的地（pushやreplaceメソッド）、途中での休憩（refreshメソッド）、途中で見つけた興味深い場所への迂回（prefetchメソッド）、後戻り（backメソッド）、または前進（forwardメソッド）など、あなたがどこへ行きたいかに応じて適切な指示を出します。
