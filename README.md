# QRCodeLibJava
QRCodeLibJavaは、Javaで書かれたQRコード生成ライブラリです。  
JIS X 0510に基づくモデル２コードシンボルを生成します。

## 特徴
- 数字・英数字・8ビットバイト・漢字モードに対応しています
- 分割QRコードを作成可能です
- 1bppまたは24bpp BMPファイル(DIB)へ保存可能です
- 1bppまたは24bpp Imageオブジェクトとして取得可能です  
- 画像の配色(前景色・背景色)を指定可能です
- 8ビットバイトモードでの文字コードを指定可能です


## クイックスタート
QRCodeLibプロジェクト、またはビルドした QRCodeLib.dll を参照設定してください。


## 使用方法
### 例１．単一シンボルで構成される(分割QRコードではない)QRコードの、最小限のコードを示します。

```java
import java.awt.Image;

import ys.qrcode.ErrorCorrectionLevel;
import ys.qrcode.Symbols;
import ys.qrcode.Symbol;

public void Example() {
    Symbols symbols = new Symbols();
    symbols.appendString("012345abcdefg");

    Image image = symbols.get(0).get24bppImage();
}
```

### 例２．誤り訂正レベルを指定する
Symbolsクラスのコンストラクタ引数 ecLevel に、ErrorCorrectionLevel列挙型の値を設定します。

```java
Symbols symbols = new Symbols(ErrorCorrectionLevel.H);
```

### 例３．型番の上限を指定する
Symbolsクラスのコンストラクタ引数 maxVersion を設定します。
```java
Symbols symbols = new Symbols(10);
```

### 例４．8ビットバイトモードで使用する文字コードを指定する
Symbolsクラスのコンストラクタ引数 byteModeCharset を設定します。
```java
Symbols symbols = new Symbols("utf-8");
```

### 例５．分割QRコードを作成する
Symbolsクラスのコンストラクタ引数 allowStructuredAppend を設定します。型番の上限(maxVersion引数)を指定しない場合は、型番40を上限として分割されます。

```java
Symbols symbols = new Symbols(true);
```

型番1を超える場合に分割し、各QRコードのImageオブジェクトを取得する例を示します。

```java
Symbols symbols = new Symbols(1, true);
symbols.AppendString("abcdefghijklmnopqrstuvwxyz");

for (Symbol symbol : symbols) {
    Image image = symbol.get24bppImage();
}
```

### 例６．BMPファイルへ保存する
SymbolクラスのSave1bppDIB、またはSave24bppDIBメソッドを使用します。

```java
Symbols symbols = new Symbols();
symbols.appendString("012345abcdefg");
Symbol symbol = symbols.get(0);

symbol.save1bppDIB("D:\\qrcode1bpp1.bmp");
symbol.save1bppDIB("D:\\qrcode1bpp2.bmp", 10); // 10 pixel par module
symbol.save24bppDIB("D:\\qrcode24bpp3.bmp");
symbol.save24bppDIB("D:\\qrcode24bpp4.bmp", 10); // 10 pixel par module
```