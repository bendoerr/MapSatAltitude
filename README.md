MapSatAltitude
==============

This is a command-line tool, written in Octave/Matlab, to answer the question:
	"What orbit should I use to most efficiently scan `some planetary body`
	with `some supported scanner` given that only want to use one vessel?"


Supported Scanners
==================

Scanners are defined in scanners.txt. This is a simple, tab-delimited table containing
information needed to make the calculation and some information to make the output prettier.

When running `MapSatAltitude.m`, the response to `Scanner name?` should be the first column of one
of these rows:

```
Name	FOV	HalfFOV	AltitudeMin	AltitudeIdeal	AltitudeMax	LongName
RADAR	5.00	2.50	5000.00		5000.00		500000.00	SCAN RADAR Altimetry Sensor
Multi	4.00	2.00	5000.00		250000.00	500000.00	SCAN Multispectral Sensor
SAR	2.00	1.00	5000.00		750000.00	800000.00	SCAN SAR Altimetry Sensor
KSmall	2.20	1.10	250000.00	250000.00	250000.00	KE-S210 Compact Survey Unit
KMedium	2.20	1.10	1200000.00	1200000.00	1200000.00	KE-S110 Medium Survey Unit
```

Supported Planets
==================

Planets are defined in `PlanetInfos.txt`. This has the same format as the scanners file, with different fields.

```
Name	Radius		Day		GM			SOI		Atmo
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Earth	6371000.00	86400.002	398600441800000.000	923795000.000	180000.000
Moon	1737100.00	2360584.685	4902800000000.000	66009800.000	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% Original Planets from here down ...
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kerbol	26160000.00	432000.000	1172332800000000000.000	999999999999.00	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Moho	250000.00	1210000.000	168609378654.509	9646663.000	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Eve	700000.00	80500.000	8171730229210.87	85109365.000	96000.000
Gilly	13000.00	28255.000	8289449.81471		126123.270	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kerbin	600000.00	21600.000	3531600000000.000	84159286.000	69078.000
Mun	200000.00	138984.380	65138397520.7807	2429559.100	0.000
Minmus	60000.00	40400.000	1765800026.31247	2247428.400	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Duna	320000.00	65517.859	301363211975.098	47921949.000	41446.000
Ike	130000.00	65517.862	18568368573.144		1049598.900	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Dres	138000.00	34800.000	21484488600.000		32832840.000	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Jool	6000000.00	36000.00	282528004209995.000	2455985185.000	200000.00
Laythe	500000.00	52980.879	1962000029236.08	3723645.800	50000.000
Vall	300000.00	105962.090	207481499473.751	2406401.400	0.000
Tylo	600000.00	211926.360	2825280042099.95	10856518.000	0.000
Bop	65000.00	544507.400	2486834944.41491	1221061.000	0.000
Pol	44000.00	901902.620	721702080.000		1042138.900	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Eeloo	210000.00	19460.000	74410814527.0496	119082942.000	0.000
```

Example Session
==============

```
> octave MapSatAltitude.m

GNU Octave, version 3.6.1
Copyright (C) 2012 John W. Eaton and others.
This is free software; see the source code for copying conditions.
There is ABSOLUTELY NO WARRANTY; not even for MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.  For details, type `warranty'.

Octave was configured for "x86_64-pc-linux-gnu".

Additional information about Octave is available at http://www.octave.org.

Please contribute if you find this software useful.
For more information, visit http://www.octave.org/help-wanted.html

Read http://www.octave.org/bugs.html to learn how to submit bug reports.

