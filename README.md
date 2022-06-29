
# コーディング規約

コードは他人が最短で理解できるように書かなければならない

短いコード < 理解するまでに時間のかからないコード

## コメント
1. **コードからすぐに分かることはコメントしない**
1. **コードに対する大切な考えはコメントに記録する(メモ書き）**
1. **定数にはなぜその値なのか「背景」までコメントする**
1. **質問されそうなことを想像して、コメントに書く**
1. **ハマりそうな罠をコメントで告知する**
1. **「全体像」のコメントを記述する**
1. **コメントは簡潔にしておく（１行目安）**
1. **曖昧な代名詞や抽象的な言葉は避ける**
1. **関数の動作を正確に伝える**
1. **コメントが正確でない記述量が増えてしまう場合は、実例を用いて簡潔にかく**
1. **コードの意図を書く**

___
例１:コードからすぐ分かることはコメントしない
```java
// 失敗例）profitに新しい値を設定する
void SetProfit(double profit);

// 失敗例）このAccountからprofitを返す
double GetProfit;
```
例２：コードに対する大切な考えはコメントに記録（メモ）する
```java
//　このデータだとハッシュテーブルよりもバイナリツリーの方が40早かった。
//　左右の比較よりもハッシュの計算コストの方が高い

//　ヒューリスティックだと単語が漏れることがあるが仕方ない。100%は難しい。

//　このクラスは汚くなっている
//　サブクラス’ResourceNode’を作って整理した方が良いかもしれない。
```
例３：定数には、なぜその値なのか「背景」までコメントする
```java
NUM_THREADS = 8 // 値は[>=2 * num_processors]で十分

// 合理的な限界値。人間はこんなに読めない。
const int MAX_RSS_SUBSCRIPTIONS = 1000;

IMAGE_QUALITY = 0.72; // 0.72ならユーザはファイルサイズと品質の面で妥協できる。
```
例5：ハマりそうな罠をコメントで告知する
```java
// メールを送信する外部サービスを呼び出している（１分でタイムアウト）
void SendEmail(string to, string subject, string body);

// 実行時間は（タグの数 * タグの深さの平均）なので、ネストの深さに気を付ける
def FixBrokenHtml(html);
```
例6：「全体像」のコメントを記述する
```java
// これはビジネスロジックとデータベースをつなぐグルーコードだから、アプリケーションから直接使ってはいけない
// このクラスは複雑に見えるが、単なるキャッシュであるため、システムのことは感知していない
```
例7：コメントは簡潔にしておく
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
例8：曖昧な代名詞や抽象的な言葉は避ける
```java
// データをキャッシュに入れる。だだし、先に"その"サイズをチェックする
//                          ↓
// データをキャッシュに入れる。ただし、先に"データ"のサイズをチェックする。
```
例9：関数の動作を正確に伝える
```java
// このファイルに含まれる行数を返す（行数というのは曖昧でわかりいくい）
int CountLines(string filename) {}
//          ↓
// このファイルに含まれる改行文字（'¥n')を数える
int CountLines(string filename) {}
```
例10：コメントの量が増える・正確でない場合、実例を用いて簡潔に書く
```java
// 失敗例：'src'の先頭や末尾にある'chars'を除去する（charsが複数あったら？charsは文字列？・・）
String Strip(String src, String chars) {}

//実例：Strip("abba/a/ba", "ab")は"/a/"を返す
String Strip(String src, String chars) {}
```
例11：コードの意図を書く
```java
// 失敗例）listを逆順にイテレートする
for(list<Product>::reverse_iterator it = products.rbegin();it != products.rend(); ++it)
	DisplayPrice(it->price);

// 改善例）値段の高い順に表示する。
for(list<Product>::reverse_iterator it = products.rbegin();・・・)
```

___
## 命名

1. **曖昧・抽象的ではなく明確な単語を選ぶ**
1. **汎用的な変数名は避ける**
1. **接尾辞や接頭文字に情報を追加する**
1. **スコープの範囲によって長さを決める（他のエンジニアも分かるように）**
1. **それぞれの命名にフォーマットを用意する**
1. **誤解されない命名をつける**
___

例１：曖昧・抽象的ではなく明確な単語を選ぶ
```java
// 失敗例１）　抽象的な変数名(get)

// 失敗例2）　抽象的な変数名(Size)

// 失敗例3）　抽象的な変数名(Stop)

// 失敗例４）　抽象的なメソッド命名
	// 任意のTCP/IPポートがリッスンできるかを確認するメソッド
	ServerCanStart() //抽象的
	→CanListenOnPort() //具体的
```
例２：汎用的な変数名は避ける
```java
// 失敗例１）　汎用的な変数名（tmpやretval）

```
例３：接尾辞や接頭文字に情報を追加する
```java
// 良い例１）　　値の単位が必要な場合は、単位を追加する
var start_ms = (new Date()).gateTime();
var elapsed_ms = (new Date()).gateTime() - start_ms;

// 良い例２）　配列やオブジェクトを格納する場合、接尾辞に情報を追加する
var user_list = ['jone', 'divd', 'jesica'];
var user_obj = {'name': 'jone', 'age':20};

// 良い例３）　その他セキュリティのバグにつながるような重要な属性を追加する

// 信用できる受信データかどうかを変数名で区別する
untrustedUrl, unsafeMessageBody // 信用できない
trustedUrl, safeMessageBody // 信用できる
```

| 状況 | 変数名 | 改善後 |
| :--- | :---: | :---: |
| 暗号化されていないプレインテキストなpassword | 暗号化されていないプレインテキストなpassword | plaintext_password |
| ユーザーが入力したエスケープされていないcomment | comment | unescaped_comment |
| UTF-8に変えたhtmlの文字コード | html | html_utf8 |
| 入力されたdataをURLにエンコードした | data | data_urlenc |

例4：スコープの範囲によって長さを決める
```java
// 良い例）新しく配属されたエンジニアが一眼でわかる変数になるように、
// 頭文字で省略したり、不要な単語を捨てる
if(debug) {
	map<string,int> m; //変数mの型・初期値・廃棄方法などがすぐに見えるので「m」の命名で良い
	LokUpNamesNumbers(&8);
	Print(m);
}
```
例５：名前のフォーマットで情報を伝える
| 対象 | 命名フォーマット |
| :--- | :--- |
| クラス名 | CamelCase（キャメルケース） | 
| 変数名 | lower_separeted（小文字アンダースコア） | 
| 定数 | CONSTANT_NAME（大文字アンダースコア） |
| クラスのメンバ変数 | offset_（末尾に_をつける） |
| htmlのクラス | main_content（ _ ） |
| htmlのid | middle-id ( - ) |
___
## 条件式とループ

1. **条件式は左側に調査対象、右側に比較他対象を置く**
1. **if文は否定系より肯定系を使い、関心の引く条件や目立つ条件を先に書く**
1. **複雑な条件式はド・モルガの法則を使う**
1. **関数から早く返す**
1. **ネストを浅くするために、「失敗ケース」を早めに返す**
1. **ループ内部のネストを削除するために、"continue"や"break"を利用する**
___
例１：条件式の引数の並び順
| 左側 | 右側 |
| :--- | :--- |
| 調査対象」の式。変化する | 比較対象の式。あまり変化しない | 

```java
if (length >= 10) //○
if (10 <= length) //✖️

while (bytes_received < bytes_expected) //○
while (bytes_expected > bytes_received) //✖️
```
例２：if文は否定系より肯定系を使い、関心の引く条件や目立つ条件を先に書く

```java
// 失敗例：expand_allのことが頭に浮かんでしまう。
if (!url.HasQueryParameter("expand_all")) {
	response.Render(items);
	・・・
} else {
	for (int i = 0; i < items.size(); i++) {
		items[i].Expand();
	}
		・・・
}
-----------------------------------------------------
// 成功例
if (url.HasQueryParameter("expand_all")) {
	for (int i = 0; i < items.size(); i++) {
		items[i].Expand();
	}
	・・・
} else {
	response.Render(itmes);
	・・・
}
```
例３：複雑な条件式はド・モルガの法則を使う
```java
// ド・モルガンの法則 = [not]を括り出して、[and]と[or]を逆転する

if (!(file_exists && !is_protected))Error("Sorry, could not read file.");
↓
// ド・モルガンの法則
if (!(file_exists || is_protected)) Error("Sorry, could not read file.");
```
例４：関数から早く返す
```java
// 関数からは早く返すことを意識する
public boolean Contains(String str, String substr) {
	if (str == null || substr == null) return false;
	if (substr.equals("")) return true;
	・・・
}
```
例５：ネストを浅くする(失敗ケースを早めに返す)
```java
// 失敗例
if (user_result == SUCCESS) {
	if (permission_result != SUCCESS) {
		reply.WriteErrors("error reading permissions");
		reply.Done();
		return;
	}
	reply.WriteErrors("");
} else {
	reply.WriteErrors(user_result);
}
reply.Done()

--------------------------------------------------------

// 改善例（深さレベルが２→１に浅くなった）
if (user_result != SUCCESS) {
	reply.WriteErrors(user_result);
	reply.Done();
	return;
}
if (permission_result != SUCCESS) {
	reply.WriteErrors(permission_result);
	reply.Done();
	return;
}
reply.WriteErrors("");
reply.Done();
```
例６：ループ内部のネストを削除するために、"continue"や"break"を利用する
```java
// 失敗例）ループのネストが深い失敗例
for (int = 0; i <results.size(); i++) {
	if (results[i] != NULL) {
		non_null_count++;

		if (results[i] -> name != "") {
			cont << "Considering candidate..." << end;
			...
		}
	}
}
------------------------------------------------------------------
// 成功例）continueを使ってネストを浅くする
for (int i = 0; i < results.size(); i++) {
	if (results[i] == NULL) continue;
	non_null_count++;

	if (results[i]->name="") continue;
	cont << "Considering candidate..." << end;
}
```

## ロジックと変数
1. **巨大な式を分割するために説明変数を使用する**
1. **コードをわかりやすくするために、要約変数を使用する**
1. **複雑なロジックを「反対」を使って簡単にする**
1. **巨大な式を分割する**
1. **一時変数・中間結果・制御フロー変数など不要な変数を削除する**
1. **変数のスコープを縮める**
1. **変数には一度だけ書き込む**
___
例１：巨大な式を分割するために説明変数を使用する
```java
// 失敗例
if (line.split(':')[0].strip() == "root"){
	// ...
}
-----------------------------------------------------
// 成功例）説明変数を使用する
username = line.split(':')[0].strip();
if (username == "root") {
	// ...
}
```
例２：コードをわかりやすくするために、要約変数を使用する
```java
// 失敗例
if (request.user.id == document.owner_id) {
	// ユーザーはこの文章を編集できる
}
--------------------------------------------------------------
//　成功例）　要約変数を設定する
final boolean user_owns_document = (request.user.id == document.owner.id);
if (user_owns_document) {
	// ユーザーはこの文章を編集できる
}
```
例３：複雑なロジックを「反対」を使って簡単にする
```java
// 複雑なロジック（終端が他の範囲と重なっているかを確認するロジック）
return (begin >= other.begin && begin < other.end) ||
			 (end > other.begin && end <= other.end) ||
			 (begin <= other.begin && end >= other.end);
----------------------------------------------------------------------------
// 「反対」を使って簡潔にする
// 反対を使ったロジック（終端が他の範囲と重なっていないかを確認するロジック）
bool Range::OverlapWith(Range other) {
	if (other.end <= begin) return false; // 一方の終点が、この始点よりも前にある
	if (other.begin >= end) return false; // 一方の視点が、この終点よりも後にある

	return true; // 残ったものは重なっている
}

```
例４：巨大な式を分割する
```javascript
// 失敗例）　すぐに理解できないコード
var update_highlight = function (message_num) {
	if ($("#vote_value" + message_num).html() === "Up") {
		 $("#thumbs_up" + message_num).addClass("highlight");
		 $("#thumbs_down" + message_num).removeClass("highlight");
	} else if ($("#vote_value" + message_num).html() === "Down") {
		 $("#thumbs_up" + message_num).removeClass("highlight");
		 $("#thumbs_down" + message_num).addClass("highlight");
	} else {
		 $("#thumbs_up" + message_num).addClass("highlighted");
		 $("#thumbs_down" + message_num).removeClass("highlighted");
	}
};
----------------------------------------------------------------------
// 改善例）　似ているコードを、ようやく変数として関数の上部に抽出する
var update_highlight = function (message_num) {
	var thumbs_up = $("#thumbs_up" + message_num);
	var thumbs_down = $("#thumbs_down" + message_num);
	var vote_value = $("#vote_up" + message_num).html();
	var hi = "higjlighted";

	if (vote_value === "Up") {
		thumbs_up.addClass(hi);
		thumbs_down.removeClass(hi);
	} else if(vote_value === "Down") {
		thumbs_up.removeClass(hi);
		thumbs_down.removeClass(hi);
	} else {
		thumbs_up.removeClass(hi);
		thumbs_down.removeClass(hi);
  }
```
例５：一時変数・中間結果・制御フロー変数など不要な変数を削除する

（一時変数を削除する)
```java
// 不要な一時変数
now = datetime.datetime.now();
root_message.list_view_time = now;
```
このnowは以下の理由から意味のない変数である
- 複雑な式を分割していない
- datetime.datetime.now()のままでも十分に明確だ。
- 一度しか使っていないので、重複コードの削除になっていない。

