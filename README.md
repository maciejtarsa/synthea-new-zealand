# Synthea adaptation for New Zealand
Synthea<sup>TM</sup> is a Synthetic Patient Population Simulator modeling the medical history of synthetic patients. The default setup includes all areas of United States. A number of adaptations for other countries have been attempted. This repository is my attempt to adapt it for the population of New Zealand.<br>
Synthea GitHub: https://github.com/synthetichealth/synthea<br>
Synthea International GitHub: https://github.com/synthetichealth/synthea-international<br>

## Data sources
The main source of the input data was the 2018 New Zealand national census, from which a subset of data has been used (input folder).<br>
Source: https://www.stats.govt.nz/topics/census

## Tools
All analysis was conducted in Jupyer Notebook using Google Colab. Python packages used included Pandas and GeoPy.

## Data processing
For adaptation to other countries, Synthea requires a very specific set of files with specific information included. The following files needed adapting:<br><br>
<b>geography</b><br>
- `demographics.csv`
- `timezones.csv`
- `zipcodes.csv`<br>

<b>payers</b><br>
- `insurance_companies.csv`<br>

<b>providers</b><br>
- `hospitals.csv`
- `primary_care_facilities.csv`
- `urgent_care_facilities.csv`

<b>`synthea.properties`</b><br>

Producing the file `demographic.csv` was the most time consuming part. It included agregating together infomrmation from 4 subsets of the census - ethnicity, education level, population, income level. The goal was to combine data to obtain the following per areas of New Zealand: region, estimated population per area and per region, gender split, ethnicity split, age group split, income group split and education level split.<br><br>
As Synthea by default uses USA population, the ethnicity is geared towards the population of the US. This means that some countries would be harder to adapt. For example, the main ethnicities in New Zealand are `European`, `Maori` and `Pacific Islanders`. Within Synthea, `European` would be classed as `White` and both `Maori` and `Pacific Islanders` as `Native`. Some important information about differences between ethnicities could be lost.<br><br>
Obtaining region per area was difficult as I was unable to find a complete list of which area belongs to each region. As a result, I used a package GeoPy, which is capable of producing an address based on a place name - from that address I was able to extract the region name. A number of location couldn't be found, in which case they were classifies as `Area outside`.<br><br>
GeoPy was also used to produce file `zipcodes.csv`, which include postcode and geographical coordinates for each area from file `demographics.csv`
