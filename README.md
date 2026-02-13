# QSAR_yamane_2026-02

本スクリプトは、**二値分類（inactive / active）** を対象に、

- 前処理（Yeo-Johnson → 標準化 → 低分散除去 → 相関除去）
- 学習（**SMOTEは train のみに適用**してリーク回避）
- 複数モデルの性能評価（AUC / F1 / MCC / 感度 / 特異度 など）
- **ACE-style Conformal Prediction（ACE-CP）**
- **HOMO（温度補正なし）との比較**
- **予測集合の幅（難易度）クインタイル別 conditional coverage 評価**
- **CustomS（モデル固有の不確実性 s(x) を使うACE）**
- **固定3モデルコンセンサス（KNN + LDA + LR）** ＋重み付き投票
- 外部候補（biopla_output.csv）への推論＋高信頼候補抽出
- 以上の結果を **CSV / 図（PNG） / Excel（summary_outputs.xlsx）** として出力を行います。

入力データ

1-1) 学習・評価用データ
- **ファイル名**：`output_選択後.csv`
- **エンコード**：`cp932`（スクリプト内で `encoding="cp932"` 指定）
- **必須カラム**
  - `AC50_Active`：目的変数（カテゴリ）。空欄行は除外されます。
- **特徴量（説明変数）の範囲**
  - `df.iloc[:, 19:]`（**19列目以降を特徴量として使用**）
- **欠損**
  - 特徴量側は `dropna()` で欠損行を削除します（欠損が多いと件数が減るので注意）。
 

2-1) 外部候補データ（biopla）
- **ファイル名**：`biopla_output.csv`
- **エンコード**：`cp932`
- **必須条件**
  - `output_選択後.csv` の特徴量列（`X.columns`）を **すべて含む**
  - 欠損行は `dropna()` で除外
- ある場合のみ、スクリプト末尾で外部推論・候補抽出・図作成が実行されます。


## 3. 依存環境
### 3-1) 推奨環境
- Python 3.9+（3.8でも動く場合あり）
- Windows環境でcp932を前提に運用する想定

### 3-2) 必須パッケージ
- numpy
- pandas
- matplotlib
- scikit-learn
- imbalanced-learn
- openpyxl（Excel出力）

### 3-3) 任意パッケージ（入っていれば自動で使用）
- xgboost
- lightgbm
- catboost





