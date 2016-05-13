World Food Facts (Germany)
==========================

This project is part of [Udacity's Nanodegree Data Analyst](https://www.udacity.com/course/data-analyst-nanodegree--nd002). In this project I am carrying out a exploratory data analysis. The project is descriptive and includes univariate, bivariate, and multivariate analyses. I chose a dataset about food products from Germany: The World Food Facts.

The [World Food Facts](http://world.openfoodfacts.org/data) dataset is a french initiative. It collects food products from around the world. The dataset is provided by **Open Food Facts** under an [Open Database License](http://opendatacommons.org/licenses/odbl/1.0/) and can be analyzed via [Kaggle](https://www.kaggle.com/openfoodfacts/world-food-facts). Customers and food manufacturers can freely contribute to the dataset.

In this Exploratory Data Analysis I will try to get some insights into the food products of **Germany**. Being from Germany I am interested in the nutritional value of the products I can find in German supermarkets.

Data Cleaning
=============

There are in total 59999 food products in the dataset. Each food product has 159 variables. Not every variable will be of interest for this analysis. I will focus my analysis on **products from Germany**. When I filter the dataset for German products the entire dataset is reduced 2554 products. In order to select variables that contain meaningful information I checked the dataset for NAs. Variables with a lot of **NAs** should not be included in the analysis. For this analysis I will remove features with more than 40% of NAs.

    ##                                      variable perc_na
    ## 1                     nutrition_score_fr_100g   0.337
    ## 2                     nutrition_score_uk_100g   0.337
    ## 3                                   salt_100g   0.324
    ## 4                                 sodium_100g   0.324
    ## 5                          saturated_fat_100g   0.322
    ## 6                                 sugars_100g   0.316
    ## 7                               proteins_100g   0.301
    ## 8                                    fat_100g   0.295
    ## 9                          carbohydrates_100g   0.294
    ## 10                                energy_100g   0.287
    ## 11                                additives_n   0.192
    ## 12                ingredients_from_palm_oil_n   0.192
    ## 13    ingredients_that_may_be_from_palm_oil_n   0.192
    ## 14                                       code   0.000
    ## 15                                        url   0.000
    ## 16                                    creator   0.000
    ## 17                           created_datetime   0.000
    ## 18                     last_modified_datetime   0.000
    ## 19                               product_name   0.000
    ## 20                               generic_name   0.000
    ## 21                                   quantity   0.000
    ## 22                                  packaging   0.000
    ## 23                             packaging_tags   0.000
    ## 24                                     brands   0.000
    ## 25                                brands_tags   0.000
    ## 26                                 categories   0.000
    ## 27                            categories_tags   0.000
    ## 28                              categories_en   0.000
    ## 29                                    origins   0.000
    ## 30                               origins_tags   0.000
    ## 31                       manufacturing_places   0.000
    ## 32                  manufacturing_places_tags   0.000
    ## 33                                     labels   0.000
    ## 34                                labels_tags   0.000
    ## 35                                  labels_en   0.000
    ## 36                                  emb_codes   0.000
    ## 37                             emb_codes_tags   0.000
    ## 38                   first_packaging_code_geo   0.000
    ## 39                                cities_tags   0.000
    ## 40                            purchase_places   0.000
    ## 41                                     stores   0.000
    ## 42                                  countries   0.000
    ## 43                             countries_tags   0.000
    ## 44                               countries_en   0.000
    ## 45                           ingredients_text   0.000
    ## 46                                  allergens   0.000
    ## 47                                     traces   0.000
    ## 48                                traces_tags   0.000
    ## 49                                  traces_en   0.000
    ## 50                               serving_size   0.000
    ## 51                                  additives   0.000
    ## 52                             additives_tags   0.000
    ## 53                               additives_en   0.000
    ## 54             ingredients_from_palm_oil_tags   0.000
    ## 55 ingredients_that_may_be_from_palm_oil_tags   0.000
    ## 56                         nutrition_grade_fr   0.000
    ## 57                              pnns_groups_1   0.000
    ## 58                              pnns_groups_2   0.000
    ## 59                                     states   0.000
    ## 60                                states_tags   0.000
    ## 61                                  states_en   0.000
    ## 62                              main_category   0.000
    ## 63                           main_category_en   0.000
    ## 64                                  image_url   0.000
    ## 65                            image_small_url   0.000

Most features do contain a lot of missing values. Out of 159 features, 65 features meet the NA criteria (less than 40%). Not all of these features are of interest for this analysis. I will therefore select only relevant features.

    ## Observations: 2,554
    ## Variables: 21
    ## $ product_name            (fctr) Sour Fruit Gummies, Jelly Fish, Tabas...
    ## $ generic_name            (fctr) , , , , , Senf, Vitamin D3, , , , , ,...
    ## $ brands                  (fctr) Candy Crush, Candy Crush, Tabasco, , ...
    ## $ brands_tags             (fctr) candy-crush, candy-crush, tabasco, , ...
    ## $ categories_en           (fctr) Sugary snacks,Confectioneries,Candies...
    ## $ origins                 (fctr) , , , , , , , , Costa Rica, , , , , ,...
    ## $ pnns_groups_1           (fctr) Sugary snacks, Sugary snacks, unknown...
    ## $ pnns_groups_2           (fctr) Sweets, Sweets, unknown, , Fruits, Dr...
    ## $ manufacturing_places    (fctr) , , , , , , , , , , , , , , Italien, ...
    ## $ additives_en            (fctr) E428 - Gelatin,E330 - Citric acid,E33...
    ## $ nutrition_grade_fr      (fctr) d, c, , , , , , , , , , , , c, a, , b...
    ## $ main_category_en        (fctr) Sugary snacks, Sugary snacks, , , Pla...
    ## $ energy_100g             (dbl) 1360, 586, NA, NA, NA, NA, NA, NA, 61,...
    ## $ fat_100g                (dbl) 0.0, 0.0, NA, NA, NA, NA, NA, NA, 0.0,...
    ## $ saturated_fat_100g      (dbl) 0.0, 0.0, NA, NA, NA, NA, NA, NA, NA, ...
    ## $ carbohydrates_100g      (dbl) 75.0, 34.0, NA, NA, NA, NA, NA, NA, 1....
    ## $ sugars_100g             (dbl) 57.5, 24.0, NA, NA, NA, NA, NA, NA, NA...
    ## $ proteins_100g           (dbl) 5.0, 0.0, NA, NA, NA, NA, NA, NA, 3.0,...
    ## $ salt_100g               (dbl) 0.1270, 0.0762, NA, NA, NA, NA, NA, NA...
    ## $ nutrition_score_fr_100g (dbl) 14, 6, NA, NA, NA, NA, NA, NA, NA, NA,...
    ## $ nutrition_score_uk_100g (dbl) 14, 6, NA, NA, NA, NA, NA, NA, NA, NA,...

We managed to drill down the database to 21 variables. These features now contain less than 40% of NAs and can be used for further analysis.

Univariate Plots Section
========================

Macronutritions
---------------

I will begin to explore the **macronutritions**: That is, **fat**, **proteins**, and **carbohydrates**.

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20fat-1.png)<!-- -->

Most products do not contain a lot of **fat**. The distribution is **skewed left**.

For the purpose of a healthy diet is is crucial to investigate **saturated fat** as it has been linked to *cardiovascular diseases*.

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20saturated%20fat-1.png)<!-- -->

