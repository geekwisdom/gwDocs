# GeekWisdom Tool Documentation

## GWSettings: GeekWisdom Settings Component

### Overview

The GWSettings component allows your application to read and write settings
in a wide variety of file formasts and databases. You can use this component
to easily switch fro one file forat to another seemlessly

Supported formats include:

* Java .properties file (text and xml)
* .NET/Mono .config file (xml)
* Windows 'INI' format file
* Database Connection (GetSetting/WriteSetting stored procedures)

The GWSettings component attempts to determine the correct type of file
or database being used and automatically reads the file according to that format.


### Main Methods/Functions

~~~~

Object: GWSettings

Method:  GetSetting (FromLocation,SettingName,Defaultvalue)
Returns: The value of the setting 'SettingName' from the loation at FromLocation
         If the setting cannot be found, returns the value of Defaultvalue

Method:  WriteSetting (FromLocation,SettingName,SettingValue)
Returns: Sets the SettingValue into SettingName within FromLocation
         **This method is not yet implemented**

~~~~

FromLocation:

If file exitension is '.mdb' or '.accdb', the routine will try and read
the 'settings table' of an access database **Not yet implemented**

If the file extension is .config attempts to read the value as a .NET
config file.

If the file extension is .properties attempts to read the file as a JAVA
properties file

If the file appears to be a DSN or database connection string, attempts
to open the connection and call the GetSetting stored procedure to
retrieve the setting

### Examples

1. Read a .NET config flie from PHP. Fetch the setting called 'LogVerbosity'

~~~~
require_once __DIR__ . '/../../../autoload.php'; // Autoload files using
use \org\geekwisdom\GWSettings;

$mysm = new GWSettings();
$LogVerbosity = $mysm->GetSetting( __DIR__ . "/../tests/test.config","test","0");
echo "LogVerbosity is $LogVerbosity\n";

~~~~
Sample test.config

~~~~
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <appSettings>
      <add key="LogVerbosity" value="10" />
      <add key="Key1" value="1" />
      <add key="Key2" value="2" />
   </appSettings>
</configuration>
~~~~

### References

[Back to Main](README.md)
