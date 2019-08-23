# 工科のための数学シリーズ

仕様の変更や追加で随時加筆，修正予定

## 2019/08/16

## 文書構造

章見出し（`\chapter`）

節見出し（`\section`）

項（`\subsection`）

小項（`\subsubsection`）

その他，jbookなどの標準的な仕様に準拠

### main.tex
文書ファイルは各章ごとに分けて執筆してください．
ファイル名は`Chap01.tex`のように章番号を付けます．

```latex
\includeonly{
	Chap01,
	Chap02,
	Chap03,
	Chap05,
	Chap06,
	}
```
全体的な章の数によって増減させる必要があります．

`\begin{document}..\end{document}`の間の構成は次のようになります．（「章末問題解答」については後述）

```latex
\begin{document}
\frontmatter
   \tableofcontents
\mainmatter
   \include{Chap01}% 1章
   \include{Chap02}% 2章
   ....
   ....
\begin{章末問題解答}% 章末問題開始
\makeatletter
   \@input{Ans01}% 1章の解答
   \@input{Ans02}% 2章の解答
    ....
    ....
\makeatletter
\end{章末問題解答}% 終了
\printindex
\end{document}
```


### 数式

amsmathパッケージ，bmパッケージ，nccmathパッケージは読み込み済

### 用意した環境
* 各章の導入文（`\chapter`の直下）

   ```latex
   \begin{abstract}
   \end{abstract}
   ```
   
   現段階では`\newenvironment{abstract}{\par}{\par}`のような単なる段落ですが，将来的に何らかの差別化がされる可能性あります．

* theorem系の環境`\begin{ENV*}[]` `*=番号無し`，`[ ]=見出し`
  * 定義 `\begin{定義}`
  * 定理 `\begin{定理}`
  * 補題 `\begin{補題}`
  * 系   `\begin{系}`
  * 命題 `\begin{命題}`
  * 注意 `\begin{注意}`

> theorem系の環境は`*`を付加すると番号が発生しません．`[ ]`で見出しが付きます．
>
> ```latex
> \begin{定義*}[見出し]
> ```


* **証明**
  
  * QEDあり
    ```latex
    \begin{証明}
    \end{証明}
    ```
   * 終端へのQEDなし（独立行数式で終わる場合などに対する`\QED`の`\tag*`による手動指定）
     ```latex
     \begin{証明*}
      ○○○○○○○○○○○○○○○○○○○○○○○○
      ○○○○○○○○○○○○○○○○○○○○○○○○
       \begin{align}
        x & y= z\\
        x & y= z \tag*{\QED}
        \end{aling}
      \end{証明*}
     ```
     
     いずれも（`[ ]`で見出しが付きます）
* **コラム**
   ```latex
    \begin{コラム}
    \end{コラム}
   ```
   改ページがされて，網掛けをした枠で囲みます．（脚注に制限あり）

* **章末問題**
  
  ```latex
  \begin{章末問題}
    \item[問題1] 
    \item[問題2] 
    \item[問題3] 
  \end{章末問題}
  ```
   > `問題1`などのラベルは自動発生も可能ですが，執筆時に記述の**位置**が分からなくなるので，
   > あえて手動で打った方が良いという要望もあり，そのようにしています．
   > これは次項の「解答」も同様です．

* **章末問題 解答**
章末問題と同じフォーマットですが，章を明示させるために網掛けした体裁を用意しています．

  ```latex
 \shadebox{第1章}
   \item[問題1]
   \item[問題2]
   \item[問題3] 
  ```
  ファイル構成は共著での作業を考慮して章ごとの独立した管理になっています．
  
  ```latex
  \begin{章末問題解答}
\makeatletter
   \@input{Ans01}
   \@input{Ans02}
   ....
   ....
\makeatletter
\end{章末問題解答}
  ```
  ファイル名に関しては，`Ans(章番号).tex`としてください．
  必要に応じて，main.texの`\@input{}`を増減させてください．
  
  > 環境名としては，「章末問題解答」ですが，
  > 個々のファイルでは，`\begin{章末問題解答}\end{章末問題解答}`は不要です．


## 執筆について
### label名の命名規則

相互参照のための`\ref`と`\label`では，全体においてユニークなラベルを与える必要がありますが，
共著の場合，知らず知らず重複してしまうケースがありえますので，共通の命名規則が必要です．

従来からの慣例の一例として，`[章番号][図や数式など対象を示すワード][任意の文字，数字]`などがあります．

```latex
\label{C01:fig:1}
\label{C02:eq:13}
```
（**[章番号]**の代わりに**[執筆者のイニシャル]**なども）

### 索引の読みについて
和文の場合，「よみ」を指定しますが，音引き（ー）は直前の語の母音を指定してください．


* アーキテクチャ→あ**あ**きてきちゃ
* ユニタリー行列→ゆにたり**い**ぎょうれつ

また，中黒（・）は読みには含めません．

* 実効的**スピン・スピン**相互作用→じっこうてき**すぴんすぴん**そうごさよう



### デフォルトで読ませているパッケージ

```latex
\usepackage{amsmath}
\usepackage[OT1,T1]{fontenc}
\usepackage{textcomp}
\usepackage{lmodern}
\usepackage[deluxe]{otf}
\usepackage{graphicx,xcolor}
\usepackage{amsmath}
\usepackage{bm}
\usepackage{nccmath}%% 数式で\begin{fleqn}[0pt]など
\usepackage{enumitem}%% 箇条書きのカスタマイズ
\usepackage{emathMw}% 回り込み
\usepackage{makeidx}
\usepackage{macros} 
   \RequirePackage{amsthm}
   \RequirePackage{tcolorbox}
     \tcbuselibrary{raster,skins,breakable,xparse}
```