Most products do not contain a lot of **saturated fat**. The distribution is sort of bimodal. There is tiny peak of products that contain around 50g of saturated fat per 100g.

    ##  [1] Deutsche Markenbutter milfina      
    ##  [2] Deutsche Markenbutter mild gesäuert
    ##  [3] Butter streichzart                 
    ##  [4] Deutsche Markenbutter              
    ##  [5] Süßrahmbutter                      
    ##  [6] Sauerrahm Butter                   
    ##  [7] Allgäuer Bauernbutter              
    ##  [8] Alpenbutter                        
    ##  [9] Butter aus frischem Rahm           
    ## [10] Deutsche Markenbutter mildgesäuert 
    ## [11] Deutsche Markenbutter              
    ## [12] Butter                             
    ## [13] Bio Almbutter                      
    ## [14] Deutsche Markenbutter              
    ## [15] Butter Süssrahm                    
    ## [16] Sauerrahm-Butter                   
    ## [17] Kokosraspeln, grob geraspelt       
    ## [18] Deutsche Markenbutter              
    ## [19] Deutsche Markenbutter              
    ## [20] Butter mit Atlantik-Meersalz       
    ## [21] Deutsche Markenbutter mildgesäuert 
    ## [22] Süßrahmbutter                      
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

These are **butter** products. In terms of a healthy diet one shouldn't eat too much butter.

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20proteins-1.png)<!-- -->

The distribution of **protein** is **skewed to the left**. There are few products with a lot of protein. These are **food supplements** for weight loss or muscle training.

    ##  [1] Blattgelatine weiss                                     
    ##  [2] Body Shape Protein Shake 90 Plus L-Carnitine            
    ##  [3] Protein 90 Shake Plus L-Carnitine                       
    ##  [4] 3K Protein Shake Stracciatella                          
    ##  [5] 85+ Protein Erdebeere                                   
    ##  [6] 3K Protein Vanille                                      
    ##  [7] Soja Protein Schokolade                                 
    ##  [8] Impact Whey Unflavourrd                                 
    ##  [9] Milk Protein Smooth                                     
    ## [10] Impact Whey Protein Apple Crumble & Custard Flavour     
    ## [11] Impact Whey Protein White Chocolate                     
    ## [12] Impact Whey Protein Raspberry Stevia Flavour            
    ## [13] Impact Whey Protein Blueberry & Raspberry Stevia Flavour
    ## [14] 100% Whey Gold Standard Double Rich Chocolate Flavour   
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20carbohydrates-1.png)<!-- -->

The distribution of **carbohydrates** is also **skewed left**. Most products do not contain a lot of carbohydrates. The distribution is slightly **bimodal**.

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20sugar-1.png)<!-- -->

The distribution of sugar is sort of similar. It is also **skewed left** and **bimodal**.

Nutritional Value
-----------------

### Nutritional score

