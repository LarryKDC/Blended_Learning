#ST Math
The ST Math data file is uploaded every friday afternoon to an SFTP hosted by ST Math. The files are cumulative from week to week. The raw data from that file is stored in the table custom.instruction_blended_stmath_LJ. The raw data is then transformed and inserted into the table custom.Instruction_Blended_Fact_v2.

##Key Measures
###Progress
*Progress1:* The field K_5_Progress is inserted into custom.Instruction_Blended_Fact_v2.Progress1. The field represents the percentage of the grade level objectives the student has completed. It is a cumulative YTD value.

*Progress2:* The weekly change in K_5_Progress is calculated by taking the difference in values between the current week and the previous week and is inserted into custom.Instruction_Blended_Fact_v2.Progress2. (Value is the difference between the 2 most recent records and may not reflect the week to week difference if ST Math fails to deliver the file.)

###Mastery
*Mastery:* This value represents the percent progress made per half hour of usage. It is calculated using K_5_Progress (custom.Instruction_Blended_Fact_v2.Progress1) and the field custom.instruction_blended_stmath_LJ.alt_src_time. This field is technically not reflective of mastery, but the K_5_Mastery field provided by ST Math is no longer being used by KIPP DC. 

###Usage
*Usage:* The weekly value of custom.instruction_blended_stmath_LJ.minutes_logged_last_week is instered into the usage field in the table custom.Instruction_Blended_Fact_v2. In this field ST Math does not account for students inactivity or failure to log out, which results in usage values of 1000 minutes or more in a week. If the value si greater than 300 then it is replaced with median usage value for the classroom that week. 

*Alt_Usage:* ST Math provides a cumulative usage value that accounts for inactivity and failure to log out, alt_src_time. This value is used to calculate efficiency (Mastery). A weekly value is calculated in a similar way to weekly progress (so it has the same potential issues) and is inserted in the field Alt_Usage in the fact table.

*Usage_Outlier:* This is a binary field indicating whether the usage time was greater than 300. It is used for reporting purposes to identify students with imputed usage values.

*Usage times reset when the material grade level is changed.

###Alerts
*Alerts:* The alerts field in the fact table is null. 

*Has_Alerts:* Has_Alerts is a binary (1 or 0) field that is 1 when the cur_hurdle_num_tries from the raw data is greater than 9, otherwise it is 0. This field indicates a student that is stuck an objective.

###Material Grade Level
This is the GCD field from the raw data, is the grade level of the objectives the student is currently working on. 
