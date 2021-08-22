# Synthea adaptation for New Zealand
Synthea<sup>TM</sup> is a Synthetic Patient Population Simulator modeling the medical history of synthetic patients. The default setup includes all areas of United States. A number of adaptations for other countries have been attempted. This repository is my attempt to adapt it for the population of New Zealand.<br>
Synthea GitHub: https://github.com/synthetichealth/synthea<br>
Synthea International GitHub: https://github.com/synthetichealth/synthea-international<br>

## Data sources
The main source of the input data was the 2018 New Zealand national census, from which a subset of data has been used (input folder).<br>
Source: https://www.stats.govt.nz/topics/census

## Tools
All analysis was conducted in Jupyer Notebook using Google Colab. Python packages used included Pandas and GeoPy.

## Data preprocessing
Synthea requires a very specific set of files with specific information included. The following files needed adapting:<br>
<b>geography</b><br>
- demographics.csv
- timezones.csv
- zipcodes.csv<br>

<b>payers</b><br>
- insurance_companies.csv<br>

<b>providers</b><br>
- hospitals.csv
- primary_care_facilities.csv
- urgent_care_facilities.csv

<b>synthea.properties</b><br>

Producing the file demographic.csv was the most time consuming part. It included agregating together infomrmation from 4 subsets of the census - ethnicity, education level, population, income level. The goal was to combine data to obtain the following per areas of New Zealand: region, estimated population per area and per region, gender split, ethnicity percentages, age group percentages, income group percentages and education level percentages.<br><br>
Obtaining region per area was difficult as I was unable to find a complete list of which area belongs to each region. As a result, I used a package GeoPy, which is capable of producing an address based on a place name - from that address I was able to extract the region name.<br><br>
GeoPy was also used to produce file zipcodes.csv, which include postcode and geographical coordinated for each area from file demographics.csv
