# Assessment Needs Mapping


Welcome!

This code was originally developed by [Celine Gross](https://github.com/Cece78), [Chris Owen](https://github.com/chowen94) and [Kaj Siebert](https://github.com/kws) at Social Finance as part of a grant funded programme to support Local Authorities to collaborate on data analysis. The programme was called the ‘Front Door Data Collaboration’. It was supported financially by the Christie Foundation and Nesta (through the ‘What Works Centre for Children’s Social Care’). The LAs whose staff guided its development were Bracknell Forest, West Berkshire, Southampton, and Surrey. It also benefitted from advice from the National Performance and Information Managers Group.

We are happy to share this code hoping that others may benefit from a quick way to analyse their CIN Census returns and postcode data to get new insights about the needs present at assessment in their local authority. 

This code is for data analysts from a Local Authority or from another body wishing to analyse CIN Census and Postcode data. Little Python knowledge is required to run this code.
This page may be relevant for you you even if you're not a data analyst: we are presenting some outputs of the analysis further down that may interest you.

You can find more info about Social Finance Digital Labs on our website https://www.sfdl.org.uk/ and our blog https://medium.com/social-finance-uk.



## What does this code do?

**What do the needs identified at assessment look like in my area? Where are there geographic hotspots or pockets of need?**

The assessments understaken by children's services in a local authority to asssess a child's level of need capture whether a range of different types of need are present for that child.
The trends in needs identified in these assessments can paint a picture of the broader needs of the local authority, and by mapping these geographically, it may be able to support a local authority to understand:
- Where are the highest number of children having assessments coming from? How has this changed from the previous year?
- For the most common needs identified at assessment in the local authority, where are these coming from geographically, and how is this changing over time?

Amongst other things, this could support a local authority in making decisions about where to target different early help interventions, or to understand the effectiveness of previous interventions.

## How to run this programme

### Requirements

To run this programme, you will need to:
- Have installed Python and created a conda environment aligned with [requirements.txt](requirements.txt).
- Have run our Annex A and CIN Census cleaner (steps 10, 20 and optional 30) and Logger (step 50) code to get your CIN Census return into a "log" shape suitable for analysis. This code can be found in the FrontDoorDataCollaboration repository. **We advise that you create a log of at least two years of CIN Census data to get a meaningful analysis over time.**
- Have populated the Excel Template contained in this file, 'assessment_postcode_data.xlsx' with Assessment Closure Date, Postcode and CUID for all assessments over the same two year period.
- Download the relevant geographic shapes files and save locally:
    - Postcode latitude and longitude- 'ukpostcodes.zip': https://www.freemaptools.com/download-uk-postcode-lat-lng.htm
    - LSOA boundaries - 'Lower_Layer_Super_Output_Areas_December_2011_Generalised_Clipped__Boundaries_in_England_and_Wales.geojson' 'https://data.gov.uk/dataset/fa883558-22fb-4a1a-8529-cffdee47d500/lower-layer-super-output-area-lsoa-boundaries
    - Local Authority boundaries - 'Local_Authority_Districts_December_2017_Generalised_Clipped_Boundaries_in_United_Kingdom_WGS84.geojson': https://data.gov.uk/dataset/daaafdcc-f7c7-41ff-80eb-b0b15efd1414/local-authority-districts-december-2017-generalised-clipped-boundaries-in-united-kingdom-wgs84

### How to: code

Once that is done, open the assessments_needs_mapping notebook and follow the steps detailed below:
1. **Input required**: define the filepaths to the log, to the postcodes data and to the folder in which the output of the analysis will be downloaded.
2. **Input required**: specify the name of the local authority for whom the analysis is taking place. This will drive the mapping component of the tool
3. Run the rest of the notebook
4. The output of the code is a series of maps of the specified local authority, with accompanying spreadsheets, in case of interest in further exploration of the data. The maps are as follows:
- **Assessment Level** (Data can be found in 'Assessment Prevalence and Change by LSOA.xlsx)
    -**Total Assessments**: Shows the prevalence of assessments by LSOA
    -**Change in Assessments**: Shows the change in volume of assessments from the previous year in absolute terms
- **Risk Factor Level**: These maps will be created for the top 5 risk factors by volume in the past year (Data can be found per Risk Factor, as 'Risk Factor Prevalence and Change by LSOA)
    -**Prevalence of Risk Factor**: Shows the prevalence of assessments where that risk factor was identified
    -**Change in Risk Factor**: Shows the change in prevalence of risk factor from the previous year in absolute terms
- **risk-factors-current-previous**: This Excel Spreadsheet shows the prevalence and change by risk factor across the whole authority. It contains the data used to determine the top 5 risk factors for which maps are made.

You're done!

## Assumptions and Caveats

**Log data** - We are assuming that users have run their CIN Census files through our Annex A and CIN Census cleaner and our Log code generator. This is to ensure typos in column names or in data fields are identified and standardized before we start the analysis.

**Clean data** - The analysis is only as good as the data it is based on. Although running your CIN Census data through the cleaner and Log code might improve its quality, there is a risk that missing and/or incorrect data could get in the way of the analysis (in particular for the events matching process described below).

**Mapping and matching data** - In order to map an assessment and the needs identified, we need to have a postcode. This presents a variety of challenges that may impact on the data displayed:
- If we cannot match an postcode to the assessment using the postcode template provided, it will not be mapped. This tool will only be as good as the postcode data provided, so if a large number of assessments appear to be dropped, look at whether the information put into the template is accurate.
- Postcodes are regularly changing, and so some newer postcodes will not match with the data we are using to plot the needs on a map. If so these assessments will also be dropped. In the tests we have run, this tends to be less than 1% of entries.
- Many authorities, for whatever reason, have postcodes from outside their local authority. To ensure we can create a map of the needs within the local authority, we have excluded assessments where the postcode specified was from outside of the local authority.

**Implications**: All of the above make up relatively small amounts of data, so should have a low impact on the final mapping. Despite this, they are important to remain aware of when considering using this information to inform decision making

**Plotting all needs** - Given the large number of different needs, and the relatively small prevalence of many of them, we have created maps only for the top 5 needs by volume. If there is a desire to plot more needs, this is entirely possible within the code, but more specialised Python knowledge may be required.


## Contributing

We'd be very happy for you to contribute! Head over to [CONTRIBUTING.md](CONTRIBUTING.md) for more information.
      

