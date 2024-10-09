# Using Excel to Scrape Websites

## Link to the websites that are scraped using Excel
1. <a href = "https://www.timeanddate.com/weather/india/kolkata/ext">Kolkata Weather Forecast</a>

## Power Query Steps - Using M language 

```m
let
    Source = Web.BrowserContents("https://www.timeanddate.com/weather/india/kolkata/ext"),
    #"Extracted Table From Html" = Html.Table(Source, {{"Column1", "TBODY TH"}, {"Column2", ".soft"}, {"Column3", ".wt-ic + *"}, {"Column4", ".small"}, {"Column5", ".small + *"}, {"Column6", "TD:nth-child(6)"}, {"Column7", "TD:nth-child(8)"}, {"Column8", "TD:nth-child(9)"}, {"Column9", "TD:nth-child(10)"}, {"Column10", "TD:nth-child(11)"}, {"Column11", "TD:nth-child(12)"}, {"Column12", "TD:nth-child(13)"}, {"Column13", ".smaller:nth-child(2)"}}, [RowSelector="TBODY TR"]),
    #"Changed Type" = Table.TransformColumnTypes(#"Extracted Table From Html",{{"Column1", type date}, {"Column2", type text}, {"Column3", type text}, {"Column4", type text}, {"Column5", type text}, {"Column6", type text}, {"Column7", Percentage.Type}, {"Column8", Percentage.Type}, {"Column9", type text}, {"Column10", type text}, {"Column11", type time}, {"Column12", type time}, {"Column13", type text}}),
    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Date"}}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Renamed Columns",{{"Date", type date}}),
    #"Renamed Columns1" = Table.RenameColumns(#"Changed Type1",{{"Column2", "Day"}, {"Column3", "Temperature (Celicius)"}, {"Column4", "Weather"}, {"Column5", "Feels Like(Celcius)"}, {"Column6", "Wind Speed(km/h)"}, {"Column7", "Humidity(%)"}, {"Column8", "Chance of Precipitation(%)"}, {"Column9", "Amout of Precipitation(mm)"}, {"Column10", "UV (Sun)"}, {"Column11", "Sunrise"}, {"Column12", "Sunset"}}),
    #"Changed Type2" = Table.TransformColumnTypes(#"Renamed Columns1",{{"Sunrise", type time}}),
    #"Replaced Value" = Table.ReplaceValue(#"Changed Type2","°C","",Replacer.ReplaceText,{"Temperature (Celicius)","Feels Like(Celcius)"}),
    #"Split Column by Delimiter" = Table.SplitColumn(#"Replaced Value", "Temperature (Celicius)", Splitter.SplitTextByDelimiter("/", QuoteStyle.Csv), {"Temperature (Celicius).1", "Temperature (Celicius).2"}),
    #"Changed Type3" = Table.TransformColumnTypes(#"Split Column by Delimiter",{{"Temperature (Celicius).1", Int64.Type}, {"Temperature (Celicius).2", Int64.Type}}),
    #"Renamed Columns2" = Table.RenameColumns(#"Changed Type3",{{"Temperature (Celicius).1", "Temperature High (Celicius)"}, {"Temperature (Celicius).2", "Temperature Low (Celicius)"}}),
    #"Replaced Value1" = Table.ReplaceValue(#"Renamed Columns2","km/h","",Replacer.ReplaceText,{"Wind Speed(km/h)"}),
    #"Changed Type4" = Table.TransformColumnTypes(#"Replaced Value1",{{"Humidity(%)", type number}, {"Chance of Precipitation(%)", type number}}),
    #"Replaced Value2" = Table.ReplaceValue(#"Changed Type4","mm","",Replacer.ReplaceText,{"Amout of Precipitation(mm)"}),
    #"Changed Type5" = Table.TransformColumnTypes(#"Replaced Value2",{{"Amout of Precipitation(mm)", type number}}),
    #"Replaced Errors" = Table.ReplaceErrorValues(#"Changed Type5", {{"Amout of Precipitation(mm)", 0}}),
    #"Extracted Text Before Delimiter" = Table.TransformColumns(#"Replaced Errors", {{"UV (Sun)", each Text.BeforeDelimiter(_, "("), type text}}),
    #"Changed Type6" = Table.TransformColumnTypes(#"Extracted Text Before Delimiter",{{"UV (Sun)", Int64.Type}}),
    #"Reordered Columns" = Table.ReorderColumns(#"Changed Type6",{"Date", "Day", "Temperature High (Celicius)", "Temperature Low (Celicius)", "Weather", "Feels Like(Celcius)", "Wind Speed(km/h)", "Humidity(%)", "Chance of Precipitation(%)", "Amout of Precipitation(mm)", "UV (Sun)", "Column13", "Sunrise", "Sunset"}),
    #"Renamed Columns3" = Table.RenameColumns(#"Reordered Columns",{{"Column13", "UV Category"}}),
    #"Extracted Text Between Delimiters" = Table.TransformColumns(#"Renamed Columns3", {{"UV Category", each Text.BetweenDelimiters(_, "(", ")"), type text}})
in
    #"Extracted Text Between Delimiters"
```

