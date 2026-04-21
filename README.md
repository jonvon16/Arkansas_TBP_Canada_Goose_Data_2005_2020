# Data associated with Veon et al. (2026), Evaluating harvest liberalization strategies on population dynamics of southern latitude temperate-breeding Canada geese
This repository (Veon 2025) contains 1) Program MARK Arkansas Canada goose banding and encounter data, as well as 2) harvest probability and abundance data/calculations, associated with the manuscript: Veon et al., Evaluating harvest liberalization strategies on population dynamics of southern latitude temperate-breeding Canada geese. All banding and encounter data used these files is available upon request from the USGS Bird Banding Labratory (USGS BBL 2021).

## AR_CAGO_2005_2020_MARK_Input_File.tmp.txt

This file contains the encounter histories used to develop models in Program Mark for the Arkansas temperate-breeding Canada Goose population (2005-2020).

### Data Access:

All banding data can be accessed through one of the various data request options at the USGS Bird Banding Laboratory (BBL) Banding and Encounter Data Request website.

Link (may need to copy and paste into browser): https://www.usgs.gov/labs/bird-banding-laboratory/science/banding-and-encounter-data-requests

### Lineage:

To derive the input file, we first filtered raw banding data (.CSV acquired from the Bird Banding Laboratory) using the following filters:

- Canada goose species code: 1720 and 1723
- Arkansas Game and Fish Commission Permit number: 6569
- Known age hatch year (2) or local (4) and after hatch year (1)
- Sex: unknown (0), male (4), and female (5)
- Band type: aluminum\butt-end toll free (1) or aluminum\butt-end web address (41 or W1)
- How obtained code: shot (1) that occurred during the hunting season (September through February)

We then used an excel pivot table to create a column with all band numbers that met criteria. We then created columns for each spring and summer of banding (Year A) and the following hunting season (Year B). The resulting number string from those years concatenated is Live Dead Live Dead (LDLD) format. A “0’ means the goose was not encountered. A “1” means the goose was encountered. We created two final columns for age at the end of LDLD string (to the left of the semicolon): the first of the two numbers represent a “local” or “hatch year” Canada goose at capture. The second of the two numbers represents an “after hatch year” goose at capture. A “1” was inserted for the correct age and a “0” for the incorrect age. Finally, we concatenated all columns using the final notation:

 /* Band Number */ All Encounter History Values for Each Year A & B, Local, AHY; 
 
(e.g., /* 127851987 */ 00000000000000000000000000000010 0 1;)

This final set of concatenated string values was used for the input file.

## ARCAGO_LincolnEstimate_Data_2005_2020

### Sheets:

*ARCAGO_AHY_Lincoln*
- Worksheet used to calculate abundance of adult >1 year old temperate breeding Canada geese.

*ARCAGO_HY_Lincoln*
- Worksheet used to calculate abundance of juvenile ≤1 year old temperate breeding Canada geese.

*LocalGooseCorrectionFactor*
- Worksheet used to calculate the proportion of temperate breeding Canada geese that originated in Arkansas (used in corrections to total estimated abundance).

### Sheet Column Descriptions:
*ARCAGO_AHY_Lincoln & ARCAGO_HY_Lincoln Columns:*

- **Band Year**
  - The year for the spring/summer geese were banded

- **N banded**
  - Number of geese banded.

- **N recovered (direct)**
  - Number of geese harvested (of those banded the spring/summer before) in the following winter

- **Direct recovery rate drr**
  - drr = N recovered (direct) / N banded (year t)

- **Var drr**
  - Variance of drr; Var = (drr * (1-drr)) / (N banded-1)

- **SE drr**
  - Standard error of drr; SE = √Var drr

- **Reporting rate rho**
  - Band reporting probabilities from Arnold et al. (2020), with linear predicted values for years after 2010

- **Var rho**
  - Variance of reporting probabilities; Var = SE rho^2 (see below)

- **SE rho**
  - Standard error of band reporting probabilities from Arnold et al. (2020), with linear predicted values for years after 2010

- **Harvest rate h**
  - h = drr / rho

