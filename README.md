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
  Time (mean ± σ):      44.3 ms ±  12.0 ms    [User: 36.6 ms, System: 8.0 ms]
  Range (min … max):    26.1 ms …  57.9 ms    47 runs

Benchmark #2: node build/manySetCall.js
  Time (mean ± σ):      42.3 ms ±  12.5 ms    [User: 35.3 ms, System: 7.3 ms]
  Range (min … max):    25.5 ms …  60.7 ms    90 runs

Benchmark #3: node build/object.js
  Time (mean ± σ):      46.3 ms ±  12.7 ms    [User: 38.0 ms, System: 8.7 ms]
  Range (min … max):    24.1 ms …  62.2 ms    80 runs

Benchmark #4: node build/separatedData.js
  Time (mean ± σ):      43.5 ms ±  14.9 ms    [User: 35.0 ms, System: 8.6 ms]
  Range (min … max):    25.3 ms …  80.8 ms    97 runs

Benchmark #5: build/map
  Time (mean ± σ):       3.5 ms ±   1.5 ms    [User: 2.1 ms, System: 2.4 ms]
  Range (min … max):     0.0 ms …   5.7 ms    354 runs

  Warning: Command took less than 5 ms to complete. Results might be inaccurate.

Summary
  'build/map' ran
   11.94 ± 6.24 times faster than 'node build/manySetCall.js'
   12.28 ± 6.77 times faster than 'node build/separatedData.js'
   12.50 ± 6.37 times faster than 'node build/constructor.js'
   13.07 ± 6.69 times faster than 'node build/object.js'

```

### 2

```txt

Benchmark #1: node build/constructor.js
  Time (mean ± σ):      42.4 ms ±  12.4 ms    [User: 34.7 ms, System: 8.1 ms]
  Range (min … max):    24.7 ms …  70.8 ms    97 runs

Benchmark #2: node build/manySetCall.js
  Time (mean ± σ):      41.6 ms ±  11.9 ms    [User: 33.6 ms, System: 8.4 ms]
  Range (min … max):    24.3 ms …  62.1 ms    65 runs

Benchmark #3: node build/object.js
  Time (mean ± σ):      38.5 ms ±   9.4 ms    [User: 31.2 ms, System: 7.5 ms]
  Range (min … max):    25.3 ms …  58.1 ms    66 runs

Benchmark #4: node build/separatedData.js
  Time (mean ± σ):      42.4 ms ±  11.5 ms    [User: 35.6 ms, System: 7.1 ms]
  Range (min … max):    25.0 ms …  59.6 ms    70 runs

Benchmark #5: build/map
  Time (mean ± σ):       2.6 ms ±   1.5 ms    [User: 1.9 ms, System: 1.9 ms]
  Range (min … max):     0.0 ms …   6.2 ms    333 runs

  Warning: Command took less than 5 ms to complete. Results might be inaccurate.

Summary
  'build/map' ran
   14.58 ± 8.81 times faster than 'node build/object.js'
   15.73 ± 9.79 times faster than 'node build/manySetCall.js'
   16.04 ± 10.04 times faster than 'node build/constructor.js'
   16.06 ± 9.88 times faster than 'node build/separatedData.js'

```

### 3

```txt

Benchmark #1: node build/constructor.js
  Time (mean ± σ):      48.7 ms ±  11.9 ms    [User: 39.8 ms, System: 9.2 ms]
  Range (min … max):    25.7 ms …  66.3 ms    42 runs

Benchmark #2: node build/manySetCall.js
  Time (mean ± σ):      50.4 ms ±  11.9 ms    [User: 41.4 ms, System: 9.3 ms]
  Range (min … max):    26.6 ms …  69.3 ms    40 runs

Benchmark #3: node build/object.js
  Time (mean ± σ):      42.7 ms ±  11.3 ms    [User: 34.7 ms, System: 8.2 ms]
  Range (min … max):    26.3 ms …  60.7 ms    48 runs

Benchmark #4: node build/separatedData.js
  Time (mean ± σ):      44.8 ms ±  12.9 ms    [User: 37.5 ms, System: 7.6 ms]
  Range (min … max):    26.6 ms …  62.1 ms    64 runs

Benchmark #5: build/map
  Time (mean ± σ):       4.0 ms ±   1.9 ms    [User: 2.4 ms, System: 2.5 ms]
  Range (min … max):     0.0 ms …   6.6 ms    316 runs

  Warning: Command took less than 5 ms to complete. Results might be inaccurate.

Summary
  'build/map' ran
   10.75 ± 5.87 times faster than 'node build/object.js'
   11.27 ± 6.29 times faster than 'node build/separatedData.js'
   12.26 ± 6.57 times faster than 'node build/constructor.js'
   12.68 ± 6.75 times faster than 'node build/manySetCall.js'

```

## 環境

2021-10-04

```bash
$ node -v
v16.10.0

$ hyperfine --version
hyperfine 1.11.0

$ go version
go version go1.17.1 linux/amd64
```
