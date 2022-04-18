# NINF - Nutritional Information Framework

This document describes a framework for comunication of nutritional information through a machine readable, human deductable expansional string.

# Examples
The string `ninf://K:185/D:50/P:8.6/F:6.8/Fs:3/C:22.4/Cs:6.6/AA` will result in the following image

![ninf://K:185/D:50/P:8.6/F:6.8/Fs:3/C:22.4/Cs:6.6/AA](test.png "ninf://K:185/D:50/P:8.6/F:6.8/Fs:3/C:22.4/Cs:6.6/AA")

## Rationale
Nutritional tracking has many uses, food labeling laws have been brought up in many countries to help the public understand better what is in the foods they buy. In some scenarios this information can be further extended if consumed by a computer, app or terminal.
1. Nutritional tracking for diet
2. Nutritional tracking for health(diabetes, anemia)
3. Accecebility(low vision)
4. Alergens


## Structure
ninf:// is the protocol that starts the string, every parameter is then folowed in any order(but the most important should come first) in a `key:value` pair

The valid keys can be consulted on the provisional key list but any non conflicting adititions can be made. 
The keys should be as minimal as possible, with one letter being the prefered for base metrics. 
Category metric keys are supported and should consist of a Capital letter for the Category and a lowercase letter for the metric. `Ae` is from the `Alergens` category, metric `peanuts`. Another example is `Fs`, `Fm` or `Fp` which are all Fats(saturate, mono-unsaturate, poly-unsaturate)
The unit for each key is stated on the reference table and can be change with a unit modification key(`U`)

## Referance Table
reference values [taken](https://europa.eu/youreurope/business/product-requirements/food-labelling/nutrition-declaration/index_en.htm) from the EU.

|Key|Name|Unit|
|---|----|------|
||**Base**||
|K|Kcal|Kcal|
|D|Dose|g|
|P|Protein|g|
|F|Fat|g|
|Fs|Fat Saturates|g|
|Fm|Fat Mono-Unsaturates|g|
|Fp|Fat PolyUnsaturates|g|
|C|Carbohydrate|g|
|Cs|Sugar|g|
|Csa|Added Sugar|g|
|Cp|Polyols|g|
|Cs|Starch|g|
|Cf|Fibre|g|
|Na|Salt|mg|
||**Generic**||
|N|Name||
|W|Weight|g|
|V|Volume|dl|
|Av|Alcohol Volume|%|
|**V/B**|**Vitamins**||
|Va|Vitamin A|μg|
|Vd|Vitamin D|μg|
|Ve|Vitamin E|mg|
|Vk|Vitamin K|μg|
|Vc|Vitamin C|mg|
|B1|Thiamin|mg|
|B2|Riboflavin|mg|
|B3|Niacin|mg|
|B5|Pantothenic acid|mg|
|B6|Vitamin B6|mg|
|B7|Biotin|μg|
|B9|Folic Acid|μg|
|B12|Vitamin B12|μg|
|**M**|**Minerals**||
|Kp|Potassium|mg|
|Ph|Phosphorus|mg|
|Cl|Cloride|mg|
|Ca|Calcium|mg|
|Mg|Magnesium|mg|
|Fe|Iron|mg|
|Cu|Copper|mg|
|Zn|Zinc|mg|
|Mn|Manganese|mg|
|Fl|Fluor|mg|
|Se|Selenium|μg|
|Mo|Molybdenum|μg|
|I|Iodine|μg|
|**A**|**Alergens**||
|AA|All alergens||
|Aa|Cerials Containing gluten||
|Ab|Crustaceans||
|Ac|Eggs||
|Ad|Fish||
|Ae|Peanuts||
|Af|Soybeans||
|Ag|Milk(including lactose)||
|Ah|Nuts||
|Al|Celery||
|Am|Mustard||
|An|Sesame seeds||
|Ao|Sulphur dioxide and sulphites||
|Ap|Lupin||
|Ar|Molluscs||
|**P**|**Protein Aminoacids**||
|Phi|Histidine||
|Pi|Isoleucine||
|Pl|Leucine||
|Ply|Lysine||
|Pm|Methionine||
|Pp|Phenylalanine||
|Pt|Threonine||
|Ptp|Tryptophan||
|Pv|Valine||
|Pa|Arginine|mg|
|Pc|Cysteine|mg|
|Pgl|Glutamine|mg|
|Pgy|Glycine|mg|
|Ppr|Proline|mg|
|Ps|Serine|mg|
|Ptr|Tyrosine|mg|
|Pal|Alanine|mg|
|Pag|Asparagine|mg|
|Pat|Aspartic |mg|
|Pgc|Glutamic |mg|



## Custom Usage and Extensions
The goal of this system is serve as a solid framework but also to be expandable for particular use cases. Schema defenition of new keys is suported, as well as redifining the units of the already established keys(hello 🇺🇸).
### Changing unints
The special key prefix `U` is used to redefine Units of other keys, for example to change `K` from `Kcal` to `Kjoule`, you can append `UK:Kj` to the vector
### Metric Key declaration
To declare new metrics the special key prefix `X` can be used. For example to add `Added sugar` as a metrig, one can define it by appending `XCag:Added sugar` to the vector. By default all added metrics are assumed to be in grams, but you can define it's unit with the `U` key as above. This can also be used to redefine any key.

# Contributing
This is a work in progress and open for contributions, all done in github open for discussion. If reworks come in the future that would change the protocol significantly a new major version will be added to the string, or something like that, maybe let's define a `Vx` key for it. I'm sure there are some typos and duplications somewhere.