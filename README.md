[![](https://github.com/jindaxiang/aktools/workflows/build/badge.svg)](https://github.com/jindaxiang/aktools/actions)

# AKTools

AKTools is a package for local HTTP server for AKShare!

It depends on AKShare and FastAPI.

```shell
pip install aktools
```

## AKShare

[Please visit AKShare's Documentation](https://akshare.xyz/)

## FastAPI

[Please visit FastAPI's Documentation](https://fastapi.tiangolo.com/)

# Demo

## Installation[windows]

```shell
pip install akshare, fastapi, uvicorn
```

## Run CMD command[windows]

1. cd into the path of aktools: `cd aktools/core/`,
2. then type the cmd command: `uvicorn api:app --port 8080 --reload`, 
3. type `http://127.0.0.1:8080/stock_zh_a_hist` in your Chrome for test

# Test-Postman

![](https://dss-1252952517.cos.ap-chengdu.myqcloud.com/image-20211209235248006.png)

# Test-R

R-Program

```shell
library(RCurl)  # 需要先安装该包
library(jsonlite)  # 需要先安装该包
options (warn = -1)  # 该行有助于在无参数请求时去掉 warning 信息

temp_df <-
  getForm(
    uri = 'http://127.0.0.1:8080/api/stock_zh_a_hist',
    symbol = '000001',
    period = 'daily',
    start_date = '20211109',
    end_date = '20211209',
    adjust = 'hfq',
    .encoding = "utf-8"
  )
inner_df <- fromJSON(temp_df)
inner_df
```

Result

```
         日期    开盘    收盘    最高    最低      成交量     成交额    振幅  涨跌幅  涨跌额 换手率
1  2021-11-09 3009.83 3017.96 3037.46 2974.07 1240573 2163193120 2.11   0.60  17.88   0.64
2  2021-11-10 3006.58 2996.83 3008.20 2957.82 1220851 2109735152 1.67  -0.70 -21.13   0.63
3  2021-11-11 2988.70 3151.23 3164.23 2983.82 2084729 3752413856 6.02   5.15 154.40   1.07
4  2021-11-12 3144.73 3138.23 3196.74 3112.22  957546 1753072720 2.68  -0.41 -13.00   0.49
5  2021-11-15 3151.23 3164.23 3196.74 3126.85  655090 1203764096 2.23   0.83  26.00   0.34
6  2021-11-16 3152.85 3130.10 3182.11 3121.97  601110 1099113408 1.90  -1.08 -34.13   0.31
7  2021-11-17 3118.72 3112.22 3143.10 3091.09  664640 1203859184 1.66  -0.57 -17.88   0.34
8  2021-11-18 3108.97 3061.84 3113.85 3050.46  799844 1430058304 2.04  -1.62 -50.38   0.41
9  2021-11-19 3061.84 3118.72 3133.35 3045.58  786372 1414506384 2.87   1.86  56.88   0.41
10 2021-11-22 3099.22 3113.85 3134.97 3078.09  738618 1337768176 1.82  -0.16  -4.87   0.38
11 2021-11-23 3112.22 3074.84 3151.23 3042.33 1235978 2213817584 3.50  -1.25 -39.01   0.64
12 2021-11-24 3056.96 3073.21 3086.22 3039.08  741311 1316774400 1.53  -0.05  -1.63   0.38
13 2021-11-25 3052.09 3042.33 3060.21 3034.21  603533 1068221312 0.85  -1.00 -30.88   0.31
14 2021-11-26 3032.58 3026.08 3040.71 3016.33  694500 1219937312 0.80  -0.53 -16.25   0.36
15 2021-11-29 2998.45 3014.70 3024.46 2990.33  512595  895105984 1.13  -0.38 -11.38   0.26
16 2021-11-30 3019.58 3003.33 3042.33 2988.70  733616 1280384560 1.78  -0.38 -11.37   0.38
17 2021-12-01 3001.70 3035.83 3056.96 2991.95  706925 1243666848 2.16   1.08  32.50   0.36
18 2021-12-02 3032.58 3027.71 3063.46 2991.95  994798 1749164560 2.36  -0.27  -8.12   0.51
19 2021-12-03 3035.83 3037.46 3045.58 2998.45  707600 1242375056 1.56   0.32   9.75   0.36
20 2021-12-06 3069.96 3110.60 3185.36 3061.84 2145625 3896385168 4.07   2.41  73.14   1.11
21 2021-12-07 3143.10 3169.11 3203.24 3118.72 1616444 2979968976 2.72   1.88  58.51   0.83
22 2021-12-08 3167.48 3170.73 3183.73 3120.35  980281 1798691056 2.00   0.05   1.62   0.51
23 2021-12-09 3173.98 3208.11 3266.62 3154.48 1455887 2726663440 3.54   1.18  37.38   0.75
```

# Test-MATLAB

MATLAB-Program

```
api = 'http://127.0.0.1:8080/api/';
url = [api 'stock_zh_a_hist'];
options = weboptions('ContentType','json', 'CharacterEncoding', 'utf-8');
data = webread(url, options, symbol = '000001', period = 'daily', start_date = '20211109', end_date = '20211209', adjust = 'hfq');
data % 由于 MATLAB 无法显示中文字段名，请自行修改为英文字段，参考链接：http://iso2mesh.sourceforge.net/cgi-bin/index.cgi?jsonlab/Doc/Examples
```

Result

```
'2021-11-09'	3009.83000000000	3017.96000000000	3037.46000000000	2974.07000000000	1240573	2163193120.00000	2.11000000000000	0.600000000000000	17.8800000000000	0.640000000000000
'2021-11-10'	3006.58000000000	2996.83000000000	3008.20000000000	2957.82000000000	1220851	2109735152.00000	1.67000000000000	-0.700000000000000	-21.1300000000000	0.630000000000000
'2021-11-11'	2988.70000000000	3151.23000000000	3164.23000000000	2983.82000000000	2084729	3752413856.00000	6.02000000000000	5.15000000000000	154.400000000000	1.07000000000000
'2021-11-12'	3144.73000000000	3138.23000000000	3196.74000000000	3112.22000000000	957546	1753072720.00000	2.68000000000000	-0.410000000000000	-13	0.490000000000000
'2021-11-15'	3151.23000000000	3164.23000000000	3196.74000000000	3126.85000000000	655090	1203764096.00000	2.23000000000000	0.830000000000000	26	0.340000000000000
'2021-11-16'	3152.85000000000	3130.10000000000	3182.11000000000	3121.97000000000	601110	1099113408.00000	1.90000000000000	-1.08000000000000	-34.1300000000000	0.310000000000000
'2021-11-17'	3118.72000000000	3112.22000000000	3143.10000000000	3091.09000000000	664640	1203859184.00000	1.66000000000000	-0.570000000000000	-17.8800000000000	0.340000000000000
'2021-11-18'	3108.97000000000	3061.84000000000	3113.85000000000	3050.46000000000	799844	1430058304.00000	2.04000000000000	-1.62000000000000	-50.3800000000000	0.410000000000000
'2021-11-19'	3061.84000000000	3118.72000000000	3133.35000000000	3045.58000000000	786372	1414506384.00000	2.87000000000000	1.86000000000000	56.8800000000000	0.410000000000000
'2021-11-22'	3099.22000000000	3113.85000000000	3134.97000000000	3078.09000000000	738618	1337768176.00000	1.82000000000000	-0.160000000000000	-4.87000000000000	0.380000000000000
'2021-11-23'	3112.22000000000	3074.84000000000	3151.23000000000	3042.33000000000	1235978	2213817584.00000	3.50000000000000	-1.25000000000000	-39.0100000000000	0.640000000000000
'2021-11-24'	3056.96000000000	3073.21000000000	3086.22000000000	3039.08000000000	741311	1316774400.00000	1.53000000000000	-0.0500000000000000	-1.63000000000000	0.380000000000000
'2021-11-25'	3052.09000000000	3042.33000000000	3060.21000000000	3034.21000000000	603533	1068221312.00000	0.850000000000000	-1	-30.8800000000000	0.310000000000000
'2021-11-26'	3032.58000000000	3026.08000000000	3040.71000000000	3016.33000000000	694500	1219937312.00000	0.800000000000000	-0.530000000000000	-16.2500000000000	0.360000000000000
'2021-11-29'	2998.45000000000	3014.70000000000	3024.46000000000	2990.33000000000	512595	895105984	1.13000000000000	-0.380000000000000	-11.3800000000000	0.260000000000000
'2021-11-30'	3019.58000000000	3003.33000000000	3042.33000000000	2988.70000000000	733616	1280384560.00000	1.78000000000000	-0.380000000000000	-11.3700000000000	0.380000000000000
'2021-12-01'	3001.70000000000	3035.83000000000	3056.96000000000	2991.95000000000	706925	1243666848.00000	2.16000000000000	1.08000000000000	32.5000000000000	0.360000000000000
'2021-12-02'	3032.58000000000	3027.71000000000	3063.46000000000	2991.95000000000	994798	1749164560.00000	2.36000000000000	-0.270000000000000	-8.12000000000000	0.510000000000000
'2021-12-03'	3035.83000000000	3037.46000000000	3045.58000000000	2998.45000000000	707600	1242375056.00000	1.56000000000000	0.320000000000000	9.75000000000000	0.360000000000000
'2021-12-06'	3069.96000000000	3110.60000000000	3185.36000000000	3061.84000000000	2145625	3896385168.00000	4.07000000000000	2.41000000000000	73.1400000000000	1.11000000000000
'2021-12-07'	3143.10000000000	3169.11000000000	3203.24000000000	3118.72000000000	1616444	2979968976.00000	2.72000000000000	1.88000000000000	58.5100000000000	0.830000000000000
'2021-12-08'	3167.48000000000	3170.73000000000	3183.73000000000	3120.35000000000	980281	1798691056.00000	2	0.0500000000000000	1.62000000000000	0.510000000000000
'2021-12-09'	3173.98000000000	3208.11000000000	3266.62000000000	3154.48000000000	1455887	2726663440.00000	3.54000000000000	1.18000000000000	37.3800000000000	0.750000000000000

```