# JavaScript の Map の簡易ベンチマーク

連想配列を作るときに Map を使うかオブジェクトで済ませるか、Map はどうやって作るのがいいのかを検証したかった。

100 件のデータを登録して、その中からひとつを取得、出力する時間を[`hyperfine`](https://github.com/sharkdp/hyperfine)で比べた。

## 実行

1. `Node`, `hyperfine`のインストール
1. `npm run build`
1. `npm run bench`

## 結果

どれもたいして変わらないっぽい……？

### 1

```txt

Benchmark #1: node build/constructor.js
  Time (mean ± σ):      42.0 ms ±   2.4 ms    [User: 35.8 ms, System: 7.7 ms]
  Range (min … max):    36.7 ms …  49.5 ms    55 runs

Benchmark #2: node build/manySetCall.js
  Time (mean ± σ):      42.3 ms ±   1.8 ms    [User: 36.2 ms, System: 7.5 ms]
  Range (min … max):    36.8 ms …  48.7 ms    65 runs

Benchmark #3: node build/object.js
  Time (mean ± σ):      41.6 ms ±   2.4 ms    [User: 36.1 ms, System: 6.8 ms]
  Range (min … max):    35.4 ms …  50.5 ms    66 runs

Benchmark #4: node build/separatedData.js
  Time (mean ± σ):      42.6 ms ±   2.2 ms    [User: 36.0 ms, System: 8.0 ms]
  Range (min … max):    36.5 ms …  50.2 ms    64 runs

Summary
  'node build/object.js' ran
    1.01 ± 0.08 times faster than 'node build/constructor.js'
    1.02 ± 0.07 times faster than 'node build/manySetCall.js'
    1.02 ± 0.08 times faster than 'node build/separatedData.js'

```

### 2

```txt

Benchmark #1: node build/constructor.js
  Time (mean ± σ):      41.9 ms ±   1.9 ms    [User: 35.6 ms, System: 7.7 ms]
  Range (min … max):    37.1 ms …  47.0 ms    57 runs

Benchmark #2: node build/manySetCall.js
  Time (mean ± σ):      43.2 ms ±   2.6 ms    [User: 36.9 ms, System: 7.6 ms]
  Range (min … max):    38.7 ms …  53.1 ms    62 runs

Benchmark #3: node build/object.js
  Time (mean ± σ):      43.1 ms ±   3.0 ms    [User: 36.8 ms, System: 7.7 ms]
  Range (min … max):    37.2 ms …  52.8 ms    52 runs

Benchmark #4: node build/separatedData.js
  Time (mean ± σ):      42.0 ms ±   2.2 ms    [User: 36.7 ms, System: 6.8 ms]
  Range (min … max):    36.5 ms …  50.5 ms    65 runs

Summary
  'node build/constructor.js' ran
    1.00 ± 0.07 times faster than 'node build/separatedData.js'
    1.03 ± 0.09 times faster than 'node build/object.js'
    1.03 ± 0.08 times faster than 'node build/manySetCall.js'

```

### 3

```txt

Benchmark #1: node build/constructor.js
  Time (mean ± σ):      46.2 ms ±   6.4 ms    [User: 38.4 ms, System: 8.9 ms]
  Range (min … max):    38.7 ms …  78.2 ms    60 runs

Benchmark #2: node build/manySetCall.js
  Time (mean ± σ):      44.9 ms ±   3.4 ms    [User: 38.4 ms, System: 7.9 ms]
  Range (min … max):    38.5 ms …  56.7 ms    63 runs

Benchmark #3: node build/object.js
  Time (mean ± σ):      49.6 ms ±  11.1 ms    [User: 41.1 ms, System: 9.8 ms]
  Range (min … max):    37.8 ms …  80.2 ms    63 runs

Benchmark #4: node build/separatedData.js
  Time (mean ± σ):      46.8 ms ±   4.3 ms    [User: 39.7 ms, System: 8.3 ms]
  Range (min … max):    40.3 ms …  60.0 ms    56 runs

Summary
  'node build/manySetCall.js' ran
    1.03 ± 0.16 times faster than 'node build/constructor.js'
    1.04 ± 0.12 times faster than 'node build/separatedData.js'
    1.10 ± 0.26 times faster than 'node build/object.js'

```

## 環境

2019-12-30

```bash
$ node -v
v13.5.0

$ hyperfine --version
hyperfine 1.9.0

$ go version
go version go1.13.5 linux/amd64
```
