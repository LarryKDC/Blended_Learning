
# Instruction Data Block
The custom instruction data block allows users to interact with and analyze student performance data on several personalized learning platforms.

#Getting Started

##Usage

##Tables
###Dim and Fact
####Fact
The Instruction_Blended_Fact_v2 table contains the primary set of measures used for evaluating student progress.
* Progress
* Usage
* Mastery
* Alerts

The definitions of these fields varies by platform. See the sub-folder readme files for details descriptions.

####DimStudent
This DimStudent table includes dimension values related to student attributes. All values represent a students **current** status. There is no historical information in this table. For example, the school in the SchoolName field is the school in which the student is currently enrolled.

####Platform Progress
This table is used to define expected progress on a platform. The table contains one record per school per day. It reports the total days in the school year, and the total days to date. Those values are used to calculated expected progress on any given day. The table does not update nightly. It must be manually run at the beginning of each school. If there is a change to the school calendar, the query needs to be run in order to reflect those changes.

The table should be joined on the platform key, date, and school.

###Example Query
``` SQL
SELECT *
FROM [custom].[Instruction_Blended_Fact_v2] [Instruction_Blended_Fact_v2]
INNER JOIN [dw].[DW_dimStudent] [DW_dimStudent] ON ([Instruction_Blended_Fact_v2].[StudentKEY] = [DW_dimStudent].[StudentKEY])
``` 

###Rolling over from the new school year
* Run the platform progress query for the new school year
...

###Implementation Notes


###Questions or Concerns
Contact <datasupport@kippdc.org>
