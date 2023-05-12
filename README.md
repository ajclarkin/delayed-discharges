# delayed-discharges
Code for looking at the proportion and number of patients who are discharged directly home from Critical Care.

No patient identifiable information is stored.


### Exporting Data from WardWatcher
Data comes from WardWatcher. The initial search should be for the year in question. To add additional months just search for that data and it will be added to the main data file with rudimentary de-duplication.

Search for patients discharged between the first and last day of analysis period. For example 01/05/2022 to 31/05/2022. Date searches are inclusive. Once the patient list has been found export it using a quick report with the following columns:
- Discharged on (date)
- Discharged at (time)
- Gap between ready & discharge (mins)
- Destination (type)
- Destination (name)
- Reason discharged
- Date ready for discharge
- Time ready for discharge
- Date admitted to this unit
- Time admitted to this unit

Save this file as tab-separated to the data_raw folder. (CSV would also work. For other exports in WW it doesn't because it does not apply quotes correctly if the field contains a comma. Annoying.)


### Import Data
This uses ImportUnified.Rmd. It reads in the exported data and then adds it to data_processed/data.csv This supersedes ImportDischargeData.Rmd and ImportDelayData.Rmd.

Edit the *imports* chunk and set `filename_in = ` to the new data file. Then run the script.



### Generate the Report
Run GenerateReport.Rmd and this will take the most recent 12 months of data from data_processed/data.csv and create the report. Chart labels are updated automatically.

The charts showing percentage of patients discharged going home and count of patients going home are exported to images/ as rate.jpg and count.jpg (prepended with latest year-month).


## Delay Data
This looks at the delays between ready for discharge and discharge. This uses the same data source built from ImportUnified.Rmd and generates a pdf report.

Files:
- ImportUnified.Rmd
- DelaysReport.Rmd

 
