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

1. UTF-8 文字列を用いて印刷する方法

        <<送信データはUTF-8>>  

        ^XA
        ^PW406
        ^LL0203
        ^LS0
        ^FO90,50
        ^BQN,2,4
        ^FH\^FDLA,\20あいうえお^FS
        ^PQ1,0,1,Y^XZ

    ※ \20は日本語印刷時に文字化けを防止するための先頭データ
    
    [サンプル](./あいうえお%20-%20UTF8-文字.prn)

    
</br>

1. UTF-8 Hexデータを用いて印刷する方法

        <<送信データはUTF-8>>  

        ^XA
        ^PW406
        ^LL0203
        ^LS0
        ^FO90,50
        ^BQN,2,4
        ^FH\^FDLA,\20\E3\81\82\E3\81\84\E3\81\86\E3\81\88\E3\81\8A^FS
        ^PQ1,0,1,Y^XZ


    [サンプル](./あいうえお%20-%20UTF8-Hex.prn)

</br>


1. Shift-JIS 文字列を用いて印刷する方法


        ^XA
        ^PW406
        ^LL0203
        ^LS0
        ^FO90,50
        ^BQN,2,4
        ^FH\^FDLA,\20あいうえお^FS
        ^PQ1,0,1,Y^XZ

    [サンプル](./あいうえお%20-%20SJIS-文字.prn)
    
</br>

1. Shift-JIS Hexを用いて印刷する方法


        ^XA
        ^PW406
        ^LL0203
        ^LS0
        ^FO90,50
        ^BQN,2,4
        ^FH\^FDLA,\20\82\A0\82\A2\82\A4\82\A6\82\A8^FS
        ^PQ1,0,1,Y^XZ

    [サンプル](./あいうえお%20-%20SJIS-文字.prn)


---