- **Var h**
  - Variance of h; Var h = (Var drr / rho^2) + (drr^2 * Var rho) / rho^4

- **SE h**
  - Standard error of h; SE h = √Var h

- **Padding & Royle (H adjust)**
  - Harvest estimate survey bias correction factor from Padding and Royle (2012)

- **Total Harvest – H (unadjusted)**
  - Total cackling-Canada goose harvest estimates for Arkansas from Raftovich et al. (2022)

- **Harvest Correction Factor bias and AR Breeders**
  - Correction factor for harvest used to represent temperate-breeding Canada geese that originated in Arkansas. Proportion of Arkansas’ total cackling-Canada goose harvest that is temperate-breeding Canada geese (0.85) x proportion of temperate-breeding Canada geese harvested in Arkansas that originated in Arkansas (0.94) = 0.80

- **Total Harvest – SE H (unadjusted)**
  - Standard error of total harvest unadjusted; SE = Total harvest (unadjusted) * 0.1

- **Total Harvest – CV H (unadjusted)**
  - Coefficient of variation for harvest unadjusted; SE H (unadjusted) / Total Harvest (unadjusted)

- **Adjusted Total Harvest - adj-H (adjusted - Final)**
  - Padding and Royle H adjust * Total Harvest (unadjusted) * Harvest Correction Factor bias and AR Breeders

- **Adjusted Total Harvest - Var adj-H (adjusted - Final)**
  - (adj-H * CV H)^2
    
- **N**
  - Abundance of Arkansas temperate-breeding Canada geese; N = ((N banded + 1) * (adj-H + 1) * rho / (N recovered [direct] + 1)) - 1

- **Var (N) – subpart 1: Var (b/r)**
  - Variance of the number of bandings divided by the number of direct recoveries;
  - Var (b/r) = (N banded + 1) * (N banded - N recovered [direct]) / (((N recovered [direct] + 1)^2) * (N recovered [direct] + 2))

- **Var (N) – subpart 2: Var (BH/r)**
  - Variance of the number of bandings divided by the number of direct recoveries corrected for adjusted harvest;
  - Var (BH/r) = (N banded / N recovered [direct])^2 * Var adj-H + adj-H^2 * Var b/r

- **Var (N)**
  - Variance of estimated abundance; Var (N) =(((N banded * adj-H) / N recovered [direct])^2) * Var rho + rho^2 * Var(BH/r)

- **SE (N)**
  - Standard error of abundance estimate; SE = √Var (N)

- **CL (N)**
  - 95% Confidence Level; 1.96 * SE (N)

*LocalGooseCorrectionFactor*

- **Harvest Year**
  - Winter waterfowl harvest season (recovery period) following spring/summer banding period (e.g., 2005B = 2005-2006 waterfowl season)

- **Harvested in Arkansas (AHY + L)**
  - Number of Canada geese (both adult and juvenile) banded in Arkansas and harvested in Arkansas

- **Harvested in Other State (AHY + L)**
  - Number of Canada geese (both adult and juvenile) banded in Arkansas and harvested in any location outside of Arkansas

- **Total Harvested**
  - Total number of Canada geese harvested in Arkansas and other locations that were originally banded in Arkansas.

- **Proportion AR Resident**
  - Proportion of Canada geese that are Arkansas residents; Proportion AR Resident = (Harvested in Arkansas [AHY + L] / Total Harvested [AHY + L]) * 100

- **Average Annual AR Resident CAGOs**
  - Average annual proportion of Canada geese harvested in Arkansas.

- **STD_Dev**
  - Standard deviation of annual proportion values of Canada geese harvested in Arkansas

- **SE**
  - Standard error of annual proportion values of Canada geese harvested in Arkansas

## References
USGS Bird Banding Laboratory [USGS BBL]. 2021. North American bird banding and band encounter data set. U.S. Geological Survey, Laurel, Maryland, USA.

Veon, J. T. 2025. Evaluating harvest liberalization strategies on population dynamics of southern latitude temperate-breeding Canada geese. Dataset. Zenodo. (https://doi.org/10.5281/zenodo.18027556).

