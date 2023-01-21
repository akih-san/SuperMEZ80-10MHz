# SuperMEZ80-10MHz

SuperMEZ80にEMUZ80モニタを移植しました。

MEZで使用ているCPUはzilog Z84C0010PEG 10MHzのCMOS版Z80です。定格の10MHzで使用しています。

ROMプログラム容量の関係でPIC18F47Q84のみサポートしています。

PICのファームウェアに、UARTのXON/XOFFフロー制御を実装し、115.2Kbpsの通信ができます。

CPUが10MHz以下のものを使用する場合は、ファームのボーレートを調整する必要があります。

// UART3 initialize

//	U3BRG = 416;	// 9600bps @ 64MHz

//	U3BRG = 208;	// 19200bps @ 64MHz

//	U3BRG = 104;	// 38400bps @ 64MHz

U3BRG = 34;		// 115200bps @ 64MHz

サンプルボーレートが幾つか選べますので、トライアンドエラーを行ってみてください。

TeraTermでの接続例です。

https://user-images.githubusercontent.com/112370246/213708107-5d3125b2-3d94-4d20-b701-4bde53d1b619.png)

2通りのプログラムを公開します。


１．メモリの空き容量重視のプログラム


モニタープログラムのみＰＩＣに書き込まれています。起動時に、メモリの後方（Ｄ０００Ｈ）にモニターは転送され、
40番地からフリーエリアとなります。

（一般的には100Hからなんでしょうけど、割り込み無いので、40Hからフリーとした）

まぁ、シャープのMZ-80クリーンコンピュータ・・・みたいな（笑）

BASIC等のプログラムは、モニタのロード機能を使います。115Kで通信しますので、ロードも早いです。

書き込むファイルは、

SuperMEZ80_10MHz_Q8x.X.production.hexです。ロードするプログラムは、programフォルダにあります。

PICのファームウェアソースは、emuz80_z80ram.cです。


２．EMUZ80と同じ形式


EMUZ80と同様にPICに、GBASIC、TINY BASIC、GAME80、GAME80コンパイラを収納してあります。

フリーエリアは３２Ｋとなります。３２Ｋで十分だという方は、こちらを使用してください。

書き込むファイルは、

SuperMEZ80_10MHz_Q8x_all.X.X.production.hexです。

PICのファームウェアソースは、emuz80_z80ram_all.cです。


((((( モニタの機能拡張 )))))


モニタRev.B04では、LGコマンド（Load and Go）の機能を追加しました。

ヘキサファイルをロード後、ロードした先頭アドレスにジャンプします。


（メモリマップ）

[SuperMEZ80メモリマップ.pdf](https://github.com/akih-san/SuperMEZ80-10MHz/files/10466937/SuperMEZ80.pdf)


（サンプルプログラム）

・GAME80用のライフゲーム

・startrek_classic

懐かしいaltair basic star trekをGBASICで動かせるようにしてみました。

元のソースは、( http://www.bobsoremweb.com/startrek.html )で公開されています。

（Z80のプログラムソース）

EMUZ80-MON Rev.B04 ( https://github.com/akih-san/EMUEMUZ80-MON )で公開していますので、

そちらを参照してください。
