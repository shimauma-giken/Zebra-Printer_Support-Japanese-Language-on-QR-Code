# Zebra-Printer_Support Japanese Language on QR Code

### Link-OS: QRコードに日本語データを追加する方法


![1742464592333](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiy_mFz7jmhDD_q5s9RX1t9lmBZ4q1sOTN1LZWU_Aa5a2dba3XYj-g80_B_-PzOM_BPwhJhuSrwm6dCLoB6i2kFcPExxutuR5IoUWgR7lRQK5Z9XzpEvjT-Ih9obdAnVCRF2Zg4exV2w4w/s400/computer_mojibake.png)

QRコードに日本語をデータとして格納することができますが、適切に対処しないとスキャナやスマホカメラで読み取ったときに文字化けが発生します。Link-OSプリンタでにおいて、QRコードを印刷するときの正しいZPLコード記述方法を列記します。

</br>

### 文字化けの仕組み

QRコードにはQRコードは、数字、英字、漢字、カナ、ひらがな、記号、バイナリ、制御コードといったあらゆるデータが扱えるなど、高い汎用性をもっています。
しかし、日本語を含むマルチバイトコードをQRに格納する場合は、スキャナやスマホカメラの仕様に合った文字コードを用いる必要があります。下記のようにQR格納データと読み取り機側の文字コードが異なる場合は文字化けが発生します。

</br>

|QR側文字コード|スキャナ側文字コード|
|-|-|
|UTF-8| Shift-JIS |
|Shift-JIS  | UTF-8|

</br>

スキャナ側に設定されている文字コードは各メーカにお問合せください。

</br>
</br>


### 文字コード別に印刷する例 （データ：あいうえお）

1. UTF-8 で印刷する方法

        <<送信データはUTF-8>>  

        ^XA
        ^FH\^FDLA,あいうえお^FS
        ^PQ2,0,1,Y^XZ

    [サンプル](./あいうえお%20-%20UTF8-文字化け例.prn)

1. Shift-JIS で印刷する方法

        <<送信データはShift-JIS>>  
        
        ^XA
        ^FH\^FDLA,あいうえお^FS
        ^PQ2,0,1,Y^XZ

    [サンプル](./あいうえお%20-%20SJIS.prn)

1. Shift-JIS で印刷する方法 (文字コードを用いた方法）

        ^XA
        ^FH\^FDLA,\82\A0\82\A2\82\A4\82\A6\82\A8^FS
        ^PQ2,0,1,Y^XZ

    [サンプル](./あいうえお%20-%20SJIS文字コード.prn)

---