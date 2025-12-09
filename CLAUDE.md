---
name: pine-script-v6
description: TradingView Pine Script v6コード生成。インジケーター、ストラテジー、ライブラリの作成。v6構文、命名規則、スクリプト構成に準拠。「Pine Script」「TradingView」「インジケーター作成」「トレーディング戦略」「テクニカル分析ツール」などのリクエスト時に使用。
---

# Pine Script v6 スキル

TradingView Pine Script v6 を使用したインジケーター、ストラテジー、ライブラリの作成ガイド。

## バージョン宣言

すべてのスクリプトは必ず以下で開始:

```pinescript
//@version=6
```

## スクリプト構成

以下の順序でコードを構成:

```
<license>           // ライセンス表記
<version>           // //@version=6
<declaration>       // indicator() / strategy() / library()
<imports>           // import文
<constants>         // 定数宣言
<inputs>            // input.*()
<functions>         // ユーザー定義関数
<calculations>      // 計算ロジック
<strategy_calls>    // strategy.*() (ストラテジーのみ)
<visuals>           // plot(), label, line等
<alerts>            // alertcondition()
```

## 命名規則

| 対象        | 規則          | 例                              |
| ----------- | ------------- | ------------------------------- |
| 変数・関数  | camelCase     | `maFast`, `pivotHi()`           |
| 定数        | SNAKE_CASE    | `BULL_COLOR`, `MAX_LOOKBACK`    |
| 入力変数    | 末尾に Input  | `maLengthInput`, `showAvgInput` |
| 配列        | 末尾に Array  | `levelsArray`, `colorsArray`    |
| テーブル    | 末尾に Table  | `resultsTable`                  |
| プロット ID | 末尾に PlotID | `maPlotID`                      |

## 宣言文テンプレート

### インジケーター

```pinescript
indicator(
    title = "My Indicator",
    shorttitle = "MI",
    overlay = true,
    max_lines_count = 500,
    max_labels_count = 500
)
```

### ストラテジー

```pinescript
strategy(
    title = "My Strategy",
    shorttitle = "MS",
    overlay = true,
    initial_capital = 100000,
    default_qty_type = strategy.percent_of_equity,
    default_qty_value = 100,
    commission_type = strategy.commission.percent,
    commission_value = 0.1
)
```

## v6 重要変更点

### 型キャストの厳格化

```pinescript
// ❌ v5では可能だがv6ではエラー
float val = 0.0
if val  // int/floatからboolへの暗黙キャスト不可

// ✅ v6での正しい書き方
if val != 0
if not na(val) and val != 0
```

### bool は na を取れない

```pinescript
// ❌ v6ではエラー
bool flag = na

// ✅ v6での正しい書き方
bool flag = false
```

### 遅延評価 (and/or)

```pinescript
// v6ではand/orは遅延評価される
// 左辺がfalseならandの右辺は評価されない
if bar_index > 0 and close[1] > open[1]
    // 安全にclose[1]にアクセス可能
```

### 動的 request.\*()

```pinescript
// v6ではrequest.*()はデフォルトで動的に実行可能
// ループや条件分岐内で呼び出し可能
for tf in timeframes
    data = request.security(syminfo.tickerid, tf, close)
```

### for ループの動的境界

```pinescript
// v6ではforループの終了条件が各反復で再評価される
// 固定境界が必要な場合は事前に変数に代入
int limit = array.size(arr)
for i = 0 to limit - 1
    // ...
```

## コーディング規約

### スペース

```pinescript
// 演算子の両側にスペース
int a = close > open ? 1 : -1
float c = d > e ? d - e : d

// 単項演算子は例外
float a = -b

// カンマ後、名前付き引数にスペース
plot(close, color = color.red)
```

### 行の折り返し

```pinescript
// 4の倍数でないインデントで折り返し（2スペース推奨）
plot(
  series = close,
  title = "Close",
  color = color.blue,
  show_last = 10
)
```

### 定数での var 非使用