**Step 1: Extract Data from a Web Page**
```m
Source = Web.BrowserContents("https://www.timeanddate.com/weather/india/kolkata/ext")
```
- Purpose: This step fetches the web content from the specified URL, which contains weather data for Kolkata, India.

**Step 2: Extract HTML Table**
```m
#"Extracted Table From Html" = Html.Table(Source, ...)
```
- Purpose: Extracts the table data from the HTML source using a predefined mapping of columns to HTML elements. Each column corresponds to specific parts of the table (e.g., temperature, weather conditions).

**Step 3: Change Column Types**
```m
#"Changed Type" = Table.TransformColumnTypes(...)
```
- Purpose: Changes the data types of the extracted columns to appropriate types, such as date, text, percentage, and time.

**Step 4: Rename Columns**
```m
#"Renamed Columns" = Table.RenameColumns(...)
```
- Purpose: Renames columns for better readability, changing their names from default names (e.g., "Column1") to meaningful ones (e.g., "Date", "Day", "Weather").

**Step 5: Change Data Type of Date Column**
```m
#"Changed Type1" = Table.TransformColumnTypes(...)
```
- Purpose: Ensures that the Date column is correctly typed as date.

**Step 6: Rename More Columns**
```m
#"Renamed Columns1" = Table.RenameColumns(...)
```
- Purpose: Renames more columns to make them easier to understand (e.g., renaming Column3 to "Temperature (Celsius)" and so on).

**Step 7: Further Change of Column Types**
```m
#"Changed Type2" = Table.TransformColumnTypes(...)
```
- Purpose: Adjusts the column types for sunrise and sunset columns to the time type.

**Step 8: Remove "°C" Suffix**
```m
#"Replaced Value" = Table.ReplaceValue(...)
```
- Purpose: Removes the "°C" symbol from the temperature columns, so the data can be properly transformed into numbers.

**Step 9: Split Temperature Column**
```m
#"Split Column by Delimiter" = Table.SplitColumn(...)
```
- Purpose: Splits the "Temperature (Celsius)" column into two separate columns: one for high and one for low temperatures.

**Step 10: Change Data Type of Temperature Columns**
```m
#"Changed Type3" = Table.TransformColumnTypes(...)
```
- Purpose: Converts the newly split temperature columns into Int64 (integer) type.

**Step 11: Rename Temperature Columns**
```m
#"Renamed Columns2" = Table.RenameColumns(...)
```
- Purpose: Renames the temperature columns to reflect their high and low values more clearly.

**Step 12: Remove "km/h" Suffix from Wind Speed**
```m
#"Replaced Value1" = Table.ReplaceValue(...)
```
- Purpose: Removes the "km/h" suffix from the wind speed column for better numeric processing.

**Step 13: Change Column Types for Humidity and Precipitation**
```m
#"Changed Type4" = Table.TransformColumnTypes(...)
```
- Purpose: Changes the data types for the humidity and precipitation columns to numeric types (percentage for humidity).

**Step 14: Remove "mm" Suffix from Precipitation**
```m
#"Replaced Value2" = Table.ReplaceValue(...)
```
- Purpose: Removes the "mm" suffix from the amount of precipitation to allow numeric calculations.

**Step 15: Replace Errors in Precipitation Column**
```m
#"Replaced Errors" = Table.ReplaceErrorValues(...)
```
- Purpose: Replaces any errors in the precipitation column with a value of 0 to ensure there are no invalid entries.

**Step 16: Extract Text Before Delimiter in UV Index Column**
```m
#"Extracted Text Before Delimiter" = Table.TransformColumns(...)
```
- Purpose: Extracts the numeric value from the UV index column, leaving out any additional text (e.g., extracting the number from "3 (Moderate)").

**Step 17: Convert UV Index to Integer**
```m
#"Changed Type6" = Table.TransformColumnTypes(...)
```
- Purpose: Converts the UV index values to Int64 (integer) type.

**Step 18: Reorder Columns**
```m
#"Reordered Columns" = Table.ReorderColumns(...)
```
- Purpose: Reorders the columns to a more logical sequence for readability.

**Step 19: Rename UV Category Column**
```m
#"Renamed Columns3" = Table.RenameColumns(...)
```
- Purpose: Renames the column containing the UV category (e.g., "Moderate", "High") for clarity.

**Step 20: Extract Text Between Parentheses in UV Category**
```m
#"Extracted Text Between Delimiters" = Table.TransformColumns(...)
```
- Purpose: Extracts the text between parentheses from the UV category (e.g., from "3 (Moderate)" it will extract "Moderate").

**Final Output**
```m
in #"Extracted Text Between Delimiters"
```
- Purpose: Returns the final table after all transformations have been applied.

This markdown breaks down each step, explaining the transformations applied to the data in a structured manner.





