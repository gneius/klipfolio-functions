Klipfolio Formula Functions Reference
----------------------------

The reference guide table includes a categorized list of all the functions and their details. Klipfolio functions are separated into the following categories: Data Manipulation, Logic, Math, Text, Date/Time, and Statistics.

The purpose of each function is described along with information on how to use them. To help you find the function you're looking for, use CTRL+F  or Command+F to search keywords like "align data".

### Details 

#### ARRAY

Use ARRAY to join together single values and return them as a single list of data in the order provided.

**Syntax and Parameters**: `ARRAY ( data  )`

`data`: The values to join together including strings or columns of data from different data sources.

**When to use this function**: To combine data from multiple sources, such as data sources and results references.

**Example**:

Uses the _Example: Live Sales Data_ data source

`ARRAY ( @Customer Contact, @Sales Rep )` 

The result of this formula returns a single list as a combination of values in both columns.

In this example ARRAY is used to add the value, "Exception" to the list of data.

`ARRAY ("Exception", @Customer Type)`

The result of this formula returns: Exception, Direct Billed, Customer, Distributor, Partner, Reseller

#### BLANK

Use BLANK to return one blank value or a specified number of blank values.

**Syntax and Parameters**: `BLANK ( [count] )`

`count`: \[optional\] The number of blank items to be returned. Negative numbers are treated as positives. The maximum number for the count parameter is 1000000.

**When to use this function**: To replace a blank with a non-blank.

**Example**:

`BLANK(5)`

The result of this formula returns 5 blank values.

Uses the _Example: Live Sales Data_ data source

In this example BLANK is used to replace the 0s in the Qty column with "No value"

`REPLACE(@Qty, BLANK(), "No value")`

The result of this formula returns the data in the Qty column with all blanks replaced with: No value.

#### COUNTDISTINCT

Use COUNTDISTINCT to count the number of unique items in each group. The results are returned in alphabetical order and aligned with the results of the GROUP function.

**Syntax and Parameters**: `COUNTDISTINCT ( values )`

`values`: A list of 1 or more values.

**Related functions:**

