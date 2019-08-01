# Predictive Maintenance
There are a lot of unscheduled maintenance events that cause delays and disruptions on turbofan engines.

# Datasets
https://ti.arc.nasa.gov/tech/dash/groups/pcoe/prognostic-data-repository/#turbofan.

NASA Turbofan fault dataset produced from the C-MAPP aircraft health monitoring tool.
Engine degradation simulation was carried out using C-MAPSS. Four different were sets simulated under different combinations of operational conditions and fault modes. Records several sensor channels to characterize fault evolution. The data set was provided by the Prognostics CoE at NASA Ames.

Data Elements:
* unit number
* time, in cycles
* operational setting 1
* operational setting 2
* operational setting 3
* sensor measurement 1
* sensor measurement 2 ...
* sensor measurement 26

Wishlist data:

Historical Pilot reports of incidents
Flight crew maintenance observations
Maintenance log books
Weather/Turbulence conditions
Frequency of use
Load conditions
Geographic location of hangar
Fuel Quality

# Modeling Strategy
1. Check data quality - clean noise 
- e.g. per readme.txt file, the data is contaminated with sensor noise
- scrub timestamps to common format
- create new column (FAN_ID) in RUL* file
2. EDA
Plot sensor reading values  against operational settings (define independent and dependent variables)
Remove features that do not matter
Calculate RUL for training set by engine type
Merge RUL to test data to prepare for validation
3. Create Regression Model
4. Train, Test, Validate

# End Goal
Calculate RUL for an engine type using sensor readings and operational settings to alert engineers when engine is getting close to end of life.


Notes:
$ wc -l RUL*
 	100 RUL_FD001.txt
 	259 RUL_FD002.txt
 	100 RUL_FD003.txt
 	248 RUL_FD004.txt

$ tail -1 t*_FD001.txt
==> test_FD001.txt <==
100 198 0.0013 0.0003 100.0 518.67 642.95 1601.62 1424.99 14.62 21.61 552.48 2388.06 9155.03 1.30 47.80 521.07 2388.05 8214.64 8.4903 0.03 396 2388 100.00 38.70 23.1855  

==> train_FD001.txt <==
100 200 -0.0032 -0.0005 100.0 518.67 643.85 1600.38 1432.14 14.62 21.61 550.79 2388.26 9061.48 1.30 48.20 519.30 2388.26 8137.33 8.5036 0.03 396 2388 100.00 38.37 23.0522  

$ tail -1 t*_FD002.txt
==> test_FD002.txt <==
259 123 42.0033 0.8400 100.0 445.00 549.77 1342.50 1126.96 3.91 5.71 138.37 2212.27 8339.14 1.02 41.93 130.93 2388.40 8105.28 9.3458 0.02 331 2212 100.00 10.63 6.3480  

==> train_FD002.txt <==
260 316 35.0036 0.8400 100.0 449.44 556.64 1374.61 1145.52 5.48 8.01 194.33 2225.12 8478.44 1.02 42.50 183.09 2390.38 8185.35 9.3998 0.02 338 2223 100.00 14.75 8.8446  

$ tail -1 t*_FD003.txt
==> test_FD003.txt <==
100 247 0.0023 0.0004 100.0 518.67 643.19 1592.54 1407.20 14.62 21.58 562.32 2388.30 9094.27 1.31 47.71 529.59 2388.29 8169.24 8.3191 0.03 392 2388 100.00 39.41 23.6536  

==> train_FD003.txt <==
100 152 0.0000 0.0003 100.0 518.67 643.64 1599.04 1436.06 14.62 21.61 550.96 2388.26 9066.52 1.30 48.12 519.48 2388.24 8136.98 8.5150 0.03 396 2388 100.00 38.56 23.0847  

$ tail -1 t*_FD004.txt
==> test_FD004.txt <==
248 281 35.0075 0.8402 100.0 449.44 556.40 1378.58 1140.70 5.48 8.00 194.26 2223.50 8392.96 1.02 42.08 181.88 2388.59 8098.17 9.3964 0.02 335 2223 100.00 14.72 8.8502  

==> train_FD004.txt <==
249 255 42.0030 0.8400 100.0 445.00 549.85 1369.75 1147.45 3.91 5.69 142.47 2212.52 8391.31 1.05 42.60 134.32 2388.66 8144.33 9.1207 0.02 333 2212 100.00 10.66 6.4341  





