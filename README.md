# How to install rmagick on Windows 10

## Rake を使って Rmagick を Windows 10 にインストールする手順

### 導入対象

*   1. ImageMagick-6
*   2. rmagick 2.15.4

## 1. ImageMagick

### ダウンロードの注意点

*   使用する Ruby の環境 "x64 or x86(32-bit)" に合わせたバイナリを選択。
*   dll 付きのバイナリを選択。
*   rmagick 2.15.4 は最新の ImageMagick 7 に未対応のようなので、ImageMagick 6 をダウンロードすること。

（例） Ruby x64 の場合:
*   ImageMagick-*-Q*-x64-dll.exe (例： ImageMagick-6.9.5-5-Q16-x64-dll.exe)

（例） Ruby x86(32-bit) の場合:
*   ImageMagick-*-Q*-x86-dll.exe (例： ImageMagick-6.9.5-5-Q16-x86-dll.exe)

### ImageMagick 6 の最新版の場所

*   [ImageMagick binaries - ImageMagick](http://www.imagemagick.org/download/binaries/)

### 注意!

通常の [Windows Binary Release - ImageMagick 7](http://www.imagemagick.org/script/binary-releases.php#windows) では rmagick 2.15.4 のインストールに失敗します。ImageMagick 6 をダウンロードすること。


### インストール

インストール先は、デフォルトのインストールパスを使用します。

私の環境では以下のフォルダにインストールされました。
```
C:\Program Files (x86)\ImageMagick-6.9.5-Q16
```

### インストール時の必須オプション

以下の2つを必ず選択すること

*   Add application directory to your system path
*   Install development headers and libraries for C and C++


## 2. RMagick

rake コマンドを使ってインストールします。

### rakefile を取得

```
>git clone https://github.com/icm7216/How-to-install-RMagick-on-Windows.git
>cd How-to-install-RMagick-on-Windows

```

`rake`コマンドを実行して RMagick のインストールを開始
```
>rake
:found install path
 => C:\Program Files (x86)\ImageMagick-6.9.5-Q16
gem install rmagick --platform=ruby -- --with-opt-dir="C:\Program Files (x86)\ImageMagick-6.9.5-Q16" --with-opt-lib="C:\Program Files (x86)\ImageMagick-6.9.5-Q16\lib" --with-opt-include="C:\Program Files (x86)\ImageMagick-6.9.5-Q16\include"
Fetching: rmagick-2.15.4.gem (100%)
Temporarily enhancing PATH to include DevKit...
Building native extensions with: '--with-opt-dir=C:\Program Files (x86)\ImageMagick-6.9.5-Q16 --with-opt-lib=C:\Program Files (x86)\ImageMagick-6.9.5-Q16\lib --with-opt-include=C:\Program Files (x86)\ImageMagick-6.9.5-Q16\include'
This could take a while...
Successfully installed rmagick-2.15.4
Parsing documentation for rmagick-2.15.4
Installing ri documentation for rmagick-2.15.4
Done installing documentation for rmagick after 8 seconds
1 gem installed
```
これで gem のインストールが完了しました。



## RMagick の動作確認

```
>ruby hello_rmagick.rb
```

上記コマンドを実行後、カレントディレクトリに `Hello_RMagick.png` が出力されればOKです。

![Hello_RMagick.png](./img/Hello_RMagick.png)

おめでとうございます。これでインストール完了です。


# Rake の薦め

通常の RMagick の Windows 環境へのインストールでは ImageMagick のインストールパスと、 include および lib のパスをあわせて指定します。そのため、以下のような長いコマンドラインを作成しなければなりませんでした。

win版 rmagickインストール用のコマンドライン
```
gem install rmagick ^
--platform=ruby -- ^
--with-opt-dir="[path to ImageMagick]" ^
--with-opt-lib="[path to ImageMagick]\lib" ^
--with-opt-include="[path to ImageMagick]\include"
```

----

バージョンアップのため新しい gem をインストールする場合、この作業はとても面倒です。このような場合、はじめに`rakefile`を作成しておけば、2回目以降は`rake`コマンドだけで簡単にインストールできるようになります。



確認環境:

*   Windows 10 pro (64 bit)
*   Ruby 2.3.1 (32 bit)
*   Devkit 32-472 (32 bit)

私の確認環境では Ruby x86 32-bit なので、 ImageMagick 6 の最新版（Aug 11, 2016 現在） [ImageMagick-6.9.5-5-Q16-x86-dll.exe](http://www.imagemagick.org/download/binaries/ImageMagick-6.9.5-5-Q16-x86-dll.exe)をインストールして確認しました。


参考：

* [Installing on Windows · rmagick/rmagick Wiki - GitHub](https://github.com/rmagick/rmagick/wiki/Installing-on-Windows)インストールに於けるいくつかの注意点が書かれています。
* [ruby - Installing RMagick on Windows - Stack Overflow](http://stackoverflow.com/questions/36242042/installing-rmagick-on-windows)
* [[ruby]RMagick導入[windows7]|Akanetrip](http://hatobane.github.io/uncategorized/rmagick-install/)
* [RMagick 2.12.0: How to use RMagick](https://rmagick.github.io/usage.html#annotation)
