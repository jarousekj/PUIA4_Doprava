# PUIA4_Doprava
## 1. Cíl projektu
Cílem tohoto projektu bylo porovnat výsledky klasifikace předtrénovaných modelů s nepředtrénovanými modely neuronových sítí - pro klasifikaci v dopravě. Konkrétně se jednalo o klasifikaci různých druhů dopravních prostředků z obrázků z veřejně přístupných datasetů z Kaggle.


## 2. Použité datasety
Pro tuto úlohu jsme použili celkem 2 různé datasety z Kaggle. První dataset obsahoval pouze čtyři různé třídy (Bus, Car, Motorcycle, Truck), přičemž každá z nich obsahovala 100 vzorků.  

https://www.kaggle.com/datasets/kaggleashwin/vehicle-type-recognition#  

Druhý dataset byl několikrát větší, než první dataset a obsahoval celkem 6 tříd (Bike, Car, Motorcycle, Plane, Ship, Train) a každá třída obsahovala celkem 800 vzorků  

https://www.kaggle.com/datasets/mohamedmaher5/vehicle-classification/data  


## 3. Postup řešení
Jako první jsme použili nepředtrénovaný model, se kterým jsme pracovali v průběhu roku na cvičení (využíván pro klasifikaci MNIST), který jsme částečně upravili, zejména jsme přidali převod obrázků do šedého tónu a augmentaci pro rozšíření trénovacího datasetu. Tento model jsme poté trénovali postupně na obou zmíněných datasetech a také třetím datasetu, který vznikl sloučením předchozích dvou. Pro vyhodnocení jsme použili metriku accuracy a vyhodnotili model vždy v závislosti na trénovacích i testovacích datech (viz. tabulka níže).  

| Test/Train   | Data_small | Data_large | Data_merged |
|--------------|:----------:|:----------:|:-----------:|
| **Data_small**  |   65 / 69   |   92 / 87   |    47 / 80    |
| **Data_large**  |   70 / 72   |   80 / 75   |    82 / 80    |
| **Data_merged** |   71 / 70   |   89 / 88   |    74 / 74    |  

ksxkoxksciv