The database has two features with information about the product's nutritional value. There is a score from France (**nutrition\_score\_fr\_100g**) and a score from the UK (**nutrition\_score\_uk\_100g**). Let us see how they differ.

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20nutritional%20scores-1.png)<!-- -->![](world_food_facts_eda_files/figure-markdown_github/Histogram%20nutritional%20scores-2.png)<!-- -->

Obviously the variables are not drastically different from another. The British system seems to be more conservative (overall the products are rated less healthy). For further analysis I will stick to the **French** system.

From a first glimpse at the nutritional value, the distribution looks a little bit **bimodal**. There is a high peak at around a score of 0. These might be water products that are neither nutritional valuable nor non-valuable. Another peak seems to be around a score of 15.

Nutritional grade
-----------------

Apart from the nutritional score there is a feature about the nutrional grade of the products (**nutrition\_grade\_fr**). The grade system is very similar to the grade system in schools. **a** is supposed to be a healthy product, whereas **e** is an unhealthy product.

![](world_food_facts_eda_files/figure-markdown_github/Nutritional%20grade%20of%20products-1.png)<!-- -->

Many products do not have a grade. The graded products have a sort of uniform distribution.

Other variables
---------------

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20of%20kcal-1.png)<!-- -->

Energy in food is most often measured in **kilojoule**. Customers are usually more accustomed to **kilocalories**. Therefore I created a new variable **kcal\_100g** that used the usual [conversion](http://www.rapidtables.com/convert/energy/kj-to-kcal.htm).

The distribution has three peaks and is skewed left. The mean is 246.24. Some products are very high in kcals. Let us see which:

    ##  [1] Coconpure                                      
    ##  [2] Vita D'or                                      
    ##  [3] Macadamia geröstet & gesalzen                  
    ##  [4] Pecannusskerne naturbelassen                   
    ##  [5] Natives Olivenöl Extra                         
    ##  [6] Deutsche Markenbutter milfina                  
    ##  [7] Deutsche Markenbutter mild gesäuert            
    ##  [8] Olivenöl nativ extra                           
    ##  [9] Macadamia                                      
    ## [10] Olivenöl fruchtig                              
    ## [11] Sesamöl nativ                                  
    ## [12] Palmin soft                                    
    ## [13] Butaris                                        
    ## [14] Macadamias                                     
    ## [15] Hubertus Schmalz aus Gänse- und Schweineschmalz
    ## [16] Butter streichzart                             
    ## [17] Pflanzen Margarine                             
    ## [18] Deutsche Markenbutter                          
    ## [19] Süßrahmbutter                                  
    ## [20] Sauerrahm Butter                               
    ## [21] Allgäuer Bauernbutter                          
    ## [22] Alpenbutter                                    
    ## [23] Butter aus frischem Rahm                       
    ## [24] Deutsche Markenbutter mildgesäuert             
    ## [25] Deutsche Markenbutter                          
    ## [26] Butter                                         
    ## [27] Bio Almbutter                                  
    ## [28] Zwiebel-Schmalz                                
    ## [29] Jordan Olivenöl                                
    ## [30] Sesamöl                                        
    ## [31] Deutsche Markenbutter                          
    ## [32] Bio-Kokosspeisefett                            
    ## [33] Bio Kokosöl                                    
    ## [34] Butter Süssrahm                                
    ## [35] Sauerrahm-Butter                               
    ## [36] Chilenische Walnuss Kerne                      
    ## [37] Deutsche Markenbutter                          
    ## [38] Sonnenblumen Margarine                         
    ## [39] Natives Olivenöl Extra                         
    ## [40] Deutsche Markenbutter                          
    ## [41] Butter mit Atlantik-Meersalz                   
    ## [42] Pflanzen-Margarine                             
    ## [43] Reines Sonnenblumenöl                          
    ## [44] Deutsche Markenbutter mildgesäuert             
    ## [45] Süßrahmbutter                                  
    ## [46] Kalamata g.U. Olivenöl                         
    ## [47] Bio Baby-Beikost-Öl                            
    ## [48] Extra Vergine                                  
    ## [49] GranFruttato                                   
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

Looking at the list above olive oil, sunflower oil and butter are very high in kcals. These products are on the right hand side in the histogram above.

![](world_food_facts_eda_files/figure-markdown_github/Histogram%20salt-1.png)<!-- -->

There is not much **salt** in most products. Just very few have a lot of salt. I reckon these are salt products :)

It would be also interesting to find out which brands produce most products?

![](world_food_facts_eda_files/figure-markdown_github/Barchart%20common%20brands-1.png)<!-- -->

Most products sold in Germany are made by **Gut & Günstig**. **Alnatura** comes in second place.

![](world_food_facts_eda_files/figure-markdown_github/Most%20common%20groups-1.png)<!-- -->

Most products are **dairy products**. **Beverages** and **sugary snacks** come in second place. Almost half of the products do not a group assigned.

Univariate Analysis
===================

### What is the structure of your dataset?

