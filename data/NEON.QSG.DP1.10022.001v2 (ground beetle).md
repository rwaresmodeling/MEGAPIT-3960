# Ground beetles sampled from pitfall traps (DP1.10022.001)

## Measurement
Ground beetles (Coleoptera: Carabidae) and vertebrate bycatch from pitfall traps, counted and identified to species if possible.

## Collection methodology
16oz deli containers with either 150mL or 250mL of propylene glycol are used as NEON pitfall traps. 3 traps are deployed at 10 distributed base plots for 2 weeks at a time throughout the growing season. Traps are located in the East, West, and South regions of the plots 20m from the center. After field collection, samples are sorted in the lab. Invertebrate bycatch is separated and archived. Vertebrate bycatch is identified to species if possible and archived. Carabids are sorted and identified to species if possible and a subset are pinned or pointed. Of those, another subset is sent to an expert taxonomist and/or a DNA barcoding facility.

For information about disturbances, land management activities, and other incidents that may impact data at NEON sites, see the [Site management and event reporting (DP1.10111.001)](https://data.neonscience.org/data-products/DP1.10111.001) data product.

![Image 1](https://raw.githubusercontent.com/NEONScience/NEON-quick-start-guides/9eda564cc095d3c4edfe4e19fe67ab86f4e8b04b/DP1.10022.001/Image1.PNG)  
Example of a distributed base plot with current beetle pitfall sampling location. 
  
## Data package contents
bet_fielddata: Ground beetle metadata on field collection  
bet_expertTaxonomistIDRaw: Ground beetle identifications by expert taxonomists - raw  
bet_bycatchIDHistory: Identification history for beetle bycatch records where identifications have changed  
bet_identificationHistory: Beetle identification history for records where identifications have changed  
bet_expertTaxonomistIDProcessed: Ground beetle identifications by expert taxonomists - desynonomized  
bet_archivepooling: Pitfall samples pooled by NEON technicians  
bet_parataxonomistID: Ground beetle pinning/pointing and identifications by NEON parataxonomists  
bet_sorting: Sorting of field-collected pitfall samples by NEON parataxonomists  
variables: Description and units for each column of data in data tables  
readme: Data product description, issue log, and other metadata about the data product  
validation: Description of data validation applied at the points of collection and ingest  

## Data quality
In the bet_fielddata table, the cupStatus, lidStatus, fluidLevel, and sampleCondition fields indicate the status and condition of collection materials and samples at the time of collection. In the tables containing taxonomic identifications, the identificationQualifier field indicates if there was uncertainty in the identification, and the sampleCondition field indicates the condition of samples at the time of identification. In cases in which identifications have changed over time, records are made in the bet_identificationHistory table.

Please note that quality checks are comprehensive but not exhaustive; therefore, unknown data quality issues may exist. Users are advised to evaluate quality of the data as relevant to the scientific research question being addressed, perform data review and post-processing prior to analysis, and use the data quality information and issue logs included in download packages to aid interpretation.
  
## Table joining
|Table 1|Table 2|Join by field(s)|
|------------------------|------------------------|-------------------------------|
bet_fielddata|bet_sorting|sampleID
bet_sorting|bet_parataxonomistID|subsampleID
bet_sorting|bet_archivepooling|Not fully automatable: multiple subsampleIDs are pooled into subsampleIDList
bet_parataxonomistID|bet_archivepooling|Not fully automatable: multiple subsampleIDs are pooled into subsampleIDList
bet_parataxonomistID|bet_expertTaxonomistIDProcessed|individualID
bet_parataxonomistID|bet_expertTaxonomistIDRaw|individualID
bet_sorting|bet_identificationHistory|identificationHistoryID
bet_parataxonomistID|bet_identificationHistory|identificationHistoryID
bet_expertTaxonomistIDProcessed|bet_identificationHistory|identificationHistoryID
bet_expertTaxonomistIDRaw|bet_identificationHistory|identificationHistoryID
bet_archivepooling|bet_expertTaxonomistIDProcessed|Not fully automatable: multiple subsampleIDs are pooled into subsampleIDList, and multiple individualIDs are in each subsampleID
bet_archivepooling|bet_expertTaxonomistIDRaw|Not fully automatable: multiple subsampleIDs are pooled into subsampleIDList, and multiple individualIDs are in each subsampleID
bet_archivepooling|bet_fielddata|Requires intermediate table: Join via bet\_sorting table using sampleID, subsampleID, and subsampleIDList. See entries for bet\_sorting.
bet_expertTaxonomistIDProcessed|bet_expertTaxonomistIDRaw|individualID
bet_expertTaxonomistIDProcessed|bet_fielddata|Requires intermediate table: Join via bet\_sorting and bet\_parataxonomistID tables.
bet_expertTaxonomistIDProcessed|bet_sorting|Requires intermediate table: Join via the bet_parataxonomistID table.
bet_expertTaxonomistIDRaw|bet_fielddata|Requires intermediate table: Join via bet\_sorting and bet\_parataxonomistID tables.
bet_expertTaxonomistIDRaw|bet_sorting|Requires intermediate table: Join via the bet_parataxonomistID table.
bet_fielddata|bet_parataxonomistID|Requires intermediate table: Join via the bet_sorting table.
  
## Documentation
- [Standard Operating Procedure: CMNH Verification of Data Entry for Identifications](https://data.neonscience.org/api/v0/documents/CMNH-20-002_DataVerifSOP_20201113)  
CMNH-20-002_DataVerifSOP_20201113 | 143.2 KiB | PDF  
- [Processing shipments of specimens for NEON at CMNH](https://data.neonscience.org/api/v0/documents/CMNH_Receiving_SOP)  
CMNH_Receiving_SOP | 40.6 KiB | PDF  
- [Essig Museum of Entomology University of California, Berkeley. Standard Operating Procedures and Protocols for Ground Beetle Morphological Identification and Museum Services. Rev 3.](https://data.neonscience.org/api/v0/documents/ESSIG_carabidtaxonID_SOP2021_Rev3)  
ESSIG_carabidtaxonID_SOP2021_Rev3 | 124 KiB | PDF  
- [TOS Science Design for Ground Beetle Abundance and Diversity](https://data.neonscience.org/api/v0/documents/NEON.DOC.000909vC)  
NEON.DOC.000909vC | 1.1 MiB | PDF  
- [TOS Protocol and Procedure: BET – Ground Beetle Sampling](https://data.neonscience.org/api/v0/documents/NEON.DOC.014050vN)  
NEON.DOC.014050vN | 4.9 MiB | PDF  
- [NEON User Guide to Ground Beetles Sampled from Pitfall Traps (DP1.10022.001)](https://data.neonscience.org/api/v0/documents/NEON_beetle_userGuide_vF)  
NEON_beetle_userGuide_vF | 642.6 KiB | PDF  

For more information on data product documentation, see:  
https://data.neonscience.org/data-products/DP1.10022.001  

## Citation
To cite data from Ground beetles sampled from pitfall traps (DP1.10022.001), see citation here:  
https://data.neonscience.org/data-products/DP1.10022.001  
For general guidance in citing NEON data and documentation, see the citation guidelines page:  
https://www.neonscience.org/data-samples/guidelines-policies/citing  

## Contact Us
NEON welcomes discussion with data users! Reach out with any questions or concerns about NEON data: [Contact Us](https://www.neonscience.org/about/contact-us)
