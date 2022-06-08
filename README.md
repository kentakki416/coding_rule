
# コーディング規約

### コードは他人が最短で理解できるように書かなければならない

**短いコード** < **理解するまでに時間のかからないコード**

## コメント
#### コメントの目的は書き手の意図を読み手に伝えること
* コードからすぐに分かることはコメントしない

```java
// 失敗例）profitに新しい値を設定する
void SetProfit(double profit);

// 失敗例）このAccountからprofitを返す
double GetProfit;
```

* コードに対する大切な考えはコメントに記録する(メモ書き）
```java
//　このデータだとハッシュテーブルよりもバイナリツリーの方が40早かった。
//　左右の比較よりもハッシュの計算コストの方が高い

//　ヒューリスティックだと単語が漏れることがあるが仕方ない。100%は難しい。

//　このクラスは汚くなっている
//　サブクラス’ResourceNode’を作って整理した方が良いかもしれない。
```
* 定数にはなぜその値なのか「背景」までコメントする
```java
NUM_THREADS = 8 // 値は[>=2 * num_processors]で十分

// 合理的な限界値。人間はこんなに読めない。
const int MAX_RSS_SUBSCRIPTIONS = 1000;

IMAGE_QUALITY = 0.72; // 0.72ならユーザはファイルサイズと品質の面で妥協できる。
```
* 質問されそうなことを想像して、コメントに書く
「なぜそのような実装にしたのか」「他の実装方法ではダメなのか」思われる箇所には適切にコメントする

* ハマりそうな罠をコメントで告知する
```java
// メールを送信する外部サービスを呼び出している（１分でタイムアウト）
void SendEmail(string to, string subject, string body);

// 実行時間は（タグの数 * タグの深さの平均）なので、ネストの深さに気を付ける
def FixBrokenHtml(html);
```

* 「全体像」のコメントを記述する
```java
// これはビジネスロジックとデータベースをつなぐグルーコードだから、アプリケーションから直接使ってはいけない
// このクラスは複雑に見えるが、単なるキャッシュであるため、システムのことは感知していない
```

#### コメントは画面領域を取るため、正確で簡潔に書く必要がある
* コメントは簡潔にしておく（１行目安）
```java
//（失敗例）
// intはCategoryType
// pairの最初のfloatは'score'
// 2つ目は’weight'
typedef hash_map<int, pair<float, float> >ScoreMap;

//（改善例）
// CategoryType -> (score, weight)
typedef hash_map<int, pair<float, float> > ScoreMap;
```
* 曖昧な代名詞や抽象的な言葉は避ける
```java
// データをキャッシュに入れる。だだし、先に"その"サイズをチェックする
//                          ↓
// データをキャッシュに入れる。ただし、先に"データ"のサイズをチェックする。
```
* 関数の動作を正確に伝える
```java
// このファイルに含まれる行数を返す（行数というのは曖昧でわかりいくい）
int CountLines(string filename) {}
//          ↓
// このファイルに含まれる改行文字（'¥n')を数える
int CountLines(string filename) {}
```
* コメントが正確でない記述量が増えてしまう場合は、実例を用いて簡潔にかく

```java
// 失敗例：'src'の先頭や末尾にある'chars'を除去する（charsが複数あったら？charsは文字列？・・）
String Strip(String src, String chars) {}

//実例：Strip("abba/a/ba", "ab")は"/a/"を返す
String Strip(String src, String chars) {}
```

* コードの意図を書く
コードの動作をそのまま書くのではなく、コードの意図を書く（情報密度の高い言葉を使う）

```java
// 失敗例）listを逆順にイテレートする
for(list<Product>::reverse_iterator it = products.rbegin();it != products.rend(); ++it)
	DisplayPrice(it->price);

// 改善例）値段の高い順に表示する。
for(list<Product>::reverse_iterator it = products.rbegin();・・・)
```

## 変数
#### 変数名に情報を詰め込む

* 明確な単語を選ぶ
```java
// 1. getという命名は抽象的 
// => 例：インターネットから取得する場合、FetchPage()やDownloadPage()の方が明確
```
