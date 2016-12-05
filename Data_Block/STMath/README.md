#ST Math
The ST Math data file is uploaded every friday afternoon to an SFTP hosted by ST Math. The files are cumulative from week to week. The raw data from that file is stored in the table custom.instruction_blended_stmath_LJ. The raw data is then transformed and inserted into the Fact table.

##Key Measures
###Progress
The field K_5_Progress is inserted into Instruction_Blended_Fact_v2.Progress1. The field represents the percentage of the grade level objectives the student has completed. It is a cumulative YTD value.

A YTD total to the minutes_logged_last_week field is calculated with each upload and that is inserted into the Progress2 field. This field is then used to calculate efficiency.

Efficiency = Progress1/(Progress2/30). It is the percent progress per half hour made by a student. It is currently being calculated directly in the workbook, rather than in the data source. However, future updates will incorporate it into the mastery field. The Progess2 value will also be replaced with the alt_src_time, but we are waiting on ST Math to confirm some details regarding the values in that field.

###Mastery
The current mastery field is, K_5_Mastery, is not included in any reports and will be replaced with the Efficiency measure.

###Usage
The weekly value of minutes_logged_last_week is instered into the usage field in the fact table.

###Alerts
The alerts field in the fact table is null. 
Has Alerts is a binary (1 or 0) field that is 1 when the cur_hurdle_num_tries from the raw data is greater than 9, otherwise it is 0. 

###Material Grade Level
This is the GCD field from the raw data, is the grade level of the objectives the studen is currently working on. 

##Additional Measures
###Usage Outlier
This is a binary indicator (1 or 0) indicating whether the minutes_logged_last_week is not reporting correctly because the student failed to log out.

###Median Usage
This is the median weekly usage to date of a given students. It is calculated using the set of values in minutes_logged_last_week up to a given report date. When the minutes_logged_last_week is greater than 300, this value is substituted for the primary usage field. This generally occurs when a student fails to log out of ST Math. 
