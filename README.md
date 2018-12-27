# katalonstudio
Katalon Studioのテスト実行のサンプルプロジェクト。

## 構成
```
├─ project - …           Katalon Studioのテストケース
└─ Jenkinsfile           Jenkinsパイプライン
```
## 前提
 - `Katalon Studio`が`C:\KatalonStudio`にインストールされている(`C:\KatalonStudio\katalon.exe`)
 - インターネット接続可能な端末であること(テストはGoogleで検索する処理)

## Jenkinsパイプライン概要
 - 「パイプライン」ジョブを想定したパイプライン
 -  テスト結果のレポートを成果物として保存