There are 2554 products with 22 features in the dataset. The dataset contains factors and numerics.

    ##                         vars    n     mean       sd   median  trimmed
    ## product_name*              1 2554 29577.08 15254.02 36122.50 31152.86
    ## generic_name*              2 2554  9754.62  9016.39  7100.50  9489.17
    ## brands*                    3 2554  7860.68  5398.59  9794.00  7966.00
    ## brands_tags*               4 2554  6191.53  4357.25  7684.00  6226.96
    ## categories_en*             5 2554  4028.82  4053.26  2709.50  3568.25
    ## origins*                   6 2554   294.79   805.38     1.00    42.26
    ## pnns_groups_1*             7 2554      NaN       NA       NA      NaN
    ## pnns_groups_2*             8 2554      NaN       NA       NA      NaN
    ## manufacturing_places*      9 2554   343.98   859.26     1.00    87.12
    ## additives_en*             10 2554   964.64  2264.16     1.00   287.66
    ## nutrition_grade_fr*       11 2554     2.93     1.76     3.00     2.80
    ## main_category_en*         12 2554   482.60   499.15   168.00   409.28
    ## energy_100g               13 1820  1030.26   821.38   891.00   944.96
    ## fat_100g                  14 1801    13.57    18.85     4.00     9.76
    ## saturated_fat_100g        15 1731     6.23     9.64     2.10     4.39
    ## carbohydrates_100g        16 1802    22.57    26.28    10.10    18.52
    ## sugars_100g               17 1748    11.57    18.33     4.20     7.07
    ## proteins_100g             18 1784     8.74    10.71     5.60     6.88
    ## salt_100g                 19 1727     1.12     6.67     0.15     0.42
    ## nutrition_score_fr_100g   20 1694     7.31     9.09     5.00     6.70
    ## nutrition_score_uk_100g   21 1694     7.62     9.70     4.00     7.04
    ## kcal_100g                 22 1820   246.24   196.31   212.95   225.85
    ##                              mad min      max    range  skew kurtosis
    ## product_name*            9069.06   1 46654.00 46653.00 -0.84    -0.87
    ## generic_name*           10525.72   1 22349.00 22348.00  0.05    -1.83
    ## brands*                  6720.63   1 15414.00 15413.00 -0.23    -1.57
    ## brands_tags*             5848.12   1 12562.00 12561.00 -0.14    -1.57
    ## categories_en*           3255.05   1 13172.00 13171.00  0.90    -0.60
    ## origins*                    0.00   1  3415.00  3414.00  2.77     6.01
    ## pnns_groups_1*                NA Inf     -Inf     -Inf    NA       NA
    ## pnns_groups_2*                NA Inf     -Inf     -Inf    NA       NA
    ## manufacturing_places*       0.00   1  3824.00  3823.00  2.81     6.61
    ## additives_en*               0.00   1  8943.00  8942.00  2.50     4.91
    ## nutrition_grade_fr*         2.97   1     6.00     5.00  0.33    -1.31
    ## main_category_en*         247.59   1  2371.00  2370.00  0.98     0.27
    ## energy_100g               924.40   0  3760.00  3760.00  0.73    -0.25
    ## fat_100g                    5.78   0   100.00   100.00  2.06     4.72
    ## saturated_fat_100g          2.97   0    93.00    93.00  3.03    14.37
    ## carbohydrates_100g         12.90   0   103.50   103.50  1.13    -0.06
    ## sugars_100g                 5.49   0   103.50   103.50  2.43     5.92
    ## proteins_100g               7.12   0    86.00    86.00  3.15    15.68
    ## salt_100g                   0.21   0    99.93    99.93 13.69   194.58
    ## nutrition_score_fr_100g     9.64 -12    29.00    41.00  0.49    -0.76
    ## nutrition_score_uk_100g    10.38 -12    29.00    41.00  0.47    -1.06
    ## kcal_100g                 220.94   0   898.66   898.66  0.73    -0.25
    ##                             se
    ## product_name*           301.84
    ## generic_name*           178.41
    ## brands*                 106.82
    ## brands_tags*             86.22
    ## categories_en*           80.20
    ## origins*                 15.94
    ## pnns_groups_1*              NA
    ## pnns_groups_2*              NA
    ## manufacturing_places*    17.00
    ## additives_en*            44.80
    ## nutrition_grade_fr*       0.03
    ## main_category_en*         9.88
    ## energy_100g              19.25
    ## fat_100g                  0.44
    ## saturated_fat_100g        0.23
    ## carbohydrates_100g        0.62
    ## sugars_100g               0.44
    ## proteins_100g             0.25
    ## salt_100g                 0.16
    ## nutrition_score_fr_100g   0.22
    ## nutrition_score_uk_100g   0.24
    ## kcal_100g                 4.60

    ## Observations: 2,554
    ## Variables: 22
    ## $ product_name            (fctr) Sour Fruit Gummies, Jelly Fish, Tabas...
    ## $ generic_name            (fctr) , , , , , Senf, Vitamin D3, , , , , ,...
    ## $ brands                  (fctr) Candy Crush, Candy Crush, Tabasco, , ...
    ## $ brands_tags             (fctr) candy-crush, candy-crush, tabasco, , ...
    ## $ categories_en           (fctr) Sugary snacks,Confectioneries,Candies...
    ## $ origins                 (fctr) , , , , , , , , Costa Rica, , , , , ,...
    ## $ pnns_groups_1           (chr) "sugary snacks", "sugary snacks", "unk...
    ## $ pnns_groups_2           (chr) "sweets", "sweets", "unknown", "", "fr...
    ## $ manufacturing_places    (fctr) , , , , , , , , , , , , , , Italien, ...
    ## $ additives_en            (fctr) E428 - Gelatin,E330 - Citric acid,E33...
    ## $ nutrition_grade_fr      (fctr) d, c, , , , , , , , , , , , c, a, , b...
    ## $ main_category_en        (fctr) Sugary snacks, Sugary snacks, , , Pla...
    ## $ energy_100g             (dbl) 1360, 586, NA, NA, NA, NA, NA, NA, 61,...
    ## $ fat_100g                (dbl) 0.0, 0.0, NA, NA, NA, NA, NA, NA, 0.0,...
    ## $ saturated_fat_100g      (dbl) 0.0, 0.0, NA, NA, NA, NA, NA, NA, NA, ...
    ## $ carbohydrates_100g      (dbl) 75.0, 34.0, NA, NA, NA, NA, NA, NA, 1....
    ## $ sugars_100g             (dbl) 57.5, 24.0, NA, NA, NA, NA, NA, NA, NA...
    ## $ proteins_100g           (dbl) 5.0, 0.0, NA, NA, NA, NA, NA, NA, 3.0,...
    ## $ salt_100g               (dbl) 0.1270, 0.0762, NA, NA, NA, NA, NA, NA...
    ## $ nutrition_score_fr_100g (dbl) 14, 6, NA, NA, NA, NA, NA, NA, NA, NA,...
    ## $ nutrition_score_uk_100g (dbl) 14, 6, NA, NA, NA, NA, NA, NA, NA, NA,...
    ## $ kcal_100g               (dbl) 325.04816, 140.05752, NA, NA, NA, NA, ...

