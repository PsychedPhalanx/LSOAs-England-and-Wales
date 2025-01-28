# Exploring Deprivation and Ethnic Diversity in England and Wales: An LSOA-Level Analysis
*This project explores the relationships between deprivation, ethnicity, and rurality, at the Lower Super Output Area (LSOA) level in England and Wales, using Census 2021 data.*

## Contents
1. [**Aims**](#1-aims)
2. [**Datasets Used**](#2-datasets-used)
3. [**Introduction**](#3-introduction)
   - [**What Are LSOAs?**](#what-are-lsoas)
   - [**Understanding Deprivation**](#understanding-deprivation)
   - [**Ethnicities of England and Wales**](#ethnicities-of-england-and-wales)
   - [**Rurality and Its Impact**](#rurality-and-its-impact)
4. [**Key Findings**](#4-key-findings)
   - [**Deprivation**](#deprivation)
   - [**Ethnicity**](#ethnicity)
   - [**Rurality vs Urbanity**](#rurality-vs-urbanity)
5. [**Conclusion**](#5-conclusion)
6. [**References**](#6-references)

## 1. **Aims**
- To conduct geospatial analysis, identifying regions of England and Wales with (a) high levels of deprivation and (b) high concentrations of ethnic minorities.
- To assess the relationship between ethnic demographics and levels of deprivation.
- To examine the impact of rurality on (a) deprivation levels and (b) concentrations of ethnic minorities.

## 2. **Datasets Used**

## 3. **Introduction**

### **What Are LSOAs?**
Lower layer Super Output Areas (LSOAs) are small geographical units used for statistical purposes in England and Wales. LSOAs were introduced following the Census 2001 to mitigate the challenges posed to statistical analysis using historically-used geographical units: greatly varying population sizes, as in the case of wards; lacking coverage of the entirety of England and Wales, as in the case of parishes; and boundaries subject to change, as in the case of wards, parishes, local authorities and parliamentary constituencies. 

By contrast, LSOAs have relatively uniform population sizes, cover the whole of England and Wales and have stable boundaries. LSOAs comprise between 400 and 1,200 households and have a usually resident population between 1,000 and 3,000 persons. There are 33,755 LSOAs in England and 1,917 in Wales.

These properties make LSOAs ideal for statistical analysis. Their relatively small size allows for the identification of localised trends that may otherwise be obscurred in larger geographical units. Kensington and Chelsea, for example, known for its affluence and composed of a total of 101 LSOAs, ranks 101st out of 345 local authorities in terms of deprivation, with 1st being the most deprived.

![Deprivation Plot for Kensington and Chelsea](./Images/Kensington_and_Chelsea_deprivation_plot.png)


### **Understanding Deprivation**
The ONS considers entire households to be deprived based on four dimensions:
- Education
   - A household is classified as deprived in the education dimension if no one has at least level 2 education and no one aged 16 to 18 years is a full-time student.
- Employment
   - A household is classified as deprived in the employment dimension if any member, not a full-time student, is either unemployed or economically inactive due to long-term sickness or disability.
- Health
  - A household is classified as deprived in the health dimension if any person in the household has general health that is bad or very bad or is identified as disabled.
- Housing
   - A household is classified as deprived in the housing dimension if the household's accommodation is either overcrowded, in a shared dwelling, or has no central heating.

The ONS data only gives the number of households deprived in 0, 1, 2, 3 or 4 dimensions per LSOA, but not which specific dimension(s) a household is deprived in. This restricts our ability to understand which factors are driving deprivation in each LSOA. As a result, our analysis can identify LSOAs or local authorities with high levels of deprivation but cannot provide insights into which dimensions of deprivation (education, employment, health or housing) are most prevalent. A more complete analysis ought to collate data on each of these four dimensions seperately, in order to identify LSOAs underperforming in each dimension.
 
### **Ethnicities of England and Wales**

### **Rurality and Its Impact**

## 4. **Key Findings**

### **Deprivation**

### **Ethnicity**

### **Rurality vs Urbanity**

## 5. **Conclusion**

## 6. **References**