*   [GROUP](#GROUP)
*   [GROUPBY](#GROUPBY)

**When to use this function:** To aggregate data according to specified groups.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example COUNTDISTINCT is used to count how many instances of US, Canada, and Mexico are in the Country column.

`COUNTDISTINCT (@Country)`

The result of this formula returns: 362, 87, 283.

**Note**: You can also use the Group and Aggregate actions to return results similar to COUNTDISTINCT. Actions are available in the Klip Editor. [Learn more about the actions menu.](/hc/en-us/articles/222017088)

**Learn more**:

*   [GROUP, GROUPBY, and COUNTDISTINCT](https://support.klipfolio.com/hc/en-us/articles/215547998)

#### DATASOURCE

Use the DATASOURCE function to indirectly refer to a data source field, by specifying the datasource ID (a unique 32-digit hexadecimal identifier) and a pointer to the field in the datasource.

**Syntax and Parameters**: `DATASOURCE ( datasource_id, pointer )`

`datasource_id:` A data source identifier, typed as a literal string.

`pointer:` A reference to a field (column, cell, or XPath) in the data source, typed as a literal string.

**When to use this function**: To access a specific sheet name in an Excel/Google workbook where the sheet name is indicated by a variable or to access a specific XPath in a JSON/XML datasource that is inaccessible by XPath manipulation.

**Example**:

In this example, the values in column B of the data source specified is returned.

`DATASOURCE("7883812ca90512b23668d0ac2be4a245","B:B")`

The result of this formula is the list of Products in column B.

**Note**: The DATASOURCE function is used with raw data sources and not modelled data sources. 

**Learn more:**

*   [DATASOURCE function](https://support.klipfolio.com/hc/en-us/articles/216182577)
*   [Klips: Where do I find IDs for Dashboards, Klips and data sources?](https://support.klipfolio.com/hc/en-us/articles/115002121008) and [PowerMetrics: Where do I find my data source ID number?](https://support.klipfolio.com/hc/en-us/articles/360053647153-PowerMetrics-Where-do-I-find-my-data-source-ID-number-)

#### GROUP

Use GROUP to group data into unique instances and hide duplicate values. The results are returned in alphabetical order.

**Syntax and Parameters**: `GROUP ( values )`

`values`: A list of 1 or more values

**Related functions:**

*   [COUNTDISTINCT](#COUNTDISTINCT)
*   [GROUPBY](#GROUPBY)

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, all repeating values are grouped into one instance.

`GROUP (@Country)`

The result of this formula is Canada, Mexico, and US.

**Note**: You can also use the Group action to return the same results as GROUP. Actions are available in the Klip Editor. [Learn more about the actions menu.](/hc/en-us/articles/222017088)

**Learn more**:

*   [GROUP, GROUPBY, and COUNTDISTINCT](https://support.klipfolio.com/hc/en-us/articles/215547998)

#### GROUPBY

Use GROUPBY to return values based on a specified aggregation method so that the unique values align with a parallel column.

**Syntax and Parameters**: `GROUPBY (values, measure, [method])`

`values:` A list of 1 or more values.

`measure:` A list of 1 or more values. Values and measure must have the same number of items.

`method:`\[optional\] The aggregation method to use when grouping. The default method is SUM.

**Related functions:**

*   [COUNTDISTINCT](#COUNTDISTINCT)
*   [GROUP](#GROUP)

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, the result of the formula sums the total number of days of activity per country.

`GROUPBY(@Country, @Days of Activity)`

The result of this formula returns: 5,270, 796, 3,895. The result is returned in the order the Country column is grouped in.

**Note**: You can also use the Group action to return results similar to GROUP and GROUPBY. Actions are available in the Klip Editor. [Learn more about the actions menu.](/hc/en-us/articles/222017088)

**More examples**:

Uses the _Example: Live Sales Data_ data source

GROUPBY can be used to format your data as a comma separated list.

`GROUPBY(@Sales Rep, @Days of Activity, Join)`

The result of this formula returns the days of activity associated to each Sales Rep (Ahmed Arthurs) in a comma separated list. The first ten values of the comma separated list for Ahmed Arthurs are:

5.0,13.0,14.0,17.0,14.0,30.0,12.0,23.0,10.0,6.0

**Note**: To see the comma separated list in your Klip, use the **Properties** panel to set the Data **Format as** Text.

**Learn more**:

*   [GROUP, GROUPBY, and COUNTDISTINCT](https://support.klipfolio.com/hc/en-us/articles/215547998)

#### FIRST

Use FIRST to return the first values in a list of data where the number of values is specified by the count parameter.

**Syntax and Parameters**: `FIRST( values , [count] )`

`values:` A list of 1 or more items.

`count:` \[optional\] The number of items to return from the data.

**Examples**:

Uses the _Example: Live Sales Data_ data source

`FIRST(@Company Name)`

The result of this formula is the first value in the Company Name column: ADVANCE communications.

`FIRST(@Company Name, 5)`

The result of this formula is the first five values of the Company Name column: ADVANCE communications, Nakamesh Import Consortium, Salamander Syndicate, Hahne-Kedar, Accelerant Investments.

**Note**: If the value of the count parameter is greater than the number of items in the column, all items will be returned. If the data is grouped and there are fewer unique values than the value of the count parameter, only the number of unique values will be returned.

#### LAST

Use LAST to return the last values in a list of data where the number of values is specified by the count parameter.

**Syntax and Parameters**: `LAST( values , [count] )`

`values:` A list of 1 or more values.

`count:` \[optional\] The number of items to return from the data.

**Examples**:

Uses the _Example: Live Sales Data_ data source

`LAST(@Company Name)`

The result of this formula is the last value in the Company Name column: Hahne Kader.

`LAST(@Company Name, 5)`

The result of this formula is the last five values of the Company Name column: Janus, Ltd., Pacific Export Company, Bamberly Trust Corporation, Bamberly Trust Corporation, Hahne-Kedar

**Note**: If the value of the count parameter is greater than the number of items in the column, all items will be returned. If the data is grouped and there are fewer unique values than the value of the count parameter, only the number of unique values will be returned.

#### LOOKUP

Use LOOKUP to correlate data between two data sources. For each **input** item, search for the first match in **keys** and return the value at the corresponding position in **results**. If there is no match, a blank is returned.

**Syntax and Parameters**: `LOOKUP(input, keys, results)`

`input:` A list of 1 or more items.

`keys:` A list of 1 or more items that intersects with the input list.

`results:` A list of 1 or more items from the same source as keys. Must contain the same number of items as keys.

**When to use this function**: To correlate data between data sources and to align data across sub-components (for example, in a Bar/Line chart to align a series with the X-axis).

**Example**:

Uses the _Example: Live Sales Data_ data source and _Example: Product Data_ data source

In this example, the first data source, Example: Live Sales Data is the primary data source and Example: Product Data is the secondary data source. Both data sources contain the same Product column. The intersecting Product column is used as a guide to align the data in the primary and secondary data sources.

`LOOKUP (@Product, @Product, @Shipping Location)`

The result of this formula returns the data in the Shipping Location column from the secondary data source aligned with the data in the Product column and additional columns in the primary data source.

**Related Links:**

*   [LOOKUP function](https://support.klipfolio.com/hc/en-us/articles/216182777)
*   [How do I align data using the LOOKUP function?](https://support.klipfolio.com/hc/en-us/articles/215548148)

#### MAP/MAPFLAT

Use MAPFLAT/MAP to repeat a formula or datasource reference (specified by the **formula** parameter) for each value in the **values** parameter.

**Syntax and Parameters**: `MAPFLAT( values, variable name, formula)`

`values:` A list of 1 or more values.

`variable name:` Name of the variable used in the formula parameter, typed as a literal string.

`formula:` Formula which uses variable name (entered as a $variable) and is executed for each item in values. If the formula returns more than 1 item, only the first value is returned.

**When to use this function**: To aggregate data over a set of account IDs by repeating a reference to a dynamic datasource where the account ID is passed in as a variable.

**Note**: We recommend using MAPFLAT rather than MAP because MAPFLAT supports returning multiple items per first parameter while MAP returns only 1 item (if the formula returns >1 item, only the first item is returned).

**Learn more**:

*   [MAPFLAT and MAP](https://support.klipfolio.com/hc/en-us/articles/216182487)

#### PADVALUES

Use PADVALUES to return selected values with padding or additional values at the end of the data.

**Syntax and Parameters**: `PADVALUES ( values, times, [with value] )`

`values:` A list of 1 or more items.

`times:` The number of values to add to the data in the values parameter. The maximum number is 1000000.

`with value`: \[optional\] The value to add. If not specified, values are padded with blanks.

**When to use this function:** To make two lists of data the same size and to ensure data alignment.

**Example**:

Uses _Example: Product Data_ data source

`PADVALUES(@Billing, 4, "None")`

This formula adds "None" four times to the end of the Billing column.

**More examples**:

In this example the difference between the number of values in column B and column C is used as the amount of values to pad column C with. 

`PADVALUES (@C:C, COUNTALL(@B:B)-COUNTALL(@C:C))`

**Note**: This example uses a raw data source because modelled data source columns do not require padding.

#### REPEAT

Use REPEAT to replicate one or more values and return a list containing the number of copies specified.

**Syntax and Parameters**: `REPEAT (values, times)`

`values:` A list of 1 or more items.

`times:` The number of times to repeat the values. If less than or equal to 0, 0 items are returned. The maximum number of times is 1000000.

**Example**:

`REPEAT``("Canada", 3)`

The result of this formula is Canada, Canada, Canada

**More examples**:

Uses the _Example: Live Sales Data_ data source

This example uses a Bar/Line chart. For the Series sub-component, the average Revenue value is repeated to create a target line. The number of times the average Revenue value is repeated is calculated using COUNT to count the amount of values on the X-Axis. 

`REPEAT(AVERAGE(@Revenue), COUNT (!X Axis)`

The result of this formula is a target line on your Bar/Line chart.

#### REPLACE

Use REPLACE to replace items that match a specified value with another value.

**Syntax and Parameters**: `REPLACE( values, matching, [with value] )`

`values:` A list of 1 or more values.

`matching:` A list of 1 or more values to be replaced.

`with value:` \[optional\]

**Example**:

In this example, all values matching "US" in the Country column are replaced with "USA".

`REPLACE(@Country,"US","USA")`

Uses the _Example: Live Sales Data_ data source

This example shows a nested replace where all values matching "US" in the Country column are replaced with "USA" and all values matching "Canada" in the Country column are replaced with "CA".

`REPLACE(REPLACE(@Country, "US","USA"),"Canada","CA")`

#### REVERSE

Use REVERSE to reverse the order of a list of values.

**Syntax and Parameters**: `REVERSE( values )`

`values:` A list of 1 or more values.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, all the values in the Date column are returned in the reverse order.

`REVERSE(@Date)` 

In this example, SLICE specifies that REVERSE should only be applied to the last 12 items in the Date column.

`REVERSE(SLICE(@Date, -12))`

#### SELECT

Use SELECT to select values from a list according to specified criteria.

**Syntax and Parameters**: `SELECT ( data, condition )`

`data:` A list of 1 or more items.

`condition:` A list of true and false values, typically a formula which combines 1 or more Logic functions. Data and condition must have the same number of items.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example returns the value from the Product column when the value in Customer Type contains "Distributor".

`SELECT(@Product, @Customer Type="Distributor")`

The first ten results of this formula are Bread, Bread, Eggs, Bread, Milk, Milk, Eggs, Milk, Butter, Butter.

**Learn more**:

*   [SELECT](https://support.klipfolio.com/hc/en-us/articles/216182567)

#### SET

Use SET to assign the values listed in the second parameter to the variables listed in the first parameter.

**Syntax and Parameters**: `SET ( variable names, values,` `expression )`

`variable names:` 1 or more variable names, typed as literal strings (must be the same number as values parameter).

`values:` A list of 1 or more items.

`expression:` Data source reference or a formula which uses variable names (entered as variables).

**When to use this function**: assign values for dynamic datasources that have multiple variables.

**Learn more**:

*   [SET](https://support.klipfolio.com/hc/en-us/articles/215547598)

#### SLICE

Use the SLICE function to return the subset of values between the start and end positions. If start and end parameters are not specified the first row is removed.

**Syntax and Parameters**: `SLICE ( values, [start] ,` `[end])`

`values:` A list of 1 or more items.

`start:` \[optional\] Indicates the number of items sliced off the top.

`end:` \[optional\] Indicates the position of the last item to be returned.

**When to use this function**: Often used to remove row headers from data.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, the first row of data is removed from the Product column.

`SLICE ( @Product )`

In this example, the subset of values between row 1 and 6 are returned.

`SLICE( @Product, 1, 6 )`

The result of this formula is Milk, Milk, Bread, Eggs, Eggs

**Note:** If start and end parameters contain negative values, values are returned from the end of the list.

#### SORT

Use the SORT function to sort values according to the specified order.

**Syntax and Parameters**: `SORT ( values, type,` `[return values])`

`values:` A list of 1 or more values.

`type:` The sort order. Choose between: ascending, ascending numeric, descending, or descending numeric.

`return values:` \[optional\] A list of 1 or more values that corresponds to the values parameter.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, the Qty column is returned in descending numeric order.

`SORT ( @Qty, descending numeric )`

The result of this formula returns the values in the Qty column descending from 15.

**Note**: You can also use the Sort action to return results similar to SORT. Actions are available in the Klip Editor. [Learn more about the actions menu.](/hc/en-us/articles/222017088)

#### SPLICE

Use the SPLICE function to return the values in the values parameter but delete the number of values specified in the count parameter from the position specified in the index parameter. Optionally inserts the value in the insert parameter at index

**Syntax and Parameters**: `SPLICE ( values, index, count,``[insert])`

`values:` A list of 2 or more values.

`index:` Position in the array to begin the splice.

`count:` Number of values to delete.

`insert:` \[optional\] Value to insert.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example returns the values in the Sales Rep column with one value from position 5 (which is row 6, because row 1 is counted as 0), Tyrell Turek, removed and the value Mariam Rama added to the same position.

`SPLICE(@Sales Rep, 5 , 1 , "Mariam Rama")`

The first ten results of this formula are: Renaldo Recore, Wendell Wark, Jeffry Jarrett, Virgil Valenti, Ahmed Arthurs, Mariam Rama, Wendell Wark, Phil Phung, Virgil Valenti, Carmine Carman

#### TRIM

Use the TRIM function to remove the values specified in the pattern parameter or to remove all blank values if no pattern is provided.

**Syntax and Parameters**: `TRIM ( values,` `[pattern] )`

`values:` A list of 1 or more values.

`pattern:` \[optional\] 1 or more items to be removed.

**Example**:

Uses _Example: Product Data_ data source

This example removes all blank values from the Shipping location column.

`TRIM(@Shipping location)`

Uses the _Example: Live Sales Data_ data source

This example removes Milk from the Product column.

`TRIM(@Product, "Milk")`

**Note:** The pattern parameter is case sensitive.

Logic
-----

### Function

### Details 

####   AND

Use AND to return the results of conditions. Returns true if a condition is true, otherwise returns false. The AND function tests each value in the condition.

**Syntax and Parameters**: `AND ( condition )`

`condition`: 1 or more values to test.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, the formula returns true for every row of data that matches all three conditions in the formula.

`AND(@Customer Type="Distributor", @Price Base="3.04", @Price Retail="4.79")`

The first five results of this formula are true, false, false, false, false.

**More examples**:

Uses the _Example: Live Sales Data_ data source

AND is often used with SELECT to return values from a specified list when multiple conditions are true. In this example, the value in the Customer Type column is returned when the corresponding Country column has the value of Canada and when the corresponding Price Base column has a value of 2.34.

`SELECT( @Customer Type, AND( @Country= "Canada", @Price Base= "2.34" ))`

The first ten rows of data return Distributor, Distributor, Distributor, Distributor, Distributor, Distributor, Direct Customer, Reseller, Distributor, Reseller.

####   BETWEEN

Use BETWEEN to return true or false if a value is numerically between a (inclusive) start and end.

**Syntax and Parameters**: `BETWEEN ( values, start, end  )`

`values`: A list of 1 or more numeric items.

`start`: Numeric start of range.

`end`: Numeric end of range.

**When to use this function**: To determine if a list of dates falls within a specific date range (all dates must be in Unix time format).

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, the formula returns true if the number of active days are between 5 and 25 and false if they are not.

`BETWEEN(@Days of Activity, 5, 25)`

The first ten results of data return false, false, false, true, true, false, true, true, false, false.

**More examples**:

Uses the _Example: Live Sales Data_ data source

In this example, the values in Company Names are displayed if the corresponding dates fall between the start and end of the current month.

`SELECT(@Company Name ,(BETWEEN( DATE( @Date, "yyyy-MM-dd hh:mm:ss" ) , DATE_STARTOF( TODAY(), month), (DATE_ENDOF( TODAY(), month) ))))`

**Note**: The DATE function is used to convert the dates to Unix Time format, enabling DATE\_STARTOF, TODAY, and DATE\_ENDOF to accurately recognize the dates.

####   IF

Use IF to test a condition and specify the result of the condition if it evaluates to true or false.

**Syntax and Parameters**: `IF` `( condition , if true , if false )`

`condition`: A list of 1 or more values to test.

`if true`: Data returned if the condition is true.

`if false`: Data returned if the condition is false.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example returns the value for the Company Name column if the corresponding value in the Country column is Canada. If the Country value is not Canada, the formula returns a blank value.

`IF(@Country="Canada",@Company Name, BLANK())`

**More examples**:

Uses the _Example: Live Sales Data_ data source

In this example IF is used to establish a true and false condition. AND is used to create a statement with multiple conditions. This statement is saying if the dates from the Date column fall in the last year and the Customer Type column lists that date as having a customer that is a Direct Customer, then return the Revenue value. If these conditions are not met, return 0.

`IF(AND(DATE_IN(DATE(@Date, "yyyy-MM-dd HH:mm:ss"),year,-1),@Customer Type="Direct Customer"),@Revenue, 0)`

The first ten results of this formula are 0, 0, 27.81, 0, 18.32, 0, 0, 10.85, 0, 0.

**Note**: It is strongly recommended to only nest up to two IF formulas. If more conditions are needed, use SWITCH or SELECT instead.

**Related links:**

*   [How do I align data using the IF function?](https://support.klipfolio.com/hc/en-us/articles/216182997)

####   IN

Use IN to return true or false to determine whether the values are present in the set parameter.

**Syntax and Parameters**: `IN ( values, set )`

`values`: A list of 1 or more values.

`set`: A list of 1 or more values.

**Example**:

Uses the _Example: Live Sales Data_ data source

`IN (@Sales Rep, "Ahmed Arthurs")`

The first ten values return as true, false, false, true, false, false, false, true, false, false.

####   NOT

Use NOT to reverse the logical value of each item in values (false returns as true and true returns as false).

**Syntax and Parameters**: `NOT ( values )`

`values`: A list of 1 or more values that evaluates to true or false.

**Example**:

Uses the _Example: Live Sales Data_ data source

`NOT(@Sales Rep="Ahmed Arthurs")`

The result of this formula returns true for every instance in Sales Rep that does not contain Ahmed Arthurs and false for every instance that does contain Ahmed Arthurs.

####   OR

For each condition, returns true if at least one of the conditions is true and returns false if none of the conditions are true.

**Syntax and Parameters**: `OR (condition )`

`condition`: A list of 1 or more true/false values, typically the result of a comparison or formula.

**Example**:

In this example, the formula returns true if at least one of the conditions is met and false if both conditions are not met.

`OR(@Customer Type="Distributor", @Country="Mexico")`

The result of this formula true, false, true, true, true, true, false, true, true, true.

####   SWITCH

Use SWITCH to switch a value to another value based on whether the case is evaluated to be true. If no match is found null is returned.

**Syntax and Parameters**: `SWITCH (` `data, case, values,[case, value],[“_default_”,value])`

`data`: A list of 1 or more values.

`case`: The condition to be evaluated as either true or false.

`values`: The value to be returned if the case is true.

**Note:** `case` and `value` can be repeated as many times as necessary to cover all conditions.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula changes the data in the Product column based on three switch statements. All instances of Bread are switched to BREAD, all instances of Milk are reversed using the TEXT\_REVERSE function, all instances of Eggs are changed to the number 3, and nothing is returned for Cheese because it does not exist in the Product column.

`SWITCH(@Product,"Bread","BREAD","Milk",TEXT_REVERSE("Milk"),"Eggs","3","Cheese","2")`

The first five results of this formula are BREAD, kliM, kliM, BREAD, 3.

**NOTE:** Specify `_default_` to assign a default function to be performed if no other cases match.

Math
----

### Function

### Details 

#### ABS

Use the ABS function to calculate the absolute (positive) value of all numeric values in a range of data. Returns 0 for non-numeric values and blank values.

**Syntax and Parameters**:

`ABS (data )`

`data`: A list of 1 or more values

**Example**:

`ABS (-4)` 

This formula returns the absolute value of -4: 4

#### AVERAGE

Use the AVERAGE function to return the average of all numeric items. Non-numeric and blank items are ignored.

**Syntax and Parameters**:

`AVERAGE (data )`

`data`: A list of 1 or more values to find the average of.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula calculates the average amount of days active.

`AVERAGE(@Days of Activity)`

The result of this formula returns: 13.2238 

**Note**: You can use the **Properties** panel to set the **Decimal Places**.

#### AVERAGEIF

Use the AVERAGEIF function to return the average of all numeric items in the average range parameter corresponding to a true value in a condition.

**Syntax and Parameters**: `AVERAGEIF (condition, average range )`

`condition`: A list of 1 or more true/false values.

`average range`: A list of 1 or more numeric items. Non-numeric values return as 0.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula calculates the average Revenue value for each time the Product column contained Milk.

`AVERAGEIF(@Product="Milk",@Revenue)`

The result of this formula returns: 27.488 

**Note**: You can use the **Properties** panel to set the **Decimal Places**.

#### CEILING

Use CEILING to round numbers up to the nearest multiple of significance. Non-numeric values return as 0.

**Syntax and Parameters**: `CEILING ( data, significance )`

`data`: A list of 1 or more values to round up.

`significance`: \[optional\] The multiple to round up to.

**Example**:

`CEILING ( -2.5 )` 

This formula returns -2.5 rounded up: -2

#### COUNT

Use COUNT to return a count of all non-blank (numeric and text) items in data.

**Syntax and Parameters**: `COUNT ( data )`

`data`: A list of 1 or more items.

**Example:**

Uses _Example: Product Data_ data source

In this example the number of shipments is calculated by the COUNT of the values in the Shipping location column of data.

`COUNT ( @Shipping location )` 

This formula returns: 754

#### COUNTALL

Use COUNTALL to count all numbers, text, and blank values and return the count as a single value.

**Syntax and Parameters**: `COUNTALL ( data )`

`data`: A list of 1 or more items.

**Example:**

Uses _Example: Product Data_ data source

In this example all values in the Shipping location column of data are counted, including blank values.

`COUNTALL ( @Shipping location )` 

This formula returns: 784

#### COUNTBLANK

Use COUNTBLANK to count all blank values and return the count as a single value.

**Syntax and Parameters**: `COUNTBLANK ( data )`

`data`: A list of 1 or more items.

**Example:**

Uses _Example: Product Data_ data source

In this example all blank values in the Shipping location column of data are counted.

`COUNTBLANK ( @Shipping location )` 

This formula returns: 30

#### COUNTIF

Use COUNTIF to test each value in a condition and count the true results of the condition.

**Syntax and Parameters**: `COUNTIF ( condition )`

`condition`: A list of true and false values.

**Example:** 

Uses _Example: Product Data_ data source

This example counts the number of shipments that are from the warehouse.

`COUNTIF ( @Shipping location="warehouse" )` 

This formula returns: 30

#### COUNTNUMERIC

Use COUNTNUMERIC to count all the numeric values in a list of data.

**Syntax and Parameters**: `COUNTNUMERIC ( data  )`

`data`: A list of 1 or more items.

**Example**:

Uses _Example: Product Data_ data source

This example counts the numeric values in the Units column of data and does not include the text value "none" in the count.

`COUNTNUMERIC( @Units )` 

This formula returns: 667

#### CUMULATIVE

Use CUMULATIVE to calculate the cumulative sums in a list of numeric data.

**Syntax and Parameters**: `CUMULATIVE ( data  )`

`data`: A list of 1 or more numeric items.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example the values in the Qty column are summed after each row of data.

`CUMULATIVE ( @Qty )` 

The first ten results of this formula are: 10, 22, 31, 34, 38, 43, 55, 60, 66, 80

#### CUMULATIVE\_DIFFERENCE

Use CUMULATIVE\_DIFFERENCE to calculate the difference between the current and previous values from a list of values.

**Syntax and Parameters**: `CUMULATIVE_DIFFERENCE ( data,` `first value )`

`data`: A list of 1 or more numeric items.

`first value`: Specify the way the first value should be treated by choosing one of the options below:

*   `Ignore first value (default)`: Ignores the first value and returns the first cumulative difference as the first value.
*   `Use first value`: Returns the first value in the data and then returns the cumulative difference from the first value.
*   `Use zero`: Returns zero as the first value.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example the values in the Qty column are summed after each row of data.

`CUMULATIVE_DIFFERENCE ( @Qty, Ignore first value )` 

The first ten results of this formula are: 2, -3,-6,1,1,7,-7,1,8,1

#### FLOOR

Use FLOOR to round numbers down to the nearest multiple of significance. Non-numeric values return as 0.

**Syntax and Parameters**: `FLOOR ( data )`

`data`: A list of 1 or more values to round down.

`significance`: \[optional\] The multiple to round down to.

**Example**:

`FLOOR ( -2.5 )` 

This formula returns -2.5 rounded up: -3

####  MAX

Use MAX to return the maximum value from a list of numeric values.

**Syntax and Parameters**: `MAX ( value  )`

`value`: A list of 1 or more numeric values.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula calculates the maximum number of days active from the Days of Activity column of data.

`MAX( @Days of Activity )` 

The result of this formula is 30.

####  MEDIAN

Use MEDIAN to return the middle value from a list of numeric values.

**Syntax and Parameters**: `MEDIAN ( value  )`

`value`: A list of 1 or more numeric values.

**Example**:

Uses the _Example: Live Sales Data_ data source

`MEDIAN ( @Days of Activity )` 

This formula returns the maximum number of days active: 13 

#### MIN

Use MIN to return the minimum value from a list of numeric values.

**Syntax and Parameters**: `MIN ( value  )`

`value`: A list of 1 or more numeric values.

**Example**:

Uses the _Example: Live Sales Data_ data source

`MIN ( @Days of Activity )` 

This formula returns the minimum number of days active: 0.

####  MOD

Use MOD to return the remainder of each value after dividing each value by the modulus value.

**Syntax and Parameters**: `MOD ( values, modulus  )`

`values`: A list of 1 or more numeric values.

`modulus`: Divisor

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula returns the remainder of the active days after each value is divided by 5.

`MOD ( @Days of Activity, 5 )` 

The first ten results of this formula are: 0 4, 2, 3, 4, 1, 4, 4, 3, 0

#### MODE

Use MODE to return the most frequently occurring lowest value found in a list of items.

**Syntax and Parameters**: `MODE ( value )`

`value`: A list of 1 or more numeric values.

**Example**:

Uses the _Example: Live Sales Data_ data source

`MODE ( @Days of Activity )` 

This formula returns: 17.

#### POWER

Use POWER to raise each base to the specified exponent.

**Syntax and Parameters**: `POWER ( bases, exponent  )`

`bases`: A list of 1 or more numeric items.

`exponent`: A single numeric value.

**Example**:

`POWER(20,3)`

The result of this formula is: 8000

#### ROUND

Use ROUND to return a number that is rounded to a specified number of digits or to a whole number if no digits are provided.

**Syntax and Parameters**: `ROUND ( data, digits  )`

`data`: The number to round.

`digits`: The number of digits to round the number to.

**Example**:

`ROUND(65.29,1)`

The result of this formula is 65.3.

#### SUM

Use SUM to return the sum of all non-blank values in a range of data. SUM calculates based on how the data parameter is defined.

**Syntax and Parameters**: `SUM ( data )`

`data`: A list of 1 or more numeric items.

**Example**:

Uses the _Example: Live Sales Data_ data source

*   If the data parameter is defined with a vector, `SUM (@Revenue)`, the sum of the column is returned: 26012.90.
*   If the data parameter is defined with two vectors, `SUM(@Price Retail,@Price Base),`the sum of each pair of corresponding values (A1+B1, A2+B2...) is returned in a list: 7.83, 6.18, 5.43, 7.33, 7.91.
*   If the data parameter is defined with a vector and scalar, `SUM(@Price Retail,1)`, the sum of each value and the scalar (A1+1, A2+1...) is returned in a list: 5.79, 4.84, 4.09, 5.29, 5.58.

#### SUMIF

Use the SUMIF function to allow you to sum the values in a range that meet a certain condition.

**Syntax and Parameters**:  `SUMIF( condition, sum range )`

`condition`: A list of true or false values.

`sum range`: A list of 1 or more numeric items. Non-numeric values return as 0.

**Example**:

In this example, for every instance of Bread in the Product column, sum the corresponding Revenue values.

`SUMIF( @Product="Bread", @Revenue )` 

The result of this formula is the sum of all Revenue values when the Product column contains Bread: 6974.13

Text
----

### Function

### Details 

####  CAPITALIZE

Use CAPITALIZE to change the first letter in each word to uppercase.

**Syntax and Parameters**: `CAPITALIZE ( data )`

`data`: The text value or values

**Example**:

`CAPITALIZE ("canada")` 

The result of this formula is Canada.

#### CONCAT

Use the CONCAT function to join two or more values into one text string.

**Syntax and Parameters**: `CONCAT ( data )`

`data`: The value or values to join together.

**Example**:

Uses _Example: Product Data_ data source

In this example, " Units" is appended to every value in the Units column.

`CONCAT(@Units, " Units")`

The first five results of this formula are 9 Units, 5 Units, 2 Units, 4 Units, 7 Units.

**More examples**:

Uses the _Example: Live Sales Data_ data source

In this example, the values in the Country column are appended to the main Wikipedia link. Using the **Format as** option in the **Properties** panel, the data is set to Hyperlink.

`CONCAT("https://en.wikipedia.org/wiki/", @Country)`

The result of this formula displays a link to each country's Wikipedia page.

Uses _Example: Product Data_ data source

In this example CONCAT is used to display the total number of units sold for 2018. The formula uses SUM to sum the total number of units from the Units column. NUMBERFORMAT is wrapped around the SUM function to ensure the numeric display of the sum is not using decimal places. CONCAT adds text to the display of the data. 

`CONCAT( "Total for 2018: ", NUMBERFORMAT(SUM(@Units))," Units sold" )`

This formula returns: Total for 2018: 3401 Units sold

#### CONTAINS

Use the CONTAINS function to test each value in the haystack parameter to see if it contains the value in the needle parameter.

**Syntax and Parameters**: `CONTAINS ( haystack, needle )`

`haystack`: A list of 1 or more items.

`needle`: The case-sensitive item to search for in the haystack parameter.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, true is returned for all values in the Customer Type column that contain "Customer".

`CONTAINS(@Customer Type, "Customer")`

The first five results of this formula are false, false, true, false, true

**More Examples:**

Uses the _Example: Live Sales Data_ data source

In this example, the Price Base is returned for every instance of Mexico in the Country column.

`SELECT(@Price Base, CONTAINS(@Country, "Mexico"))`

The first five results of this formula are 3.04, 2.34, 3.04, 3.33, 1.42

#### COUNTRY\_CLEAN

Use the COUNTRY\_CLEAN function to avoid multiple variations of a country’s name and return all the country names in the same form, either as full names or as ISO 3166 standardized names. If a value cannot be identified as a country, INVALID COUNTRY will display.

**Syntax and Parameters**: `COUNTRY_CLEAN (data, [ISO format])`

`data`: A list of countries in text

`ISO Format`: \[optional\] ISO 3166-1 alpha-code

**Examples**:

`COUNTRY_CLEAN(ARRAY(“Canada,MX,Canada,CAN,CA,US,United States,USA”))`

The result is country names display in their full form, for example, Canada, Mexico, Canada, Canada, Canada, United States, United States, United States.

`COUNTRY_CLEAN(ARRAY(“Canada,MX,Canada,CAN,CA,US,United States,USA”),ISO Alpha-2)`

The result is country names display using the 2-character ISO code, for example, CA, MX, CA, CA, CA, US, US, US.

`COUNTRY_CLEAN(ARRAY(“Canada,MX,Canada,CAN,CA,US,United States,USA”),ISO Alpha-3)`

The result is country names display using the 3-character ISO code, for example, CAN, MEX, CAN, CAN, CAN, USA, USA, USA.

#### INDEXOF

Use INDEXOF to search the values in the text parameter for the specified occurrence of the search text (case sensitive) parameter and return the position of where it is found. If search text is not found at the specified occurrence, null is returned.

**Syntax and Parameters**: `INDEXOF ( text, search text, [occurence] )`

`text`: A list of 1 or more values.

`search text`: The text string to search for.

`occurrence`: \[optional\] The occurrence to search for.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example returns the position of the second occurrence of "Car" (referring to the value Carmine Carman) in the Sales Rep column.

`INDEXOF(@Sales Rep, "Car",2)`

The result of this formula returns 8 for every instance of Carmine Carman in the Sales Rep column.

#### JOIN

The JOIN function takes a set of values, joins these values with the glue parameter (a comma is used if glue is not specified), and returns them as a single value.

**Syntax and Parameters**: `JOIN( data, [glue] )`

`data`: A list of 1 or more values.

`glue`: \[optional\] A value or symbol to join the values in the data parameter with.

**Example**:

Uses the _Example: Live Sales Data_ data source

`JOIN (``@Product,"*")`

This formula returns all values in the Product column as one, with \* between each value. For example the beginning of the result looks like this: Bread\*Milk\*Milk\*Bread\*Eggs\*Eggs\*Milk\*Butter

#### LASTINDEXOF

Use LASTINDEXOF to search the values in the text parameter for the last occurrence of the search text (case sensitive) parameter and return the position of where it is found. If search text is not found at the specified occurrence, null is returned.

**Syntax and Parameters**: `LASTINDEXOF ( text, search text, [occurence] )`

`text`: A list of 1 or more values.

`search text`: The text string to search for.

`occurrence`: \[optional\] The occurrence to search for.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example returns the position of the second occurrence of "Car" (referring to the value Carmine Carman) in the Sales Rep column.

`LASTINDEXOF(@Sales Rep, "Car")`

The result of this formula returns 8 for every instance of Carmine Carman in the Sales Rep column.

#### LEFT

Use the LEFT function to return the first character or a specified number of characters starting from the first value on the left.

**Syntax and Parameters**: `LEFT ( text, [number] )`

`text`: A list of 1 or more values.

`number`:\[optional\] The number of characters to return.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula returns the first letter of every value in the Product column.

`LEFT(@Product)`

The first ten results of the formula are B, M, M, B, E, E, M, B, B, B.

Uses the _Example: Live Sales Data_ data source

This formula returns the first 2 letters of every value in the Product column. 

`LEFT(@Product, 2)`

The first ten results of the formula are Br, Mi, Mi, Br, Eg, Eg, Mi, Bu, Bu, Br.

#### LENGTH

Use the LENGTH function to count the number of characters in a text string.

**Syntax and Parameters**: `LENGTH ( text )`

`text`: A list of 1 or more values.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, LENGTH is used to return the count of characters in each Company Name. 

`LENGTH( @Company Name )`

The first five results of the formula are 25, 11, 7, 24, 18.

#### LOWER

Use the LOWER function to change all characters in the values parameter to lowercase.

**Syntax and Parameters**: `LOWER ( data )`

`data`: A list of 1 or more values.

**Example**:

Uses the _Example: Live Sales Data_ data source

`LOWER( @Company Name )`

The first five results of the formula are bamberly trust corporation, janus, ltd., eclipse, taggert transcontinental, 5 icarus lines, inc.

#### NUMBERFORMAT

Use the NUMBERFORMAT function to take a set of values, treat them as numbers, and return them as text with as many digits of decimal places as specified by the precision parameter.

**Syntax and Parameters**: `NUMBERFORMAT ( data, [precision], [separator] )`

`data`: A list of 1 or more items.

`precision`: \[optional\] The number of decimal places to return.

`separator`: \[optional\] The separator can be set to the desired thousands separator character. The example below sets a comma separator.

**Example**:

Uses the _Example: Live Sales Data_ data source

`NUMBERFORMAT( @Price Retail, 1, "," )`

The first ten results of this formula return 4.8, 3.8, 3.1, 4.3, 4.6, 4.6, 3.8, 2.2, 2.4, 3.5

**Note**: If the data parameter is defined with text values or a blank, the results will be returned as a 0.

#### REMOVE\_EMOJI

Emojis are pictographs most often seen in social media data sources, such as Facebook posts. They may also appear in other data source types. As new emojis are developed, new encoding is used and sometimes this encoding cannot be processed by Klipfolio.

The **REMOVE\_EMOJI** function is used to strip emojis from data so the remaining data can be processed.

**Syntax and Parameters**: `REMOVE_EMOJI ( text )`

`text`: The text field containing the emoji icons.

**Example**:

Where message and name point to the /data/message and /data/from/name fields in a Facebook data source.

*   To display Facebook posts which may contain emojis: `REMOVE_EMOJI( message )`
*   To select specific Facebook posts which may contain emojis: `SELECT( REMOVE_EMOJI( message ), ( name = Klipfolio ) )`

**Note**: If the selected data does not contain emojis, the REMOVE\_EMOJI function returns the selected data as is.

#### RIGHT

Use the RIGHT function to return the first character or a specified number of characters starting from the right of the first value.

**Syntax and Parameters**: `RIGHT ( text, [number] )`

`text`: A list of 1 or more values.

`number`:\[optional\] The number of characters to return.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula returns the last letter of every value in the Product column.

`RIGHT (@Product)`

The first ten results of the formula are d, k, k, d, s, s, k, r, r, d.

Uses the _Example: Live Sales Data_ data source

This formula returns the last 2 letters of every value in the Product column. 

`RIGHT (@Product, 2)`

The first ten results of the formula are ad, lk, lk, ad, gs, gs, lk, er, er, ad.

####  SUBSTITUTE

The SUBSTITUTE function replaces a set of characters with another set of characters in a text string. If the occurrence parameter is specified, that occurrence is substituted, otherwise, all occurrences are substituted.

**Syntax and Parameters**: `SUBSTITUTE ( text, old text, new text, [occurence] )`

`text`: The values to be manipulated.

`old text`: The values that will be replaced.

`new text`: The values to replace the values in old text_._

`occurrence`: \[optional\] Indicates the instance that will be replaced.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example SUBSTITUTES every instance of "-" with "/".  

`SUBSTITUTE(@Date,"-","/")`

The first five results of this formula are:

2017/01/01 04:29:18

2017/01/01 10:26:56

2017/01/02 14:03:59

2017/01/02 17:35:23

2017/01/03 04:22:45

Uses the _Example: Live Sales Data_ data source

This example SUBSTITUTES only the second instance of "-" with "/".

`SUBSTITUTE(@Date,"-","/", 2)`

The first five results of this formula are:

2017-01/01 04:29:18

2017-01/01 10:26:56

2017-01/02 14:03:59

2017-01/02 17:35:23

2017-01/03 04:22:45

**Note**: While the SUBSTITUTE function is similar to the REPLACE function, the SUBSTITUTE function is used to replace part of a value.

####  SUBSTITUTE\_REGEX

Use SUBSTITUTE\_REGEX to substitute text based on a specific pattern, such as location in text.

REGEX (REGular EXPression) is a standard for describing patterns in text. There are several online resources, such as [regexr.com](https://regexr.com/), that describe how to define REGEX expressions.

**Syntax and Parameters**: `SUBSTITUTE_REGEX ( text , old text , new text , [occurence])`

`text`: A list of 1 or more text strings.

`old text`: The regular expression.

`new text`: The values to replace the values in old text_._

`occurence`: \[optional\] Indicates the instance that will be replaced.

**Example**:

The regex anchor, ^, is used to match only when 'a' is the first character in a text string.

`SUBSTITUTE_REGEX( ARRAY(" apples, banana, orange"), "^a", "x")`

The result of this formula is xpple, bread, eggs. 

The regex anchor, $, matches the last character in a  text string and the pipe (|) indicates 'or'.

`SUBSTITUTE_REGEX( ARRAY("apple, banana, orange"), "^a|a$", "x")`

The result of this formula is xpple, bananx, orange. 

#### SUBSTRING

Use the SUBSTRING function to return a sub-string of text from a string of text.

**Syntax and Parameters**: `SUBSTRING ( text , from , [to]  )`

`text`: The text you want the sub-string of.

`from`: The start position of the sub-string specified as a number.

`to`: \[optional\] The end position of the sub-string specified as a number.

**Example**:

Uses the _Example: Live Sales Data_ data source

This formula returns the characters from the foutrth value to the end of the values in the Sales Rep column.

`SUBSTRING(@Sales Rep, 4)`

The first five results of this formula are ldo Recore, ell Wark, ry Jarrett, il Valenti, d Arthurs.

####  TEXT\_REVERSE

Use the TEXT\_REVERSE function to reverse the order of text or numbers in the data.

**Syntax and Parameters**: `TEXT_REVERSE ( data )`

`data`: A list of 1 or more values.

**Example**:

Uses the _Example: Live Sales Data_ data source

This example returns the reverse of each value in the Product column.

`TEXT_REVERSE (@Product)`

The first five results of this formula are daerB, kliM, kliM, daerB, sggE.

#### TRIM\_WHITESPACE

Use the TRIM\_WHITESPACE function to return the text without leading and trailing spaces.

**Syntax and Parameters**: `TRIM_WHITESPACE ( text )`

`text`: A list of 1 or more values.

**Example**:

`TRIM_WHITESPACE ("  Reseller, Distributor,   Customer  ")`

The result of this formula returns: Reseller, Distributor, Customer without the leading or trailing spaces.

#### TRUNCATE

Truncates text to the specified number of characters, starting from the position parameter and optionally inserting a style character.

**Syntax and Parameters**: `TRUNCATE ( text, number, [position], [style] )`

`text`: A list of 1 or more text strings.

`number`: The position to end the substring, where the first character in text is at position 0.

`position`: \[optional\] Identifies where to place the `style` parameter (start, end, split).

`style`: \[optional\] blank, period, ellipsis.

**Example**:

This example cuts off the text string after 5 characters and adds an ellipsis to the end of the value.

`TRUNCATE("abcdefghijklmnopqrstuvwxyz", 5, "end", "ellipsis")`

The result of this formula is abcde...

#### UPPER

Use the UPPER function to change all characters in the values parameter to uppercase.

**Syntax and Parameters**: `UPPER ( data )`

`data`: A list of 1 or more values.

**Example**:

`UPPER( @Company Name )`

The first five results of this formula are BAMBERLY TRUST CORPORATION, JANUS, LTD., ECLIPSE, TAGGERT TRANSCONTINENTAL, ICARUS LINES, INC.

#### URLDECODE

The Klipfolio URLDECODE function decodes data that is encoded for use in a URL using URLENCODE, UTF-8, to plain text.

**Syntax and Parameters**: `URLDECODE ( data  )`

`data`: 1 or more URL-encoded values.

**Example**:

`URLDECODE("https%3A%2F%2Fwww.klipfolio.com%2Fklipfolio-certification")`

The result of this formula is https://www.klipfolio.com/klipfolio-certification.

#### URLENCODE

Use the URLENCODE function to encode data to be safely used in URLs.

**Syntax and Parameters**: `URLENCODE ( data )`

`data`: 1 or more plaintext values.

**Example**:

`URLENCODE("https://www.klipfolio.com/klipfolio-certification")`

The result of this formula is https%3A%2F%2Fwww.klipfolio.com%2Fklipfolio-certification.

When using Date/Time functions in Klipfolio, it is important to remember that formulas process the dates in Unix time format. This means that human readable date formats have to be converted before they can be used in formulas. When converting dates, the format of the date (that you want to convert) must be specified and must be entered as a string surrounded by quotes in the formula. [Learn more about Date/Time formats.](https://support.klipfolio.com/hc/en-us/articles/216182377)

**Note**: You can use an external Unix time converter to find the Unix time format of readable dates.

Time zones are an optional parameter available for specification in Date/Time functions. However, time zones can also be set at your account level and do not typically need to be set individually for every formula. [Learn more about time zones in Klipfolio.](https://support.klipfolio.com/hc/en-us/articles/115000128514)

Date/Time
---------

### Function

### Details 

####  COUNT\_DAYS

Use COUNT\_DAYS to return the number of whole days between two dates. You can also exclude a day of the week or a holiday from the results.

**Syntax and Parameters**:

`COUNT_DAYS (start, end, [exclude DOW], [holidays], [timezone])`

`start:` The start date to count from. Unix time format.

`end:` The end date to count until. Unix time format.

`exclude DOW`: \[optional\] 1 or more days of the week to exclude from the count. Options include: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.

`holidays:` \[optional\] 1 or more dates to exclude from the count. Unix time format.

`timezone:` \[optional\] The time zone.

**Example**:

This example counts the number of days between November 1, 2018 and November 10, 2018 with Sunday excluded from the count.

`COUNT_DAYS(` `1541040562,` `1541818162, Sunday )`

The result of this formula is 8. 

This example counts the number of days between November 10, 2018 and November 1, 2018 with Sunday excluded from the count.

`COUNT_DAYS(` `1541040562,` `1541818162, Sunday )`

The result of this formula is -8.

**Note:** When using Unix format, the results will vary depending on the time of the day.

**More examples:**

This example counts the number of days between November 1, 2018 and November 10, 2018 just like the example above. However, in this example the dates in the data are not in Unix time format and must use the DATE function to convert the dates to Unix time format. Additionally, this example excludes both Saturday and Sunday from the count.

`COUNT_DAYS(DATE("11/01/2018","MM/dd/yyyy"),DATE("11/10/2018","MM/dd/yyyy"), ARRAY("Sun","Sat"))`

The result of this formula is 7.

#### DATE

Use DATE to convert dates specified in a given format into Unix time format.

**Syntax and Parameters**: `DATE ( dates , format , [timezone] )`

`dates`: A list of 1 or more date/time values.

`format`: The date format of the values in the dates parameter.

`timezone`: The time zone.

**Example**:

Uses the _Example: Live Sales Data_ data source

`DATE ( @Date, "yyyy-MM-dd HH:mm:ss" )` 

The result of this formula lists all the dates in the Date column in Unix time format. For example, the first five results return as 1483262958, 1483284416, 1483383839, 1483396523, 1483435365.

This example converts an entire date and time stamp to Unix time format.

`DATE("2017-04-03T04:18:38.943Z","yyyy-MM-dd'T'HH:mm:ss")`

The result of this formula is 1491207518.

**Learn more**:

*   [DATE and DATEVALUE](https://support.klipfolio.com/hc/en-us/articles/215547988)
*   [How to use Date/Time formats](https://support.klipfolio.com/hc/en-us/articles/216182377)
*   [How to use time zones](https://support.klipfolio.com/hc/en-us/articles/115000128514)

#### DATE\_ADD

Use DATE\_ADD to add or subtract time to or from given date/time values. Results are returned in Unix time format.

**Syntax and Parameters**: `DATE_ADD ( values , unit , amount, [timezone] )`

`values`: A list of 1 or more values in Unix time format.

`unit`: The unit to add to the date. Options include: second, minute, hour, day, week, month, quarter, year.

`amount`: The number of units to add. Use a negative number to subtract units.

`timezone`: \[optional\] The time zone.

**Example**:

This example adds 6 days to today's date. 

`DATE_ADD( TODAY() , day , 6 )`

Since today is November 18, 2018, the result of this formula is 1543035600. (The Unix time format of November 24, 2018)

This example subtracts 6 days from today's date. 

`DATE_ADD( TODAY() , day , -6 )`

Since today is November 18, 2018, the result of this formula is 1541998800. (The Unix time format of November 12, 2018)

#### DATE\_CLOSEST

Use the DATE\_CLOSEST function to find the closest day of the week (in Unix time format) before or after a given date.

**Syntax and Parameters**: `DATE_CLOSEST( values , dow , [direction], [timezone])`

`values`: A list of 1 or more values in Unix time format.

`dow`: Day of the week. Options include: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.

`direction`: \[optional\] The direction. Options include forward or backward.

`timezone`: \[optional\] The time zone.

**Example**:

This example returns the Unix time format of the closest Friday before the current date, 1542641280, November 19, 2018.

`DATE_CLOSEST( "1542641280", Friday, backward )`

The result of this formula is 1542382080 (the Unix time format of November 16, 2018).

This example returns the date closest to the last Monday from 11/18/18. The DATE function is used to convert the original date, 11/18/18, to Unix time format to be processed using the DATE\_CLOSEST function. The dates are then wrapped in a DATEVALUE function so the format the date returns the results in is d-MMM-yyyy.

`DATEVALUE( DATE_CLOSEST( DATE( "11/18/18" , "M/d/yy" ) , Monday , backward ), "d-MMM-yyyy" )`

The result of this formula 12-Nov-2018.

#### DATE\_CONVERT

Use the DATE\_CONVERT function to convert values from one date format to another date format.

**Syntax and Parameters**: `DATE_CONVERT ( values , format in , format out )`

`values`: A list of 1 or more date/time values.

`format in`: The current date format of the date/time values.

`format out`: The date/time format you want to convert the dates to.

**Example**:

`DATE_CONVERT("9/11/2018", "d/M/yyyy", "MMM dd, yyyy")`

The result of this formula returns Nov 09, 2018.

####  DATE\_ENDOF

Use DATE\_ENDOF to return the date in the values parameter at the end of the given unit parameter.

**Syntax and Parameters**: `DATE_ENDOF ( values, unit, [relative value], [first], [timezone] )`

`values`: A list of 1 or more values in Unix time format.

`unit`: The unit to return the values in. Options include week, month, quarter, year.

`relative value`: \[optional\] Number of units to add or subtract.

`first`: \[optional\] The starting point for the unit parameter, when the unit parameter is set to week or year (not applicable otherwise). **Note:** If you specify the first value, you must also provide a relative value.

Options include Sunday (default), Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.

Options include January (default), February, March, April, May, June, July, August, September, October, November, December.

`timezone`: \[optional\] The time zone.

**Example**:

Uses the _Example: Live Sales Data_ data source

In this example, the formula returns the end date in Unix time format of each week, two weeks prior to the date in the Date column. The DATE\_ENDOF function also specifies that the results should return with Monday as the start of the week. The DATE function is used to convert the dates in the Date column to Unix time format.

`DATE_ENDOF(DATE(@Date,"yyyy-MM-dd HH:mm:ss"),week ,-2 ,Monday )`

#### DATE\_IN

Use DATE\_IN to return true or false depending on whether or not the given dates fall within the specified time period.

**Syntax and Parameters**: `DATE_IN ( values, unit, [relative value], [first], [timezone] )`

`values`: A list of 1 or more values in Unix time format.

`unit`: The unit to return the values in. Options include week, month, quarter, year.

`relative value`: \[optional\] Number of units to add or subtract.

`first`: \[optional\] The starting point for the unit parameter, when the unit parameter is set to week or year (not applicable otherwise). **Note:** If you specify the first value, you must also provide a relative value.

Options include Sunday (default), Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.

Options include January (default), February, March, April, May, June, July, August, September, October, November, December.

`timezone`: \[optional\]

**Example**:

This example returns true or false depending on whether the dates in the Date column fall in the year before the current year. The DATE function is used to convert the dates in the Date column to Unix time format.

`DATE_IN(DATE(@Date,"yyyy-MM-dd HH:mm:ss"), year, -1)`

#### DATERANGE

Use DATERANGE to return a list of dates between and including the start and end dates.

**Syntax and Parameters**: `DATERANGE ( start, end, [format] )`

`start`: A list of 1 or more values in Unix time format.

`end`: last date in range.

`format`: \[optional\] required if start and end dates are in a format other than the default or in Unix time (default input is M/d/yyyy, default output is MM/dd/yyyy).

**Example**:

`DATERANGE("05/01/2018","05/04/2018","MM/dd/yyyy")`

The result of this formula is 05/01/2018, 05/02/2018, 05/03/2018, 05/04/2018.

**Learn more**:

*   [DATERANGE](https://support.klipfolio.com/hc/en-us/articles/216182657)

#### DATE\_SET

Use DATE\_SET to set a specified date unit to a set value.

**Syntax and Parameters**: `DATE_SET ( values, unit, unit value, [timezone] )`

`values`: A list of 1 or more values in Unix time format.

`unit`: Options include second, minute, hour, day, month, year.

`unit value`: The value to be assigned to the unit parameter.

`timezone`: \[optional\] The time zone.

**Example**:

In this example, the date is set to 7 months from the current date.

`DATE_SET( 1542747573, month, 7 )`

The result of this formula is 1532116773.

#### DATE\_STARTOF

Use DATE\_STARTOF to return the date in the values parameter at the start of the given unit parameter.

**Syntax and Parameters**: `DATE_STARTOF ( values, unit, [relative value], [first], [timezone] )`

`values`: A list of 1 or more values in Unix time format.

`unit`: The unit to return the values in. Options include week, month, quarter, year.

`relative value`: \[optional\] Number of units to add or subtract.

`first`: \[optional\] The starting point for the unit parameter, when the unit parameter is set to week or year (not applicable otherwise). **Note:** If you specify the first value, you must also provide a relative value.

Options include Sunday (default), Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.

Options include January (default), February, March, April, May, June, July, August, September, October, November, December.

`timezone`: \[optional\] The time zone.

**Example**:

In this example, the formula returns the start date in Unix time format of each week, two weeks prior to the date in the Date column. The DATE\_STARTOF function also specifies that the results should return with Monday as the start of the week. The DATE function is used to convert the dates in the Date column to Unix time format.

`DATE_STARTOF(DATE(@Date,"yyyy-MM-dd HH:mm:ss"),week ,-2 ,Monday )`

#### DATE\_UNITVALUE

Use DATE\_UNITVALUE to return the value of the specified unit from the given date/time values.

**Syntax and Parameters**: `DATE_UNITVALUE ( values, unit, [first], [timezone] )`

`values`: A list of 1 or more values in Unix time format.

`unit`: The unit to return the values in. Options include second, minute, hour, day, day of week, day of year, week, week of month, month, quarter, year.

`first`: \[optional\] The starting point for the unit parameter, when the unit parameter is set to week or year (not applicable otherwise).

Options include Sunday (default), Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.

Options include January (default), February, March, April, May, June, July, August, September, October, November, December.

`timezone`: \[optional\] The time zone.

**Example**:

This formula returns the week number of all the dates in the Date column. The DATE function is used to convert the dates in the Date column to Unix time format.

`DATE_UNITVALUE(DATE(@Date,"yyyy-MM-dd HH:mm:ss"), week)`

####  DATEVALUE

Use DATEVALUE to convert dates that are in Unix time format to a specified (human readable) format.

**Syntax and Parameters**: `DATEVALUE ( dates, [format], [timezone] )`

`dates`: A list of 1 or more values in Unix time format.

`format`: \[optional\] The format you want to convert your dates to.

`timezone`: \[optional\] The time zone.

**Example**:

`DATEVALUE(1542690000, "yyyy/MM/dd")` 

The result of this formula is 2018/11/20.

**Learn more**:

*   [DATE and DATEVALUE](https://support.klipfolio.com/hc/en-us/articles/215547988)

####  NOW

Use NOW to return the current date and time in Unix time format. Milliseconds are given as 3 decimal places.

**Syntax and Parameters**: `NOW ( [timezone] )`

**Example**:

In these examples, NOW is wrapped in the DATEVALUE function so that the current date and time are returned in the format provided instead of Unix time format.

`DATEVALUE( NOW(), "dd-MM-yyyy")`

The result of this formula is 20-11-2018. 

`DATEVALUE( NOW(), "h:mm:ss" )`

The result of this formula is 9:39:57.

#### TIME

Use the TIME function to convert a date/time duration, specified as a combination of days, hours, minutes and seconds, to number of seconds.

**Syntax and Parameters**: `TIME ( values, format )`

`values`: A list of 1 or more date/time durations.

`format`: The format of the date/time duration.

Supported formats include:

*   hh:mm:ss
*   hh:mm
*   dd:hh:mm:ss
*   dd:hh:mm
*   dd:hh
*   d
*   h
*   m
*   s
*   ss
*   dd
*   mm
*   hh
*   ss
*   mmss
*   ddhhmmss

**Example**:

`TIME("1:47:67:800", "d:h:m:s")` 

The result of this formula is 260,420 seconds

`TIME(ARRAY("01:08","02:16"), "dd:hh")`

The result of this formula is 115200, 230400 seconds.

#### TODAY

Use the TODAY function to return the Unix time format date for today's date.

**Syntax and Parameters**: `TODAY ( [timezone] )`

**Example**:

In this example the TODAY function is used to establish a DATE\_STARTOF value, which is asking for the first date of the week relative to today's date.

`DATE_STARTOF(TODAY(), week)` 

The result of this formula is the Unix time format for November 18, 2018 assuming that today is November 20, 2018: 1542517200

####  YESTERDAY

Use the YESTERDAY function to return the Unix time format date for yesterday's date.

**Syntax and Parameters**: `YESTERDAY ( [timezone] )`

**Example**:

This example returns the dates (in Unix time format) within the specified date range. YESTERDAY is used to satisfy the end parameter in the DATERANGE function. DATE is used to convert the date format of November 10, 2018 to Unix time format so the date can be processed in the formula.

`DATERANGE(DATE("11/10/2018","MM/dd/yyyy"),YESTERDAY())` 

This formula returns ten dates (yesterday was November 19, 2018) in Unix time format:

1541826000, 1541912400, 1541998800, 1542085200, 1542171600, 1542258000, 1542344400, 1542430800, 1542517200, 1542603600

Statistics
----------

### Function

### Details 

#### ERF

ERF computes the standard error function integrated between the _lower limit_ and _upper limit_, or between the _lower limit_ and infinity if no _upper limit_ is provided.

#### ERFC

ERFC computes the complement of the standard error function integrated between the _lower limit_ and infinity.

#### MA\_CUMULATIVE

MA\_CUMULATIVE returns the cumulative moving average for each of the given values.

#### MA\_EXPONENTIAL

MA\_EXPONENTIAL returns the exponential moving average for each of the given values using the given period "n".

#### MA\_SIMPLE

MA\_SIMPLE returns the simple moving average for the previous "n" data points for each of the given values.

#### NORMSDIST

Use NORMSDIST to take a single value or a list of values and return the normal standard distribution of each value provided.

####   RANK

Use RANK to return the rank of each item according to the order of values in a list of data.

**Syntax and Parameters**: `RANK ( data, [order] )`

`data`: A list of 1 or more values.

`order`:\[optional\] The order to rank the values in. Options include ascending or descending.

**Example**:

Uses the _Example: Live Sales Data_ data source.

`RANK(GROUP(@Days of Activity), ascending)`

This first five results of this formula are 2, 11, 12, 13, 14.

####   SLOPE

Use SLOPE to calculate the slope of the linear regression line represented by columns of known x and y values.

#### STANDARDIZE

Use STANDARDIZE to standardize each value in a column of values using a supplied mean and a supplied standard deviation.

#### STDEV

STDEV computes the standard deviation for a random sampled population using the (n-1) method.

####   STDEVP

STDEVP computes the standard deviation for a complete population using the (n) method.

####   VARIANCE

Use VARIANCE to compute the variance for a random sample population of values (n-1) method.

#### VARIANCEP

Use VARIANCEP to compute the variance for a complete population of values (n) method.

####   ZTEST

Use ZTEST to compute the one-tailed probability-value of a z-test. For a given hypothesized population mean, μ0, ZTEST returns the probability that the sample mean would be greater than the average of observations in the data set (array) - that is, the observed sample mean.
