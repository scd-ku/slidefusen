# Slide Fusen

スライド表示にコメントの弾幕とふせんボードを重ね、Gemini分類やグラフ表示ができるWebアプリです。

## Web app

https://scd-ku.github.io/slidefusen/

## Firebase

This repository uses the dedicated Firebase project:

`scd-ku-slidefusen`

It does not share Firestore data with the other SCD applications.

## 授業ルーム方式

- 教員が「新しい授業を始める」を押すと6文字の授業コードを作成します。
- Firebase Anonymous Authentication により、授業を作成したブラウザがそのルームの教員になります。
- 生徒はQRコードまたは授業コードで参加し、Googleアカウント等のログイン操作は不要です。
- 生徒は投稿・閲覧・いいねができます。
- 教員だけがGemini分類・削除・全消去などの管理操作を実行できます。
- データは `rooms/{roomId}/notes/{noteId}` に保存され、授業ごとに分離されます。

> 教員権限は授業を作成したブラウザの匿名Firebase IDに紐づきます。サイトデータを消去すると、そのルームの教員権限を失うことがあります。

## Firebase 初回設定

Firebase Consoleで以下を設定してください。

1. Authentication → Sign-in method → **Anonymous** を有効化
2. Firestore Database → `(default)` データベースを作成
3. Firestore → Rules で、このリポジトリの `firestore.rules` を貼り付けて公開

Firebase CLIを使う場合は、対象プロジェクトを選択したうえで:

```bash
firebase deploy --only firestore:rules
```

## Security

- Firebase Web API key はWebクライアント設定であり、認可の秘密鍵としては使用しません。
- Firestoreの権限制御はFirebase Authenticationと `firestore.rules` で行います。
- Firebase Web API key をGemini APIキーとして使わないでください。
- Gemini APIキーはGitHubやFirestoreへ保存しません。
- Gemini APIキーは学校の共用端末に残らないよう、localStorageへの保存を廃止しています。
- 詳細は [SECURITY.md](SECURITY.md) を参照してください。

## License

© 2026 Science Communication Design Laboratory, Kagawa University

- **Code:** MIT License
- **Documentation and educational materials:** CC BY 4.0
- Third-party software, libraries, data, fonts, images, maps, and other external materials remain subject to their respective licenses and terms.

See [LICENSE](./LICENSE) for details.
