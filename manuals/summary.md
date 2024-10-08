# React Native Expoについて

## Summary

React Native Expoプロジェクトを構築すると、次のようなフォルダ構成が生成されます。各フォルダとファイルは以下のような役割を持ちます。

### プロジェクトのフォルダ構成

```
ReactNativePracApp/
├── app/                # アプリの各画面やレイアウトのファイルを格納
│   ├── (tabs)/        # タブナビゲーション関連のレイアウト
│   ├── +html.tsx      # HTMLに関連する画面
│   ├── +not-found.tsx # 見つからなかった時の画面
│   └── _layout.tsx    # レイアウトを定義するファイル
├── assets/             # アプリで使用する画像やフォントなどの静的リソース
│   ├── fonts/         # フォントファイルを格納
│   └── images/        # 画像ファイルを格納
├── components/         # UIコンポーネントを格納
│   ├── __tests__/     # テストファイル
│   ├── navigation/    # ナビゲーション関連のコンポーネント
│   ├── Collapsible.tsx
│   ├── ExternalLink.tsx
│   ├── HelloWave.tsx
│   ├── ParallaxScrollView.tsx
│   ├── ThemedText.tsx
│   └── ThemedView.tsx
├── constants/          # 定数ファイルを格納（例: カラーコード）
├── hooks/              # カスタムフックを格納
├── manuals/            # マニュアルやドキュメント
├── scripts/            # プロジェクト管理のためのスクリプト
├── node_modules/       # インストールされた依存パッケージ
├── App.js              # アプリのエントリーポイント
├── app.json            # Expoの設定ファイル
├── babel.config.js     # Babelの設定ファイル
├── package.json        # プロジェクトの依存関係やスクリプトの設定
├── tsconfig.json       # TypeScriptの設定ファイル
└── README.md           # プロジェクトの概要や実行方法の説明
```

- **assets/** */: アプリで使用する画像やフォントなどの静的リソースを格納します。

- **node_modules/** */: インストールされた依存パッケージが格納されます。通常、npm install や yarn install コマンドで生成されます。

- **App.js**: アプリのエントリーポイントとなるファイルです。ここでコンポーネントの構成を定義し、全体のナビゲーションを管理します。

- **app.json**: Expoの設定ファイルです。アプリ名やプラットフォーム固有の設定が記述されています。

- **package.json**: プロジェクトの依存関係やスクリプトの設定が記載されたファイルです。

これらのフォルダとファイルにより、Expoプロジェクトは効率的に構成・管理されます。<br><br>

React Nativeによるモバイルアプリを構築したい時、Androidエミュレータや開発環境が必要ですが、手っ取り早く構築したい場合、Expoを利用します。<br><br>

もちろん、もっとReact Nativeの機能を使いたい場合、Android Studioに移行可能です。<br>

## ページの追加方法

### ページファイルを作成:

- app/ フォルダ内に新しい .tsx ファイルを作成します（例: app/newPage.tsx）。
- このファイルでページに表示するコンポーネントを作成します。

```typescript
// app/newPage.tsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function NewPage() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>This is a new page!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#fff',
  },
  text: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});
```

### ナビゲーションに追加:

- 新しいページをナビゲーションに追加するには、App.js またはナビゲーション関連のファイルを編集します。
- 例えば、React Navigationを使用している場合は、新しいページをスタックナビゲーターに追加します。

```typescript
// App.js
import 'react-native-gesture-handler';
import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './app/HomeScreen';
import NewPage from './app/newPage';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="NewPage" component={NewPage} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

### コンポーネントの追加方法

1. components/ フォルダに新しいコンポーネントファイルを作成:

- 例えば、components/MyButton.tsx というファイルを作成し、ボタンコンポーネントを実装します。

```typescript
// components/MyButton.tsx
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

export default function MyButton({ onPress, title }) {
  return (
    <TouchableOpacity style={styles.button} onPress={onPress}>
      <Text style={styles.text}>{title}</Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: '#007bff',
    padding: 10,
    borderRadius: 5,
    alignItems: 'center',
  },
  text: {
    color: '#fff',
    fontSize: 16,
  },
});
```

2. 作成したコンポーネントを他のページで使用:

- 例えば、App.js や他のページで MyButton コンポーネントをインポートして使用します。

```typescript
import MyButton from './components/MyButton';

// 使用例
<MyButton title="Click Me" onPress={() => alert('Button Pressed!')} />
```

### リビルド方法

- Expoを使用している場合、変更を保存するとホットリロードによって自動的にアプリが更新されます。

  - ホットリロード: ファイルを保存すると、アプリが自動的に更新され、変更がすぐに反映されます。
  - 手動で再ビルドする場合:
    - ターミナルで以下のコマンドを実行してアプリを再起動します。

```bash
npx expo start
```