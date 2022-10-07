# GeoCMD

位置情報を扱うのに使えそうなシェルスクリプト群 / Shell scripts for location information processing.

# コマンド / Commands

## calcdist

入力された緯度・経度の点間の距離を計算する。複数点与えた場合は、入力順に距離を計算し、その累計値も表示する。

This command calculates distance between points represented by latitude and longitude. When you provide more than
two points, this calculates distance between points in order of input and display total distance.

### 使い方 / Usage

```bash
cat example.txt | calcdist
```
```bash
Input File: example.txt
    33.65007 130.21171
    33.64949 130.21234
    33.64918 130.21232
    33.64785 130.21346
    33.64682 130.21521
    33.64560 130.21679
```
```bash
Output
    # latitude longitude distance_from_previous_point total_distance
    33.65007 130.21171 0 0
    33.64949 130.21234 86.91245 86.91245
    33.64918 130.21232 34.43400 121.34645
    33.64785 130.21346 181.50708 302.85353
    33.64682 130.21521 198.50780 501.36133
    33.64560 130.21679 199.48357 700.84490
```

### オプション / Options

```
    -t input_separator    入力値の区切りを input_separator にする。デフォルト値は半角スペース。
                          Set separator of input stream to 'input_separator'.
                          Default separator is ' ' (Space 0x20)
    -o output_separator   出力値の区切りを output_separator にする。デフォルト値は半角スペース。
                          Set separator of output stream to 'output_separator'.
                          Default separator is ' ' (Space 0x20)
```

## nnsearch

マニュアル作成中 / In progress...

