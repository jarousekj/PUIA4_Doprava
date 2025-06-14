# PUIA4_Doprava
## 1. Cíl projektu
Cílem tohoto projektu bylo porovnat výsledky klasifikace předtrénovaných modelů s nepředtrénovanými modely neuronových sítí - pro klasifikaci v dopravě. Konkrétně se jednalo o klasifikaci různých druhů dopravních prostředků z obrázků z veřejně přístupných datasetů z Kaggle.


## 2. Použité datasety
Pro tuto úlohu jsme použili celkem 2 různé datasety z Kaggle. První dataset obsahoval pouze čtyři různé třídy (Bus, Car, Motorcycle, Truck), přičemž každá z nich obsahovala 100 vzorků.  

Data_small: https://www.kaggle.com/datasets/kaggleashwin/vehicle-type-recognition#  

Druhý dataset byl několikrát větší, než první dataset a obsahoval celkem 6 tříd (Bike, Car, Motorcycle, Plane, Ship, Train) a každá třída obsahovala celkem 800 vzorků  

Data_large: https://www.kaggle.com/datasets/mohamedmaher5/vehicle-classification/data  


## 3. Postup řešení
Jako první jsme použili nepředtrénovaný model, se kterým jsme pracovali v průběhu roku na cvičení (využíván pro klasifikaci MNIST), který jsme částečně upravili, zejména jsme přidali převod obrázků do šedého tónu a augmentaci pro rozšíření trénovacího datasetu. Tento model jsme poté trénovali postupně na obou zmíněných datasetech a také třetím datasetu, který vznikl sloučením předchozích dvou. Pro vyhodnocení jsme použili metriku accuracy a vyhodnotili model vždy v závislosti na trénovacích i testovacích datech (viz. tabulka níže).  

| Test/Train   | Data_small | Data_large | Data_merged |
|--------------|:----------:|:----------:|:-----------:|
| **Data_small**  |   65 / 69   |   92 / 87   |    47 / 80    |
| **Data_large**  |   70 / 72   |   80 / 75   |    82 / 80    |
| **Data_merged** |   71 / 70   |   89 / 88   |    74 / 74    |  

Odkaz na kód spustitelný v Collab: https://colab.research.google.com/drive/19TI562B0AJEgCYxvvDSlGcbq44wXqzbT?usp=sharing
<p>&nbsp;</p>

Dále jsme namísto předchozího modelu pro klasifikaci použili předtrénovaný model, konkrétně ResNet50, který jsme pouze dotrénovali na stejných datasetech jako předchozí nepředtrénovaný model. Váhy základního modelu ResNet50 jsme nechali zmražené a přidali navíc pooling a dropout. Pro vyhodnocení jsme opět použili metriku accuracy (abychom měli porovnatelné výsledky) a provedli vyhodnocení taktéž v závislosti na trénovacích i testovacích datech (viz, tabulka níže).  

| Test/Train     | Data_small | Data_large | Data_merged |
|----------------|:----------:|:----------:|:-----------:|
| **Data_small**  |   97 / 94   |   98 / 99   |    84 / 98    |
| **Data_large**  |   76 / 98   |   99 / 98   |    99 / 95    |
| **Data_merged** |   79 / 98   |   99 / 99   |    99 / 98    |  

Odkaz na kód spustitelný v Collab: https://colab.research.google.com/drive/15dcYAy_YbsvIPMV_XHV1awia1XUsrQFf?usp=sharing

<p>&nbsp;</p>  

## 4. Závěr
Z tabulek zmíněných výše je patrné, že použití předtrénovaných modelů pro klasifikaci je daleko přesnější než použití modelů nepředtrénovaných, zejména pak pro naše relativně malé datasety (400 a 4800 vzorků). Z tabulek je také zřejmé, že při trénování na sloučených datech (Data_merged) a testování například na malém datasetu (Data_small) není accuracy po vyhodnocení úplně vyhovující. Pro odhalení příčiny tohoto problému vykreslujeme konfúzní matici (viz. níže), která nám ilustruje, které třídy bývají nejčastěji zaměněny, což může být způsobeno absencí některých tříd v různých datasetech (například Truck (třída v datasetu Data_small) zařazen v datasetu Data_large ve třídě Car (Společná třída pro oba datasety)).  
První matice, kterou vidíme níže popisuje případ, kdy jsme předtrénovaný model dotrénovali na sloučených datech (Data_merged) a testovali na malém datasetu (Data_small), můžeme zde vidět, že často nastává špatná klasifikace třídy Truck do třídy Car, jelikož ve velkém datasetu, který je součástí Data_merged, máme některé obrázky třídy Truck zařazené ve třídě Car, kvůli absenci třídy Truck v Data_large.

<p align="center">
  <img src="Images/confusion_matrix.png" alt="Popis obrázku" width="500"/>
</p>  

Druhá matice, kterou vidíme, níže ukazuje případ, kdy jsme předtrénovaný model dotrénovali na malém datasetu (Data_small) a testovali na velkém datasetu (Data_large). Můžeme zde dobře vidět, že třídu Car nám model rozdělil do tříd Car a Truck, což opět odpovídá absenci třídy Truck ve velkém datasetu. 

<p align="center">
  <img src="Images/confusion_matrix1.png" alt="Popis obrázku" width="500"/>
</p>