For information about changes from previous versions, type `news'.

Scanner name? RADAR
[SCAN RADAR Altimetry Sensor] Ideal Altitude Calculator.
Planet name? Kerbin
Minimum Sidelap? (Default is 1.00. Press Enter to skip) : 
Maximum Sidelap? (Default is 1.25. Press Enter to skip) : 
Numerical Resolution? ("Uber","Very",["Hi"], or "Low".) : 
Rational Number Numerical Resolution: High (1.00e-04)




Planet:     Kerbin
Radius:     600 km
Sync.Orbit: 2868.75 km
SOI:        84159.29 km
Day Length: 6h  0m 0s

Scan line resolution: 200
Field of view: 5.000000 deg
Sidelap range: 1.000000 - 1.250000
Altitude Range: 69.1 km - 500.0 km in 8.6 m steps (50001 possible zones)
Minimum altitude chosen because:
	[Kerbin] has an atmosphere until 69.1 km

Maximum Altitude chosen because:
	[SCAN RADAR Altimetry Sensor] has a maximum range of 500.00 km


 Number of Zones: 121

---------------------------
Kerbin, Sidelap 1 - 1.25:
                      SMA         Altitude         Inclination Orbital   Time to Scan       Swath    Resolution
Zone  Res  Sidelap             Ideal      +/- Range    (deg)   Period   Ideal       diff     Width   (deg)   (km) 
========================================================================================================

  1  241/442  (1.02)  699.199 km   99.199  +/-  0.04 km  84.81   0h 32.6m   119h 59.7m +00.7m    0.8  0.0041  43.32 m
  2  247/453  (1.04)  699.251 km   99.251  +/-  0.04 km  84.81   0h 32.6m   122h 59.7m +00.7m    0.8  0.0041  43.34 m
  3  253/464  (1.07)  699.294 km   99.294  +/-  0.03 km  84.81   0h 32.6m   125h 59.7m +00.6m    0.8  0.0041  43.36 m
  4  259/475  (1.09)  699.346 km   99.346  +/-  0.04 km  84.81   0h 32.6m   128h 59.6m +00.7m    0.8  0.0041  43.38 m
  5  265/486  (1.12)  699.389 km   99.389  +/-  0.03 km  84.81   0h 32.6m   131h 59.7m +00.6m    0.8  0.0041  43.40 m
  6  271/497  (1.14)  699.432 km   99.432  +/-  0.03 km  84.81   0h 32.6m   134h 59.7m +00.6m    0.8  0.0041  43.42 m
  7  277/508  (1.17)  699.475 km   99.475  +/-  0.03 km  84.80   0h 32.6m   137h 59.8m +00.5m    0.8  0.0041  43.44 m
  8  283/519  (1.20)  699.510 km   99.510  +/-  0.03 km  84.80   0h 32.6m   140h 59.7m +00.6m    0.8  0.0041  43.45 m
  9  289/530  (1.22)  699.553 km   99.553  +/-  0.03 km  84.80   0h 32.6m   143h 59.8m +00.5m    0.8  0.0042  43.47 m
 10  295/541  (1.25)  699.587 km   99.587  +/-  0.03 km  84.80   0h 32.6m   146h 59.8m +00.5m    0.8  0.0042  43.49 m
 11  281/515  (1.23)  703.129 km  103.129  +/-  0.03 km  84.76   0h 32.9m   140h 59.7m +00.5m    0.9  0.0043  45.04 m
 12  275/504  (1.20)  703.164 km  103.164  +/-  0.03 km  84.76   0h 32.9m   137h 59.7m +00.6m    0.9  0.0043  45.05 m
 13  269/493  (1.18)  703.207 km  103.207  +/-  0.03 km  84.76   0h 32.9m   134h 59.7m +00.6m    0.9  0.0043  45.07 m
 14  263/482  (1.15)  703.250 km  103.250  +/-  0.03 km  84.76   0h 32.9m   131h 59.7m +00.6m    0.9  0.0043  45.09 m
 15  257/471  (1.13)  703.302 km  103.302  +/-  0.04 km  84.76   0h 32.9m   128h 59.7m +00.7m    0.9  0.0043  45.11 m
 16  251/460  (1.10)  703.345 km  103.345  +/-  0.03 km  84.76   0h 32.9m   125h 59.7m +00.6m    0.9  0.0043  45.13 m
 17  245/449  (1.08)  703.397 km  103.397  +/-  0.04 km  84.76   0h 32.9m   122h 59.6m +00.7m    0.9  0.0043  45.15 m
 18  239/438  (1.05)  703.448 km  103.448  +/-  0.04 km  84.76   0h 32.9m   119h 59.6m +00.7m    0.9  0.0043  45.17 m
 19  233/427  (1.02)  703.500 km  103.500  +/-  0.05 km  84.76   0h 32.9m   116h 59.6m +00.8m    0.9  0.0043  45.20 m
 20  181/330  (1.01)  732.182 km  132.182  +/-  0.02 km  84.43   0h 34.9m    96h 00.3m +00.2m    1.1  0.0055  57.73 m
 21  171/311  (1.05)  745.722 km  145.722  +/-  0.09 km  84.28   0h 35.9m    92h 59.5m +01.1m    1.2  0.0061  63.64 m
 22  182/331  (1.12)  745.817 km  145.817  +/-  0.08 km  84.28   0h 35.9m    98h 59.5m +00.9m    1.2  0.0061  63.68 m
 23  193/351  (1.19)  745.903 km  145.903  +/-  0.08 km  84.28   0h 35.9m   104h 59.5m +01.0m    1.2  0.0061  63.72 m
 24  192/349  (1.20)  748.747 km  148.747  +/-  0.07 km  84.24   0h 36.1m   104h 59.6m +00.9m    1.2  0.0062  64.96 m
 25  181/329  (1.13)  748.833 km  148.833  +/-  0.09 km  84.24   0h 36.1m    98h 59.5m +01.0m    1.2  0.0062  65.00 m
 26  170/309  (1.07)  748.936 km  148.936  +/-  0.09 km  84.24   0h 36.1m    92h 59.5m +01.1m    1.2  0.0062  65.04 m
 27  155/281  (1.06)  763.191 km  163.191  +/-  0.12 km  84.08   0h 37.1m    86h 59.4m +01.2m    1.4  0.0068  71.27 m
 28  171/310  (1.17)  763.303 km  163.303  +/-  0.09 km  84.08   0h 37.2m    95h 59.5m +01.0m    1.4  0.0068  71.32 m
 29  165/299  (1.15)  765.544 km  165.544  +/-  0.09 km  84.05   0h 37.3m    92h 59.5m +01.0m    1.4  0.0069  72.30 m
 30  149/270  (1.04)  765.665 km  165.665  +/-  0.13 km  84.05   0h 37.3m    83h 59.4m +01.3m    1.4  0.0069  72.35 m
 31  142/257  (1.03)  772.292 km  172.292  +/-  0.09 km  83.97   0h 37.8m    80h 59.3m +00.9m    1.4  0.0072  75.25 m
 32  152/275  (1.11)  774.309 km  174.309  +/-  0.02 km  83.95   0h 38.0m    87h 00.5m +00.2m    1.5  0.0073  76.13 m
 33  126/227  (1.04)  796.984 km  196.984  +/-  0.18 km  83.68   0h 39.6m    74h 59.2m +01.5m    1.6  0.0082  86.04 m
 34  131/236  (1.08)  797.165 km  197.165  +/-  0.16 km  83.67   0h 39.7m    77h 59.3m +01.4m    1.6  0.0082  86.11 m
 35  136/245  (1.12)  797.329 km  197.329  +/-  0.16 km  83.67   0h 39.7m    80h 59.3m +01.4m    1.6  0.0082  86.19 m
 36  141/254  (1.16)  797.484 km  197.484  +/-  0.14 km  83.67   0h 39.7m    83h 59.3m +01.3m    1.6  0.0082  86.25 m
 37  146/263  (1.20)  797.631 km  197.631  +/-  0.13 km  83.67   0h 39.7m    86h 59.3m +01.3m    1.6  0.0082  86.32 m
 38  151/272  (1.25)  797.760 km  197.760  +/-  0.12 km  83.67   0h 39.7m    89h 59.3m +01.2m    1.6  0.0082  86.37 m
 39  144/259  (1.23)  805.827 km  205.827  +/-  0.13 km  83.57   0h 40.3m    86h 59.4m +01.3m    1.7  0.0086  89.90 m
 40  139/250  (1.19)  805.973 km  205.973  +/-  0.15 km  83.57   0h 40.3m    83h 59.3m +01.4m    1.7  0.0086  89.96 m
 41  134/241  (1.15)  806.128 km  206.128  +/-  0.16 km  83.57   0h 40.3m    80h 59.3m +01.4m    1.7  0.0086  90.03 m
 42  129/232  (1.11)  806.301 km  206.301  +/-  0.17 km  83.57   0h 40.3m    77h 59.3m +01.5m    1.7  0.0086  90.11 m
 43  124/223  (1.07)  806.490 km  206.490  +/-  0.18 km  83.56   0h 40.4m    74h 59.2m +01.5m    1.7  0.0086  90.19 m
 44  119/214  (1.02)  806.689 km  206.689  +/-  0.21 km  83.56   0h 40.4m    71h 59.2m +01.7m    1.7  0.0086  90.28 m
 45  111/199  (1.03)  823.133 km  223.133  +/-  0.09 km  83.36   0h 41.6m    69h 00.3m +00.7m    1.9  0.0093  97.46 m
 46  125/224  (1.17)  825.356 km  225.356  +/-  0.13 km  83.33   0h 41.8m    77h 59.2m +01.1m    1.9  0.0094  98.43 m
 47  115/206  (1.09)  827.450 km  227.450  +/-  0.22 km  83.31   0h 41.9m    71h 59.2m +01.8m    1.9  0.0095  99.35 m
 48  119/213  (1.14)  831.527 km  231.527  +/-  0.21 km  83.26   0h 42.2m    74h 59.1m +01.7m    1.9  0.0097  0.101 km
 49  128/229  (1.24)  834.061 km  234.061  +/-  0.16 km  83.23   0h 42.4m    80h 59.3m +01.4m    2.0  0.0098  0.102 km
 50  109/195  (1.06)  834.268 km  234.268  +/-  0.24 km  83.23   0h 42.5m    68h 59.2m +01.8m    2.0  0.0098  0.102 km
 51  103/184  (1.03)  841.860 km  241.860  +/-  0.27 km  83.13   0h 43.0m    65h 59.0m +01.9m    2.0  0.0101  0.106 km
 52  117/209  (1.17)  842.102 km  242.102  +/-  0.21 km  83.13   0h 43.1m    74h 59.1m +01.7m    2.0  0.0101  0.106 km
 53  121/216  (1.23)  845.653 km  245.653  +/-  0.20 km  83.09   0h 43.3m    77h 59.2m +01.6m    2.0  0.0102  0.107 km
 54  107/191  (1.09)  845.877 km  245.877  +/-  0.24 km  83.08   0h 43.3m    68h 59.2m +01.8m    2.1  0.0103  0.107 km
 55   97/173  (1.00)  850.548 km  250.548  +/-  0.07 km  83.03   0h 43.7m    63h 00.8m +00.5m    2.1  0.0105  0.109 km
 56  106/189  (1.10)  851.815 km  251.815  +/-  0.25 km  83.01   0h 43.8m    68h 59.0m +01.8m    2.1  0.0105  0.110 km
 57  101/180  (1.06)  854.314 km  254.314  +/-  0.28 km  82.98   0h 44.0m    65h 59.1m +02.0m    2.1  0.0106  0.111 km
 58  105/187  (1.12)  857.994 km  257.994  +/-  0.09 km  82.93   0h 44.3m    69h 00.5m +00.6m    2.2  0.0108  0.113 km
 59   95/169  (1.03)  863.760 km  263.760  +/-  0.32 km  82.86   0h 44.7m    62h 58.9m +02.1m    2.2  0.0110  0.115 km
 60  104/185  (1.13)  864.053 km  264.053  +/-  0.26 km  82.86   0h 44.7m    68h 59.0m +01.9m    2.2  0.0110  0.115 km
 61  113/201  (1.23)  864.303 km  264.303  +/-  0.22 km  82.86   0h 44.8m    74h 59.1m +01.7m    2.2  0.0110  0.115 km
 62  112/199  (1.25)  870.094 km  270.094  +/-  0.22 km  82.78   0h 45.2m    74h 59.2m +01.7m    2.3  0.0113  0.118 km
 63  103/183  (1.15)  870.353 km  270.353  +/-  0.27 km  82.78   0h 45.2m    68h 59.1m +01.9m    2.3  0.0113  0.118 km
 64   94/167  (1.05)  870.655 km  270.655  +/-  0.33 km  82.78   0h 45.3m    62h 59.0m +02.1m    2.3  0.0113  0.118 km
 65  102/181  (1.16)  876.662 km  276.662  +/-  0.16 km  82.70   0h 45.7m    68h 58.9m +01.1m    2.3  0.0115  0.121 km
 66   97/172  (1.12)  880.566 km  280.566  +/-  0.30 km  82.65   0h 46.0m    65h 58.9m +02.0m    2.3  0.0117  0.123 km
 67  101/179  (1.17)  883.281 km  283.281  +/-  0.28 km  82.62   0h 46.2m    68h 59.1m +02.0m    2.4  0.0118  0.124 km
 68   92/163  (1.08)  884.720 km  284.720  +/-  0.19 km  82.60   0h 46.4m    62h 58.7m +01.2m    2.4  0.0119  0.124 km
 69   87/154  (1.03)  889.555 km  289.555  +/-  0.38 km  82.54   0h 46.7m    59h 58.8m +02.3m    2.4  0.0121  0.126 km
 70  100/177  (1.19)  889.900 km  289.900  +/-  0.28 km  82.53   0h 46.8m    68h 59.0m +02.0m    2.4  0.0121  0.127 km
 71   95/168  (1.15)  894.519 km  294.519  +/-  0.32 km  82.48   0h 47.1m    65h 59.0m +02.1m    2.5  0.0123  0.129 km
 72   81/143  (1.00)  903.181 km  303.181  +/-  0.44 km  82.36   0h 47.8m    56h 58.6m +02.5m    2.5  0.0126  0.132 km
 73   98/173  (1.22)  903.560 km  303.560  +/-  0.30 km  82.36   0h 47.8m    68h 58.9m +02.1m    2.5  0.0127  0.133 km
 74   89/157  (1.12)  907.249 km  307.249  +/-  0.36 km  82.31   0h 48.1m    62h 59.0m +02.3m    2.6  0.0128  0.134 km
 75   80/141  (1.02)  911.696 km  311.696  +/-  0.46 km  82.26   0h 48.5m    56h 58.5m +02.6m    2.6  0.0130  0.136 km
 76   88/155  (1.13)  915.048 km  315.048  +/-  0.37 km  82.21   0h 48.8m    62h 59.0m +02.3m    2.6  0.0131  0.138 km
 77   96/169  (1.24)  917.746 km  317.746  +/-  0.31 km  82.18   0h 49.0m    68h 58.8m +02.1m    2.7  0.0133  0.139 km
 78   79/139  (1.03)  920.487 km  320.487  +/-  0.47 km  82.14   0h 49.2m    56h 58.9m +02.6m    2.7  0.0134  0.140 km
 79   83/146  (1.09)  921.736 km  321.736  +/-  0.43 km  82.13   0h 49.3m    59h 58.5m +02.5m    2.7  0.0134  0.141 km
 80   91/160  (1.20)  924.106 km  324.106  +/-  0.34 km  82.10   0h 49.5m    65h 59.1m +02.2m    2.7  0.0135  0.142 km
 81   78/137  (1.05)  929.338 km  329.338  +/-  0.11 km  82.03   0h 49.9m    56h 59.4m +00.6m    2.7  0.0137  0.144 km
 82   73/128  (1.00)  938.016 km  338.016  +/-  0.53 km  81.92   0h 50.6m    53h 58.6m +02.8m    2.8  0.0141  0.148 km
 83   77/135  (1.06)  938.534 km  338.534  +/-  0.48 km  81.91   0h 50.6m    56h 58.6m +02.6m    2.8  0.0141  0.148 km
 84   81/142  (1.12)  938.999 km  338.999  +/-  0.43 km  81.90   0h 50.7m    59h 58.7m +02.5m    2.8  0.0141  0.148 km
 85   85/149  (1.17)  939.421 km  339.421  +/-  0.40 km  81.90   0h 50.7m    62h 58.8m +02.4m    2.8  0.0142  0.148 km
 86   89/156  (1.23)  939.809 km  339.809  +/-  0.35 km  81.89   0h 50.8m    65h 58.9m +02.2m    2.8  0.0142  0.148 km
 87   83/145  (1.20)  956.632 km  356.632  +/-  0.41 km  81.67   0h 52.1m    62h 58.8m +02.4m    3.0  0.0149  0.156 km
 88   79/138  (1.14)  957.072 km  357.072  +/-  0.46 km  81.67   0h 52.2m    59h 58.7m +02.6m    3.0  0.0149  0.156 km
 89   75/131  (1.08)  957.563 km  357.563  +/-  0.51 km  81.66   0h 52.2m    56h 58.7m +02.7m    3.0  0.0149  0.156 km
 90   71/124  (1.03)  958.106 km  358.106  +/-  0.56 km  81.65   0h 52.2m    53h 58.6m +02.8m    3.0  0.0149  0.156 km
 91   82/143  (1.21)  965.535 km  365.535  +/-  0.02 km  81.56   0h 52.9m    63h 00.0m +00.1m    3.1  0.0153  0.160 km
 92   74/129  (1.10)  967.466 km  367.466  +/-  0.33 km  81.53   0h 53.0m    56h 59.4m +01.7m    3.1  0.0153  0.161 km
 93   77/134  (1.17)  976.067 km  376.067  +/-  0.49 km  81.42   0h 53.7m    59h 58.9m +02.7m    3.1  0.0157  0.164 km
 94   73/127  (1.11)  977.515 km  377.515  +/-  0.54 km  81.40   0h 53.8m    56h 58.4m +02.8m    3.2  0.0158  0.165 km
 95   80/139  (1.24)  983.927 km  383.927  +/-  0.45 km  81.31   0h 54.4m    62h 58.5m +02.6m    3.2  0.0160  0.168 km
 96   72/125  (1.12)  987.995 km  387.995  +/-  0.56 km  81.26   0h 54.7m    56h 58.7m +02.9m    3.2  0.0162  0.170 km
 97   64/111  (1.01)  992.899 km  392.899  +/-  0.71 km  81.19   0h 55.1m    50h 58.2m +03.3m    3.3  0.0164  0.172 km
 98   79/137  (1.25)  993.433 km  393.433  +/-  0.34 km  81.18   0h 55.2m    62h 58.6m +02.0m    3.3  0.0164  0.172 km
 99   71/123  (1.14)  998.664 km  398.664  +/-  0.57 km  81.11   0h 55.6m    56h 58.7m +02.9m    3.3  0.0166  0.174 km
100   67/116  (1.08)  1001.698 km  401.698  +/-  0.44 km  81.07   0h 55.8m    53h 59.1m +02.1m    3.4  0.0168  0.176 km
101   63/109  (1.02)  1005.042 km  405.042  +/-  0.57 km  81.03   0h 56.1m    50h 58.7m +02.6m    3.4  0.0169  0.177 km
102   70/121  (1.15)  1009.584 km  409.584  +/-  0.59 km  80.97   0h 56.5m    56h 58.4m +03.0m    3.4  0.0171  0.179 km
103   73/126  (1.22)  1016.927 km  416.927  +/-  0.53 km  80.87   0h 57.1m    59h 58.7m +02.8m    3.5  0.0174  0.182 km
104   62/107  (1.03)  1017.573 km  417.573  +/-  0.75 km  80.86   0h 57.2m    50h 58.5m +03.4m    3.5  0.0174  0.182 km
105   69/119  (1.16)  1020.917 km  420.917  +/-  0.43 km  80.81   0h 57.5m    56h 59.1m +02.2m    3.5  0.0176  0.184 km
106   65/112  (1.10)  1025.313 km  425.313  +/-  0.68 km  80.75   0h 57.8m    53h 58.1m +03.2m    3.5  0.0177  0.186 km
107   61/105  (1.05)  1030.475 km  430.475  +/-  0.78 km  80.68   0h 58.3m    50h 58.5m +03.5m    3.6  0.0180  0.188 km
108   68/117  (1.17)  1032.431 km  432.431  +/-  0.63 km  80.65   0h 58.4m    56h 58.1m +03.1m    3.6  0.0180  0.189 km
109   71/122  (1.24)  1038.990 km  438.990  +/-  0.41 km  80.56   0h 59.0m    59h 58.8m +02.2m    3.7  0.0183  0.192 km
110   60/103  (1.06)  1043.687 km  443.687  +/-  0.79 km  80.50   0h 59.4m    50h 58.1m +03.5m    3.7  0.0185  0.194 km
111   67/115  (1.18)  1044.411 km  444.411  +/-  0.63 km  80.49   0h 59.4m    56h 58.4m +03.1m    3.7  0.0185  0.194 km
112   66/113  (1.20)  1056.735 km  456.735  +/-  0.65 km  80.32   1h 00.5m    56h 58.5m +03.1m    3.8  0.0191  0.200 km
113   59/101  (1.07)  1057.477 km  457.477  +/-  0.82 km  80.31   1h 00.6m    50h 58.3m +03.6m    3.8  0.0191  0.200 km
114   55/94   (1.01)  1065.388 km  465.388  +/-  0.75 km  80.20   1h 01.2m    47h 58.5m +03.0m    3.9  0.0194  0.203 km
115   65/111  (1.21)  1069.430 km  469.430  +/-  0.69 km  80.14   1h 01.6m    56h 58.6m +03.3m    3.9  0.0196  0.205 km
116   58/99   (1.08)  1071.576 km  471.576  +/-  0.86 km  80.11   1h 01.8m    50h 57.9m +03.7m    3.9  0.0197  0.206 km
117   61/104  (1.15)  1077.342 km  477.342  +/-  0.78 km  80.03   1h 02.3m    53h 58.5m +03.5m    4.0  0.0199  0.209 km
118   64/109  (1.22)  1082.401 km  482.401  +/-  0.55 km  79.96   1h 02.7m    56h 58.7m +02.6m    4.0  0.0201  0.211 km
119   57/97   (1.09)  1086.279 km  486.279  +/-  0.88 km  79.91   1h 03.1m    50h 58.0m +03.7m    4.1  0.0203  0.213 km
120   63/107  (1.23)  1095.889 km  495.889  +/-  0.72 km  79.77   1h 03.9m    56h 58.5m +03.3m    4.1  0.0207  0.217 km
121   53/90   (1.04)  1096.759 km  496.759  +/-  1.02 km  79.76   1h 04.0m    47h 58.2m +04.0m    4.1  0.0207  0.217 km
```


The numerator in the 2nd (Res -- Resonance) column is the number of unique equitorial crossings in the total period (Time to Scan column).

