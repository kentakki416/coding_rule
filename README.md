
# コーディング規約

コードは他人が最短で理解できるように書かなければならない

短いコード **<** 理解するまでに時間のかからないコード
___
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
<br>

#### 例１) コードからすぐ分かることはコメントしない
```java
// 失敗例）profitに新しい値を設定する
void SetProfit(double profit);

// 失敗例）このAccountからprofitを返す
double GetProfit;
```
<br>

#### 例２) コードに対する大切な考えはコメントに記録（メモ）する
```java
//　このデータだとハッシュテーブルよりもバイナリツリーの方が40早かった。
//　左右の比較よりもハッシュの計算コストの方が高い

//　ヒューリスティックだと単語が漏れることがあるが仕方ない。100%は難しい。

//　このクラスは汚くなっている
//　サブクラス’ResourceNode’を作って整理した方が良いかもしれない。
```
<br>

#### 例３) 定数には、なぜその値なのか「背景」までコメントする
```java
NUM_THREADS = 8 // 値は[>=2 * num_processors]で十分

// 合理的な限界値。人間はこんなに読めない。
const int MAX_RSS_SUBSCRIPTIONS = 1000;

IMAGE_QUALITY = 0.72; // 0.72ならユーザはファイルサイズと品質の面で妥協できる。
```
<br>

#### 例5) ハマりそうな罠をコメントで告知する
```java
// メールを送信する外部サービスを呼び出している（１分でタイムアウト）
void SendEmail(string to, string subject, string body);

// 実行時間は（タグの数 * タグの深さの平均）なので、ネストの深さに気を付ける
def FixBrokenHtml(html);
```
<br>

#### 例6) 「全体像」のコメントを記述する
```java
// これはビジネスロジックとデータベースをつなぐグルーコードだから、アプリケーションから直接使ってはいけない
// このクラスは複雑に見えるが、単なるキャッシュであるため、システムのことは感知していない
```
<br>

#### 例7) コメントは簡潔にしておく
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
<br>

#### 例8) 曖昧な代名詞や抽象的な言葉は避ける
```java
// データをキャッシュに入れる。だだし、先に"その"サイズをチェックする
//                          ↓
// データをキャッシュに入れる。ただし、先に"データ"のサイズをチェックする。
```
<br>

#### 例9) 関数の動作を正確に伝える
```java
// このファイルに含まれる行数を返す（行数というのは曖昧でわかりいくい）
int CountLines(string filename) {}
//          ↓
// このファイルに含まれる改行文字（'¥n')を数える
int CountLines(string filename) {}
```
<br>

#### 例10) コメントの量が増える・正確でない場合、実例を用いて簡潔に書く
```java
// 失敗例：'src'の先頭や末尾にある'chars'を除去する（charsが複数あったら？charsは文字列？・・）
String Strip(String src, String chars) {}

//実例：Strip("abba/a/ba", "ab")は"/a/"を返す
String Strip(String src, String chars) {}
```
<br>

#### 例11) コードの意図を書く
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
<br>

#### 例１) 曖昧・抽象的ではなく明確な単語を選ぶ
```java
// 失敗例１）　抽象的な変数名(get)

// 失敗例2）　抽象的な変数名(Size)

// 失敗例3）　抽象的な変数名(Stop)

// 失敗例４）　抽象的なメソッド命名
	// 任意のTCP/IPポートがリッスンできるかを確認するメソッド
	ServerCanStart() //抽象的
	→CanListenOnPort() //具体的
```
<br>

#### 例２) 汎用的な変数名は避ける
```java
// 失敗例１）　汎用的な変数名（tmpやretval）

```
<br>

#### 例３) 接尾辞や接頭文字に情報を追加する
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

<br>

#### 例4) スコープの範囲によって長さを決める
```java
// 良い例）新しく配属されたエンジニアが一眼でわかる変数になるように、
// 頭文字で省略したり、不要な単語を捨てる
if(debug) {
	map<string,int> m; //変数mの型・初期値・廃棄方法などがすぐに見えるので「m」の命名で良い
	LokUpNamesNumbers(&8);
	Print(m);
}
```
<br>

#### 例５) 名前のフォーマットで情報を伝える
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
<br>

#### 例１) 条件式の引数の並び順
| 左側 | 右側 |
| :--- | :--- |
| 調査対象」の式。変化する | 比較対象の式。あまり変化しない | 

```java
if (length >= 10) //○
if (10 <= length) //✖️

while (bytes_received < bytes_expected) //○
while (bytes_expected > bytes_received) //✖️
```
<br>

