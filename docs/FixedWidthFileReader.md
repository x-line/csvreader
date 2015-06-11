FixedWidthFileReader 
========

Fixed width files are plain text files that contain data in a tabular format where each row is represented on a new line, and columns are each a specified width. The values that fit in each column should be less or equal to the width of that column, or else they will be truncated. Values are usually padded right with a character (e.g. a space ' ' character to bring up the length to match the column width.

This class is used to read in data from a fixed width file. 

<br />

Example Usage
-------------

This example assumes you have a file on your system called C:\data.txt which is simple text file containing data consisting of fixed column width.

In this file there are three columns, where the first column is 5 chars wide, and the last two columns are each 10 chars wide.

```cs
var reader = new FixedWidthFileReader(@"C:\data.csv", "5,10, 10");
DataTable dataTable = reader.ReadAsDataTable();
```
<br />

Constructors:
-------------

Supported options: Filepath, stream, or text

Note: All examples, here assume a fixed width file which has three columns, where the first column is 5 chars wide, and the last two columns are each 10 chars wide.


Open using a filepath 
```cs
string filepath = @"C:\data.txt";
var reader = new FixedWidthFileReader(filepath, "5,10, 10");
```

Open as Stream
```cs
using (var streamreader = new StreamReader(stream))
{
    reader = new FixedWidthFileReader(streamreader, "5,10, 10");
    //...Code here
}
```

Open as Text
```cs
var text = "1  John";
reader = new FixedWidthFileReader();
reader.ColWidths = new int[] {5,10,10};
reader.OpenAsString(text);
```
<br />

Methods
-------------

Read to a XML string:
```cs
string xml = reader.ReadAsXml();
```

Read to a .NET DataTable:
```cs
DataTable dataTable = reader.ReadAsDataTable();
```
<br />


Properties:
-------------

###ColWidths
As rows are read in, each one split using fixed widths as specified by the ColWidths property

**Default**: None 

```cs
//To specify the column widths
reader.ColWidths = new int[] { 5, 10, 10 };
```
<br/>


###DataRow
How many lines to skip before stating to read in data. 
This can be used to start reading the file from any position in the file (i.e. from row 1000 for example).

**Default**: 0

```cs
//To skip 10 lines before starting to read in data:
reader.DataRow = 10;
```
<br/>


###HeaderRow
How many rows to skip before trying to read in the column titles.
By default the first line is assumed to contain a FixedWidth list of column or header titles. 
When outtputting the data as a DataTable, it will be possible to read refer to values using these header titles. 
When converting to a custom class, the reader will look for properties on your custom class with the same name referred to in these header titles.

**Default**: 0

```cs
//To tell the reader to not attempt to read in any column titles:
reader.HeaderRow = -1;

//To skip 10 lines before trying to read in the column titles:
reader.HeaderRow = 10;
```
<br/>

