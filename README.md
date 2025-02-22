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

Lower layer Super Output Areas (LSOAs) are small geographical units used for statistical purposes in England and Wales. LSOAs were introduced following the Census 2001 to mitigate the challenges posed to statistical analysis using historically-used geographical units: greatly varying population sizes, as in the case of wards; lacking coverage of the entirety of England and Wales, as in the case of parishes; and boundaries subject to change, as in the case of wards, parishes, local authorities and parliamentary constituencies [[1]](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies) [[2]](https://ocsi.uk/2019/03/18/lsoas-leps-and-lookups-a-beginners-guide-to-statistical-geographies/).

By contrast, LSOAs have relatively uniform population sizes, cover the whole of England and Wales and have stable boundaries. LSOAs comprise between 400 and 1,200 households and have a usually resident population between 1,000 and 3,000 persons. There are 33,755 LSOAs in England and 1,917 in Wales [[1]](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies).

![LSOA Boundaries](./Images/LSOA_boundaries.png)

These properties make LSOAs ideal for statistical analysis. Their relatively small size allows for the identification of localised trends that may otherwise be obscurred in larger geographical units. Kensington and Chelsea, for example, known for its affluence and composed of a total of 101 LSOAs, exhibits considerable disparities in terms of deprivation.

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
   - A household is classified as deprived in the housing dimension if the household's accommodation is either overcrowded, in a shared dwelling, or has no central heating [[3]](https://www.ons.gov.uk/census/census2021dictionary/variablesbytopic/demographyvariablescensus2021/householddeprivation).

The ONS data only gives the number of households deprived in 0, 1, 2, 3 or 4 dimensions per LSOA, but not which specific dimension(s) a household is deprived in. This restricts our ability to understand which factors are driving deprivation in each LSOA. As a result, our analysis can identify LSOAs or local authorities with high levels of deprivation but cannot provide insights into which dimensions of deprivation (education, employment, health or housing) are most prevalent. A more complete analysis ought to collate data on each of these four dimensions seperately, in order to identify LSOAs underperforming in each dimension.

### **Ethnicities of England and Wales**

Similarly to the other data collected by the ONS, ethnicity is self-reported by individuals. This can be problematic in the case of ethnicity due to the "subjective, multifaceted, and changing nature of ethnic identification" [[4]](https://www.ons.gov.uk/methodology/classificationsandstandards/measuringequality/ethnicgroupnationalidentityandreligion).

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
  
This analysis only considers the five broad ethnic groups - White, Mixed, Asian, Black, and Other - without accounting for their subgroups. This simplification greatly limits the efficacy of our analysis as disparities in outcomes exist within the broad groups. Chinese students, for instance, are known to achieve higher academic outcomes than all other ethnicities, including even White British students, whilst Pakistani and Bangladeshi students - both within the same, broader Asian group - typically have lower levels of educational attainment. In the Black ethnic group, individuals of Black African descent tend to experience better educational and employment outcomes than those of Black Caribbean descent [[5]](https://www.ons.gov.uk/peoplepopulationandcommunity/culturalidentity/ethnicity/articles/ethnicgroupdifferencesinhealthemploymenteducationandhousingshowninenglandandwalescensus2021/2023-03-15) [[6]](https://doi.org/10.1080/1369183X.2018.1539241). A similar situation also holds for the White ethnic group, where Gypsy or Irish Traveller students experience significantly lower educational attainment compared to their White British peers [[7]](https://assets.publishing.service.gov.uk/media/5a7a4459ed915d1a6421c3e4/DFE-RR043.pdf).
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

This analysis uses the 2011 'Rural-Urban Classification for small area geographies' or RUC for short, as no official classification exists from more recent years[[8]](https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf). The RUC is concerned with Output Areas (OAs), the lowest level of geographical area for census statistics, composed of between 40 and 250 households, which are the subunits of LSOAs [[1]](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeographies/census2021geographies).

Applied to LSOAs, the RUC places LSOAs into one of eight categories, ordered from 'most urban' to 'most rural', based on the dominant classification of their constituent OAs: [[8]](https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf)

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

Such a binary classification is in line with the ONS', likewise, binary classification of Output Areas into either 'Urban' or 'Rural'. OAs are classified as 'Urban' if the broader area within which the OA is found has a population of over 10,000; all other OAs are classified as 'Rural' [[9]](https://www.ons.gov.uk/methodology/geography/geographicalproducts/ruralurbanclassifications/2011ruralurbanclassification).

Additionally, rurality is a variable included in our analysis in order to see how it intersects with deprivation and ethnic demography. The relative level of rurality or urbanity, made explicit by the four separate categories for each, is therefore unimportant for our concerns. Using a binary classification in place of the eight categories, thus, increases the reliability of our results whilst also simplifying our analysis.

The most important reason to use a binary classification, however, is due to the signifcant changes that occured to LSOAs between 2011 and 2021, detailed below.

#### Changes to LSOAs 2011-2021

First, several LSOAs had their boundaries modified. More importantly, between 2011 and 2021, an additional 919 LSOAs were created. The rationale for both of these changes was to ensure that population and household thresholds were maintained across all LSOAs [[10]](https://www.ons.gov.uk/methodology/geography/ukgeographies/statisticalgeographies).

Within this decade, we expect several LSOAs to have changed in terms of their classification as per the RUC 2011, i.e., their membership of one of the eight categories. For example, an LSOA that belonged to the 'Urban city and town' category may have been 'promoted' to 'Urban minor conurbation' due to increasing urbanisation. Without RUC data from 2021, we cannot give a definite value for the number of LSOAs affected in this way. 

Using a binary classification almost completely mitigates this issue as we consider it extremely unlikely for an LSOA categorised as 'Rural' in 2011 to become 'Urban' in 2021. The reverse change, i.e., a change from 'Urban' to 'Rural', is, of course, impossible.

#### Data Processing: Modal Classification Approach

Each of the 919 'new' LSOAs lacked a classification as per the RUC 2011. As such, they also lacked a classification as per our binary approach. To give each of these 919 LSOAs a classification, the modal classification of each local authority was computed, and any LSOAs that lacked a classification were ascribed the modal classification. For example, take a fictitious local authority composed of a total of ten LSOAs, two of which are 'new', six of which were given the classification of 'Urban', and the remaining two 'Rural'. As the most common classification for that local authority would be 'Urban', the two 'new' LSOAs would be classified as 'Urban'.

![Rural-Urban](./Images/map_rural_urban.png)


## Key Findings
Content for Key Findings.

### Deprivation

Again, entire households are considered deprived by the ONS. As such, the data either indicates the absolute number of deprived households, or the percentage of deprived households. See the first five rows of the data pertaining to deprivation in LSOAs in England and Wales:


| LSOA Code | Total Households | Not-N | Not-% | 1-N | 1-%  | 2-N | 2-%  | 3-N | 3-% | 4-N | 4-% | LSOA Name       | Deprived % |
|-----------|------------------|-------|-------|-----|------|-----|------|-----|-----|-----|-----|-----------------|------------|
| E01011954 | 963              | 389   | 40.4  | 304 | 31.6 | 207 | 21.5 | 62  | 6.4 | 1   | 0.1 | Hartlepool 001A | 59.6       |
| E01011969 | 603              | 306   | 50.7  | 199 | 33.0 | 89  | 14.8 | 9   | 1.5 | 0   | 0.0 | Hartlepool 001B | 49.3       |
| E01011970 | 488              | 251   | 51.4  | 170 | 34.8 | 61  | 12.5 | 6   | 1.2 | 0   | 0.0 | Hartlepool 001C | 48.6       |
| E01011971 | 519              | 325   | 62.6  | 147 | 28.3 | 45  | 8.7  | 2   | 0.4 | 0   | 0.0 | Hartlepool 001D | 37.4       |
| E01033465 | 740              | 459   | 62.0  | 209 | 28.2 | 66  | 8.9  | 6   | 0.8 | 0   | 0.0 | Hartlepool 001F | 38.0       |

The final column is not included in the original dataset. Column names have either been modified or abbreviated for clarity. 'Not-N', '1-N', '2-N', etc., indicate the number of households in an LSOA that are deprived in the corresponding number of measures: 'Not-N' gives the number of households not deprived in any measure, '1-N' gives the number of households deprived in a singular measure, etc. The neighbouring percentage columns, e.g., 'Not-%', '1-%', etc., give the percentage of households deprived in the corresponding number of measures.

See the below summary statistics:

|             | Total Households |     Not-N     |    Not-%    |     1-N     |    1-%    |     2-N     |    2-%    |     3-N     |    3-%    |     4-N     |    4-%    | Deprived %  |
|-------------|------------------|---------------|-------------|-------------|-----------|-------------|-----------|-------------|-----------|-------------|-----------|-------------|
| count       | 35,672           | 35,672        | 35,672      | 35,672      | 35,672    | 35,672      | 35,672    | 35,672      | 35,672    | 35,672      | 35,672    | 35,672      |
| mean        | 695              | 336           | 48          | 232         | 34        | 99          | 14        | 26          | 4         | 2           | 0        | 52          |
| std         | 144              | 103           | 11          | 53          | 4         | 44          | 6         | 21          | 3         | 2           | 0        | 11          |
| min         | 400              | 70            | 13          | 81          | 16        | 9           | 2         | 0           | 0         | 0           | 0         | 19          |
| 25%         | 601              | 264           | 41          | 196         | 31        | 66          | 10        | 10          | 2         | 0           | 0         | 44          |
| 50%         | 665              | 325           | 49          | 226         | 34        | 93          | 14        | 20          | 3         | 1           | 0         | 51          |
| 75%         | 767              | 394           | 56          | 261         | 36        | 127         | 18        | 37          | 5         | 2           | 0         | 60          |
| max         | 1,980            | 1,052         | 81          | 723         | 60        | 379         | 37        | 191         | 19        | 35          | 5         | 87          |


It is reasonable to expect correlations to exist between several of these columns. We expect a negative correlation between 'Not-%' and '1-%', '2-%', '3-%', etc. - As the percentage of households not deprived in any measure increases, the percentage of households deprived in any number of measures ought to decrease. We expect positive correlations to exist between the percentage of households deprived in some number of measures, excluding 0 - if an LSOA has an abudance of households deprived in a singular measure, it will likely have a higher number of households deprived in two and three and four measures. A simple correlation heatmap affirms these contentions:

![Deprivation Heatmap](./Images/heatmap_deprivation.png)

The summary statistics indicate a great disparity in the percentages for the relevant columns, e.g., observe the statistics for the '3-%' and '4-%' columns compared to those for 'Not-%' and '1-%'. This disparity, coupled with the relatively strong correlations between the percentages of households deprived in some number of measures, was reason to derive a singular metric for deprivation, called 'Deprived %', present in the data shown. 'Deprived %' gives the percentage of households in an LSOA that are deprived in any number of measures, excluding 0, and was trivially computed by summing all the relavent percentage columns. Having a singular metric to measure deprivation simplifies our analyis, but prevents us from locating LSOAs with high proportions of households deprived in numerous measures.

See the below histogram showing the distribution of household deprivation across all LSOAs in England and Wales, where each LSOA's value represents the percentage of households deprived in at least one measure.

![Deprivation Histogram](./Images/hist_deprived.png)

The plot shows the percentage of households experiencing deprivation in at least one measure ranges from approximately 20% to 85% across different areas. The peak of this distribution occurs between 45-50% deprivation, where we find approximately 4,200 LSOAs. Statistical testing strongly rejects the hypothesis of normality (D'Agostino's K² test statistic = 1065.25, p < 0.001), indicating that the distribution significantly deviates from a normal distribution despite its superficially bell-shaped appearance. This finding informs our use of non-parametric methods in future hypothesis tests.

The distribution exhibits a notable positive skew, with a longer tail extending towards higher deprivation levels. This skewness indicates that while most areas cluster around moderate levels of deprivation, there are some areas experiencing particularly high levels of household deprivation. Most LSOAs (approximately 80%) fall between 35% and 65% deprivation levels, with relatively few areas showing either very low (<25%) or very high (>75%) deprivation. This concentration around moderate levels suggests that extreme deprivation, while present, is not typical across England and Wales.

The below chloropleth map visualises the percentage of households deprived in at least measure for all LSOA in England and Wales, with colours ranging from green (lower deprivation) through to red (high deprivation).

![Deprivation Map](./Images/map_deprived.png)

The geospatial visualisation reveals clear patterns of household deprivation across England and Wales. Major urban centres, particularly in northern England, show notably higher deprivation levels (orange to red colouring). London displays a distinct pattern with higher deprivation concentrated in its eastern regions, while its western areas show lower deprivation levels (green colouring) - a divide that has considerably diminished in its intensity in recent years [[11]](https://centreforlondon.org/wp-content/uploads/2016/08/CFLJ3887-Inside-out-inequality_12.125_WEB.pdf). The Welsh Valleys and several coastal regions, particularly along the east coast, exhibit concentrated areas of higher deprivation. This coastal pattern reflects challenges faced by British seaside towns, including seasonal employment and poor transport connectivity, as highlighted in parliamentary research [[12]](https://publications.parliament.uk/pa/ld201719/ldselect/ldseaside/320/320.pdf).

In contrast, large swaths of rural England, especially in the south and central regions, demonstrate consistently lower deprivation levels. This pattern contributes to the well-documented north-south divide in England, where northern regions generally experience higher levels of deprivation and poorer socioeconomic outcomes [[13]](https://www.ippr.org/research/publications/state-of-the-north-2024). However, the visualisation shows significant local variations, particularly around major northern cities, suggesting that the relationship between geography and deprivation is not straightforward. The presence of both highly deprived and affluent areas within close proximity, particularly in urban settings, indicates the localised nature of deprivation and the importance of analysing patterns at the LSOA level.

### Ethnicity
See the first five rows of the data relating to ethnicity below:

| LSOA Code  | Total  | Asian | Asian % | Black | Black % | Mixed | Mixed % | White  | White % | Other | Other % | LSOA Name       | Non-White | Non-White % |
|------------|--------|-------|---------|-------|---------|-------|---------|--------|---------|-------|---------|----------------|-----------|-------------|
| E01011954  | 2284.0 | 19.0  | 0.8     | 0.0   | 0.0     | 6.0   | 0.3     | 2248.0 | 98.4    | 11.0  | 0.5     | Hartlepool 001A | 36.0      | 1.6         |
| E01011969  | 1345.0 | 6.0   | 0.4     | 0.0   | 0.0     | 6.0   | 0.4     | 1329.0 | 98.8    | 4.0   | 0.3     | Hartlepool 001B | 16.0      | 1.2         |
| E01011970  | 1070.0 | 7.0   | 0.7     | 0.0   | 0.0     | 4.0   | 0.4     | 1059.0 | 99.0    | 0.0   | 0.0     | Hartlepool 001C | 11.0      | 1.0         |
| E01011971  | 1323.0 | 5.0   | 0.4     | 0.0   | 0.0     | 5.0   | 0.4     | 1311.0 | 99.1    | 2.0   | 0.2     | Hartlepool 001D | 12.0      | 0.9         |
| E01033465  | 1954.0 | 12.0  | 0.6     | 2.0   | 0.1     | 11.0  | 0.6     | 1914.0 | 98.0    | 15.0  | 0.8     | Hartlepool 001F | 40.0      | 2.0         |

In contrast to the deprivation data, the ONS collates ethnicity information in terms numbers of people. See the summary statistics below:

| Statistic | Total       | Asian       | Asian %     | Black       | Black %     | Mixed       | Mixed %     | White       | White %     | Other       | Other %     | Non-White   | Non-White % |
|-----------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|
| count     | 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000| 35672.000000|
| mean      | 1670.710249 | 154.618300  | 8.611112    | 67.537873   | 3.784091    | 48.157771   | 2.808354    | 1365.201475 | 82.800950   | 35.194831   | 1.997334    | 305.508774  | 17.199050   |
| std       | 354.184425  | 266.791618  | 13.583344   | 125.314551  | 6.646866    | 38.791511   | 2.044719    | 409.690590  | 20.192162   | 53.080967   | 2.820652    | 395.156155  | 20.192162   |
| min       | 997.000000  | 0.000000    | 0.000000    | 0.000000    | 0.000000    | 0.000000    | 0.000000    | 15.000000   | 0.800000    | 0.000000    | 0.000000    | 0.000000    | 0.000000    |
| 25%       | 1440.000000 | 18.000000   | 1.200000    | 5.000000    | 0.300000    | 20.000000   | 1.300000    | 1162.000000 | 76.400000   | 5.000000    | 0.300000    | 54.000000   | 3.400000    |
| 50%       | 1605.000000 | 52.000000   | 3.200000    | 17.000000   | 1.100000    | 36.000000   | 2.200000    | 1370.000000 | 92.000000   | 14.000000   | 0.900000    | 129.000000  | 8.000000    |
| 75%       | 1833.000000 | 164.000000  | 9.700000    | 68.000000   | 4.000000    | 66.000000   | 3.900000    | 1566.000000 | 96.600000   | 43.000000   | 2.500000    | 397.000000  | 23.600000   |
| max       | 9899.000000 | 2608.000000 | 96.300000   | 1624.000000 | 62.100000   | 663.000000  | 18.500000   | 7111.000000 | 100.000000  | 926.000000  | 35.200000   | 3518.000000 | 99.200000   |


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

[3] Office for National Statistics (ONS) (2021). *Household Deprivation - Census 2021 Variables by Topic*. Available at: [https://www.ons.gov.uk/census/census2021dictionary/variablesbytopic/demographyvariablescensus2021/householddeprivation](https://www.ons.gov.uk/census/census2021dictionary/variablesbytopic/demographyvariablescensus2021/householddeprivation)

[4] Office for National Statistics (ONS) (2021). *Ethnic Group, National Identity, and Religion*. Available at: [https://www.ons.gov.uk/methodology/classificationsandstandards/measuringequality/ethnicgroupnationalidentityandreligion](https://www.ons.gov.uk/methodology/classificationsandstandards/measuringequality/ethnicgroupnationalidentityandreligion)

[5] Office for National Statistics (ONS) (2023). *Ethnic group differences in health, employment, education and housing shown in England and Wales' Census 2021*. Available at:
[https://www.ons.gov.uk/peoplepopulationandcommunity/culturalidentity/ethnicity/articles/ethnicgroupdifferencesinhealthemploymenteducationandhousingshowninenglandandwalescensus2021/2023-03-15](https://www.ons.gov.uk/peoplepopulationandcommunity/culturalidentity/ethnicity/articles/ethnicgroupdifferencesinhealthemploymenteducationandhousingshowninenglandandwalescensus2021/2023-03-15)

[6] Li, Y., & Heath, A. (2018). *Persisting disadvantages: A study of labour market dynamics of ethnic unemployment and earnings in the UK (2009–2015)*. *Journal of Ethnic and Migration Studies*, 46(5), 857–878. Available at: [https://doi.org/10.1080/1369183X.2018.1539241](https://doi.org/10.1080/1369183X.2018.1539241)

[7] Department for Education (2010). *Improving the Outcomes for Gypsy, Roma and Traveller Pupils: Final Report*. Available at: [https://assets.publishing.service.gov.uk/media/5a7a4459ed915d1a6421c3e4/DFE-RR043.pdf](https://assets.publishing.service.gov.uk/media/5a7a4459ed915d1a6421c3e4/DFE-RR043.pdf)

[8] Department for Environment, Food & Rural Affairs (DEFRA) (2011). *Rural-Urban Classification 2011: User Guide*. Available at: [https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf](https://assets.publishing.service.gov.uk/media/5a7cab23e5274a38e5756044/RUC11user_guide_28_Aug.pdf)

[9] Office for National Statistics (ONS) (2016) *2011 Rural/Urban Classification*. Available at:
[https://www.ons.gov.uk/methodology/geography/geographicalproducts/ruralurbanclassifications/2011ruralurbanclassification](https://www.ons.gov.uk/methodology/geography/geographicalproducts/ruralurbanclassifications/2011ruralurbanclassification)

[10] Office for National Statistics (ONS) (2021) *Statistical Geographies*. Available at:
[https://www.ons.gov.uk/methodology/geography/ukgeographies/statisticalgeographies](https://www.ons.gov.uk/methodology/geography/ukgeographies/statisticalgeographies)

[11] Centre for London (2015). *Inside Out: The New Geography of Wealth and Poverty in London*. Available at: [https://centreforlondon.org/wp-content/uploads/2016/08/CFLJ3887-Inside-out-inequality_12.125_WEB.pdf](https://centreforlondon.org/wp-content/uploads/2016/08/CFLJ3887-Inside-out-inequality_12.125_WEB.pdf)

[12] House of Lords Select Committee (2019). *The Future of Seaside Towns*. Available at: [https://publications.parliament.uk/pa/ld201719/ldselect/ldseaside/320/320.pdf](https://publications.parliament.uk/pa/ld201719/ldselect/ldseaside/320/320.pdf)

[13] Institute for Public Policy Research (IPPR) North (2023). *State of the North 2024: Overcoming Regional Inequalities*. Available at: [https://www.ippr.org/research/publications/state-of-the-north-2024](https://www.ippr.org/research/publications/state-of-the-north-2024)