#### 例２) if文は否定系より肯定系を使い、関心の引く条件や目立つ条件を先に書く

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
<br>

#### 例３) 複雑な条件式はド・モルガの法則を使う
```java
// ド・モルガンの法則 = [not]を括り出して、[and]と[or]を逆転する

if (!(file_exists && !is_protected))Error("Sorry, could not read file.");
↓
// ド・モルガンの法則
if (!(file_exists || is_protected)) Error("Sorry, could not read file.");
```
<br>

#### 例４) 関数から早く返す
```java
// 関数からは早く返すことを意識する
public boolean Contains(String str, String substr) {
	if (str == null || substr == null) return false;
	if (substr.equals("")) return true;
	・・・
}
```
<br>

#### 例５) ネストを浅くする(失敗ケースを早めに返す)
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
<br>

#### 例６) ループ内部のネストを削除するために、"continue"や"break"を利用する
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
___

## ロジックと変数
1. **巨大な式を分割するために説明変数を使用する**
1. **コードをわかりやすくするために、要約変数を使用する**
1. **複雑なロジックを「反対」を使って簡単にする**
1. **巨大な式を分割する**
1. **一時変数・中間結果・制御フロー変数など不要な変数を削除する**
1. **変数のスコープを縮める**
1. **変数には一度だけ書き込む**
___
<br>

#### 例１) 巨大な式を分割するために説明変数を使用する
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
<br>

#### 例２) コードをわかりやすくするために、要約変数を使用する
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
<br>

#### 例３) 複雑なロジックを「反対」を使って簡単にする
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
<br>

#### 例４) 巨大な式を分割する
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
<br>

#### 例５) 一時変数・中間結果・制御フロー変数など不要な変数を削除する

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
<br>

#### 例６) 変数のスコープを縮める
1. **グローバル変数はどこでどのように使われているかを追跡するのが難しい**
2. **名前空間を汚染する**

→以上の２つの理由から、

- **グローバル変数の使用はできるだけ避ける**
- **変数のスコープはできるだけ小さくする。**
- **変数はその変数を処理するコードの近くで定義する**

<br>

#### 例７) 変数には一度だけ書き込む
**constやfinalなどのイミュータブルにする方法を使う**

