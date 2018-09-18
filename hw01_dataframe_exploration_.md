Dataframe exploration
================
Zuheng(David) Xu
2018-09-11

![](https://img.buzzfeed.com/buzzfeed-static/static/enhanced/webdr02/2013/5/7/13/anigif_enhanced-buzz-26151-1367949414-13.gif)

Dataset Discription
-------------------

The dataset `larin` is available to use in R package `TSA`, which is a one dimensional time series containing 115 observations froim 1878 to 1992:

``` r
library(TSA)
data(larain)
```

``` r
summary(larain)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   4.080   9.675  14.140  14.888  18.400  40.290

Sequence plot：

``` r
plot.ts(larain)
```

<img src="Untitled_files/figure-markdown_github/pressure-1.png" style="display: block; margin: auto;" />

Time Series Analysis
--------------------

### Tools

Our goal is to build a time serie model to fit the `larain` data and predit rain volume in the future.

Some packages may be used:

| **Packages** | **Discription**                        |
|--------------|----------------------------------------|
| `TSA`        | white noise test                       |
| `tseries`    | adf test(stationary test)              |
| `forecast`   | forcast by auto generating ARIMA model |
| `astsa`      | SARIMA model                           |

### Model Building Strategy

1.  Visualize the series
2.  Stationarize the series
3.  Model identification

-   ARIMA
-   GARCH

1.  Finding optimal parameters
2.  Prediction

### White Noise and Stationary Test

Before we apply any models, we use Box-test to see if the data has any information. If it is a totally random series, then there is no point to use any model building strategy.

``` r
Box.test(larain,type="Ljung-Box")
```

    ## 
    ##  Box-Ljung test
    ## 
    ## data:  larain
    ## X-squared = 0.12634, df = 1, p-value = 0.7223

It is clearly shown on the outcome that the data is basically a white noise, which means the data is a sequence of independent sample. Therefore, there is no reason to continue.

References
----------

1.  *[Time Series Analysis and Its Applications](http://www.bookmetrix.com/detail_full/book/c7d7cfb0-3e51-4764-bd0f-a43e4d25d73a#citations)*
2.  *R in Action*

some datafrome exploration
--------------------------

Since the date I used above is a time serie data, whose only variable is time. I will use `gapminder` to practice some data amnage skill.

``` r
library(gapminder)

gapminder[1:10,]# to look the first 10 row of the dataset
```

    ## # A tibble: 10 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.

### 

Using `attach` to read the variable's name of the dataset:

``` r
attach(gapminder)
```

Let's explore `gapminder` with functions like `head`, `ncol`, `str`, `summary`.

``` r
head(gapminder) #top 6 rows 
```

    ## # A tibble: 6 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.
    ## 6 Afghanistan Asia       1977    38.4 14880372      786.

``` r
str(gapminder) # dataframe about this data
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

``` r
ncol(gapminder) #number of cols
```

    ## [1] 6

``` r
#summary(gapminder)# statistical summary 
```

### Extracting columns/rows

Let's extract a column with `$`. Maybe compute its variance.

``` r
gapminder$country #extract column variable "country" 
```

    ##    [1] Afghanistan              Afghanistan             
    ##    [3] Afghanistan              Afghanistan             
    ##    [5] Afghanistan              Afghanistan             
    ##    [7] Afghanistan              Afghanistan             
    ##    [9] Afghanistan              Afghanistan             
    ##   [11] Afghanistan              Afghanistan             
    ##   [13] Albania                  Albania                 
    ##   [15] Albania                  Albania                 
    ##   [17] Albania                  Albania                 
    ##   [19] Albania                  Albania                 
    ##   [21] Albania                  Albania                 
    ##   [23] Albania                  Albania                 
    ##   [25] Algeria                  Algeria                 
    ##   [27] Algeria                  Algeria                 
    ##   [29] Algeria                  Algeria                 
    ##   [31] Algeria                  Algeria                 
    ##   [33] Algeria                  Algeria                 
    ##   [35] Algeria                  Algeria                 
    ##   [37] Angola                   Angola                  
    ##   [39] Angola                   Angola                  
    ##   [41] Angola                   Angola                  
    ##   [43] Angola                   Angola                  
    ##   [45] Angola                   Angola                  
    ##   [47] Angola                   Angola                  
    ##   [49] Argentina                Argentina               
    ##   [51] Argentina                Argentina               
    ##   [53] Argentina                Argentina               
    ##   [55] Argentina                Argentina               
    ##   [57] Argentina                Argentina               
    ##   [59] Argentina                Argentina               
    ##   [61] Australia                Australia               
    ##   [63] Australia                Australia               
    ##   [65] Australia                Australia               
    ##   [67] Australia                Australia               
    ##   [69] Australia                Australia               
    ##   [71] Australia                Australia               
    ##   [73] Austria                  Austria                 
    ##   [75] Austria                  Austria                 
    ##   [77] Austria                  Austria                 
    ##   [79] Austria                  Austria                 
    ##   [81] Austria                  Austria                 
    ##   [83] Austria                  Austria                 
    ##   [85] Bahrain                  Bahrain                 
    ##   [87] Bahrain                  Bahrain                 
    ##   [89] Bahrain                  Bahrain                 
    ##   [91] Bahrain                  Bahrain                 
    ##   [93] Bahrain                  Bahrain                 
    ##   [95] Bahrain                  Bahrain                 
    ##   [97] Bangladesh               Bangladesh              
    ##   [99] Bangladesh               Bangladesh              
    ##  [101] Bangladesh               Bangladesh              
    ##  [103] Bangladesh               Bangladesh              
    ##  [105] Bangladesh               Bangladesh              
    ##  [107] Bangladesh               Bangladesh              
    ##  [109] Belgium                  Belgium                 
    ##  [111] Belgium                  Belgium                 
    ##  [113] Belgium                  Belgium                 
    ##  [115] Belgium                  Belgium                 
    ##  [117] Belgium                  Belgium                 
    ##  [119] Belgium                  Belgium                 
    ##  [121] Benin                    Benin                   
    ##  [123] Benin                    Benin                   
    ##  [125] Benin                    Benin                   
    ##  [127] Benin                    Benin                   
    ##  [129] Benin                    Benin                   
    ##  [131] Benin                    Benin                   
    ##  [133] Bolivia                  Bolivia                 
    ##  [135] Bolivia                  Bolivia                 
    ##  [137] Bolivia                  Bolivia                 
    ##  [139] Bolivia                  Bolivia                 
    ##  [141] Bolivia                  Bolivia                 
    ##  [143] Bolivia                  Bolivia                 
    ##  [145] Bosnia and Herzegovina   Bosnia and Herzegovina  
    ##  [147] Bosnia and Herzegovina   Bosnia and Herzegovina  
    ##  [149] Bosnia and Herzegovina   Bosnia and Herzegovina  
    ##  [151] Bosnia and Herzegovina   Bosnia and Herzegovina  
    ##  [153] Bosnia and Herzegovina   Bosnia and Herzegovina  
    ##  [155] Bosnia and Herzegovina   Bosnia and Herzegovina  
    ##  [157] Botswana                 Botswana                
    ##  [159] Botswana                 Botswana                
    ##  [161] Botswana                 Botswana                
    ##  [163] Botswana                 Botswana                
    ##  [165] Botswana                 Botswana                
    ##  [167] Botswana                 Botswana                
    ##  [169] Brazil                   Brazil                  
    ##  [171] Brazil                   Brazil                  
    ##  [173] Brazil                   Brazil                  
    ##  [175] Brazil                   Brazil                  
    ##  [177] Brazil                   Brazil                  
    ##  [179] Brazil                   Brazil                  
    ##  [181] Bulgaria                 Bulgaria                
    ##  [183] Bulgaria                 Bulgaria                
    ##  [185] Bulgaria                 Bulgaria                
    ##  [187] Bulgaria                 Bulgaria                
    ##  [189] Bulgaria                 Bulgaria                
    ##  [191] Bulgaria                 Bulgaria                
    ##  [193] Burkina Faso             Burkina Faso            
    ##  [195] Burkina Faso             Burkina Faso            
    ##  [197] Burkina Faso             Burkina Faso            
    ##  [199] Burkina Faso             Burkina Faso            
    ##  [201] Burkina Faso             Burkina Faso            
    ##  [203] Burkina Faso             Burkina Faso            
    ##  [205] Burundi                  Burundi                 
    ##  [207] Burundi                  Burundi                 
    ##  [209] Burundi                  Burundi                 
    ##  [211] Burundi                  Burundi                 
    ##  [213] Burundi                  Burundi                 
    ##  [215] Burundi                  Burundi                 
    ##  [217] Cambodia                 Cambodia                
    ##  [219] Cambodia                 Cambodia                
    ##  [221] Cambodia                 Cambodia                
    ##  [223] Cambodia                 Cambodia                
    ##  [225] Cambodia                 Cambodia                
    ##  [227] Cambodia                 Cambodia                
    ##  [229] Cameroon                 Cameroon                
    ##  [231] Cameroon                 Cameroon                
    ##  [233] Cameroon                 Cameroon                
    ##  [235] Cameroon                 Cameroon                
    ##  [237] Cameroon                 Cameroon                
    ##  [239] Cameroon                 Cameroon                
    ##  [241] Canada                   Canada                  
    ##  [243] Canada                   Canada                  
    ##  [245] Canada                   Canada                  
    ##  [247] Canada                   Canada                  
    ##  [249] Canada                   Canada                  
    ##  [251] Canada                   Canada                  
    ##  [253] Central African Republic Central African Republic
    ##  [255] Central African Republic Central African Republic
    ##  [257] Central African Republic Central African Republic
    ##  [259] Central African Republic Central African Republic
    ##  [261] Central African Republic Central African Republic
    ##  [263] Central African Republic Central African Republic
    ##  [265] Chad                     Chad                    
    ##  [267] Chad                     Chad                    
    ##  [269] Chad                     Chad                    
    ##  [271] Chad                     Chad                    
    ##  [273] Chad                     Chad                    
    ##  [275] Chad                     Chad                    
    ##  [277] Chile                    Chile                   
    ##  [279] Chile                    Chile                   
    ##  [281] Chile                    Chile                   
    ##  [283] Chile                    Chile                   
    ##  [285] Chile                    Chile                   
    ##  [287] Chile                    Chile                   
    ##  [289] China                    China                   
    ##  [291] China                    China                   
    ##  [293] China                    China                   
    ##  [295] China                    China                   
    ##  [297] China                    China                   
    ##  [299] China                    China                   
    ##  [301] Colombia                 Colombia                
    ##  [303] Colombia                 Colombia                
    ##  [305] Colombia                 Colombia                
    ##  [307] Colombia                 Colombia                
    ##  [309] Colombia                 Colombia                
    ##  [311] Colombia                 Colombia                
    ##  [313] Comoros                  Comoros                 
    ##  [315] Comoros                  Comoros                 
    ##  [317] Comoros                  Comoros                 
    ##  [319] Comoros                  Comoros                 
    ##  [321] Comoros                  Comoros                 
    ##  [323] Comoros                  Comoros                 
    ##  [325] Congo, Dem. Rep.         Congo, Dem. Rep.        
    ##  [327] Congo, Dem. Rep.         Congo, Dem. Rep.        
    ##  [329] Congo, Dem. Rep.         Congo, Dem. Rep.        
    ##  [331] Congo, Dem. Rep.         Congo, Dem. Rep.        
    ##  [333] Congo, Dem. Rep.         Congo, Dem. Rep.        
    ##  [335] Congo, Dem. Rep.         Congo, Dem. Rep.        
    ##  [337] Congo, Rep.              Congo, Rep.             
    ##  [339] Congo, Rep.              Congo, Rep.             
    ##  [341] Congo, Rep.              Congo, Rep.             
    ##  [343] Congo, Rep.              Congo, Rep.             
    ##  [345] Congo, Rep.              Congo, Rep.             
    ##  [347] Congo, Rep.              Congo, Rep.             
    ##  [349] Costa Rica               Costa Rica              
    ##  [351] Costa Rica               Costa Rica              
    ##  [353] Costa Rica               Costa Rica              
    ##  [355] Costa Rica               Costa Rica              
    ##  [357] Costa Rica               Costa Rica              
    ##  [359] Costa Rica               Costa Rica              
    ##  [361] Cote d'Ivoire            Cote d'Ivoire           
    ##  [363] Cote d'Ivoire            Cote d'Ivoire           
    ##  [365] Cote d'Ivoire            Cote d'Ivoire           
    ##  [367] Cote d'Ivoire            Cote d'Ivoire           
    ##  [369] Cote d'Ivoire            Cote d'Ivoire           
    ##  [371] Cote d'Ivoire            Cote d'Ivoire           
    ##  [373] Croatia                  Croatia                 
    ##  [375] Croatia                  Croatia                 
    ##  [377] Croatia                  Croatia                 
    ##  [379] Croatia                  Croatia                 
    ##  [381] Croatia                  Croatia                 
    ##  [383] Croatia                  Croatia                 
    ##  [385] Cuba                     Cuba                    
    ##  [387] Cuba                     Cuba                    
    ##  [389] Cuba                     Cuba                    
    ##  [391] Cuba                     Cuba                    
    ##  [393] Cuba                     Cuba                    
    ##  [395] Cuba                     Cuba                    
    ##  [397] Czech Republic           Czech Republic          
    ##  [399] Czech Republic           Czech Republic          
    ##  [401] Czech Republic           Czech Republic          
    ##  [403] Czech Republic           Czech Republic          
    ##  [405] Czech Republic           Czech Republic          
    ##  [407] Czech Republic           Czech Republic          
    ##  [409] Denmark                  Denmark                 
    ##  [411] Denmark                  Denmark                 
    ##  [413] Denmark                  Denmark                 
    ##  [415] Denmark                  Denmark                 
    ##  [417] Denmark                  Denmark                 
    ##  [419] Denmark                  Denmark                 
    ##  [421] Djibouti                 Djibouti                
    ##  [423] Djibouti                 Djibouti                
    ##  [425] Djibouti                 Djibouti                
    ##  [427] Djibouti                 Djibouti                
    ##  [429] Djibouti                 Djibouti                
    ##  [431] Djibouti                 Djibouti                
    ##  [433] Dominican Republic       Dominican Republic      
    ##  [435] Dominican Republic       Dominican Republic      
    ##  [437] Dominican Republic       Dominican Republic      
    ##  [439] Dominican Republic       Dominican Republic      
    ##  [441] Dominican Republic       Dominican Republic      
    ##  [443] Dominican Republic       Dominican Republic      
    ##  [445] Ecuador                  Ecuador                 
    ##  [447] Ecuador                  Ecuador                 
    ##  [449] Ecuador                  Ecuador                 
    ##  [451] Ecuador                  Ecuador                 
    ##  [453] Ecuador                  Ecuador                 
    ##  [455] Ecuador                  Ecuador                 
    ##  [457] Egypt                    Egypt                   
    ##  [459] Egypt                    Egypt                   
    ##  [461] Egypt                    Egypt                   
    ##  [463] Egypt                    Egypt                   
    ##  [465] Egypt                    Egypt                   
    ##  [467] Egypt                    Egypt                   
    ##  [469] El Salvador              El Salvador             
    ##  [471] El Salvador              El Salvador             
    ##  [473] El Salvador              El Salvador             
    ##  [475] El Salvador              El Salvador             
    ##  [477] El Salvador              El Salvador             
    ##  [479] El Salvador              El Salvador             
    ##  [481] Equatorial Guinea        Equatorial Guinea       
    ##  [483] Equatorial Guinea        Equatorial Guinea       
    ##  [485] Equatorial Guinea        Equatorial Guinea       
    ##  [487] Equatorial Guinea        Equatorial Guinea       
    ##  [489] Equatorial Guinea        Equatorial Guinea       
    ##  [491] Equatorial Guinea        Equatorial Guinea       
    ##  [493] Eritrea                  Eritrea                 
    ##  [495] Eritrea                  Eritrea                 
    ##  [497] Eritrea                  Eritrea                 
    ##  [499] Eritrea                  Eritrea                 
    ##  [501] Eritrea                  Eritrea                 
    ##  [503] Eritrea                  Eritrea                 
    ##  [505] Ethiopia                 Ethiopia                
    ##  [507] Ethiopia                 Ethiopia                
    ##  [509] Ethiopia                 Ethiopia                
    ##  [511] Ethiopia                 Ethiopia                
    ##  [513] Ethiopia                 Ethiopia                
    ##  [515] Ethiopia                 Ethiopia                
    ##  [517] Finland                  Finland                 
    ##  [519] Finland                  Finland                 
    ##  [521] Finland                  Finland                 
    ##  [523] Finland                  Finland                 
    ##  [525] Finland                  Finland                 
    ##  [527] Finland                  Finland                 
    ##  [529] France                   France                  
    ##  [531] France                   France                  
    ##  [533] France                   France                  
    ##  [535] France                   France                  
    ##  [537] France                   France                  
    ##  [539] France                   France                  
    ##  [541] Gabon                    Gabon                   
    ##  [543] Gabon                    Gabon                   
    ##  [545] Gabon                    Gabon                   
    ##  [547] Gabon                    Gabon                   
    ##  [549] Gabon                    Gabon                   
    ##  [551] Gabon                    Gabon                   
    ##  [553] Gambia                   Gambia                  
    ##  [555] Gambia                   Gambia                  
    ##  [557] Gambia                   Gambia                  
    ##  [559] Gambia                   Gambia                  
    ##  [561] Gambia                   Gambia                  
    ##  [563] Gambia                   Gambia                  
    ##  [565] Germany                  Germany                 
    ##  [567] Germany                  Germany                 
    ##  [569] Germany                  Germany                 
    ##  [571] Germany                  Germany                 
    ##  [573] Germany                  Germany                 
    ##  [575] Germany                  Germany                 
    ##  [577] Ghana                    Ghana                   
    ##  [579] Ghana                    Ghana                   
    ##  [581] Ghana                    Ghana                   
    ##  [583] Ghana                    Ghana                   
    ##  [585] Ghana                    Ghana                   
    ##  [587] Ghana                    Ghana                   
    ##  [589] Greece                   Greece                  
    ##  [591] Greece                   Greece                  
    ##  [593] Greece                   Greece                  
    ##  [595] Greece                   Greece                  
    ##  [597] Greece                   Greece                  
    ##  [599] Greece                   Greece                  
    ##  [601] Guatemala                Guatemala               
    ##  [603] Guatemala                Guatemala               
    ##  [605] Guatemala                Guatemala               
    ##  [607] Guatemala                Guatemala               
    ##  [609] Guatemala                Guatemala               
    ##  [611] Guatemala                Guatemala               
    ##  [613] Guinea                   Guinea                  
    ##  [615] Guinea                   Guinea                  
    ##  [617] Guinea                   Guinea                  
    ##  [619] Guinea                   Guinea                  
    ##  [621] Guinea                   Guinea                  
    ##  [623] Guinea                   Guinea                  
    ##  [625] Guinea-Bissau            Guinea-Bissau           
    ##  [627] Guinea-Bissau            Guinea-Bissau           
    ##  [629] Guinea-Bissau            Guinea-Bissau           
    ##  [631] Guinea-Bissau            Guinea-Bissau           
    ##  [633] Guinea-Bissau            Guinea-Bissau           
    ##  [635] Guinea-Bissau            Guinea-Bissau           
    ##  [637] Haiti                    Haiti                   
    ##  [639] Haiti                    Haiti                   
    ##  [641] Haiti                    Haiti                   
    ##  [643] Haiti                    Haiti                   
    ##  [645] Haiti                    Haiti                   
    ##  [647] Haiti                    Haiti                   
    ##  [649] Honduras                 Honduras                
    ##  [651] Honduras                 Honduras                
    ##  [653] Honduras                 Honduras                
    ##  [655] Honduras                 Honduras                
    ##  [657] Honduras                 Honduras                
    ##  [659] Honduras                 Honduras                
    ##  [661] Hong Kong, China         Hong Kong, China        
    ##  [663] Hong Kong, China         Hong Kong, China        
    ##  [665] Hong Kong, China         Hong Kong, China        
    ##  [667] Hong Kong, China         Hong Kong, China        
    ##  [669] Hong Kong, China         Hong Kong, China        
    ##  [671] Hong Kong, China         Hong Kong, China        
    ##  [673] Hungary                  Hungary                 
    ##  [675] Hungary                  Hungary                 
    ##  [677] Hungary                  Hungary                 
    ##  [679] Hungary                  Hungary                 
    ##  [681] Hungary                  Hungary                 
    ##  [683] Hungary                  Hungary                 
    ##  [685] Iceland                  Iceland                 
    ##  [687] Iceland                  Iceland                 
    ##  [689] Iceland                  Iceland                 
    ##  [691] Iceland                  Iceland                 
    ##  [693] Iceland                  Iceland                 
    ##  [695] Iceland                  Iceland                 
    ##  [697] India                    India                   
    ##  [699] India                    India                   
    ##  [701] India                    India                   
    ##  [703] India                    India                   
    ##  [705] India                    India                   
    ##  [707] India                    India                   
    ##  [709] Indonesia                Indonesia               
    ##  [711] Indonesia                Indonesia               
    ##  [713] Indonesia                Indonesia               
    ##  [715] Indonesia                Indonesia               
    ##  [717] Indonesia                Indonesia               
    ##  [719] Indonesia                Indonesia               
    ##  [721] Iran                     Iran                    
    ##  [723] Iran                     Iran                    
    ##  [725] Iran                     Iran                    
    ##  [727] Iran                     Iran                    
    ##  [729] Iran                     Iran                    
    ##  [731] Iran                     Iran                    
    ##  [733] Iraq                     Iraq                    
    ##  [735] Iraq                     Iraq                    
    ##  [737] Iraq                     Iraq                    
    ##  [739] Iraq                     Iraq                    
    ##  [741] Iraq                     Iraq                    
    ##  [743] Iraq                     Iraq                    
    ##  [745] Ireland                  Ireland                 
    ##  [747] Ireland                  Ireland                 
    ##  [749] Ireland                  Ireland                 
    ##  [751] Ireland                  Ireland                 
    ##  [753] Ireland                  Ireland                 
    ##  [755] Ireland                  Ireland                 
    ##  [757] Israel                   Israel                  
    ##  [759] Israel                   Israel                  
    ##  [761] Israel                   Israel                  
    ##  [763] Israel                   Israel                  
    ##  [765] Israel                   Israel                  
    ##  [767] Israel                   Israel                  
    ##  [769] Italy                    Italy                   
    ##  [771] Italy                    Italy                   
    ##  [773] Italy                    Italy                   
    ##  [775] Italy                    Italy                   
    ##  [777] Italy                    Italy                   
    ##  [779] Italy                    Italy                   
    ##  [781] Jamaica                  Jamaica                 
    ##  [783] Jamaica                  Jamaica                 
    ##  [785] Jamaica                  Jamaica                 
    ##  [787] Jamaica                  Jamaica                 
    ##  [789] Jamaica                  Jamaica                 
    ##  [791] Jamaica                  Jamaica                 
    ##  [793] Japan                    Japan                   
    ##  [795] Japan                    Japan                   
    ##  [797] Japan                    Japan                   
    ##  [799] Japan                    Japan                   
    ##  [801] Japan                    Japan                   
    ##  [803] Japan                    Japan                   
    ##  [805] Jordan                   Jordan                  
    ##  [807] Jordan                   Jordan                  
    ##  [809] Jordan                   Jordan                  
    ##  [811] Jordan                   Jordan                  
    ##  [813] Jordan                   Jordan                  
    ##  [815] Jordan                   Jordan                  
    ##  [817] Kenya                    Kenya                   
    ##  [819] Kenya                    Kenya                   
    ##  [821] Kenya                    Kenya                   
    ##  [823] Kenya                    Kenya                   
    ##  [825] Kenya                    Kenya                   
    ##  [827] Kenya                    Kenya                   
    ##  [829] Korea, Dem. Rep.         Korea, Dem. Rep.        
    ##  [831] Korea, Dem. Rep.         Korea, Dem. Rep.        
    ##  [833] Korea, Dem. Rep.         Korea, Dem. Rep.        
    ##  [835] Korea, Dem. Rep.         Korea, Dem. Rep.        
    ##  [837] Korea, Dem. Rep.         Korea, Dem. Rep.        
    ##  [839] Korea, Dem. Rep.         Korea, Dem. Rep.        
    ##  [841] Korea, Rep.              Korea, Rep.             
    ##  [843] Korea, Rep.              Korea, Rep.             
    ##  [845] Korea, Rep.              Korea, Rep.             
    ##  [847] Korea, Rep.              Korea, Rep.             
    ##  [849] Korea, Rep.              Korea, Rep.             
    ##  [851] Korea, Rep.              Korea, Rep.             
    ##  [853] Kuwait                   Kuwait                  
    ##  [855] Kuwait                   Kuwait                  
    ##  [857] Kuwait                   Kuwait                  
    ##  [859] Kuwait                   Kuwait                  
    ##  [861] Kuwait                   Kuwait                  
    ##  [863] Kuwait                   Kuwait                  
    ##  [865] Lebanon                  Lebanon                 
    ##  [867] Lebanon                  Lebanon                 
    ##  [869] Lebanon                  Lebanon                 
    ##  [871] Lebanon                  Lebanon                 
    ##  [873] Lebanon                  Lebanon                 
    ##  [875] Lebanon                  Lebanon                 
    ##  [877] Lesotho                  Lesotho                 
    ##  [879] Lesotho                  Lesotho                 
    ##  [881] Lesotho                  Lesotho                 
    ##  [883] Lesotho                  Lesotho                 
    ##  [885] Lesotho                  Lesotho                 
    ##  [887] Lesotho                  Lesotho                 
    ##  [889] Liberia                  Liberia                 
    ##  [891] Liberia                  Liberia                 
    ##  [893] Liberia                  Liberia                 
    ##  [895] Liberia                  Liberia                 
    ##  [897] Liberia                  Liberia                 
    ##  [899] Liberia                  Liberia                 
    ##  [901] Libya                    Libya                   
    ##  [903] Libya                    Libya                   
    ##  [905] Libya                    Libya                   
    ##  [907] Libya                    Libya                   
    ##  [909] Libya                    Libya                   
    ##  [911] Libya                    Libya                   
    ##  [913] Madagascar               Madagascar              
    ##  [915] Madagascar               Madagascar              
    ##  [917] Madagascar               Madagascar              
    ##  [919] Madagascar               Madagascar              
    ##  [921] Madagascar               Madagascar              
    ##  [923] Madagascar               Madagascar              
    ##  [925] Malawi                   Malawi                  
    ##  [927] Malawi                   Malawi                  
    ##  [929] Malawi                   Malawi                  
    ##  [931] Malawi                   Malawi                  
    ##  [933] Malawi                   Malawi                  
    ##  [935] Malawi                   Malawi                  
    ##  [937] Malaysia                 Malaysia                
    ##  [939] Malaysia                 Malaysia                
    ##  [941] Malaysia                 Malaysia                
    ##  [943] Malaysia                 Malaysia                
    ##  [945] Malaysia                 Malaysia                
    ##  [947] Malaysia                 Malaysia                
    ##  [949] Mali                     Mali                    
    ##  [951] Mali                     Mali                    
    ##  [953] Mali                     Mali                    
    ##  [955] Mali                     Mali                    
    ##  [957] Mali                     Mali                    
    ##  [959] Mali                     Mali                    
    ##  [961] Mauritania               Mauritania              
    ##  [963] Mauritania               Mauritania              
    ##  [965] Mauritania               Mauritania              
    ##  [967] Mauritania               Mauritania              
    ##  [969] Mauritania               Mauritania              
    ##  [971] Mauritania               Mauritania              
    ##  [973] Mauritius                Mauritius               
    ##  [975] Mauritius                Mauritius               
    ##  [977] Mauritius                Mauritius               
    ##  [979] Mauritius                Mauritius               
    ##  [981] Mauritius                Mauritius               
    ##  [983] Mauritius                Mauritius               
    ##  [985] Mexico                   Mexico                  
    ##  [987] Mexico                   Mexico                  
    ##  [989] Mexico                   Mexico                  
    ##  [991] Mexico                   Mexico                  
    ##  [993] Mexico                   Mexico                  
    ##  [995] Mexico                   Mexico                  
    ##  [997] Mongolia                 Mongolia                
    ##  [999] Mongolia                 Mongolia                
    ## [1001] Mongolia                 Mongolia                
    ## [1003] Mongolia                 Mongolia                
    ## [1005] Mongolia                 Mongolia                
    ## [1007] Mongolia                 Mongolia                
    ## [1009] Montenegro               Montenegro              
    ## [1011] Montenegro               Montenegro              
    ## [1013] Montenegro               Montenegro              
    ## [1015] Montenegro               Montenegro              
    ## [1017] Montenegro               Montenegro              
    ## [1019] Montenegro               Montenegro              
    ## [1021] Morocco                  Morocco                 
    ## [1023] Morocco                  Morocco                 
    ## [1025] Morocco                  Morocco                 
    ## [1027] Morocco                  Morocco                 
    ## [1029] Morocco                  Morocco                 
    ## [1031] Morocco                  Morocco                 
    ## [1033] Mozambique               Mozambique              
    ## [1035] Mozambique               Mozambique              
    ## [1037] Mozambique               Mozambique              
    ## [1039] Mozambique               Mozambique              
    ## [1041] Mozambique               Mozambique              
    ## [1043] Mozambique               Mozambique              
    ## [1045] Myanmar                  Myanmar                 
    ## [1047] Myanmar                  Myanmar                 
    ## [1049] Myanmar                  Myanmar                 
    ## [1051] Myanmar                  Myanmar                 
    ## [1053] Myanmar                  Myanmar                 
    ## [1055] Myanmar                  Myanmar                 
    ## [1057] Namibia                  Namibia                 
    ## [1059] Namibia                  Namibia                 
    ## [1061] Namibia                  Namibia                 
    ## [1063] Namibia                  Namibia                 
    ## [1065] Namibia                  Namibia                 
    ## [1067] Namibia                  Namibia                 
    ## [1069] Nepal                    Nepal                   
    ## [1071] Nepal                    Nepal                   
    ## [1073] Nepal                    Nepal                   
    ## [1075] Nepal                    Nepal                   
    ## [1077] Nepal                    Nepal                   
    ## [1079] Nepal                    Nepal                   
    ## [1081] Netherlands              Netherlands             
    ## [1083] Netherlands              Netherlands             
    ## [1085] Netherlands              Netherlands             
    ## [1087] Netherlands              Netherlands             
    ## [1089] Netherlands              Netherlands             
    ## [1091] Netherlands              Netherlands             
    ## [1093] New Zealand              New Zealand             
    ## [1095] New Zealand              New Zealand             
    ## [1097] New Zealand              New Zealand             
    ## [1099] New Zealand              New Zealand             
    ## [1101] New Zealand              New Zealand             
    ## [1103] New Zealand              New Zealand             
    ## [1105] Nicaragua                Nicaragua               
    ## [1107] Nicaragua                Nicaragua               
    ## [1109] Nicaragua                Nicaragua               
    ## [1111] Nicaragua                Nicaragua               
    ## [1113] Nicaragua                Nicaragua               
    ## [1115] Nicaragua                Nicaragua               
    ## [1117] Niger                    Niger                   
    ## [1119] Niger                    Niger                   
    ## [1121] Niger                    Niger                   
    ## [1123] Niger                    Niger                   
    ## [1125] Niger                    Niger                   
    ## [1127] Niger                    Niger                   
    ## [1129] Nigeria                  Nigeria                 
    ## [1131] Nigeria                  Nigeria                 
    ## [1133] Nigeria                  Nigeria                 
    ## [1135] Nigeria                  Nigeria                 
    ## [1137] Nigeria                  Nigeria                 
    ## [1139] Nigeria                  Nigeria                 
    ## [1141] Norway                   Norway                  
    ## [1143] Norway                   Norway                  
    ## [1145] Norway                   Norway                  
    ## [1147] Norway                   Norway                  
    ## [1149] Norway                   Norway                  
    ## [1151] Norway                   Norway                  
    ## [1153] Oman                     Oman                    
    ## [1155] Oman                     Oman                    
    ## [1157] Oman                     Oman                    
    ## [1159] Oman                     Oman                    
    ## [1161] Oman                     Oman                    
    ## [1163] Oman                     Oman                    
    ## [1165] Pakistan                 Pakistan                
    ## [1167] Pakistan                 Pakistan                
    ## [1169] Pakistan                 Pakistan                
    ## [1171] Pakistan                 Pakistan                
    ## [1173] Pakistan                 Pakistan                
    ## [1175] Pakistan                 Pakistan                
    ## [1177] Panama                   Panama                  
    ## [1179] Panama                   Panama                  
    ## [1181] Panama                   Panama                  
    ## [1183] Panama                   Panama                  
    ## [1185] Panama                   Panama                  
    ## [1187] Panama                   Panama                  
    ## [1189] Paraguay                 Paraguay                
    ## [1191] Paraguay                 Paraguay                
    ## [1193] Paraguay                 Paraguay                
    ## [1195] Paraguay                 Paraguay                
    ## [1197] Paraguay                 Paraguay                
    ## [1199] Paraguay                 Paraguay                
    ## [1201] Peru                     Peru                    
    ## [1203] Peru                     Peru                    
    ## [1205] Peru                     Peru                    
    ## [1207] Peru                     Peru                    
    ## [1209] Peru                     Peru                    
    ## [1211] Peru                     Peru                    
    ## [1213] Philippines              Philippines             
    ## [1215] Philippines              Philippines             
    ## [1217] Philippines              Philippines             
    ## [1219] Philippines              Philippines             
    ## [1221] Philippines              Philippines             
    ## [1223] Philippines              Philippines             
    ## [1225] Poland                   Poland                  
    ## [1227] Poland                   Poland                  
    ## [1229] Poland                   Poland                  
    ## [1231] Poland                   Poland                  
    ## [1233] Poland                   Poland                  
    ## [1235] Poland                   Poland                  
    ## [1237] Portugal                 Portugal                
    ## [1239] Portugal                 Portugal                
    ## [1241] Portugal                 Portugal                
    ## [1243] Portugal                 Portugal                
    ## [1245] Portugal                 Portugal                
    ## [1247] Portugal                 Portugal                
    ## [1249] Puerto Rico              Puerto Rico             
    ## [1251] Puerto Rico              Puerto Rico             
    ## [1253] Puerto Rico              Puerto Rico             
    ## [1255] Puerto Rico              Puerto Rico             
    ## [1257] Puerto Rico              Puerto Rico             
    ## [1259] Puerto Rico              Puerto Rico             
    ## [1261] Reunion                  Reunion                 
    ## [1263] Reunion                  Reunion                 
    ## [1265] Reunion                  Reunion                 
    ## [1267] Reunion                  Reunion                 
    ## [1269] Reunion                  Reunion                 
    ## [1271] Reunion                  Reunion                 
    ## [1273] Romania                  Romania                 
    ## [1275] Romania                  Romania                 
    ## [1277] Romania                  Romania                 
    ## [1279] Romania                  Romania                 
    ## [1281] Romania                  Romania                 
    ## [1283] Romania                  Romania                 
    ## [1285] Rwanda                   Rwanda                  
    ## [1287] Rwanda                   Rwanda                  
    ## [1289] Rwanda                   Rwanda                  
    ## [1291] Rwanda                   Rwanda                  
    ## [1293] Rwanda                   Rwanda                  
    ## [1295] Rwanda                   Rwanda                  
    ## [1297] Sao Tome and Principe    Sao Tome and Principe   
    ## [1299] Sao Tome and Principe    Sao Tome and Principe   
    ## [1301] Sao Tome and Principe    Sao Tome and Principe   
    ## [1303] Sao Tome and Principe    Sao Tome and Principe   
    ## [1305] Sao Tome and Principe    Sao Tome and Principe   
    ## [1307] Sao Tome and Principe    Sao Tome and Principe   
    ## [1309] Saudi Arabia             Saudi Arabia            
    ## [1311] Saudi Arabia             Saudi Arabia            
    ## [1313] Saudi Arabia             Saudi Arabia            
    ## [1315] Saudi Arabia             Saudi Arabia            
    ## [1317] Saudi Arabia             Saudi Arabia            
    ## [1319] Saudi Arabia             Saudi Arabia            
    ## [1321] Senegal                  Senegal                 
    ## [1323] Senegal                  Senegal                 
    ## [1325] Senegal                  Senegal                 
    ## [1327] Senegal                  Senegal                 
    ## [1329] Senegal                  Senegal                 
    ## [1331] Senegal                  Senegal                 
    ## [1333] Serbia                   Serbia                  
    ## [1335] Serbia                   Serbia                  
    ## [1337] Serbia                   Serbia                  
    ## [1339] Serbia                   Serbia                  
    ## [1341] Serbia                   Serbia                  
    ## [1343] Serbia                   Serbia                  
    ## [1345] Sierra Leone             Sierra Leone            
    ## [1347] Sierra Leone             Sierra Leone            
    ## [1349] Sierra Leone             Sierra Leone            
    ## [1351] Sierra Leone             Sierra Leone            
    ## [1353] Sierra Leone             Sierra Leone            
    ## [1355] Sierra Leone             Sierra Leone            
    ## [1357] Singapore                Singapore               
    ## [1359] Singapore                Singapore               
    ## [1361] Singapore                Singapore               
    ## [1363] Singapore                Singapore               
    ## [1365] Singapore                Singapore               
    ## [1367] Singapore                Singapore               
    ## [1369] Slovak Republic          Slovak Republic         
    ## [1371] Slovak Republic          Slovak Republic         
    ## [1373] Slovak Republic          Slovak Republic         
    ## [1375] Slovak Republic          Slovak Republic         
    ## [1377] Slovak Republic          Slovak Republic         
    ## [1379] Slovak Republic          Slovak Republic         
    ## [1381] Slovenia                 Slovenia                
    ## [1383] Slovenia                 Slovenia                
    ## [1385] Slovenia                 Slovenia                
    ## [1387] Slovenia                 Slovenia                
    ## [1389] Slovenia                 Slovenia                
    ## [1391] Slovenia                 Slovenia                
    ## [1393] Somalia                  Somalia                 
    ## [1395] Somalia                  Somalia                 
    ## [1397] Somalia                  Somalia                 
    ## [1399] Somalia                  Somalia                 
    ## [1401] Somalia                  Somalia                 
    ## [1403] Somalia                  Somalia                 
    ## [1405] South Africa             South Africa            
    ## [1407] South Africa             South Africa            
    ## [1409] South Africa             South Africa            
    ## [1411] South Africa             South Africa            
    ## [1413] South Africa             South Africa            
    ## [1415] South Africa             South Africa            
    ## [1417] Spain                    Spain                   
    ## [1419] Spain                    Spain                   
    ## [1421] Spain                    Spain                   
    ## [1423] Spain                    Spain                   
    ## [1425] Spain                    Spain                   
    ## [1427] Spain                    Spain                   
    ## [1429] Sri Lanka                Sri Lanka               
    ## [1431] Sri Lanka                Sri Lanka               
    ## [1433] Sri Lanka                Sri Lanka               
    ## [1435] Sri Lanka                Sri Lanka               
    ## [1437] Sri Lanka                Sri Lanka               
    ## [1439] Sri Lanka                Sri Lanka               
    ## [1441] Sudan                    Sudan                   
    ## [1443] Sudan                    Sudan                   
    ## [1445] Sudan                    Sudan                   
    ## [1447] Sudan                    Sudan                   
    ## [1449] Sudan                    Sudan                   
    ## [1451] Sudan                    Sudan                   
    ## [1453] Swaziland                Swaziland               
    ## [1455] Swaziland                Swaziland               
    ## [1457] Swaziland                Swaziland               
    ## [1459] Swaziland                Swaziland               
    ## [1461] Swaziland                Swaziland               
    ## [1463] Swaziland                Swaziland               
    ## [1465] Sweden                   Sweden                  
    ## [1467] Sweden                   Sweden                  
    ## [1469] Sweden                   Sweden                  
    ## [1471] Sweden                   Sweden                  
    ## [1473] Sweden                   Sweden                  
    ## [1475] Sweden                   Sweden                  
    ## [1477] Switzerland              Switzerland             
    ## [1479] Switzerland              Switzerland             
    ## [1481] Switzerland              Switzerland             
    ## [1483] Switzerland              Switzerland             
    ## [1485] Switzerland              Switzerland             
    ## [1487] Switzerland              Switzerland             
    ## [1489] Syria                    Syria                   
    ## [1491] Syria                    Syria                   
    ## [1493] Syria                    Syria                   
    ## [1495] Syria                    Syria                   
    ## [1497] Syria                    Syria                   
    ## [1499] Syria                    Syria                   
    ## [1501] Taiwan                   Taiwan                  
    ## [1503] Taiwan                   Taiwan                  
    ## [1505] Taiwan                   Taiwan                  
    ## [1507] Taiwan                   Taiwan                  
    ## [1509] Taiwan                   Taiwan                  
    ## [1511] Taiwan                   Taiwan                  
    ## [1513] Tanzania                 Tanzania                
    ## [1515] Tanzania                 Tanzania                
    ## [1517] Tanzania                 Tanzania                
    ## [1519] Tanzania                 Tanzania                
    ## [1521] Tanzania                 Tanzania                
    ## [1523] Tanzania                 Tanzania                
    ## [1525] Thailand                 Thailand                
    ## [1527] Thailand                 Thailand                
    ## [1529] Thailand                 Thailand                
    ## [1531] Thailand                 Thailand                
    ## [1533] Thailand                 Thailand                
    ## [1535] Thailand                 Thailand                
    ## [1537] Togo                     Togo                    
    ## [1539] Togo                     Togo                    
    ## [1541] Togo                     Togo                    
    ## [1543] Togo                     Togo                    
    ## [1545] Togo                     Togo                    
    ## [1547] Togo                     Togo                    
    ## [1549] Trinidad and Tobago      Trinidad and Tobago     
    ## [1551] Trinidad and Tobago      Trinidad and Tobago     
    ## [1553] Trinidad and Tobago      Trinidad and Tobago     
    ## [1555] Trinidad and Tobago      Trinidad and Tobago     
    ## [1557] Trinidad and Tobago      Trinidad and Tobago     
    ## [1559] Trinidad and Tobago      Trinidad and Tobago     
    ## [1561] Tunisia                  Tunisia                 
    ## [1563] Tunisia                  Tunisia                 
    ## [1565] Tunisia                  Tunisia                 
    ## [1567] Tunisia                  Tunisia                 
    ## [1569] Tunisia                  Tunisia                 
    ## [1571] Tunisia                  Tunisia                 
    ## [1573] Turkey                   Turkey                  
    ## [1575] Turkey                   Turkey                  
    ## [1577] Turkey                   Turkey                  
    ## [1579] Turkey                   Turkey                  
    ## [1581] Turkey                   Turkey                  
    ## [1583] Turkey                   Turkey                  
    ## [1585] Uganda                   Uganda                  
    ## [1587] Uganda                   Uganda                  
    ## [1589] Uganda                   Uganda                  
    ## [1591] Uganda                   Uganda                  
    ## [1593] Uganda                   Uganda                  
    ## [1595] Uganda                   Uganda                  
    ## [1597] United Kingdom           United Kingdom          
    ## [1599] United Kingdom           United Kingdom          
    ## [1601] United Kingdom           United Kingdom          
    ## [1603] United Kingdom           United Kingdom          
    ## [1605] United Kingdom           United Kingdom          
    ## [1607] United Kingdom           United Kingdom          
    ## [1609] United States            United States           
    ## [1611] United States            United States           
    ## [1613] United States            United States           
    ## [1615] United States            United States           
    ## [1617] United States            United States           
    ## [1619] United States            United States           
    ## [1621] Uruguay                  Uruguay                 
    ## [1623] Uruguay                  Uruguay                 
    ## [1625] Uruguay                  Uruguay                 
    ## [1627] Uruguay                  Uruguay                 
    ## [1629] Uruguay                  Uruguay                 
    ## [1631] Uruguay                  Uruguay                 
    ## [1633] Venezuela                Venezuela               
    ## [1635] Venezuela                Venezuela               
    ## [1637] Venezuela                Venezuela               
    ## [1639] Venezuela                Venezuela               
    ## [1641] Venezuela                Venezuela               
    ## [1643] Venezuela                Venezuela               
    ## [1645] Vietnam                  Vietnam                 
    ## [1647] Vietnam                  Vietnam                 
    ## [1649] Vietnam                  Vietnam                 
    ## [1651] Vietnam                  Vietnam                 
    ## [1653] Vietnam                  Vietnam                 
    ## [1655] Vietnam                  Vietnam                 
    ## [1657] West Bank and Gaza       West Bank and Gaza      
    ## [1659] West Bank and Gaza       West Bank and Gaza      
    ## [1661] West Bank and Gaza       West Bank and Gaza      
    ## [1663] West Bank and Gaza       West Bank and Gaza      
    ## [1665] West Bank and Gaza       West Bank and Gaza      
    ## [1667] West Bank and Gaza       West Bank and Gaza      
    ## [1669] Yemen, Rep.              Yemen, Rep.             
    ## [1671] Yemen, Rep.              Yemen, Rep.             
    ## [1673] Yemen, Rep.              Yemen, Rep.             
    ## [1675] Yemen, Rep.              Yemen, Rep.             
    ## [1677] Yemen, Rep.              Yemen, Rep.             
    ## [1679] Yemen, Rep.              Yemen, Rep.             
    ## [1681] Zambia                   Zambia                  
    ## [1683] Zambia                   Zambia                  
    ## [1685] Zambia                   Zambia                  
    ## [1687] Zambia                   Zambia                  
    ## [1689] Zambia                   Zambia                  
    ## [1691] Zambia                   Zambia                  
    ## [1693] Zimbabwe                 Zimbabwe                
    ## [1695] Zimbabwe                 Zimbabwe                
    ## [1697] Zimbabwe                 Zimbabwe                
    ## [1699] Zimbabwe                 Zimbabwe                
    ## [1701] Zimbabwe                 Zimbabwe                
    ## [1703] Zimbabwe                 Zimbabwe                
    ## 142 Levels: Afghanistan Albania Algeria Angola Argentina ... Zimbabwe

``` r
gapminder[1:4] #extract cols
```

    ## # A tibble: 1,704 x 4
    ##    country     continent  year lifeExp
    ##    <fct>       <fct>     <int>   <dbl>
    ##  1 Afghanistan Asia       1952    28.8
    ##  2 Afghanistan Asia       1957    30.3
    ##  3 Afghanistan Asia       1962    32.0
    ##  4 Afghanistan Asia       1967    34.0
    ##  5 Afghanistan Asia       1972    36.1
    ##  6 Afghanistan Asia       1977    38.4
    ##  7 Afghanistan Asia       1982    39.9
    ##  8 Afghanistan Asia       1987    40.8
    ##  9 Afghanistan Asia       1992    41.7
    ## 10 Afghanistan Asia       1997    41.8
    ## # ... with 1,694 more rows

``` r
gapminder[1:4,]#extract rows
```

    ## # A tibble: 4 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
