# know-how

機種固有のノウハウ

## 省電力設定について

以下のような症状があった場合には省電力設定が悪さをしている可能性があるため、全部切ってしまうと改善するかもしれない。
- CPUの動作周波数が低い状態で固定されてしまう
- streaming配信視聴中に途切れてしまう

### 省電力設定を切る方法

#### カーネルパラメータ
[参考URL](https://www.kernel.org/doc/html/v5.8/admin-guide/kernel-parameters.html)
```bash
# C-stateを無効化（C1が最大？）
# acpi_idleドライバに変更
# /etc/default/grubの中のGRUB_CMDLINE_LINUX_DEFAULTの行に以下の物を追加
intel_idle.max_cstate=0 processor.max_cstate=0
# 追加例
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash intel_idle.max_cstate=0 processor.max_cstate=0"
# 追加後、下記コマンドで反映
sudo update-grub
```

#### ワイヤレスアダプタ
[参考URL](https://gist.github.com/jcberthon/ea8cfe278998968ba7c5a95344bc8b55)
```bash
# ワイヤレスアダプタの省電力設定をoff
sudo <favorite editor> /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
# wifi.powersaveを2に変更
# 記載例
wifi.powersave = 2
```

## Wifiが途切れる
- 2.4Ghzを使用する（[参考URL](https://bugzilla.kernel.org/show_bug.cgi?id=203709)）
- [省電力設定をオフにする](#ワイヤレスアダプタ)

## サスペンド後にトラックポイントが使用できなくなる
[参考URL](https://bugzilla.redhat.com/show_bug.cgi?id=1560723)
```bash
sudo <favorite editor> /lib/systemd/system-sleep/trackpad
# 下記内容を記載

#!/bin/sh
if [ "${1}" == "post" ]; then
  # サスペンド後にトラックポイントが認識されなくなる問題の回避策
  echo -n none > /sys/devices/platform/i8042/serio1/drvctl
  sleep 1
  echo -n reconnect > /sys/devices/platform/i8042/serio1/drvctl
fi

# 実行できるよう権限変更
sudo chmod 755 /lib/systemd/system-sleep/trackpad
```

## 中ボタンでの貼り付けを禁止する
[参考URL](https://www.virment.com/thinkpad-ubuntu-how-to-disable-middle-button-paste/)
```bash
<favorite editor> ~/.profile

# 下記内容を記載
xinput set-button-map "TPPS/2 Elan TrackPoint" 1 0 3 4 5 6 7
```

## Thermal Throttlingしきい値温度が低い
[これ](https://github.com/erpalma/throttled)を使用してしきい値温度を高くできる。（自分は公式に修正されるのを待つつもり）

## トラックポイントの速度変更
[参考URL](https://wayland.freedesktop.org/libinput/doc/latest/device-quirks.html)
```bash
sudo <favorite editor> /etc/libinput/local-overrides.quirks

# 下記内容を記載
[Trackpoint Override]
MatchUdevType=pointingstick
AttrTrackpointMultiplier=2.0
```

## IM切り替え(Super + Space)時にアプリ一覧が表示される
アプリ一覧はSuper + aキーで表示できるのでアプリ一覧表示（アクティビティ画面）のショートカットキーを変更することで解決する。
```bash
gsettings set org.gnome.mutter overlay-key 'Super_R'
```