### What is/are the main feature(s) of interest in your dataset?

The main features of the dataset are features that contain information that is relevant for a healthy diet. These are all **macronutritions**, **nutritional\_score\_fr\_100g**, **nutritional\_grade\_fr** and **kcal\_100g**.

### What other features in the dataset do you think will help support your investigation into your feature(s) of interest?

For further investigation I will look into the **pnns\_groups\_1**, **pnns\_groups\_2**, and **brands** features. It will be interesting to find out if some types of products are better of worse for a healthy diet. It might also be interesting to check whether some brands are healthier than others.

### Did you create any new variables from existing variables in the dataset?

I created a new variable **kcal\_100g**. I am more accustomed to kcal than kilojoule as an indicator of energy. In order to find the most common **brands** I created the dataframe **common\_brands\_df**.

### Of the features you investigated, were there any unusual distributions? Did you perform any operations on the data to tidy, adjust, or change the form of the data? If so, why did you do this?

The **pnns\_groups\_1** variable had to be tidied. In order to avoid duplicates, I set all entries to lowercase and replaced a dash with a blank space. I also capitalized the first letter of the feature. I filtered the whole data set for german entries. Being from Germany these are the products that interest me.

### Conclusion

Most distributions of **macronutritions** are skewed left. This is not an unusual pattern though as they add up to about 100g. What striked me was that there is group of products that are very high in protein. These are bodybuilding products. No other products contain so much protein per 100g. What also struck me was the high amount of saturated fat in butter. Butter seems to be especially unhealthy as it also contains a lot of kcals. Olive and sunflower oil are also very high in kcals.

<!----------------------------- Bivarate Analysis ------------------------------------------------- -->
Bivariate Plots Section
=======================

![](world_food_facts_eda_files/figure-markdown_github/Scatterplot%20matrix-1.png)<!-- -->

    ##                         energy_100g fat_100g saturated_fat_100g
    ## energy_100g                    1.00     0.81               0.64
    ## fat_100g                       0.81     1.00               0.82
    ## saturated_fat_100g             0.64     0.82               1.00
    ## carbohydrates_100g             0.43    -0.10              -0.11
    ## sugars_100g                    0.33     0.03               0.05
    ## proteins_100g                  0.30     0.15               0.09
    ## salt_100g                     -0.07    -0.03              -0.03
    ## nutrition_score_fr_100g        0.63     0.63               0.64
    ## nutrition_score_uk_100g        0.65     0.68               0.68
    ## kcal_100g                      1.00     0.81               0.64
    ##                         carbohydrates_100g sugars_100g proteins_100g
    ## energy_100g                           0.43        0.33          0.30
    ## fat_100g                             -0.10        0.03          0.15
    ## saturated_fat_100g                   -0.11        0.05          0.09
    ## carbohydrates_100g                    1.00        0.63         -0.10
    ## sugars_100g                           0.63        1.00         -0.21
    ## proteins_100g                        -0.10       -0.21          1.00
    ## salt_100g                            -0.07       -0.07         -0.01
    ## nutrition_score_fr_100g               0.14        0.47          0.09
    ## nutrition_score_uk_100g               0.10        0.41          0.15
    ## kcal_100g                             0.43        0.33          0.30
    ##                         salt_100g nutrition_score_fr_100g
    ## energy_100g                 -0.07                    0.63
    ## fat_100g                    -0.03                    0.63
    ## saturated_fat_100g          -0.03                    0.64
    ## carbohydrates_100g          -0.07                    0.14
    ## sugars_100g                 -0.07                    0.47
    ## proteins_100g               -0.01                    0.09
    ## salt_100g                    1.00                    0.08
    ## nutrition_score_fr_100g      0.08                    1.00
    ## nutrition_score_uk_100g      0.08                    0.97
    ## kcal_100g                   -0.07                    0.63
    ##                         nutrition_score_uk_100g kcal_100g
    ## energy_100g                                0.65      1.00
    ## fat_100g                                   0.68      0.81
    ## saturated_fat_100g                         0.68      0.64
    ## carbohydrates_100g                         0.10      0.43
    ## sugars_100g                                0.41      0.33
    ## proteins_100g                              0.15      0.30
    ## salt_100g                                  0.08     -0.07
    ## nutrition_score_fr_100g                    0.97      0.63
    ## nutrition_score_uk_100g                    1.00      0.65
    ## kcal_100g                                  0.65      1.00

