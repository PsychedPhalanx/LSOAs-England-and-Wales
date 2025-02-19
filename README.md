# Exploring Deprivation and Ethnic Diversity in England and Wales: An LSOA-Level Analysis
*This project explores the relationships between deprivation, ethnicity, and rurality, at the Lower Super Output Area (LSOA) level in England and Wales, using Census 2021 data.*

## Contents

- [**Aims**](#aims)
- [**Datasets Used**](#datasets-used)
- [**Introduction**](#introduction)
    1. [**What Are LSOAs?**](#what-are-lsoas)
    2. [**Deprivation as Measured by the ONS**](#deprivation-as-measured-by-the-ons)
    3. [**Ethnicities of England and Wales**](#ethnicities-of-england-and-wales)
    4. [**The Rural/Urban Classification**](#the-ruralurban-classification)
- [**Key Findings**](#key-findings)
    1. [**Deprivation**](#deprivation)
    2. [**Ethnicity**](#ethnicity)
    3. [**Intersection of Deprivation and Ethnicity**](#intersection-of-deprivation-and-ethnicity)
    4. [**Intersections with Rurality**](#intersections-with-rurality)
    5. [**Aggregating by Local Authority District**](#aggregating-by-local-authority-district)
- [**Conclusion**](#conclusion)
- [**References**](#references)

## **Aims**

- To conduct geospatial analysis, identifying regions of England and Wales with (a) high levels of deprivation and (b) high concentrations of ethnic minorities.
- To assess the relationship between ethnic demographics and levels of deprivation.
- To examine the impact of rurality on (a) deprivation levels and (b) concentrations of ethnic minorities.

## **Datasets Used**

## **Introduction**

### **What Are LSOAs?**

Lower layer Super Output Areas (LSOAs) are small geographical units used for statistical purposes in England and Wales. LSOAs were introduced following the Census 2001 to mitigate the challenges posed to statistical analysis using historically-used geographical units: greatly varying population sizes, as in the case of wards; lacking coverage of the entirety of England and Wales, as in the case of parishes; and boundaries subject to change, as in the case of wards, parishes, local authorities and parliamentary constituencies. [[1]](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies) [[2]](https://ocsi.uk/2019/03/18/lsoas-leps-and-lookups-a-beginners-guide-to-statistical-geographies/)

By contrast, LSOAs have relatively uniform population sizes, cover the whole of England and Wales and have stable boundaries. LSOAs comprise between 400 and 1,200 households and have a usually resident population between 1,000 and 3,000 persons. There are 33,755 LSOAs in England and 1,917 in Wales.

![LSOA Boundaries](./Images/LSOA_boundaries.png)

These properties make LSOAs ideal for statistical analysis. Their relatively small size allows for the identification of localised trends that may otherwise be obscurred in larger geographical units. Kensington and Chelsea, for example, known for its affluence and composed of a total of 101 LSOAs, ranks 101st out of 345 local authorities in terms of deprivation, with 1st being the most deprived. [[3]](https://www.rbkc.gov.uk/pdf/Demographics_childdeprivation.pdf)

![Deprivation Plot for Kensington and Chelsea](./Images/kensington_and_chelsea_deprivation_plot.png)

### **Deprivation as Measured by the ONS**

The ONS considers entire households to be deprived based on four dimensions:
- Education
   - A household is classified as deprived in the education dimension if no one has at least level 2 education and no one aged 16 to 18 years is a full-time student.
- Employment
   - A household is classified as deprived in the employment dimension if any member, not a full-time student, is either unemployed or economically inactive due to long-term sickness or disability.
- Health
  - A household is classified as deprived in the health dimension if any person in the household has general health that is bad or very bad or is identified as disabled.
- Housing
   - A household is classified as deprived in the housing dimension if the household's accommodation is either overcrowded, in a shared dwelling, or has no central heating. [[4]](https://www.ons.gov.uk/census/census2021dictionary/variablesbytopic/demographyvariablescensus2021/householddeprivation)

The ONS data only gives the number of households deprived in 0, 1, 2, 3 or 4 dimensions per LSOA, but not which specific dimension(s) a household is deprived in. This restricts our ability to understand which factors are driving deprivation in each LSOA. As a result, our analysis can identify LSOAs or local authorities with high levels of deprivation but cannot provide insights into which dimensions of deprivation (education, employment, health or housing) are most prevalent. A more complete analysis ought to collate data on each of these four dimensions seperately, in order to identify LSOAs underperforming in each dimension.

### **Ethnicities of England and Wales**

Similarly to the other data collected by the ONS, ethnicity is self-reported by individuals. This can be problematic in the case of ethnicity due to the "subjective, multifaceted, and changing nature of ethnic identification". [[5]](https://www.ons.gov.uk/methodology/classificationsandstandards/measuringequality/ethnicgroupnationalidentityandreligion)

The Census 2021 provided a range of ethnic categories for individuals to choose from. Within each broad group, individuals could specify the subgroup that they most closely identified with:

- White
    - English/Welsh/Scottish/Northern Irish/British
    - Irish
    - Gypsy or Irish Traveller
    - Other White
- Mixed/Multiple ethnic groups
    - White and Black Caribbean
    - White and Black African
    - White and Asian
    - Other Mixed/Multiple ethnic group
- Asian/Asian British
    - Indian
    - Pakistani
    - Bangladeshi
    - Chinese
    - Other Asian
- Black/Black British
    - African
    - Caribbean
    - Other Black
- Other ethnic group
    - Arab
    - Any other ethnic group
  
This analysis only considers the five broad ethnic groups - White, Mixed, Asian, Black, and Other - without accounting for their subgroups. This simplification greatly limits the efficacy of our analysis as disparities in outcomes exist within the broad groups. Chinese students, for instance, are known to achieve higher academic outcomes than all other ethnicities, including even White British students, whilst Pakistani and Bangladeshi students - both within the same, broader Asian group - typically have lower levels of educational attainment. In the Black ethnic group, individuals of Black African descent tend to experience better educational and employment outcomes than those of Black Caribbean descent. [[6]](https://www.ons.gov.uk/peoplepopulationandcommunity/culturalidentity/ethnicity/articles/ethnicgroupdifferencesinhealthemploymenteducationandhousingshowninenglandandwalescensus2021/2023-03-15) [[7]](https://doi.org/10.1080/1369183X.2018.1539241) A similar situation also holds for the White ethnic group, where Gypsy or Irish Traveller students experience significantly lower educational attainment compared to their White British peers. [[8]](https://assets.publishing.service.gov.uk/media/5a7a4459ed915d1a6421c3e4/DFE-RR043.pdf)
 A more thorough analysis would disaggregate these broad ethnic categories into their subgroups, thereby allowing for more targeted interventions and a clearer picture of the underlying dynamics shaping outcomes across ethnic groups.

As per the Census 2021, there are a total of 59,597,576 total residents in England and Wales.

| Ethnicity | Number of Residents | Percentage of Total Population |
|-----------|--------------------:|------------------------------:|
| Asian     | 5,515,544          | 9.25%                         |
| Black     | 2,409,211          | 4.04%                         |
| Mixed     | 1,717,884          | 2.88%                         |
| Other     | 1,255,470          | 2.11%                         |
| White     | 48,699,467         | 81.71%                        |


![Ethnicity Barchart](./Images/bar_ethnicity.png)

### **The Rural/Urban Classification**

This analysis uses the 2011 'Rural-Urban Classification for small area geographies' or RUC for short, as no official classification exists from more recent years.[[9]](https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf) The RUC is concerned with Output Areas (OAs), the lowest level of geographical area for census statistics, composed of between 40 and 250 households, which are the subunits of LSOAs. [[1]](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies)

Applied to LSOAs, the RUC places LSOAs into one of eight categories, ordered from 'most urban' to 'most rural', based on the dominant classification of their constituent OAs: [[9]](https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf)

1. Urban (Major Conurbation)
2. Urban (Minor Conurbation)
3. Urban (City and Town)
4. Urban (City and Town in a Sparse Setting)
5. Rural (Town and Fringe)
6. Rural (Town and Fringe in a Sparse Setting)
7. Rural (Village)
8. Rural (Village in a Spare Setting)

![RUC2011](./Images/map_ruc2011.png)

See the table below for the numbers of LSOAs given each classification as per the 2011 data:

| Classification                                  | Number of LSOAs |
|-------------------------------------------------|----------------:|
| 1. Urban major conurbation                         |           11,523|
| 2. Urban minor conurbation                         |            1,208|
| 3. Urban city and town                             |           15,724|
| 4. Urban city and town in a sparse setting         |               94|
| 5. Rural town and fringe                           |            3,189|
| 6. Rural town and fringe in a sparse setting       |              197|
| 7. Rural village and dispersed                     |            2,490|
| 8. Rural village and dispersed in a sparse setting |              328|

The significant disparity in the number of LSOAs belonging to the above, eight categories poses challenges for statistical analysis, like reduced reliability of results for categories with fewer LSOAs. It is partly for this reason that this analysis aggregates these eight, separate groups into just two: 'Rural' and 'Urban'. 

| Classification | Number of LSOAs |
|-------- | -------- |
| Urban   | 29,591   |
| Rural   |   6081  |

Such a binary classification is in line with the ONS', likewise, binary classification of Output Areas into either 'Urban' or 'Rural'. OAs are classified as 'Urban' if the broader area within which the OA is found has a population of over 10,000; all other OAs are classified as 'Rural'. [[10]](https://www.ons.gov.uk/methodology/geography/geographicalproducts/ruralurbanclassifications/2011ruralurbanclassification)

Additionally, rurality is a variable included in our analysis in order to see how it intersects with deprivation and ethnic demography. The relative level of rurality or urbanity, made explicit by the four separate categories for each, is therefore unimportant for our concerns. Using a binary classification in place of the eight categories, thus, increases the reliability of our results whilst also simplifying our analysis.

The most important reason to use a binary classification, however, is due to the signifcant changes that occured to LSOAs between 2011 and 2021, detailed below.

#### Changes to LSOAs 2011-2021

First, several LSOAs had their boundaries modified. More importantly, between 2011 and 2021, an additional 919 LSOAs were created. The rationale for both of these changes was to ensure that population and household thresholds were maintained across all LSOAs. [[11]](https://www.ons.gov.uk/methodology/geography/ukgeographies/statisticalgeographies)

Within this decade, we expect several LSOAs to have changed in terms of their classification as per the RUC 2011, i.e., their membership of one of the eight categories. For example, an LSOA that belonged to the 'Urban city and town' category may have been 'promoted' to 'Urban minor conurbation' due to increasing urbanisation. Without RUC data from 2021, we cannot give a definite value for the number of LSOAs affected in this way. 

Using a binary classification almost completely mitigates this issue as we consider it extremely unlikely for an LSOA categorised as 'Rural' in 2011 to become 'Urban' in 2021. The reverse change, i.e., a change from 'Urban' to 'Rural', is, of course, impossible.

#### Data Processing: Modal Classification Approach

Each of the 919 'new' LSOAs lacked a classification as per the RUC 2011. As such, they also lacked a classification as per our binary approach. To give each of these 919 LSOAs a classification, the modal classification of each local authority was computed, and any LSOAs that lacked a classification were ascribed the modal classification. For example, take a fictitious local authority composed of a total of ten LSOAs, two of which are 'new', six of which were given the classification of 'Urban', and the remaining two 'Rural'. As the most common classification for that local authority would be 'Urban', the two 'new' LSOAs would be classified as 'Urban'.

![Rural-Urban](./Images/map_rural_urban.png)


## Key Findings
Content for Key Findings.

### Deprivation
Content for Deprivation.

![Deprivation Histogram](./Images/hist_deprived.png)

Content for Deprivation

![Deprivation Map](./Images/map_deprived.png)

### Ethnicity
Content for Ethnicity.

Add Correlation Matrix between ethnicities - use to justify white vs non-white

![White Histogram](./Images/hist_white.png)

Content for Ethnicity

![NW Histogram](./Images/hist_non_white.png)

Content for Ethnicity

![NW Map](./Images/map_minority.png)

### Intersection of Deprivation and Ethnicity
Content for Intersection of Deprivation and Ethnicity.

![Correlation Matrix](./Images/heatmap.png)

Content

![White Scatter](./Images/scatter_white_deprived.png)

Content

![Black Scatter](./Images/scatter_black_deprived.png)

Content

![Asian Scatter](./Images/scatter_asian_deprived.png)

Content

![Mixed Scatter](./Images/scatter_mixed_deprived.png)

Content

![Other Scatter](./Images/scatter_other_deprived.png)

Content

![White Scatter Greyed](./Images/scatter_grey_white_deprived.png)

Content

![Kmeans](./Images/scatter_kmeans.png)

Content

![Cluster Map](./Images/map_clusters.png)

Content

![Selected Cluster Map](./Images/map_selected_clusters.png)

Content

![Threshold Barchart](./Images/bar_proportion_eth.png)

### Intersections with Rurality
Content for Intersections with Rurality.

![Rural vs Urban Deprivation Histrogram](./Images/hist_deprived_rural_urban.png)

Content

![Rural vs Urban Ethnicity Barchart](./Images/bar_proportion_rural_urban.png)

### Aggregating by Local Authority District
Content for Aggregating by Local Authority District.

## Conclusion
Content for Conclusion.

## **References**

[1] Office for National Statistics (ONS) (2021). *Census 2021 Geographies*. Available at: [https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies)

[2] Oxford Consultants for Social Inclusion (OCSI) (2019). *LSOAs, LEPs, and Lookups: A Beginner’s Guide to Statistical Geographies*. Available at: 
[https://ocsi.uk/2019/03/18/lsoas-leps-and-lookups-a-beginners-guide-to-statistical-geographies/](https://ocsi.uk/2019/03/18/lsoas-leps-and-lookups-a-beginners-guide-to-statistical-geographies/)

[3] Royal Borough of Kensington and Chelsea (2007). *Demographics and Child Deprivation*. Available at: [https://www.rbkc.gov.uk/pdf/Demographics_childdeprivation.pdf](https://www.rbkc.gov.uk/pdf/Demographics_childdeprivation.pdf)

[4] Office for National Statistics (ONS) (2021). *Household Deprivation - Census 2021 Variables by Topic*. Available at: [https://www.ons.gov.uk/census/census2021dictionary/variablesbytopic/demographyvariablescensus2021/householddeprivation](https://www.ons.gov.uk/census/census2021dictionary/variablesbytopic/demographyvariablescensus2021/householddeprivation)

[5] Office for National Statistics (ONS) (2021). *Ethnic Group, National Identity, and Religion*. Available at: [https://www.ons.gov.uk/methodology/classificationsandstandards/measuringequality/ethnicgroupnationalidentityandreligion](https://www.ons.gov.uk/methodology/classificationsandstandards/measuringequality/ethnicgroupnationalidentityandreligion)

[6] Office for National Statistics (ONS) (2023). *Ethnic group differences in health, employment, education and housing shown in England and Wales' Census 2021*. Available at:
[https://www.ons.gov.uk/peoplepopulationandcommunity/culturalidentity/ethnicity/articles/ethnicgroupdifferencesinhealthemploymenteducationandhousingshowninenglandandwalescensus2021/2023-03-15](https://www.ons.gov.uk/peoplepopulationandcommunity/culturalidentity/ethnicity/articles/ethnicgroupdifferencesinhealthemploymenteducationandhousingshowninenglandandwalescensus2021/2023-03-15)

[7] Li, Y., & Heath, A. (2018). *Persisting disadvantages: A study of labour market dynamics of ethnic unemployment and earnings in the UK (2009–2015)*. *Journal of Ethnic and Migration Studies*, 46(5), 857–878. Available at: [https://doi.org/10.1080/1369183X.2018.1539241](https://doi.org/10.1080/1369183X.2018.1539241)

[8] Department for Education (2010). *Improving the Outcomes for Gypsy, Roma and Traveller Pupils: Final Report*. Available at: [https://assets.publishing.service.gov.uk/media/5a7a4459ed915d1a6421c3e4/DFE-RR043.pdf](https://assets.publishing.service.gov.uk/media/5a7a4459ed915d1a6421c3e4/DFE-RR043.pdf)

[9] Department for Environment, Food & Rural Affairs (DEFRA) (2011). *Rural-Urban Classification 2011: User Guide*. Available at: [https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf](https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf)

[10] Office for National Statistics (ONS) (2016) *2011 Rural/Urban Classification*. Available at:
[https://www.ons.gov.uk/methodology/geography/geographicalproducts/ruralurbanclassifications/2011ruralurbanclassification](https://www.ons.gov.uk/methodology/geography/geographicalproducts/ruralurbanclassifications/2011ruralurbanclassification)

[11] Office for National Statistics (ONS) (2021) *Statistical Geographies*. Available at:
[https://www.ons.gov.uk/methodology/geography/ukgeographies/statisticalgeographies](https://www.ons.gov.uk/methodology/geography/ukgeographies/statisticalgeographies)
