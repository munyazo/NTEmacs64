NTEmacs64
=========

Windows版Emacs(通称NTEmacs)の64ビット版

ビルド方法
----------

<http://alpha.gnu.org/gnu/emacs/pretest/emacs-24.3.92.tar.xz>
を、ソースに一切手を加ずにビルドする。

### MSYS2をインストールする
<http://sourceforge.net/projects/msys2/>
から **msys2-x86_64-20140704.exe** を取得しインストールする。

### 64ビット環境用のシェルを起動する
インストールディレクトリ直下の **mingw64_shell.bat** を起動する。

### ビルド関連パッケージのインストール
    $ pacman -S base-devel
    $ pacman -S mingw-w64-x86_64

    どっちも超時間掛かる

### ビルドとインストール
    $ export MSYSTEM=MINGW32

    デフォでMINGW64になってconfigureがコケるから騙す為 (32bitビルドになる訳ではない)
    これがミソ

    $ CFLAGS='-Ofast -march=corei7 -mtune=corei7' ./configure --prefix=c:/emacs24.4 --without-pop

    --without-pop すると movemail.exe でPOPが使えなくなるが movemail.exe のビルドが
    コケるから仕方なく… (ソースいじらずに通す方法を思案中)
    インストールディレクトリや最適化オプションは適当に

    $ make bootstrap && make install

    これでおしまい (make install-strip するとなぜかexeが壊れるw)

### 今後の予定
* ビルドしたものをコミットする
* 不具合の修正
 * 起動時に site-lisp/ が無視されている (ddskk をインストールしても、起動時に設定が有効にならない)
 * movemail.exe の POP 対応
* IMEパッチの適用
