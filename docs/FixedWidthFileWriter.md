FixedWidthFileWriter 
========

Fixed width files are plain text files that contain data in a tabular format where each row is represented on a new line, and columns are each a specified width. The values that fit in each column should be less or equal to the width of that column, or else they will be truncated. Values are usually padded right with a character (e.g. a space ' ' character to bring up the length to match the column width.

This class is used to read in data from a fixed width file. 

FixedWidthFileWriter supports using pad characters other than a space as well.
<br />

Constructors:
-------------

Supported options: DataTable

Note: All examples, here assume a fixed width file which has three columns, where the first column is 5 chars wide, and the last two columns are each 10 chars wide.

Instanciate from a .Net DataTable object and specify Column widths
```cs
var writer = new FixedWidthFileWriter(dataTable, "5,10,10");
```

Instanciate from a .Net DataTable object and determine column widths automatically
```cs
writer = new FixedWidthFileWriter(dataTable);
writer.AutoSetColumnWidths();
```
<br />

Methods
-------------

Determine the Widths of the columns based from the data
```cs
writer.AutoSetColumnWidths();
```

As above but make sure to leave a gap of 5 chars between each column
```cs
writer.AutoSetColumnWidths(5);
```

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

Properties:
-------------

###PadCharacter
As rows are read in, each one split using fixed widths as specified by the ColWidths property

**Default**: ' '  (i.e. the space character)

```cs
//To change from the default and use underscores for padding
writer.PadCharacter = '_';
```

