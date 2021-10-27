# tenji-maker-challenge
Qiita Advent Calendar 2021の特別企画、「Rubyプログラミング問題にチャレンジ！ －改訂版・チェリー本発売記念－」の提出用リポジトリです。

このアドベントカレンダー企画に参加される方はこのリポジトリをフォークし、自分の書いたコードでプルリクエストを作成してください。

## 企画の概要

この企画では「プロを目指す人のためのRuby入門」の著者である伊藤淳一（@jnchito）から、Rubyを使ったプログラミング問題を出します。「我こそは！」という人は解答となるコードを書いて、アドベントカレンダーの記事として投稿してください。

提出されたコード（記事）中から、僕・伊藤淳一が「これはイケてる！！」と思ったコードを表彰します。

## 「あれ？アドベントカレンダーってそういうもんだったっけ？」

特別企画なので細かいことは気にしないでください！！

## 参加資格

初心者から上級者までどなたでもOKです。書籍「プロを目指す人のためのRuby入門（通称チェリー本）」を持っていてもいなくても構いません。「解答したい！」と思った人から早いもの勝ちでアドベントカレンダーに参加登録していってください。

## 今回のお題「点字メーカープログラム」

この企画ではみなさんに「点字メーカープログラム」を作成してもらいます。このプログラムでは入力されたローマ字に対応する点字をテキストで出力します。以下はこのプログラムの実行例です。

```ruby 
tenji_maker = TenjiMaker.new
puts tenji_maker.to_tenji('A HI RU')
#=> o- o- oo
#   -- o- -o
#   -- oo --

puts tenji_maker.to_tenji('KI RI N')
#=> o- o- --
#   o- oo -o
#   -o -- oo
```

- ローマ字（に対応するひらがな）から点字への変換ルールは以下のwebページに説明されている内容に従うものとします。

http://www.naiiv.net/braille/?tenji-sikumi

