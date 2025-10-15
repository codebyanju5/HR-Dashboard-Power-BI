# HR Dashboard Project – DAX Measures & Overview

This file contains all the DAX calculations used in the HR Analytics Dashboard in a single block.  
It is ready to be included in a GitHub repository.

```DAX
// Total Employees
TotalEmp = COUNTROWS('HR Analytics Data')

// Employees due for promotion
Due for promotion = IF(
    ISBLANK(CALCULATE([TotalEmp],'HR Analytics Data'[Promotion Status]="Due for promotion")),
    0,
    CALCULATE([TotalEmp],'HR Analytics Data'[Promotion Status]="Due for promotion")
)

// Percentage of employees due for promotion
% Due for promotion = DIVIDE([Due for promotion],[TotalEmp],0)

// Employees not due for promotion
Not due = IF(
    ISBLANK(CALCULATE([TotalEmp],'HR Analytics Data'[Promotion Status]="Not Due")),
    0,
    CALCULATE([TotalEmp],'HR Analytics Data'[Promotion Status]="Not Due")
)

// Percentage of employees not due for promotion
% Not Due for promotion = DIVIDE([Not due],[TotalEmp],0)

// Male employees
Male = CALCULATE([TotalEmp],'HR Analytics Data'[Gender]="male")

// Percentage of male employees
% Male = DIVIDE([Male],[TotalEmp],0)

// Female employees
Female = CALCULATE([TotalEmp],'HR Analytics Data'[Gender]="female")

// Percentage of female employees
% Female = DIVIDE([Female],[TotalEmp],0)

// Employees currently on service
On service = CALCULATE([TotalEmp], 'HR Analytics Data'[Retrenchment status]= "On service")

// Employees who will be retrenched
Will be Retrenched = IF(
    ISBLANK(CALCULATE([TotalEmp],'HR Analytics Data'[Retrenchment status]="Will be retrenched")),
    0,
    CALCULATE([TotalEmp],'HR Analytics Data'[Retrenchment status]="Will be retrenched")
)

## Notes
- All measures reference 'HR Analytics Data'. Change the table name if your dataset is named differently.
- Percentages use DIVIDE() to safely handle division by zero.
- These measures can be used in cards, tables, and charts in Power BI for a complete HR analytics dashboard.
