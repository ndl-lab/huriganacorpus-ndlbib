# huriganacorpus-ndlbib
全国書誌から作成した振り仮名のデータセット

## 1.概要
国立国会図書館の全国書誌データには、幅広い年代の図書・雑誌のタイトルと、タイトルの分かち書きされた振り仮名が含まれています。
振り仮名注釈コーパス（書誌データコーパス）（以下、「本コーパス」）は、
これらのタイトルの分かち書きを行い、対応する振り仮名を付与したものです。
注釈データ中に登場する全ての漢字に振り仮名を付与してあります。大量のデータを必要とする機械学習等への利用を想定しています。

## 2.データについて
zipで圧縮されており、次のURLから取得可能です。
>>>ここにデータのURLが入る<<<

### 2.1. データの詳細
注釈コーパスデータ(タブ区切りtxt形式、UTF-8)を公開しています。
内訳は次の通りです。
>>>最終的な内訳を入れる<<<

### 2.2. フォルダ構成
>>>最終的なフォルダ構成を入れる<<<

### 2.3. 注釈コーパスデータの形式
行番号を示した行の後、入力文全体の行、入力文全体の読みの行が続き、
その後に分かち書きされた要素ごとに、「入力文の一部」「振り仮名」「注釈対象の性質（漢字、ひらがな、記号）」が改行区切りで入力文末尾まで記述されています。

下記は注釈コーパス中の「吾輩は猫である」に注釈を付与した例です。
|行番号: 360| | |
----|----|---- 
|吾輩は猫である| 		| [入力文] |
|	|ワガハイ ワ ネコ デ アル|	[入力 読み]|
|吾輩| わがはい | 漢字|
|　　|　　 	|分かち書き|
|は |	わ |	ひらがな|
|　　|　　 	|分かち書き|
|猫 |	ねこ |	漢字|
|　　|　　 	|分かち書き|
|で |	で |	ひらがな|
|　　|　　 	|分かち書き|
|ある |	ある |	ひらがな|

### 2.4. 作成手順の概要
分かち書きされた振り仮名が付与された書誌データを活用して、機械学習に基づく読み推定モデルの学習に必要となる振り仮名付きの日本語コーパスを構築しました。
書誌データのタイトルとその振り仮名のペアに対して、
既存の振り仮名注釈付きコーパスや形態素解析辞書などから事前に収集した漢字に対する振り仮名候補に基づく文字レベルのマッチングを行い、振り仮名注釈付き日本語コーパスを構築しました。
なお、前処理で、英文のタイトル、日本語で使用しないと思われる漢字を含むタイトルを除きました。
また、旧字体の一部は、新字体に変換して振り仮名注釈を行っています。
このため、入力文と振り仮名注釈で漢字の文字が異なる場合があります。
詳細は参考文献に記載の論文を参照してください。


## 3.注意点等

・書誌データの振り仮名は、現代仮名遣いと一部異なっています。
通常の振り仮名に変換したい場合には追加の置換等が必要です。ご注意ください。

書誌データの作成方法の詳細は、下記をご参照ください
書誌データQ&A
<https://www.ndl.go.jp/jp/data/faq/index.html>
「読みの基準」
<https://www.ndl.go.jp/jp/data/catstandards/characters/index.html#yomi>

・注釈コーパスデータには旧字体が含まれていますので、テキストエディタによっては、正しく文字が表示されなかったり、編集すると文字化けを起こすことがあります。

・本コーパスにおける振り仮名が正確でない場合があります。
自作ツールで正確性のチェックを行っていますが、
例えば「金田一」の振り仮名が「きんんだいち」でも、正しく振り仮名注釈ができたと判断する場合があります。
また、日本語では「川」を「かわ」「がわ」と読んだり、「匹」を「ひき」「ぴき」と読んだりするため、あいまいな文字一致を行っています。
このため「神奈川」が「かなかわ」でも正しく振り仮名注釈ができたと判断しています。

・長音符として使用している「-」は、たとえば「コ-ヒ」は、「コ(カタカナ)」「-(記号)」「ヒ(カタカナ)」となるため、後処理で「コ-ヒ(カタカナ)」に変換しています。

## 4. 背景
視覚障碍者の情報障害の改善を目指して本研究を開始しました。
重度視覚障害者は、パソコンで画面読み上げソフトを使用して、漢字交じりの文書を音声で聞いていますが、
しばしば発生する読み上げの誤りに悩まされています。
例えば、「表に出る」を「ひょうにでる」と読み上げられると理解が困難になります。
こうした誤りの訂正には機械学習による自然言語処理が有効と考えられますが、教師データとして
漢字に正しい振り仮名がつけられた大量のデータが必要なため、まずコーパスの作成に取り組みました。


## 5. 参考文献
佐藤文一, 吉永直樹, and 喜連川優. 
"書誌データ・青空文庫・点字データを用いた振り仮名注釈付き日本語コーパスの構築."
情報処理学会第15回アクセシビリティ研究会 研究報告 2021年3月

佐藤文一, 喜連川優. "事前学習済み BERT の単語埋め込みベクトルによる同形異音語の読み誤りの改善
情報処理学会第12回アクセシビリティ研究会 研究報告 2020年3月

このコーパスを利用して研究等を実施する場合には、上記の参考文献の論文を引用頂けますと幸いです。

## 7. 本件に関する問い合わせ先
lab@ndl.go.jp
何かお気づきの点がありましたら、お気軽にお問い合わせください。