**Energie** and **fat** are highly correlated (r = .81). This makes sense as one gram of fat contains 9 kcal and therefore more energy than carbohydrates and protein. **Sugar\* and **saturated fat\*\* is not correlated (r = .04). This indicates that there are no sugary products that contain a lot of saturated fat.

Looking at the scatterplots there is an interesting pattern. Some products seem to contain a lot of protein and a tiny amount of carbohydrates and fat.

![](world_food_facts_eda_files/figure-markdown_github/Scatterplot%20fat%20and%20protein-1.png)<!-- -->

Two interesting patterns emerge: (1) **Bodybuilding products** are high in protein but very low in fat. (2) Olive oils are on the other extreme. They are very high in fat but low in protein.

    ##  [1] Blattgelatine weiss                                     
    ##  [2] Body Shape Protein Shake 90 Plus L-Carnitine            
    ##  [3] Protein 90 Shake Plus L-Carnitine                       
    ##  [4] 3K Protein Shake Stracciatella                          
    ##  [5] 85+ Protein Erdebeere                                   
    ##  [6] 3K Protein Vanille                                      
    ##  [7] Soja Protein Schokolade                                 
    ##  [8] Impact Whey Unflavourrd                                 
    ##  [9] Milk Protein Smooth                                     
    ## [10] Impact Whey Protein Apple Crumble & Custard Flavour     
    ## [11] Impact Whey Protein White Chocolate                     
    ## [12] Impact Whey Protein Raspberry Stevia Flavour            
    ## [13] Impact Whey Protein Blueberry & Raspberry Stevia Flavour
    ## [14] 100% Whey Gold Standard Double Rich Chocolate Flavour   
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

    ##  [1] Coconpure              Natives Olivenöl Extra Olivenöl nativ extra  
    ##  [4] Sesamöl nativ          Butaris                Jordan Olivenöl       
    ##  [7] Sesamöl                Bio-Kokosspeisefett    Bio Kokosöl           
    ## [10] Natives Olivenöl Extra Reines Sonnenblumenöl  Kalamata g.U. Olivenöl
    ## [13] Extra Vergine          GranFruttato          
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

Let us have a look at the other macronutritions **fat** and **carbohydrates**.

![](world_food_facts_eda_files/figure-markdown_github/Scatterplot%20fat%20and%20carbohydrates-1.png)<!-- -->

There are no special food groups in this scatterplot. What is interesting is the **hole** inside the scatterplot. Very few products contain around 25% of both protein and fat.

What about **carbohydrates** and **protein**?

![](world_food_facts_eda_files/figure-markdown_github/Scatterplot%20carbohydrates%20and%20protein-1.png)<!-- -->

Again we can find the same pattern. The **bodybuilding products** are very high in protein but low in carbohydrates. Apart from that there is nothing particularly special about the dataset. ![](world_food_facts_eda_files/figure-markdown_github/Scatterplot%20nutrional%20value%20and%20fat-1.png)<!-- -->

**Saturated fact** is often associates with an unhealthy diet. **Coconut oil** and **coconut fat** are both high in saturated fat and nutritional score.

    ## [1] Bio-Kokosspeisefett Bio Kokosöl        
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

What about **saturated fat** and **fat**?

![](world_food_facts_eda_files/figure-markdown_github/Scatterplot%20saturated%20fat%20and%20fat-1.png)<!-- -->

Most products contain few fat and and saturated fat. Two products seem to contain a high amount of saturated fat.

    ## [1] Bio-Kokosspeisefett Bio Kokosöl        
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

Again, this is our **coconut oil** and **coconut fat**.

Bivariate Analysis
==================

### Talk about some of the relationships you observed in this part of the investigation. How did the feature(s) of interest vary with other features in the dataset?

