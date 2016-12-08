
# Instruction Data Block
The custom instruction data block allows users to interact with and analyze student performance data on several personalized learning platforms.

##Getting Started

###Usage

###Tables
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
This table is used to define exprected progress on ST Math. Students should complete 100% of their grade level objectives by the end of the school year. The table contains one record per school per day. It reports the total days in the school year, and the total days to date. Those values are used to calculated expected progress on any given day.

###Example Query
``` SQL
SELECT *
FROM [custom].[Instruction_Blended_Fact_v2] [Instruction_Blended_Fact_v2]
INNER JOIN [dw].[DW_dimStudent] [DW_dimStudent] ON ([Instruction_Blended_Fact_v2].[StudentKEY] = [DW_dimStudent].[StudentKEY])
``` 

###Rolling over from the new school year

...

###Implementation Notes


###Questions or Concerns
Contact <datasupport@kippdc.org>
