DelimitedFileWriter
========

CSV files are plain text files that contain data in a tabular format where each row is represented on a new line, and columns are seperated by a reserved character, such as the ',' (i.e. comma symbol). 

This class is used to output a csv file. 

DelimitedFileWriter supports using any other character to delimit new columns as well. 

<br />

Example Usage
-------------

We create some sample data, and save it to a file

```cs
//Load some data from a file
var reader = new DelimitedFileReader(@"C:\input.csv");
var dataTable = reader.ReadAsDataTable();

//Save it to a file
var writer = new DelimitedFileWriter(dataTable);
writer.WriteToFile(@"C:\output.csv");
```
<br />

Constructors
-------------

Instanciate from a .Net DataTable object
```cs
var writer = new DelimitedFileWriter(dataTable);
```

Instanciate from a list (of type 'MyClass' which you define yourself)
```cs
List<MyClass> list = new List<MyClass>();
list.Add(new MyClass() { ID = 1, Name = "John" });
writer = DelimitedFileWriter.FromList(list);
```
<br />

Methods
-------------

Write to File
```cs
writer.WriteToFile(@"C:\output.csv");
```

Write using a Stream
```cs
using (StreamWriter streamWriter = new StreamWriter(stream))
{
    writer.WriteToStream(streamWriter);
}
```
<br />

Properties
-------------

###ColumnSeperator
As rows are read in, each one split using the ColumnSeperator character. 

**Default**: , (i.e. a comma symbol)

```cs
//To change from the default and mark another character to be the column seperator:
writer.ColumnSeperator = '|';
```

###DataRow
How many lines to skip before stating to write out data. 

**Default**: 0

```cs
//To skip 10 lines before starting to write out the data:
writer.DataRow = 10;
```

###HeaderRow
How many rows to skip before writing out the column titles.

By default column titles are written out on the first line. 

**Default**: 0

```cs
//To tell the writer to not attempt to write out any column titles:
writer.HeaderRow = -1;

//To skip 10 lines before trying to write out the column titles:
writer.HeaderRow = 10;
```