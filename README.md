# GeoCMD

位置情報を扱うのに使えそうなシェルスクリプト群 / Shell scripts for geolocation information processing.

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

入力された緯度・経度の点をもとに、緯度・経度探索候補ファイル（距離を求めたいポイントのリスト）に
定義した各点との距離を求め、距離が短い順に上限値の範囲内でk個の点を出力する。

This command calculates distance between input points and points that defined in point list file
and output top k points in order of shortest distance within the upper distance limit.

### 使い方 / Usage

```bash
cat points.txt | nnsearch -f landmark_point_list.txt -d 50 -k 3
```

上記のコマンドを実行すると、points.txtに記された各点について、landmark_point_list.txt
に定義された点との距離を計算し、最大50mの範囲内で距離が短い順に3点を出力する。

When you run the command line above, the program calculates the distance between each point in
points.txt and points in landmark_point_list.txt. Next, the program output the information of
points the three nearest points within 50 meters.

```bash
Input File: points.txt
    33.65007 130.21171
    33.64949 130.21234
    33.64918 130.21232
    33.64785 130.21346
    33.64682 130.21521
    33.64560 130.21679
```
```bash
landmark_point_list.txt
    33.59381 130.22923 Landmark_A
    33.57450 130.24907 Landmark_B
    33.57897 130.25909 Landmark_C
```

### オプション / Options

```
    -f point_list_file    緯度・経度探索候補ファイル。（必須）
                          point_list_file に書かれた点の中から近い点をk個探す
                          The point list file that you want to calculate the distance to there.
    -k top_k_points       入力された緯度・経度から、point_list_file 中に定義された点のうち近い物 top_k_points 点を返す
                          デフォルト値は1
                          The program find the k nearest points in point_list_file from input point.
                          Default k is 1.
    -d distance           結果出力範囲を入力された緯度・経度を中心とした distance[m] に限る
                          デフォルト値は100
                          The program find the points within "distance" meters from input point.
                          Default distance is 100 meters.
    -t input_separator    入力値の区切りを input_separator にする。デフォルト値は半角スペース。
                          Set separator of input stream to 'input_separator'.
                          Default separator is ' ' (Space 0x20)
    -o output_separator   出力値の区切りを output_separator にする。デフォルト値は半角スペース。
                          Set separator of output stream to 'output_separator'.
                          Default separator is ' ' (Space 0x20)
```

