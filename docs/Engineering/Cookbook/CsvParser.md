# CsvReader.cs

## Introduction

In your games and programs, you might want a way to store and edit a lot of data in an simple human-readable format. CSV files are a great way to store large quantities of structured data.

Comma-Separated Values (.csv) files are a ubiquitous plaintext data format for storing tabular data. Applications like Excel and Google Sheets can export spreadsheets to a CSV format. You can also edit CSV files in any plaintext editor.

CSV files are organized into rows of comma-separated values. Each value is deliminated by a comma, and every line in the file represents a new row.

For example, consider the following table:

| Class       | Strength | Dexterity | Constitution | Intelligence | Wisdom | Charisma |
|-------------|----------|-----------|--------------|--------------|--------|----------|
| Engineer    | 12       | 12        | 10           | 18           | 8      | 14       |
| Wizard      | 8        | 12        | 8            | 20           | 14     | 8        |
| Guardsman   | 16       | 16        | 16           | 8            | 10     | 12       |
| Faresperson | 16       | 16        | 10           | 8            | 14     | 16       |

This table could be represented as the following CSV file:

```
Class,Strength,Dexterity,Constitution,Intelligence,Wisdom,Charisma
Engineer,12,12,10,18,8,14
Wizard,8,12,8,20,14,8
Guardsman,16,16,16,8,10,12
Faresperson,16,16,10,8,14,16
```
As you can see, CSV files are a great way to store high volumes of structured data in an easy-to-edit and easy-to-read format. Inventory items, enemy stat blocks, and more can be represented in CSV Files.

## CsvReader.cs

While CSV files are in plaintext, parsing them can be a challenge. This is because some data in a CSV file might contain a comma, so special precautions must be taken to ensure that programs reading a CSV file know the difference between a comma that is separating two values and commas that are actually parts of a value. The specification for CSV files is outlined in [RFC 4180](https://datatracker.ietf.org/doc/html/rfc4180).

The below code implements a CSV Reader class that can parse CSV files in accordance to RFC 4180.

```csharp
/*
CsvReader.cs
Author: Owen Bartolf

Implements a CSV Parser.
*/

using System;
using System.Collections.Generic;
using System.Text;

namespace CsvDemo
{
    /// <summary>
    /// Represents an object that can parse a CSV file and read
    /// useful values from it.
    /// </summary>
    public class CsvStringReader
    {
        public string Data { get; private set; }

        /// <summary>
        /// Standard Constructor
        /// </summary>
        /// <param name="dataToParse">The CSV string to parse</param>
        public CsvStringReader(string dataToParse)
        {
            Data = dataToParse;
        }

        /// <summary>
        /// Parses the given data contained within the object
        /// </summary>
        public void Parse()
        {
            // CSVs deliminate rows using newlines, so we will first split along newlines to get the rows.
            string[] rows = Data.Split('\n');
            
            // For each row, process each entry
            for(int rowIndex = 0; rowIndex < rows.Length; rowIndex++)
            {
                // Separate each column from each row.
                string[] columnsInRow = SeparateColumnsOfRow(rows[rowIndex]);

                for(int columnIndex = 0; columnIndex < columnsInRow.Length; columnIndex++)
                {
                    // TODO: YOUR LOGIC HERE!
                }
            }
        }

        /// <summary>
        /// Implements a row-based parsing system for a CSV File.
        /// </summary>
        /// <remarks>
        /// This makes the following assumptions:
        /// 
        /// Entries containing a COMMA are enclosed in DOUBLE QUOTES.
        /// Example: a,b,"c,d,e",f -> Entries are: [a] [b] [c,d,e] [f].
        /// 
        /// Entries containing a double quote that should be escaped/ignored
        /// should escape that double quote with another double quote
        /// Example: a,b,c"",d,"There once, was a ""dog.""" -> Entries are: [a] [b] [c"] [d] [There once, was a "dog."]
        /// </remarks>
        /// <returns>
        /// Returns a string array containing the contents of the columns of the CSV.
        /// If row does not contain any characters, this function returns an empty string array.
        /// </returns>
        public string[] SeparateColumnsOfRow(string row)
        {
            // Edge case: row is empty string
            if (row.Length == 0)
            {
                return new string[0];
            }

            // Create a collection for storing our finished records.
            List<string> finishedRecords = new List<string>();

            // Get underlying char array representation of string so we can
            // walk through it character-by-character
            char[] rowAsCharArray = row.ToCharArray();

            // Create a "holding buffer" to record the current record.
            // This allows us to build the actual record by ignoring escape characters;
            // something you couldn't do with a normal split / substring operation.
            char[] currentRecord = new char[rowAsCharArray.Length];
            int currentRecordLength = 0;

            // Declare variables to track state
            int currentIndex = 0;
            bool shouldIgnoreCommas = false;

            while (currentIndex < rowAsCharArray.Length)
            {
                char currentChar = rowAsCharArray[currentIndex];

                // Quote handling
                if (currentChar == '"')
                {
                    // If not escaped, this means we should toggle whether we are ignoring commas or not.
                    if (!IsDoubleQuoteEscaped(rowAsCharArray, currentIndex))
                    {
                        shouldIgnoreCommas = !shouldIgnoreCommas;
                    }
                    else
                    {
                        // This character is escaped by the next character. Add this character to the
                        // buffer, but then skip the next quote; the only purpose of the next quote is
                        // make this quote an actual quote and not an escape.
                        currentRecord[currentRecordLength++] = currentChar;
                        ++currentIndex;

                    }
                }
                // End of record handling
                // A record ends if we should not ignore commas and encounter one, we reach the end of the line, or we reach the end of the string.
                else if ( (!shouldIgnoreCommas && currentChar == ',') || currentChar == '\n')
                {
                    // Construct a record from the buffer
                    finishedRecords.Add(new string(currentRecord, 0, currentRecordLength));
                    currentRecordLength = 0; // Reset buffer size
                }
                else // Otherwise this is suitable to add to the current buffer.
                {
                    currentRecord[currentRecordLength++] = currentChar;
                }

                ++currentIndex;
            }

            // Finish a record if we left one unfinished
            if (currentRecordLength > 0)
            {
                // Construct a record from the buffer
                finishedRecords.Add(new string(currentRecord, 0, currentRecordLength));
                currentRecordLength = 0; // Reset buffer size
            }

            //Once done, move records from list to array
            return finishedRecords.ToArray();

        }

        /// <summary>
        /// Returns true if the double quote at the currentIndex position of the rowAsCharArray
        /// is escaped.
        /// </summary>
        /// <param name="rowAsCharArray"></param>
        /// <param name="currentIndex"></param>
        /// <returns></returns>
        private bool IsDoubleQuoteEscaped(char[] rowAsCharArray, int currentIndex)
        {
            // Return true only if the current character is a double quote, another character exists in the array, and that character is also a double quote.
            return rowAsCharArray[currentIndex] == '"' && ((currentIndex + 1) < rowAsCharArray.Length)  && rowAsCharArray[currentIndex + 1] == '"';
        }
    }
}
```