# Synthea adaptation for New Zealand
Synthea<sup>TM</sup> is a Synthetic Patient Population Simulator modeling the medical history of synthetic patients. The default setup includes all areas of United States. A number of adaptations for other countries have been attempted. This repository is my attempt to adapt it for the population of New Zealand.<br>
Synthea GitHub: https://github.com/synthetichealth/synthea<br>
Synthea International GitHub: https://github.com/synthetichealth/synthea-international<br>

## Data sources
The main source of the input data was the 2018 New Zealand national census, from which a subset of data has been used (input folder).<br>
Source: https://www.stats.govt.nz/topics/census<br>
The list of hospitals was obtained from New Zealand's Ministry of Health.
Source: https://www.health.govt.nz/your-health/services-and-support/certified-providers

## Tools
All processing was conducted in Jupyer Notebook using Google Colab. Python packages used included Pandas and GeoPy. Details of the processing are in the jupyter files: `demographics.ipynb`, `hospitals.ipynb`, `timezones.ipynb` and `zipcodes.ipynb`.

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
GeoPy was also used to produce file `zipcodes.csv`, which include postcodes and geographical coordinates for each area from file `demographics.csv`, as well as `hospitals.csv` which contains locations of hospitals in New Zealand.

## Running in Synthea
In order to run Synthea for the population of New Zealand, follow the following steps. This will generate 10 synthetic patients from New Zealand living in the area of Wellington, location Glendale.
```
git clone https://github.com/synthetichealth/synthea
git clone https://github.com/maciejtarsa/synthea-new-zealand
cd synthea-new-zealand
cp -R nz/* ../synthea
cd ../synthea
./run_synthea -p 10 Wellington Glendale
```
