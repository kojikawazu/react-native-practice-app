# React Native Expoについて

## Summary

React Nativeによるモバイルアプリを構築したい時、Androidエミュレータや開発環境が必要ですが、手っ取り早く構築したい場合、Expoを利用します。

もちろん、もっとReact Nativeの機能を使いたい場合、Android Studioに移行可能です。

## Expo構築方法

```bash
# プロジェクト構築
npx create-expo-app ReactNativePracApp

# アプリ起動(Web上で動作確認)
npm run web
```

## 実機での動作確認

```bash
# グローバルに必要なモジュールをインストール
# トンネルモードを使用して実機との接続を行うために必要です
sudo npm install -g @expo/ngrok@^4.1.0

# アプリ起動(Androidの実機で動作確認)
npx expo start --tunnel
```

- アプリが起動され、QRコードが表示されます。
- Android上では、Expo Goアプリをインストールし、そのアプリ上でQRコードを読み込みます。
- すると、デバッグアプリが実機で表示されます。