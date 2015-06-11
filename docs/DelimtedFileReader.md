DelimitedFileReader 
========

CSV files are plain text files that contain data in a tabular format where each row is represented on a new line, and columns are seperated by a reserved character, such as the ',' (i.e. comma symbol). 

This class is used to read in data from a csv file. 

DelimitedFileReader supports using any other character to delimit new columns as well. 

<br />

Example Usage
-------------

This example assumes you have a file on your system called C:\data.csv which is simple text file containing data consisting of comma seperated values

```cs
//Instanciate the DelimitedFileReader by passing in a path:
var reader = new DelimitedFileReader(@"C:\data.csv");

//Then one can read in the data in the following formats.

//XML Document:
XmlDocument xmldoc = reader.ReadAsXmlDocument();

//XML string:
string xml = reader.ReadAsXml();

//.NET DataTable:
DataTable dataTable = reader.ReadAsDataTable();

//Or to convert to a strongly typed list of a custom class you created in your project:
List<MyClass> list = reader.ToList<MyClass>();
```
<br />

Constructors:
-------------

Supported options: Filepath, stream, or text

```cs
//Open as File
string filepath = @"C:\data.txt";
var reader = new DelimitedFileReader(filepath);

//Open as Stream
using (var streamreader = new StreamReader(filepath))
{
    reader = new DelimitedFileReader(streamreader);
    //...Code here
}

//Open as Text
var text = "Example Data,1,2,3,4,5";
reader = new DelimitedFileReader();
reader.OpenAsString(text);
```
<br />

Properties:
-------------

###ColumnSeperator
As rows are read in, each one split using the ColumnSeperator character. 

**Default**: , (i.e. a comma symbol)


```cs
//To change from the default and mark another character to be the column seperator:
reader.ColumnSeperator = '|';
```


###DataRow
How many lines to skip before stating to read in data. 
This can be used to start reading the file from any position in the file (i.e. from row 1000 for example).

**Default**: 0

```cs
//To skip 10 lines before starting to read in data:
reader.DataRow = 10;
```


###HeaderRow
How many rows to skip before trying to read in the column titles.
By default the first line is assumed to contain a delimited list of column or header titles. 
When outtputting the data as a DataTable, it will be possible to read refer to values using these header titles. 
When converting to a custom class, the reader will look for properties on your custom class with the same name referred to in these header titles.

**Default**: 0

```cs
//To tell the reader to not attempt to read in any column titles:
reader.HeaderRow = -1;

//To skip 10 lines before trying to read in the column titles:
reader.HeaderRow = 10;
```


###SkipEmptyRows
As rows are read in, each one will be tested, and if found to be empty, the reader will ignore it and skip to the next row.

**Default**: True

```cs
//To tell the reader to not ignore empty rows:
reader.SkipEmptyRows = false;
```


