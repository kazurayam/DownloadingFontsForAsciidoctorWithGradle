

文書 [https://h1romas4.github.io/asciidoctor-gradle-template/index.html](AsciidoctorとGradleでつくる文書執筆環境) を補完するノウハウをここで紹介する。


## 解決すべき問題

わたしは自分のPCでこの文書のサンプルを展開し、出来たディレクトリの内容一式をGitHub上のレポジトリに格納するということをした。

「3.1 サンプル文書の変換を試す」に下記のことをせよと書いてある。わたしもやってみた。

```
$ mkdir ~/tmp
$ cd ~/tmp
```

してから

```
$ curl -L -O https://github.com/h1romas4/asciidoctor-gradle-template/archive/master.zip 
$ unzip master.zip 
$ cd asciidoctor-gradle-template-master 
$ ./gradlew docs 
BUILD SUCCESSFUL in 19s 
2 actionable tasks: 2 executed
```
この操作は成功した。ただし時間はかかった。zipファイルのサイズは160メガバイトあって、わたしのネット環境が実行速度1.2メガbpsぐらいで、curlコマンドがダンロード完了するのに3分かかった。

わたしはGitHubにasciidoctor-gradle-templateレポジトリを作り、自PC上の ~/tmp/asciidoctor-gradle-template ディレクトリの中身をまるごとアップした。

```
$ cd ~/tmp/asciidoctor-gradle-template
$ git init
$ git add .
$ git commit -m "first commit"
$ git branch -M main
$ git remote add origin git@github.com:kazurayam/asciidoctor-gradle-template.git
$ git push -u origin main
```

pushが完了するのに何分かかったか?

26分かかりました。

このプロジェクトはGitHubに格納するには巨大すぎる。

何がサイズを占めているのか？

```
$ tree -sh --du .
.
├── [1.0K]  LICENSE
├── [1.1K]  README.adoc
├── [2.5M]  build
│   ├── [2.5M]  docs
│   │   ├── [1.2M]  asciidoc
│   │   │   ├── [  64]  Chapter01
│   │   │   ├── [128K]  Chapter02
│   │   │   │   └── [128K]  images
│   │   │   │       ├── [ 54K]  AdoptOpenJDK.png
│   │   │   │       ├── [ 48K]  windows-01.png
│   │   │   │       └── [ 26K]  windows-02.png
│   │   │   ├── [1.0M]  Chapter03
│   │   │   │   └── [1.0M]  images
│   │   │   │       ├── [5.1K]  diag-sequence-sample1.svg
│   │   │   │       ├── [1.9K]  diag-sequence-sample2.svg
│   │   │   │       ├── [4.0K]  diag-sequence-sample3.svg
│   │   │   │       ├── [243K]  html.png
│   │   │   │       ├── [360K]  pdf.png
│   │   │   │       ├── [ 14K]  vscode-asciidoc-security1.png
│   │   │   │       ├── [ 35K]  vscode-asciidoc-security2.png
│   │   │   │       ├── [273K]  vscode-asciidoc.png
│   │   │   │       ├── [ 13K]  vscode-extention1.png
│   │   │   │       ├── [ 28K]  vscode-extention2.png
│   │   │   │       └── [ 46K]  windows-01.png
│   │   │   └── [ 69K]  index.html
│   │   └── [1.3M]  asciidocPdf
│   │       ├── [ 11K]  Chapter03
│   │       │   └── [ 11K]  images
│   │       │       ├── [5.1K]  diag-sequence-sample1.svg
│   │       │       ├── [1.9K]  diag-sequence-sample2.svg
│   │       │       └── [4.0K]  diag-sequence-sample3.svg
│   │       └── [1.3M]  index.pdf
│   └── [4.3K]  tmp
│       ├── [2.0K]  asciidoctor.javaexec-data
│       └── [2.1K]  asciidoctorPdf.javaexec-data
├── [2.0K]  build.gradle
├── [2.5M]  docs
│   ├── [  64]  Chapter01
│   ├── [128K]  Chapter02
│   │   └── [128K]  images
│   │       ├── [ 54K]  AdoptOpenJDK.png
│   │       ├── [ 48K]  windows-01.png
│   │       └── [ 26K]  windows-02.png
│   ├── [1.0M]  Chapter03
│   │   └── [1.0M]  images
│   │       ├── [4.8K]  diag-sequence-sample1.svg
│   │       ├── [1.8K]  diag-sequence-sample2.svg
│   │       ├── [3.8K]  diag-sequence-sample3.svg
│   │       ├── [243K]  html.png
│   │       ├── [360K]  pdf.png
│   │       ├── [ 14K]  vscode-asciidoc-security1.png
│   │       ├── [ 35K]  vscode-asciidoc-security2.png
│   │       ├── [273K]  vscode-asciidoc.png
│   │       ├── [ 13K]  vscode-extention1.png
│   │       ├── [ 28K]  vscode-extention2.png
│   │       └── [ 46K]  windows-01.png
│   ├── [ 69K]  index.html
│   └── [1.3M]  index.pdf
├── [ 83K]  gradle
│   ├── [ 25K]  repos
│   │   └── [ 25K]  gem
│   │       ├── [ 18K]  asciidoctor-nabetani-0.1.4-ruby25-patched.gem
│   │       └── [6.5K]  prawn_svg_font_patch-0.1.0.gem
│   └── [ 58K]  wrapper
│       ├── [ 58K]  gradle-wrapper.jar
│       └── [ 200]  gradle-wrapper.properties
├── [5.6K]  gradlew
├── [2.7K]  gradlew.bat
├── [  39]  settings.gradle
└── [244M]  src
    └── [244M]  docs
        └── [244M]  asciidoc
            ├── [243M]  @font
            │   ├── [ 12M]  RictyDiminished
            │   │   ├── [2.1K]  README.md
            │   │   ├── [1.5M]  RictyDiminished-Bold.ttf
            │   │   ├── [1.6M]  RictyDiminished-BoldOblique.ttf
            │   │   ├── [1.5M]  RictyDiminished-Oblique.ttf
            │   │   ├── [1.5M]  RictyDiminished-Regular.ttf
            │   │   ├── [1.5M]  RictyDiminishedDiscord-Bold.ttf
            │   │   ├── [1.6M]  RictyDiminishedDiscord-BoldOblique.ttf
            │   │   ├── [1.5M]  RictyDiminishedDiscord-Oblique.ttf
            │   │   └── [1.5M]  RictyDiminishedDiscord-Regular.ttf
            │   ├── [100M]  genshin
            │   │   ├── [4.7M]  GenShinGothic-Bold.ttf
            │   │   ├── [4.8M]  GenShinGothic-ExtraLight.ttf
            │   │   ├── [4.7M]  GenShinGothic-Heavy.ttf
            │   │   ├── [4.8M]  GenShinGothic-Light.ttf
            │   │   ├── [4.7M]  GenShinGothic-Medium.ttf
            │   │   ├── [4.7M]  GenShinGothic-Monospace-Bold.ttf
            │   │   ├── [4.8M]  GenShinGothic-Monospace-ExtraLight.ttf
            │   │   ├── [4.7M]  GenShinGothic-Monospace-Heavy.ttf
            │   │   ├── [4.8M]  GenShinGothic-Monospace-Light.ttf
            │   │   ├── [4.7M]  GenShinGothic-Monospace-Medium.ttf
            │   │   ├── [4.7M]  GenShinGothic-Monospace-Normal.ttf
            │   │   ├── [4.7M]  GenShinGothic-Monospace-Regular.ttf
            │   │   ├── [4.8M]  GenShinGothic-Normal.ttf
            │   │   ├── [4.8M]  GenShinGothic-P-Bold.ttf
            │   │   ├── [4.9M]  GenShinGothic-P-ExtraLight.ttf
            │   │   ├── [4.8M]  GenShinGothic-P-Heavy.ttf
            │   │   ├── [4.9M]  GenShinGothic-P-Light.ttf
            │   │   ├── [4.8M]  GenShinGothic-P-Medium.ttf
            │   │   ├── [4.8M]  GenShinGothic-P-Normal.ttf
            │   │   ├── [4.8M]  GenShinGothic-P-Regular.ttf
            │   │   ├── [4.7M]  GenShinGothic-Regular.ttf
            │   │   ├── [ 375]  LICENSE_E
            │   │   ├── [ 442]  LICENSE_J
            │   │   ├── [2.0K]  README_E
            │   │   ├── [6.7K]  README_GenShin.txt
            │   │   ├── [2.7K]  README_J
            │   │   └── [4.2K]  SIL_Open_Font_License_1.1.txt
            │   └── [131M]  genyo-font
            │       ├── [ 46M]  JP
            │       │   ├── [6.6M]  GenYoMinJP-Bold.ttf
            │       │   ├── [6.6M]  GenYoMinJP-ExtraLight.ttf
            │       │   ├── [6.6M]  GenYoMinJP-Heavy.ttf
            │       │   ├── [6.6M]  GenYoMinJP-Light.ttf
            │       │   ├── [6.6M]  GenYoMinJP-Medium.ttf
            │       │   ├── [6.6M]  GenYoMinJP-Regular.ttf
            │       │   └── [6.6M]  GenYoMinJP-SemiBold.ttf
            │       ├── [5.8K]  README.md
            │       ├── [4.2K]  SIL_Open_Font_License_1.1.txt
            │       └── [ 85M]  TW
            │           ├── [ 12M]  GenYoMinTW-Bold.ttf
            │           ├── [ 12M]  GenYoMinTW-ExtraLight.ttf
            │           ├── [ 12M]  GenYoMinTW-Heavy.ttf
            │           ├── [ 12M]  GenYoMinTW-Light.ttf
            │           ├── [ 12M]  GenYoMinTW-Medium.ttf
            │           ├── [ 12M]  GenYoMinTW-Regular.ttf
            │           └── [ 12M]  GenYoMinTW-SemiBold.ttf
            ├── [ 41K]  @style
            │   ├── [ 30K]  asciidoctor.css
            │   ├── [3.5K]  coderay-asciidoctor.css
            │   └── [7.2K]  pdf-theme.yml
            ├── [3.7K]  Chapter01
            │   └── [3.6K]  index.adoc
            ├── [134K]  Chapter02
            │   ├── [128K]  images
            │   │   ├── [ 54K]  AdoptOpenJDK.png
            │   │   ├── [ 48K]  windows-01.png
            │   │   └── [ 26K]  windows-02.png
            │   └── [5.6K]  index.adoc
            ├── [1.0M]  Chapter03
            │   ├── [1.0M]  images
            │   │   ├── [4.8K]  diag-sequence-sample1.svg
            │   │   ├── [1.8K]  diag-sequence-sample2.svg
            │   │   ├── [3.8K]  diag-sequence-sample3.svg
            │   │   ├── [243K]  html.png
            │   │   ├── [360K]  pdf.png
            │   │   ├── [ 14K]  vscode-asciidoc-security1.png
            │   │   ├── [ 35K]  vscode-asciidoc-security2.png
            │   │   ├── [273K]  vscode-asciidoc.png
            │   │   ├── [ 13K]  vscode-extention1.png
            │   │   ├── [ 28K]  vscode-extention2.png
            │   │   └── [ 46K]  windows-01.png
            │   └── [ 11K]  index.adoc
            ├── [ 706]  attribute.adoc
            └── [ 451]  index.adoc

 249M used in 37 directories, 121 files

```

`asciidoctor-gradle-template`プロジェクト全体が249メガバイトのところ、`@font`ディレクトリのなかにあるttfフォントのファイルが243メガバイトを占めている。

https://github.com/h1romas4/asciidoctor-gradle-template/archive/master.zip のなかにフォントファイルを含めて配布するというやりかたは良くないとおもう。

https://github.com/h1romas4/asciidoctor-gradle-template/archive/master.zip のなかからフォントファイルを含めないことにしよう。そしてサンプルを利用する人が各自で

- 源真ゴシック - SIL Open Font License 1.1 - http://jikasei.me/font/genshin/
- 源様明朝 - SIL Open Font License 1.1 - https://github.com/ButTaiwan/genyo-font
-Ricty Diminished - SIL Open Font License 1.1 - https://github.com/edihbrandon/RictyDiminished

これら3つのZIPファイルをダウンロードし、unzipせよ。そして

- `src/docs/asciidoc/@font/RictyDiminished`
- `src/docs/asciidoc/@font/genshin`
- `src/docs/asciidoc/@font/genyo-font`

の3つのディレクトリを作って、ttfファイルを収めよう。

そしてプロジェクトの `.gitignore` ファイルには

```
src/docs/asciidoc/@font/
```

と書け。こうすればGitレポジトリのなかに243メガバイトのフォントファイルを含めないようにできる。

## 解決方法

`asciidoctor-gradle-template` プロジェクトの `build.gradle` を改変して`fonts`タスクを追加した。

こうする。

```
$ cd asciidocgtor-gradle-tempalte
$ ./gradlew fonts
```

すると3つのフォントのzipファイルをダウンロードして解凍して`src/docs/asciidoc/@font`ディレクトリのなかにttfファイル群が展開される。