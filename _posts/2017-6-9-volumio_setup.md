---
layout: post
title: Volumio + MinimServer
category: Development
comments: true
tag:
 - raspberrypi
 - volumio
---

ラズパイをDLNAサーバーとするための儀式の備忘録です．

Raspbianでもよかったけど今後I2Sを使ってみたりするかもってことでVolumioを使いました．

VolumioをインストールしたRaspberry Piにログイン．

Javaをインストール．
```
sudo apt-get update && sudo apt-get install oracle-java8-jdk
```

MinimServerをダウンロード．
```
wget http://jminim.com/brac/MinimServer-0.8.4-linux-armhf.tar.gz
```

作業フォルダを作る
```
mkdir minimserver
```

tarを移動．
```
sudo mv MinimServer-0.8.4-linux-armhf.tar minimserver
```

tarを移動したディレクトリに移る．
```
cd /home/pi/minimserver
```

tarを解凍．
```
tar -zxvf MinimServer-0.8.4-linux-armhf.tar.gz
```

MinimServerのセットアップ．
```
minimserver/bin/setup
```

MinimServerをスタート．
```
minimserver/bin/startc
```

ここでLibrary のdirectoryを入力
```
>Enter content directory, or null to continue:
#/mnt/USB
```

苦労することなくこんな感じでDLNAサーバーは完成．

USBを差し込めばLibrary更新時に勝手に追加されるしすごく便利．
