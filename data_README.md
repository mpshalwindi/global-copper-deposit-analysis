Data
This folder documents every dataset used in the project and how to obtain it. Raw datasets are not
redistributed in this repository where source licences restrict republishing — instead, each source is
linked below so the integrated dataset can be rebuilt exactly. A small sample (sample_data.csv) is
included so the pipeline can be tested without the full downloads.
Datasets at a glance
#
Dataset
Access link
Accessed
Licence / terms
Used in
1
2
3
4
GCDD —
Global Copper
Deposit
Dataset
Mindat
github.com/dawn-a/
Global-copper
deposit-dataset
www.mindat.org ·
OpenMindat API
USGS MRDS mrdata.usgs.gov/
mrds
MED —
Mineral
Evolution
Database
via GCDD Max_age /
Min_age fields
Open access —see repo
licence
Terms restrict bulk copying
—API access only
Public domain (U.S. Gov)
See Golden et al. (2016);
Golden (2019)
RQ1–RQ4
(primary)
RQ1, RQ3
RQ1, RQ2,
RQ4
RQ4 (age
constraints)
1. GCDD — Global Copper Deposit Dataset (primary)
• Download: git clone https://github.com/dawn-a/Global-copper-deposit-dataset.git data/
raw/gcdd (or use the repo’s Code → Download ZIP button)
• Paper: Global Copper Deposit Dataset: A New Open-Source Database for Advanced Data Analysis
and Exploration Targeting, Geoscience Data Journal (2026), doi.org/10.1002/gdj3.70040
• Date accessed:
• Format: CSV / spreadsheet tables in the GitHub repository
• Contents: 1,483 copper deposits worldwide — deposit name, latitude/longitude, genetic type
(porphyry, sediment-hosted, magmatic sulfide, VMS, IOCG), tonnage and grade (Cu, Mo, Au, Ag,
Co, Ni, Pb, Zn), Max_age/Min_age (from MED), quantitative mineral assemblages (IMA-approved
species), plus Mindat_id / Mindat_url links to full locality records.
• Role: backbone dataset; all other sources are merged onto it.
2. Mindat
• Website: www.mindat.org
• Bulk access: OpenMindat API — docs at api.mindat.org/schema/redoc; get an API key via this
guide; Python client: pip install openmindat
• Date accessed:
• Access requirements: free registration + API key
• Terms: mindat.org/terms.php — bulk copying and redistribution of non-trivial portions is not
permitted; query via the API and do not commit raw extracts to this repository.
• Contents: mineral species, localities, and mineral–locality assemblage data used to supplement
GCDD records.

• Role: fills mineralogical fields for RQ1 and RQ3.
3. USGS MRDS — Mineral Resources Data System
• Download: mrdata.usgs.gov/mrds (map interface, search form, KML/shapefile/CSV exports, and
WMS/WFS web services)
• Date accessed:
• Format: CSV / shapefile / KML / OGC web services
• Licence: U.S. Government work — public domain; attribution requested.
• Citation: Mason, G.T. & Arndt, R.E. (1996), Mineral Resources Data System (MRDS), USGS
Data Series 20, doi.org/10.3133/ds20.
• Note: USGS ceased systematic MRDS updates in 2011; it remains the best USGS collection for
locations outside the United States.
• Role: grade–tonnage and occurrence coverage for RQ1, RQ2 and RQ4.
4. MED — Mineral Evolution Database
• Access: no separate public bulk download is available; the metallogenic age constraints curated in
MED are used through the GCDD, which integrates them as the Max_age and Min_age fields.
• References: Golden et al. (2016), Mineral Evolution Database; Golden (2019), The Mineral Evo
lution Database (PhD dissertation, University of Arizona).
• Contents: mineral locality and age information extracted from primary literature and Mindat —
chronometrically constrained occurrences and mineral–locality–age triples.
• Role: temporal constraints for the RQ4 spatio-temporal analysis (metallogenic pulses vs. super
continent cycles).
How to rebuild the integrated dataset
1. Download the GCDD as shown above (MRDS and Mindat records are pulled by the pipeline; set
your Mindat API key as the environment variable MINDAT_API_KEY).
2. Place any manually downloaded raw files in data/raw/ (git-ignored — raw files are not committed
where licences restrict redistribution).
3. Run the integration pipeline:
python src/preprocessing/build_dataset.py
4. The harmonised, analysis-ready dataset is written to data/processed/ together with a merge report
(record counts, fields harmonised, duplicates removed).
Included in this repository
File
Description
sample_data.csv
data_dictionary.md
README.md
Small subset (~ rows) for testing the pipeline without full downloads
Column-by-column definitions, units, and allowed values for the
integrated dataset

Citation
If you use these data, cite the original providers — not this repository:
• GCDD: Global Copper Deposit Dataset, Geoscience Data Journal (2026), doi.org/10.1002/
gdj3.70040
• Mindat: Ralph et al. (2024), mindat.org, Hudson Institute of Mineralogy — www.mindat.org
• USGS MRDS:Mason & Arndt (1996), USGS Data Series 20 — doi.org/10.3133/ds20
• MED:Golden et al. (2016); Golden (2019), University of Arizona