```pinescript
// ❌ 定数にvarは使用しない（パフォーマンス低下）
var int MS_IN_DAY = 86400000

// ✅ 定数は直接宣言
int MS_IN_DAY = 86400000
```

### 明示的な型宣言

```pinescript
// 推奨: 型を明示的に宣言
float maValue = ta.sma(close, 20)
int barCount = 0
string labelText = "Signal"
color plotColor = color.blue
```

## 入力パターン

```pinescript
// ————— Inputs
int lengthInput = input.int(14, "Length", minval = 1)
float multiplierInput = input.float(2.0, "Multiplier", step = 0.1)
string sourceInput = input.string("close", "Source", options = ["open", "high", "low", "close"])
color bullColorInput = input.color(color.green, "Bull Color")
bool showLabelsInput = input.bool(true, "Show Labels")
string tfInput = input.timeframe("D", "Timeframe")
```

## 関数ドキュメント

```pinescript
// @function 説明
// @param paramName (型) パラメータ説明
// @returns 戻り値の説明
functionName(paramType paramName) =>
    // 実装
```

## よく使うビルトイン

### テクニカル指標 (ta.\*)

- `ta.sma()`, `ta.ema()`, `ta.wma()`, `ta.rma()`
- `ta.rsi()`, `ta.macd()`, `ta.stoch()`
- `ta.atr()`, `ta.tr()`, `ta.bb()`
- `ta.crossover()`, `ta.crossunder()`
- `ta.highest()`, `ta.lowest()`, `ta.change()`

### ストラテジー (strategy.\*)

- `strategy.entry()`, `strategy.close()`
- `strategy.exit()`, `strategy.cancel()`
- `strategy.position_size`, `strategy.equity`

### 描画

- `plot()`, `plotshape()`, `plotchar()`
- `label.new()`, `line.new()`, `box.new()`
- `table.new()`, `table.cell()`

## サンプル: 基本インジケーター

```pinescript
//@version=6
indicator("SMA Crossover", overlay = true)

// ————— Constants
color BULL_COLOR = color.green
color BEAR_COLOR = color.red

// ————— Inputs
int fastLengthInput = input.int(10, "Fast Length", minval = 1)
int slowLengthInput = input.int(20, "Slow Length", minval = 1)

// ————— Calculations
float fastMA = ta.sma(close, fastLengthInput)
float slowMA = ta.sma(close, slowLengthInput)
bool bullCross = ta.crossover(fastMA, slowMA)
bool bearCross = ta.crossunder(fastMA, slowMA)

// ————— Visuals
plot(fastMA, "Fast MA", color.blue)
plot(slowMA, "Slow MA", color.orange)
plotshape(bullCross, style = shape.triangleup, location = location.belowbar, color = BULL_COLOR)
plotshape(bearCross, style = shape.triangledown, location = location.abovebar, color = BEAR_COLOR)

// ————— Alerts
alertcondition(bullCross, "Bullish Crossover", "Fast MA crossed above Slow MA")
alertcondition(bearCross, "Bearish Crossover", "Fast MA crossed below Slow MA")
```

## サンプル: 基本ストラテジー

```pinescript
//@version=6
strategy("RSI Strategy", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)

// ————— Inputs
int rsiLengthInput = input.int(14, "RSI Length")
int oversoldInput = input.int(30, "Oversold Level")
int overboughtInput = input.int(70, "Overbought Level")

// ————— Calculations
float rsiValue = ta.rsi(close, rsiLengthInput)

// ————— Strategy Calls
if ta.crossover(rsiValue, oversoldInput)
    strategy.entry("Long", strategy.long)
if ta.crossunder(rsiValue, overboughtInput)
    strategy.close("Long")
```

## 参照

- User Manual: https://www.tradingview.com/pine-script-docs/
- Reference: https://www.tradingview.com/pine-script-reference/v6/
- Migration Guide: https://www.tradingview.com/pine-script-docs/migration-guides/to-pine-version-6/