Nutritional data all fall within a diagonal of a scatterplot. As the macronutritions features all add up to maximal 100g the features can not add up above 100g. Linear relationsships do not occur. (1) Almost all relationships are positive. Most of these relationships are small. When I plotted fat and carbohydrates with protein some products cluster around a high protein level with a low level of the other two macronutritions. These are **bodybuilding products** as muscles need protein to grow. It is obvious that these products are distinct from other products. They are especially designed to contain a lot of protein but not much fat or carbohydrates. (2) **Products high in saturated fat** usually have a low nutrition score. This is in line with the usually recommendation to avoid saturated fats. (3) Most products that contain **fat** do not contain a high amount of **saturated fat**. Coconut oil is one exception. It even as a high nutrition score as is evident in the scatterplot of saturated fat and nutrition score.

### Did you observe any interesting relationships between the other features (not the main feature(s) of interest)?

No.

### What was the strongest relationship you found?

One of the strongest relationship was between **fat** and **saturated fat** (r = . 81). The nutritional score features correlate strongly with another (r = .97).

<!----------------------------- Multivariate Analysis ------------------------------------------------- -->
Multivariate Plots Section
==========================

![](world_food_facts_eda_files/figure-markdown_github/Density%20plot%20carbohydrates%20food%20category-1.png)<!-- -->

The food types show distinctly different distributions. **Beverages** only contain about 15 gram of **carbohydrates**. Sugary snacks are heavy in carbohydrates. **Milk and dairy products** are very low in carbohydrates.

![](world_food_facts_eda_files/figure-markdown_github/Carbohydrates,%20brands,%20fat,%20and%20proteins-1.png)<!-- -->

Fatty products are not very high in carbohydrates. No brands differs considerably in products in carbohydrates, fat, or proteins. Sugar is a very crucial carbohydrate in terms of health. Let us have a look.

![](world_food_facts_eda_files/figure-markdown_github/Density%20plot%20sugars%20food%20category-1.png)<!-- -->

The distribution for sugar is sort of similar. Some **beverages** contain a lot of sugar (~80 gram). **Sugary snacks** also contain a lot of sugar.

![](world_food_facts_eda_files/figure-markdown_github/Density%20plot%20proteins%20food%20category-1.png)<!-- -->

**Milk and dairy products** contain most protein. **Fruits and vegetables** are usually low in protein and also contain a specific amount.

![](world_food_facts_eda_files/figure-markdown_github/Density%20plot%20proteins%20nutrition_grade_fr-1.png)<!-- -->

Plotting the distribution of **graded products** on **proteins** no specific pattern emerges. The amount of **protein** does not determine wheater a product is considered healthy or not healthy. Indeed healthy products (with an **a**) often do not contain a lot of protein (yellow distribution). The same goes for unhealthy products (with an **e**).

![](world_food_facts_eda_files/figure-markdown_github/Kilocalories%20of%20different%20food%20groups-1.png)<!-- -->

**Fat and sauces** are very heavy in kcals. **Fish, meat, and eggs** usually do not contain a lot kcals.

![](world_food_facts_eda_files/figure-markdown_github/Nutritional%20score%20of%20most%20common%20brands-1.png)<!-- -->

Milkbona seems to be the most healthy brand. This is a *biased* representation because Milkbona sells milk products that usually are considered more healthy. Except for **Edeka** every brand has a bimodal distribution. Many products can be considered healthy whereas the other half can be considered unhealthy.

![](world_food_facts_eda_files/figure-markdown_github/Nutritional%20score%20in%20relation%20to%20sugar%20and%20fat-1.png)<!-- -->

Obviously products low in sugar and fat are considered more healthy. This does not come as a surprise.

![](world_food_facts_eda_files/figure-markdown_github/Nutritional%20Score%20of%20beverages-1.png)<!-- -->

It turned out that **alcohol products** do not contain data about the nutritional score. Non-alcoholic beverages show a bimodal distribution. Most drinks are low in nutritional score. Some products are considered unhealthy. Most of these products are lemonades:

    ##  [1] Premium Cola                  Schwarzer Johannisbeer-Nektar
    ##  [3] Kokosnussmilch                Bio-Kokusnussmilch           
    ##  [5] Radler Zitrone Alkoholfrei    Radler Zitrone Alkoholfrei   
    ##  [7] Zitronen Limonade             Ensinger Zitrone             
    ##  [9] Bio Kokosnussmilch            Bissinger Auerquelle Cola-Mix
    ## [11] Kokosmilch                    Ayran                        
    ## [13] Dr. Pepper Cherry             Black Tiger strong           
    ## [15] Cola American Taste           Energy Drink                 
    ## [17] Zitronen Teegetränk           Kokosnussmilch               
    ## [19] Coconut Milk                  Coca-Cola                    
    ## [21] Sprite                        Coca-Cola                    
    ## [23] Fanta Orange                  Fanta Mango Geschmack        
    ## [25] Sprite                        Coca-Cola                    
    ## [27] Coca-Cola                     Sprite                       
    ## [29] Double Choc Typ Cappucino    
    ## 46765 Levels:    알 통깨 짜왕 너구리 うどん 안성탕면 다진마늘 ... 黑瓶眼药水

![](world_food_facts_eda_files/figure-markdown_github/Nutrional%20score%20of%20product%20types-1.png)<!-- -->

**Sugary** snacks obviously are not very healthy. Appart from sugary snacks there is no product type that is of bad nutritional value per se. **Cereals and potatoes** seem to be beneficial for health. The same goes for **Fruits and vegetables**. **Milk and dairy products** have a bimodal distribution. This indicates that half of these products are not very healthy. **Beverages** by and large seem to be reasonably good. The peak of the distribution might be because of **water products**.

