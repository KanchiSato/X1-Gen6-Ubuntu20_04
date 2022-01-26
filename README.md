# X1-Gen6-Ubuntu20.04
My Ubuntu Standard Enviroment

## リポジトリの内容
自分のThinkPad X1 Gen6でのUbuntu20.04の標準環境公開用リポジトリ

下記のプロダクトを利用しています
- [Docker](https://www.docker.com/)
- [ShellCheck](https://www.shellcheck.net/)
- [EditorConfig](https://editorconfig.org/)
- [shfmt](https://github.com/mvdan/sh)
- [Semantic Commit Messages](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716)

その他詳細については[doc](doc)を参照

## マシンスペック
```bash
# 液晶サイズ
$ xrandr | grep '*'
   2560x1440     60.01*+  59.99    59.99    59.96    59.95  
```
```bash
# モデル
$ sudo dmidecode --type system | grep -e "Product Name" -e Version
	Product Name: 20KHCTO1WW
	Version: ThinkPad X1 Carbon 6th
```

## 設定スクリプト
[./scripts/setup-X1-Gen6-Ubuntu20_04](./scripts/setup-X1-Gen6-Ubuntu20_04)を実行

## GNOME Shell Extensions
- [WinTile](https://extensions.gnome.org/extension/1723/wintile-windows-10-window-tiling-for-gnome/)

## BIOS設定

BIOSバージョンごとにデフォルト設定が異なる可能性がある為、重要かもな〜と思う変更のみ記載

【UEFI BIOS Verion】  
```bash
$ sudo dmidecode --type bios | grep Version
	Version: N23ET79W (1.54 )
```

【Config】
- Keyboard/Mouse -> TrackPoint [`Enabled`]
- Keyboard/Mouse -> Trackpad [`Enabled`]
- Keyboard/Mouse -> Fn and Ctrl Key Swap [`Disabled`] 
- Keyboard/Mouse -> Sticky Key [`Disabled`]
- Keyboard/Mouse -> F1-F12 as Primary Function [`Enabled`]
<br><br>
- Power -> Intel (R) SpeedStep technology [`Disabled`]  
Mode for AC [`Maximum Perfor`]  
Mode for Battery [`Battery Optimi`]
- Power -> Adaptive Thermal Management  
Scheme for AC [`Maximize Perfo`]  
Scheme for Battery [`Balanced`]
- Power -> CPU Power Management [`Disabled`]  
- Power -> Sleep State [`Linux`]
<br><br>
- Thunderbolt BIOS Assist Mode -> [`Disabled`]

【Security】
- Fingerprint -> Predesktop Authentication [`Disabled`]
- Secure Boot Configuration -> Secure Boot [`Disabled`]