(具体例）
```javascript
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
___

## コードの再構成
1. **無関係な下位問題を積極的に見つけて抽出する**
1. **汎用コードは関数化する（分離）**
1. **既存のインターフェースを簡潔にする**
1. **一度に一つのタスクをする**
1. **ロジックを明確にする**
1. **短いコードを書く**
1. **ライブラリを活用する**
___
<br>

#### 例１) 無関係な下位問題を積極的に見つけて抽出する

**（コードを分割する手順）**

1. **関数やコードを見て「このコードの高レベルの目標は何か？」と自問する**
2. **コードの各行に対して「高レベルの目標に直接的に効果があるのか？それとも、無関係の下位問題を解決しているのか？」と自問する**
3. **無関係の下位問題を解決しているコードが相当量であれば、それらを抽出して別の関数にする。**

**※関数の前処理や後処理は”無関係な下位問題”になりやすい**

```java
// 失敗例）　コードの高レベルの目標「与えられた地点から最も近い場所を見つける」
// 与えられた経度緯度から最も近いarrayを返す
var findClosestLocation = function (lat, lng, array) {
	var closest;
	var closest_dist = Number.MAX_VALUE;
	for (var i = 0; i < array.length; i += 1) {
		// 2つの地点をラジアンに変換する
		var lat_rad = radians(lat);
		var lng_rad = radians(lng);
		var lat2_rad = radians(array[i].latitude);
		var lng2_rad = radians(array[i].longitude);

		// 「球面三角法の第二余弦定理」の公式
		var dist = Math.acos(Math.sin(lat_rad) * Math.sin(lat2_rad) +
												 Math.cos(lat_rad) * Math.cos(lat2_rad) *
												 Math.cos(lng2_rad - lng_rad));
		if (dist < closest_dist) {
			closest = array[i];
			closest_dist = dist;
		}
	}
	return closest;
};
```
この例での”無関係の下位問題”は「２つの地点（緯度経度）の球面距離を算出する」である。

```java
// 改善例）
// 無関係の下位問題を別関数に抽出
var spherical_distance = function (lat1, lng1, lat2, lng2) {
		var lat1_rad = radians(lat);
		var lng1_rad = radians(lng);
		var lat2_rad = radians(lat2);
		var lng2_rad = radians(lng2);

		// 「球面三角法の第二余弦定理」の公式
		var dist = Math.acos(Math.sin(lat_rad) * Math.sin(lat2_rad) +
												 Math.cos(lat_rad) * Math.cos(lat2_rad) *
												 Math.cos(lng2_rad - lng_rad));
};
-----------------------------------------------------------------------
var findClosestLocation = function (lat, lng, array) {
	var closest;
	var closest_dist = Number.MAX_VALUE;
	for (var i = 0; i < array.length; i += 1) {
		// 「球面三角法の第二余弦定理」の公式
		var dist = spherical_distance(lat, lng, array[i].latitude, array[i].longtude);
		if (dist < closest_dist) {
			closest = array[i];
			closest_dist = dist;
		}
	}
	return closest;
};
```
<br>

#### 例２) 汎用コードは関数化する（分離）

ファイル読み込みや文字列操作、デバッグなどの汎用的なコードは「無関係の下位問題」として新しい関数に分けるべき。
```javascript
// 例）コードの高レベル目標「サーバをAjaxで呼び出してレスポンスを処理する」
ajax_post({
	url: 'http://example.com/submit',
	data: data,
	on_success: function (response_data) {
		var str = "{¥n";
		for (var key in response_data) {
			str += " " + key + " = " + response_data[key] + "¥n";
		}
		alert(str + "}");
		//　引き続きresponse_dataの処理
	}
});
```
このコードの”無関係な下位問題”は「ディクショナリを綺麗に印字する」こと
```javascript
// 改善例）ディクショナリを綺麗に印字する処理を新しい関数に抽出する
var format_pretty = function (obj) {
	var str = "{¥n";
	for (var key in obj) {
		str += " " + key + " = " + obj[key] + "¥n";
	}
	return str + "}";
};
```
#### 例３) 既存のインターフェースを簡潔にする

引数が少なく、事前設定も必要なく、面倒なことをしなくても使えるインターフェースが好ましい。

 →既存のインターフェースを、自分で用意したラッパー関数で覆い隠すと良い

<br>

#### 例４) 一度に一つのタスクをする

1. コードが行っている「タスク」を全て列挙する
2. タスクをできるだけ異なる関数に分割する

**※ここで言う「タスク」とは、”ゆるく”使っている。**

**例）「オブジェクトが妥当かどうかを確認する」や「ツリーの全てのノードをイテレートする」など**

サンプル①：「賛成」と「反対」を押して、Scoreを計算する処理
```javascript
// 失敗例）　タスクが混在している例
var vote_changed = function (old_vote, new_vote) {
	var score = get_score();

	if (new_vote !== old_vote) {
		if (new_vote === "Up") {
			score += (old_vote === "Down" ? 2:1);
		} else if (new_vote === "Down") {
			score += (old_vote === "Up" ? 2:1);
		} else if (new_vote === "") {
			score += (old_vote === "Up" ? -1:1);
		}
	}
	set_score(score);
}
```
このコードは一度に２つのタスクを行っている。(分かりにくい）

1. **old_voteとnew_voteを数値に「バース」する。**
2. **scoreを更新する**

```javascript
// 改善例）２つのタスクを別々に解決するように書き換えたもの
// 数値をパースする
var vote_value = function(vote) {
	if (vote === "Up") {
		return +1;
	}
	if (vote === "Down") {
		return -1;
	}
	return 0;
};
--------------------------------------------------------
// スコアの更新
var vote_changed = funtion(old_vote, new_vote) {
	var score = get_score();
	score -= vote_value(old_vote); //古い値を削除
	score += vote_value(new_vote); //新しい値を追加
	set_score(score);
}
```
サンプル②：オブジェクトから値を抽出する

```javascript
// 例）タスクが混在している例を示す。
var place = location_info["LocalityName"];
if (!place) {
	place = location_info["SubAdministrativeAreaName"];
}
if (!place) {
	place = location_info["AdministrativeAreaName"];
}
if (location_info["CountryName"]) {
	place += ", " + location_info["CountryName"];
} else {
	place += ", Planet Earth";
}
return place;
```
このコードは以下の４つのタスクを行っており、拡張しづらい

- **location_infoディクショナリから値を抽出する**
- **「国」を取得し、なければ「Planet Earth」にする**
- **「都市」の優先順位を調べ、何も見つからなかったら、デフォルトで「Middle-of-Nowhere」にする**
- **placeを更新する**

```javascript
// 改善例）個別に解決するようなコード
// location_infoディクショナリから値を抽出
var town = location_info["LocalityName"];
var city = location_info["SubAdministrativeAreaName"];
var state = location_info["AdministrativeAreaName"];
var country = location_info["CountrydName"];
-------------------------------------------------------
// 先に値デフォルト値を設定して、値が見つかったら書き換える。
var second_half = "Planet Earth";
if (country) {
	second_half = country;
}
if (state && country === "USA") {
	second_half = state;
}
-------------------------------------------------------
// 都市の優先順位順にデフォルト値を設定し、値が見つかったら書き換える
var first_half = "Middle-of-Nowhere";
if (state && country !== "USA") {
	first_half = state;
}
if (city) {
	first_half = city;
}
if (town) {
	first_half = town;
}
---------------------------------------------------------
// 最後に情報をつなぎ合わせる
return first_half + ", " + second_half;
```
サンプル③：http通信毎に統計値を更新する関数
```javascript
// (失敗例)複雑なHttpDownloadオブジェクトを処理する
void UpdateCounts(HttpDownload hd) {
	//　可能であればExit Stateを見つける
	if (!hd.has_event_log() || !hd.event_log().has_exit_state()) {
		counts["Exit State"]["unknown"]++;
	} else {
		string state_str = ExitStateTypeName(hd.event_log().exit_state());
		counts["Exit State"][state_str]++;
	}
	// HTTPヘッダがなければ、残りの要素に"unknown"を設定する
	if (!hd.has_http_headers()) {
		counts["Http Response"]["unknown"]++;
		counts["Content-Type"]++;
		return;
	}
	
	HttpHeader haders = hd.http_haders();

	// HTTPレスポンスをログに記録する。なければ"unknown"と記録する
	if (!headers.has_response_code()) {
		counts["Http Response"]["unknown"]++;
	} else {
		counts["Http Response"]["code"]++;
	} 
	// Content-Typeをログに記録する。なければunknownと記録する
	if (!haders.has_content_type()) {
		counts["Content-Type"]["unknown"]++;
	} else {
		string content_type = ContentTypeMime(haders.content_type());
		counts["Content-Type"]["content_type"]++;
	}
}
```
このコードは以下の４つのタスクを行っている。


1. **キーのデフォルト値に「unknown」を使う**
2. **HttpDownloadのメンバがあるかどうかを確認する。**
3. **値を抽出して文字列に変換する**
4. **counts[ ]を更新する**

```javascript
// 改善例）タスクを別々の領域に分割した例
void UpdateCounts(HttpDownload hd) {
	// タスク：抽出したい値にデフォルト値に設定する
	string exit_state = "unknown";
	string http_response = "unknwon";
	string content_type = "unknwon";

	// タスク：HttpDownloadから値を１つずつ抽出する
	if (hd.has_event_log() && hd.event_log().has_exit_state()) {
		exit_state = ExitStateTypeName(hd.event_log().exit_state());
	}
	if (hd.has_http_headers() && hd.http_headers().has_response_code()) {
		http_response = StringPrintf("%d", hd.http_haders().response_code());
	}
	if (hd.has_http_headers() && hd.http_headers().has_content_type()) {
		content_type = ContentTypeMime(hd.http_headers().content_type());
	}

	// タスク：counts[ ]を更新する
	counts["Exit State"][exit_state]++;
	counts["Http Response"][http_response]++;
	counts["Content-Type"][content_type]++;
}
```
<br>

#### 例５）ロジックを明確に説明する

（コードを書くときに意識すること）
1. **コードの動作を簡単な言葉で同僚にもわかるように説明する**
2. **その説明の中で使っているキーワードやフレーズに注目する**
3. **その説明に合わせてコードを書く**

```javascript
// 失敗例）　ページに権限があるかないかを確認し、なければユーザーにそのことを知らせる機能
$is_admin = is_request();
if ($document) {
	if (!is_admin && ($document['username'] != $_SESSION['username'])) {
		return not_authorize();
	}
} else {
	if(!$is_admin) {
		return not_authorized();
	}
}
```
このコードにはたくさんのロジックが存在する。ロジックをもっと単純化し、簡単な言葉で説明する。

<aside>
 権限があるのは、以下の２つ。

１）管理者

２）文書の所有者（文書がある場合）

その他は、権限がない

</aside>

```javascript
// 改善例）この説明から思いついた新しい解決策（否定形を無くした形）
if (is_admin_request()) {
	//権限あり
} elseif ($document && ($document['usename'] == $_SESSION['username'])) {
	// 権限あり
} else {
	return not_authrized();
}
```
サンプル②：大きな問題にこの手法を適用する
```python
# 例）株式の購入を記録するシステム（３つのテーブルが全てtimeでソートされており、３つのtimeが一致する行だけを検索して、一致しないものは無視）
def PrintStockTransactions():
	stock_iter = db_read("SELECT time, ticker_symbol FROM ...")
	price_iter = ...
	num_shares_iter = ...
	
	# 3つのテーブルの行を一度にイテレートする
	while stock_iter and price_iter and num_shares_iter:
		stock_time = stock_iter.time
		price_time = price_iter.time
		num_shares_time = num_shares_iter.time

	# 3つの行いに同じtimeが含まれていない場合、最も過去の行をスキップする
	# 注意：最も過去の行が２つ一致しているいこともあるので、"<="は"<"にできなくなる
	if stock_time != price_time or stock_time != num_shares_time:
		if stock_time <= price_time and stock_time <= num_shares_time:
			stock_iter.NextRow()
		elif price_time <= stock_time and price_time <= num_shares_time:
			price_iter.NextRow()
		elif num_shares_time <= stock_time and num_shares_time <= price_time:
			num_shares_iter.NextRow()
		else:
			assert False # 不可能
    continue

	assert stock_time == price_time == num_shares_time

	# 一致した行を印字する
	print "@", stock_time,
	print stock_iter.ticker_symbol,
	print price_iter.price,
	print num_shares_iter.number_of_shares

	stock_iter.NextRow()
	price_iter.NextRow()
	num_shares_iter.NextRow()
```
このコードは動くがかなり分かりにくい。→これからやろうとしていることを簡単な言葉で説明する

### 解決策を言葉で説明する

1. **３つの行のイテレータを一度に読み込む**
2. **行のtime一致していなければ、一致するまでの行を進める**
3. **一致した行を印字して、行を進める**
4. **一致する行がなくなるまでこれを繰り返す**

解決策）一番汚い「一致するまで行を進める」部分を綺麗にするため、新しい関数AdvanceToMathcingTime()に抽出する

```python
def PrintStockTransactions():
	stock_iter = db_read("SELECT time, ticker_symbol FROM ...")
	price_iter = ...
	num_shares_iter = ...
	
	# 3つのテーブルの行を一度にイテレートする
	while true:
		time = AdvanceToMatchingTime(stock_iter, price_iter, num_shares_iter)
		if time is None:
			return

	# 一致した行を印字する
	print "@", stock_time,
	print stock_iter.ticker_symbol,
	print price_iter.price,
	print num_shares_iter.number_of_shares

	stock_iter.NextRow()
	price_iter.NextRow()
	num_shares_iter.NextRow()
```
同様にAdvanceToMatchingTime()を綺麗にする。↓コードに必要なことの説明

<aside>
１）現在の行のtimeを見る。一致していれば終了する。

２）一致していなければ「遅れている」行を進める。

３）行が一致するまで（あるいはイテレーションのいずれかが終了するまで）これを繰り返す

</aside>

改善例）stock_iterなどの問題に特化した詳細についれ言及せず、より簡単な命名に改善している

```python
def AdvanceToMatchingTime(row_iter1, row_iter2, row_iter3):
	while row_iter and row_iter2 and row_iter3:
		t1 = row_iter1.time
		t2 = row_iter2.time
		t3 = row_iter3.time

		if t1 == t2 == t3:
			return t1
		
		tmax = max(t1, t2, t3)

		# いづれかの行が「遅れている」のであれば、その行を進める
		# 最終的に全ての行が一致するまでwhileループを繰り返す
		if t1 < tmax: row_iter1.NextRow()
		if t2 < tmax: row_iter2.NextRow()
		if t3 < tmax: row_iter3.NextRow()
	
	return None #　一致する行が見つからない
```
<br>

#### 例６）短いコードを書く

プロジェクトが成長しても、以下のことを意識して**コードをできるだけ小さく軽量に維持する必要がある。**

●**汎用的な「ユーティリティ」コードを作って、重複コードを削除する**

**●実生のコードや無用の機能を削除する**

**●プロジェクトをサブプロジェクトに分割する**

**●コードの「重量」を意識する。軽量で機敏にしておく。**

<br>

#### 例７）ライブラリを活用する

ライブラリを活用することで、コード量を少なくできる！

### →たまには標準ライブラリを15分程度確認するべき！