![](world_food_facts_eda_files/figure-markdown_github/Boxplots%20of%20food%20types-1.png)<!-- -->

This plot shows the relationship between the **nutritional grade** and **score variable** on different **product types**. Out of the food types that get a grade **a**, fruits and vegetables are the most healthy. Very few **fats and sauces**, **sugary snacks**, and **beverages** are deemed very healthy.

Multivariate Analysis
=====================

### Talk about some of the relationships you observed in this part of the investigation. Were there features that strengthened each other in terms of looking at your feature(s) of interest?

The data strengthened the common fact that **sugary snacks** and **salty snacks** are considered unhealthy. They not only contain a lot of **kcals**, they are also very high in **carbohydrates** (especially sugar). Many **non-alcoholic beverages** show a bad **nutritional score**. These are mainly lemonades.

### Were there any interesting or surprising interactions between features?

What I found interesting is that beverages usually have a specific amount of carbohydrates and sugars. Usually they contain between 5 and 30 grams of carbohydrates. **Sugary snacks** are high in sugar and considered unhealthy. What surprised me is that beverages do not contain a lot of kcals. I suppose it is the amount that matters here. When you aim for a healthy diet one should eat a lot of **cereals and potatoes** and **fruits and vegetables**. From looking at the relationship between the features **nutritional score** and **nutritional grade** they can be considered the most healthy products.

Final Plots and Summary
=======================

### Plot One

![](world_food_facts_eda_files/figure-markdown_github/Final%20Plot%20One-1.png)<!-- -->

### Description One

Some food types are more healthy than others. The boxplot depicts this relationship. Food types are plotted on the x-axis, whereas their nutritional grade are plotted on the y-axis. According to the data **cereals and potatoes** and **fruits and vegetables** are the healthiest type of products. **Sugary snacks** can be considered quite unhealthy. **Fish, meat, and eggs\* show a considerable variation. **Beverages\*\* do vary only slightly with some extreme values.

### Plot Two

![](world_food_facts_eda_files/figure-markdown_github/Final%20Plot_Two-1.png)<!-- -->

### Description Two

There are no brands that are healhy per se. Except for **Edeka** most brands show a bimodal distribution indicating that many products are of good nutritional value with an slightly less amount of products with a lower nutritional value. From a consumer perspective one should buy products from **Edeka**. I have no data about the data's bias. It might be that the data is not a realistic depiction of the actual brands found in the supermarkets.

### Plot Three

![](world_food_facts_eda_files/figure-markdown_github/Final%20Plot%20Three-1.png)<!-- -->

### Description Three

Kilocalories are an important indicator for a healthy diet. Especially people who want to loose weight often try not to exceed a certain limit of kilocalories per day. This distribution is a depiction of the distribution of kilocalories among the most common food types. **Milk and dairy products**, **beverages**, **fish, meat, and eggs** are very low in kilocalories. **Fat and sauces**, **salty snacks**, and **sugary snacks** are very high in kilocalories. This data should not be taken by face value. **Beverages** for example do not contain a lot of kilocalories per 100g but one usually consumes way more gram of beverages than of solid food. Except for water the intake of beverages should be considered according to the total intake of beverages and not per 100g.

------------------------------------------------------------------------

Reflection
==========

Analyzing the data was tricky because of the amount of features to be considered. Many features contained missing values. Therefore I had to drill down the features to a reasonable amount. I included only variables that did not contain more than 40% of missing values. This was an arbitrary choice that I took. As I restricted myself to German products many features could not be analyzed. Particularly micronutritions (e.g. magnesium) could not be considered due to missing values.

After I finished the univarite analysis they main features became clearer. Macronutritions and the nutritional value features were the most interesting features yielding interesting results. I tried to analyze these features by food types. This was challenging because the food types are represented as factors that did not follow a stringent pattern. I had to use regular expressions in order to make sense of this feature. I changed every feature to lowercase and remove the string **unkown**. Many products did not provide a specific food type. My analyis was therefore restricted to a small fraction of the whole dataset. A bigger dataset would have yielded more interesting results.

The bivariate analysis was a little tricky. My main features did not show any real linear relationships. The only features that correlated highly were self-evident (nutritional grade - nutritional score).

When I tried to analyze alcoholic beverages it became clear that there was not enough data for the analysis. I reached a dead end.

What I particularly liked about my analyis is how it supported common wisdom about nutrition. According to the data **fruits and vegetables** are the most healthy products. **Sugary snacks** are the least beneficial products. The most interesting fact was that there is special type of products that behave very differently from the rest: **protein products**. These products are very low in **carbohydrates** and **fat** and contain an unusual high amount of protein. Mostly these products are used for muscle growth. It was intriguing that the exploratory analyis could graphically visualize these products.

As a next step I would like to build some supervised machine learning models that predict the nutritional value of a product by my main features. I could use multiple regression, support-vector machines or tree based models for this analysis. I might not have enough data to make a good model. It would still be interesting to see what prediction accuracy is possible.
