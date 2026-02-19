# Litterfall and fine woody debris production and chemistry (DP1.10033.001)

## Measurement
Dry mass in grams of litterfall and fine woody debris functional groups. Functional groups are: leaves, needles, twigs, woody material, flowers, seeds, other (lichen, mosses, other vegetative material) and mixed (unsorted material). Every 5 years, carbon, nitrogen, 13C, 15N, and ‘lignin’ as quantified by the acid detergent method are measured.

## Collection methodology
Litter is collected in elevated 0.5m^2 mesh traps; fine woody debris is collected in 0.5x3m ground traps in the tower airshed. Sites deploy either 1 or 2 pairs of elevated and ground traps at plots with qualifying vegetation. Samples from elevated traps are collected up to 13 times a year, schedule determined by local phenology. Ground traps are collected once per year. Field samples are sorted to functional group, dried, and weighed to the nearest 0.01g (samples <0.01 g recorded as 0.005g). Once every 5 years, subsamples from one bout per functional group are further processed by an external lab for C, N, 13C, 15N, and lignin.  While this timing generally holds true, from 2026-2032 each site was sampled for chemistry on a 6-year interval, see data product Issue Log for more detail. 

For information about disturbances, land management activities, and other incidents that may impact data at NEON sites, see the [Site management and event reporting (DP1.10111.001)](https://data.neonscience.org/data-products/DP1.10111.001) data product.

## Maintenance and calibration
Traps are inspected and serviced or repaired as needed during each collection event. The trapCondition field indicates the state of equipment at the time of collection. Samples are not collected from traps with significant damage.
  
![Image 1](https://raw.githubusercontent.com/NEONScience/NEON-quick-start-guides/409a0494e6edc3fca09a2f3b3c4657638e31bbbb/DP1.10033.001/Image1.jpg)  
An elevated litter trap
  
## Data package contents
ltr_litterLignin: External lab analysis of lignin concentrations in litter  
ltr_fielddata: Field collection details and sample tracking  
ltr_vegetationCover: Cover of qualifying vegetation from AOP survey  
ltr_litterCarbonNitrogen: External lab analysis of carbon and nitrogen concentrations in litter  
ltr_chemistrySubsampling: Identifiers for subsamples created for chemical analyses or archive  
ltr_pertrap: Record of trap establishment, contains date, trap type and location  
lig_externalSummary: Long-term uncertainty values for lignin analysis in plant tissue  
ltr_massdata: Dry mass of litter and fine woody debris components per trap per bout  
bgc_CNiso_externalSummary: Long-term uncertainty values for analysis of carbon and nitrogen concentrations and stable isotopes  
variables: Description and units for each column of data in data tables  
readme: Data product description, issue log, and other metadata about the data product  
validation: Description of data validation applied at the points of collection and ingest  

## Data quality
10% of dry mass samples are re-weighed by a different technician to ensure weights are correct. The massSampleID field is unique to each subsample, but replicates will exist if that subsample was reweighed for a quality check.  This is indicated by a Y in the qaDryMass field in the ltr_massdata table. In the chemical analysis data tables, analytical replicates are indicated by the field analyticalRepNumber.

The trapCondition field in the ltr_fielddata table, and the sampleCondition field in the ltr_massdata table, indicate any noted problems with the condition of the trap or the sample at the time of collection and weighing.

The analytical tables contain quality flags describing any issues that arose during lab analysis of each sample; typically these fields end in QF, for quality flag. See variables and categoricalCodes files for details on these quality flags. Tables containing the word "Summary" in the table name contain lab-specific analytical quality information, such as precision and accuracy for each analyte, based analysis of known standards run as unknowns. 

Please note that quality checks are comprehensive but not exhaustive; therefore, unknown data quality issues may exist. Users are advised to evaluate quality of the data as relevant to the scientific research question being addressed, perform data review and post-processing prior to analysis, and use the data quality information and issue logs included in download packages to aid interpretation.
  
## Standard calculations
For wrapper functions to download data from the API, and functions to merge tabular data files across sites and months, NEON provides the neonUtilities package in R and the neonutilities package in Python. See the [Download and Explore NEON Data](https://www.neonscience.org/resources/learning-hub/tutorials/download-explore-neon-data) tutorial for introductory instructions in both programming languages.

Analytical replicates, indicated by the qaDryMass and analyticalRepNumber fields, should typically be averaged to a single value before proceeding with further analyses. Additionally, if litter carbon and nitrogen were analyzed separately (co2Trapped = N and Y respectively), users may wish to combine these values first before joining to other tables.

Litter production per unit area per unit time can be estimated by summing the masses of all functional groups per trap over the desired period of time, and dividing by the collection area of the trap.
  
## Table joining
|Table 1|Table 2|Join by field(s)|
|------------------------|------------------------|-------------------------------|
ltr_pertrap|ltr_fielddata|trapID
ltr_fielddata|ltr_massdata|fieldSampleID
ltr_massdata|ltr_chemistrySubsampling|Not fully automatable: multiple massSampleIDs are pooled into massSampleIDList
ltr_chemistrySubsampling|ltr_litterCarbonNitrogen|cnSampleID
ltr_chemistrySubsampling|ltr_litterLignin|ligninSampleID
ltr_chemistrySubsampling|ltr_fielddata|Requires intermediate table: join via ltr_massdata table
ltr_fielddata|ltr_litterCarbonNitrogen|Requires intermediate table: join via the ltr\_massdata and ltr\_chemistrySubsampling tables
ltr_fielddata|ltr_litterLignin|Requires intermediate table: join via the ltr\_massdata and ltr\_chemistrySubsampling tables
ltr_litterCarbonNitrogen|ltr_litterLignin|massSampleMixtureID
ltr_litterCarbonNitrogen|ltr_massdata|Requires intermediate table: join via the ltr_chemistrySubsampling table
ltr_litterLignin|ltr_massdata|Requires intermediate table: join via the ltr_chemistrySubsampling table
bgc\_CNiso\_externalSummary|Any other table|Join not recommended. Data resolution does not match other tables.
lig_externalSummary|Any other table|Join not recommended. Data resolution does not match other tables.
ltr_pertrap|Any other table|Direct join not recommended: Data are collected only once at the establishment of each trap location. trapID is the linking variable.
  
## Documentation
- [A & L Great Lakes Laboratories Inc. SOP: Acid Detergent Fiber and Lignin Analysis in Feeds - Filter Bag Technique (for A200 and A200I)](https://data.neonscience.org/api/v0/documents/AndLGreatLakes_ADFLignin_20240201)  
AndLGreatLakes_ADFLignin_20240201 | 5.6 MiB | PDF  
- [TOS Science Design for Plant Biomass and Productivity](https://data.neonscience.org/api/v0/documents/NEON.DOC.000914vC)  
NEON.DOC.000914vC | 2.9 MiB | PDF  
- [TOS Protocol and Procedure: LTR – Litterfall and Fine Woody Debris](https://data.neonscience.org/api/v0/documents/NEON.DOC.001710vJ)  
NEON.DOC.001710vJ | 4.1 MiB | PDF  
- [NEON User Guide to Litter chemical properties and Litter stable isotopes
(DP1.10033.001)](https://data.neonscience.org/api/v0/documents/NEON_LTR_chemIso_userGuide_vF)  
NEON_LTR_chemIso_userGuide_vF | 337.7 KiB | PDF  
- [NEON User Guide to Litterfall and Fine Woody Debris Production and Chemistry (DP1.10033.001)](https://data.neonscience.org/api/v0/documents/NEON_LTR_userGuide_vF)  
NEON_LTR_userGuide_vF | 667.2 KiB | PDF  
- [University of Utah SIRFER Lab Standard Operating Procedure: Methods for NEON vegetation sample receiving, handling, grinding, weighing, encapsulating, and analyzing on IRMS and QC procedures](https://data.neonscience.org/api/v0/documents/UofUtahSIRFER_vegIso_20241001)  
UofUtahSIRFER_vegIso_20241001 | 453.1 KiB | PDF  
- [TOS Design Optimization: Litterfall and Fine Woody Debris](https://data.neonscience.org/api/v0/documents/ltr_OptimizationReport_2019)  
ltr_OptimizationReport_2019 | 305.2 KiB | PDF  

For more information on data product documentation, see:  
https://data.neonscience.org/data-products/DP1.10033.001  

## Citation
To cite data from value: "Litterfall and fine woody debris production and chemistry"
 (DP1.10033.001), see citation here:  
https://data.neonscience.org/data-products/DP1.10033.001  
For general guidance in citing NEON data and documentation, see the citation guidelines page:  
https://www.neonscience.org/data-samples/guidelines-policies/citing  

## Contact Us
NEON welcomes discussion with data users! Reach out with any questions or concerns about NEON data: [Contact Us](https://www.neonscience.org/about/contact-us)