![Screen Shot 2021-10-28 at 6.39.12.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/7465/1c80d44b-ae0f-1153-b29d-d92be6965380.png)
*引用 [全視情協:点字とは \- 点字のしくみ](http://www.naiiv.net/braille/?tenji-sikumi)*

- 点字の点が出力される部分には`o`の文字を、出力されない部分には`-`の文字をそれぞれ出力してください。
- 上の実行例のように、点字と点字の間は半角スペースで区切ってください。

### 入力テキストについて

入力テキストは半角大文字のローマ字とします。文字と文字の間は半角スペースで区切ってください。ローマ字表記の形式は訓令式とします。訓令式については以下のwebページを参考にしてください。

https://green.adam.ne.jp/roomazi/kunreisiki.html

![Screen Shot 2021-10-28 at 6.42.53.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/7465/6ff9bed3-cd5a-452c-d567-a7af7697a574.png)
*引用 [訓令式](https://green.adam.ne.jp/roomazi/kunreisiki.html)*

### 入力テキストの例

- あひる = A HI RU
- きりん = KI RI N
- しまうま = SI MA U MA
- にわとり = NI WA TO RI
- ひよこ = HI YO KO
- きつね = KI TU NE

なお、上記の入力テキストの例はこのリポジトリのテストコード内で使われています。

```ruby 
class TenjiMakerTest < Minitest::Test
  def setup
    @tenji_maker = TenjiMaker.new
  end

  def test_a_hi_ru
    tenji = @tenji_maker.to_tenji('A HI RU')
    assert_equal <<~TENJI.chomp, tenji
      o- o- oo
      -- o- -o
      -- oo --
    TENJI
  end

  def test_ki_ri_n
    tenji = @tenji_maker.to_tenji('KI RI N')
    assert_equal <<~TENJI.chomp, tenji
      o- o- --
      o- oo -o
      -o -- oo
    TENJI
  end

  # 以下省略
```

### 変換対象となるローマ字・ならないローマ字

変換対象となるローマ字は以下のとおりです。

- あいうえお、かきくけこ、（省略）、やゆよ、らりるれろ、わ、ん

仕様を簡単にするため、以下のローマ字は対応不要です。

- を
- 促音（「らっこ」のような、小さな「っ」）
- 長音（「こーもり（こうもり）」のような、伸びる音）
- 濁音（がぎぐげご、など）
- 半濁音（ぱぴぷぺぽ）
- 拗音・拗半濁音（きゃきゅきょ、ぎゃぎゅぎょ、ぴゃぴゅぴょ、など）

### その他：異常系の考慮は不要

仕様を簡単にするため、以下のような異常系の入力を考慮する必要はありません。

- 対応不要のローマ字（例 YA GI、BU TA）
- ヘボン式で入力されたローマ字（例 SHI MA U MA、KI TSU NE）
- ありえないローマ字や半角大文字以外の文字（例 XYZ、ne ko、羊）
- 半角スペースで区切られていない（例 HIYOKO）
- 半角スペースが2文字以上入っている（例 TO&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RA）
- 空文字列や文字列以外のオブジェクト（数値や`nil`）

## 技術要件

### 雛形リポジトリについて

このリポジトリはコードを提出するための雛形となるGitHubリポジトリです。

### 実行環境について

- Ruby 3.0で動作すること
- 追加でインストールが必要なgemを使用しないこと
- Bundlerは使用しないこと

### 自分が書いたコードの配置について

- 実行用プログラムは`lib`ディレクトリに置くこと。必要に応じてファイルを追加しても良い。
- テストコードは`test`ディレクトリに置くこと。必要に応じてファイルやテストパターンを追加しても良い。
- `lib`ディレクトリと`test`ディレクトリ以外のコードは触らないこと。
- 雛形リポジトリに最初から配置しているテストコードも変更不可。

### 提出の必須条件

[このリポジトリにあるテストコード](https://github.com/JunichiIto/tenji-maker-challenge/blob/main/test/tenji_maker_test.rb)がすべてパスすること。テストは`rake`コマンドで全件実行することができる。

```
$ rake
Run options: --seed 41041

# Running:

......

Finished in 0.000333s, 18018.0194 runs/s, 18018.0194 assertions/s.
6 runs, 6 assertions, 0 failures, 0 errors, 0 skips
```

## コードの提出方法

### git/GitHubに慣れている方

1. この雛形リポジトリをフォークする
2. コードが書けたらプルリクエストを作る
3. GitHub ActionのテストがパスすればOK
4. プルリクエストのリンクをアドベントカレンダーの記事に載せる

### git/GitHubに慣れていない方

1. このリポジトリのコードをローカルにダウンロードする
2. ローカルでコードを書く
3. `rake`コマンドでテストが全部パスすれば完成
4. アドベントカレンダーの記事に自分が書いたコードと`rake`コマンドの実行結果を載せる

## アドベントカレンダーの記事に書いてほしいこと

- プルリクエストのリンク、または自分が書いたコード
- ロジックの説明
- コードのアピールポイント
    - 頑張ったところ
    - 苦労したところ
    - 工夫したところ
    - 自慢したいところ
    - etc
- 伊藤さんにメッセージ（もしあればw）

## 「あれ、ちょっと待って！これだと、他の人のコードが見えちゃうんじゃ？？」

はい、見ようと思ったら見えちゃいますが、この企画に参加する人は自分がコードを提出するまで、他の人のコードはなるべく見ないようにお願いします！（今回は「性善説」でいきます）

## 表彰の選定基準

ひとことで言うと、僕が「いいね！」と思ったコードを表彰するのですが、もう少し具体的に言うと、以下のようなポイントを重視します。

- 可読性が高いコードであること
- 簡潔なコードであること
- コードの解説が読者視点を意識したものになっていること

なお、提出してもらったコードのうちいくつかは、僕のQiita記事や勉強会等で僕がコードレビューさせてもらうかもしれません。

## まとめ

この点字メーカープログラムですが、拙著「プロを目指す人のためのRuby入門」の知識があれば、ほぼ解答可能なはずです！2021年12月2日に[改訂版が発売](https://www.amazon.co.jp/dp/4774193976/)されるので、この改訂版をざーっと読んでから解答に着手するのも良いと思います :thumbsup:

過去の日付が空いていたら、その日付にあとからその日付に参加登録してしまうのもアリです。みなさんからカッコいいコードがたくさん届くのを楽しみにしています〜😄

