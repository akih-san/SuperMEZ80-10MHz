# SuperMEZ80-10MHz

SuperMEZ80にEMUZ80モニタを移植しました。
MEZで使用ているCPUはzilog Z84C0010PEG 10MHzのCMOS版Z80です。定格の10MHzで使用しています。

ROMプログラム容量の影響でPIC18F47Q84のみサポートしています。

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