```java
// 成功例
root_message.last_view_time = datetime.datetime.now();
```
（中間結果を削除する）
```java
// 失敗例）　index_to_removeは中間結果
var remove_one = function (array, value_to_remove) {
	var index_to_remove = null;
	for (var i = 0; i < array.length; i += 1) {
		if (array[i] === value_to_remove) {
			index_to_remove = i;
			break;
		}
	}
	if (index_to_remove !== null) {
		array.splice(index_to_remove, 1);
	}
};
---------------------------------------------------------------------
// 改善例）　中間結果を格納したindex_to_removeを削除
var remove_one = function (array, value_to_remove) {
	for (var i = 0; i < array.length; i+=1) {
		if (array[i] === value_to_remove) {
			array.splice(i, 1);
			return;
		}
	}
};
```
（制御フロー変数を削除する）
```java
// 失敗例）　制御フロー（done)がある場合
boolean done = false;

while(/* 条件 */ && !done) {
	if (...) {
		done = true;
		continue;
	}
}
----------------------------------------------------------------
// 改善例）　制御フロー変数を削除
while(/* 条件 */) {
	if (...) {
		break;
	}
```
例６：変数のスコープを縮める
1. **グローバル変数はどこでどのように使われているかを追跡するのが難しい**
2. **名前空間を汚染する**

→以上の２つの理由から、

- **グローバル変数の使用はできるだけ避ける**
- **変数のスコープはできるだけ小さくする。**
- **変数はその変数を処理するコードの近くで定義する**

例７：変数には一度だけ書き込む
**constやfinalなどのイミュータブルにする方法を使う**

(具体例）
```java
// 失敗例）　foundやi,elemの変数が何度も書き換えれられている
var setFirstEmptyInput = function(new_value) {
	var found = false;
	var i = 1;
	var elem = document.getElementById('input'+i);
	while (elem !== null) {
		if (elem.value === '') {
			found = true;
			break;
		}
		i++;
		elem = document.getElementById('input' + i);
	}
	if (found) elem.value = new_value;
	return elem;
}
--------------------------------------------------------------
//　改善例
var setFirstInput = function (new_value) {
	// ① (i) を[while]から[for]に変換することで省略
	for (var i = i; true; i++) {
		// ② (elem)の定義回数を一回に省略
		var elem = document.getElmentById('input' + i);
		// ③ (found)を省略するために、早めに返す
		if (elem === null) return null; // 検索失敗。空のフィールドは見つからなかった。

		if (elem.value === '') {
			elem.value = new_value;
			return elem;
		}
	}
}
```
