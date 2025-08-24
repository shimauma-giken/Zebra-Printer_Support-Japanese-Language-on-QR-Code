# Zebra-Printer_Support Japanese Language on QR Code

### Link-OS: QRコードに日本語データを追加する方法


![1742464592333](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiy_mFz7jmhDD_q5s9RX1t9lmBZ4q1sOTN1LZWU_Aa5a2dba3XYj-g80_B_-PzOM_BPwhJhuSrwm6dCLoB6i2kFcPExxutuR5IoUWgR7lRQK5Z9XzpEvjT-Ih9obdAnVCRF2Zg4exV2w4w/s400/computer_mojibake.png)

QRコードに日本語をデータとして格納することができますが、適切に対処しないとスキャナやスマホカメラで読み取ったときに文字化けが発生します。Link-OSプリンタでにおいて、QRコードを印刷するときの正しいZPLコード記述方法を列記します。

</br>

### 文字化けの仕組み

QRコードにはQRコードは、数字、英字、漢字、カナ、ひらがな、記号、バイナリ、制御コードといったあらゆるデータが扱えるなど、高い汎用性をもっています。
しかし、日本語を含むマルチバイトコードをQRに格納する場合は、スキャナやスマホカメラの仕様に合った文字コードを用いる必要があります。バーコードリーダーに合った適切なコードを記述ください。


</br>

スキャナ側に設定されている文字コードは各メーカにお問合せください。

</br>
</br>


### 文字コード別に印刷する例 （データ：あいうえお）

1. UTF-8 文字列を用いて印刷する方法


        <<送信データフォーマットはUTF-8>>  

        ^XA
        ^FO100,450^A@N,50,50,NOTOMRJ.TTF
        ^CI28^FD日ホンごﾃｽﾄ123^FS
        ^FO100,100^BQN,2,10
        ^CI14^FDLA,日ホンごﾃｽﾄ123^FS
        ^XZ

    ※ QR利用時は^CI値が異なるので注意


    </br>


1. Shift-JIS 文字列を用いて印刷する方法

        <<送信データフォーマットはShift-JIS>>  
        ^XA
        ^SEE:JIS.DAT
        ^FO100,450^A@N,50,50,E:NOTOMRJ.TTF^CI15^FD日ホンごﾃｽﾄ123^FS
        ^FO100,550^A@N,50,50,E:SGMTJ.TTF^CI15^FD日ホンごﾃｽﾄ123^FS
        ^FO100,100^BQN,2,10^CI15^FDLA,日ホンごﾃｽﾄ123^FS
        ^XZ

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

    [サンプル](./あいうえお%20-%20SJIS-Hex.prn)


---