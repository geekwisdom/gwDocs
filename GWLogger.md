# GeekWisdom Tool Documentation

## GWSettings: GeekWisdom Logging Component (GWLogger)

### Overview

The GWLogger component provides a common logging routine 'wrapper'
By default, this component wraps the corresponding 'log4' wrapper by
apache. (log4net, log4php, log4j). However you can easily extend it
to use whatever logging standard maybe required for your project or
simply leave it as is to no hassle logging and debugging

The GWLogger supports the standard log4.. file format which must be
setup and configured.

### Main Methods/Functions

~~~~

Object: GWLogger

Method: GetInstance(LogVerbosity)
Returns: An active logger sets the maximum verbosity to LogVerbosity

Method:  WriteLog (LogLevel,LogType,Message,Exception)
Returns: Writes the log entry 'Message'  into the Logger LogType IF AND ONLY IF
the LogLevel is greater or equal to the overall applicatoins LogVerbosity

~~~~

LogType:

The following values of 'LogType' affect the specific logger that is written

Enum

 * LogType.Debug: For Debug Level Logging
 * LogType.Info: For information level logging
 * LogType.Warning: For warning level logging
 * LogType.Error: For Error logging
 * LogType.Fatal: For critical system failures
 * LogType.Security: For security logging events
### Examples

1. JAVA: Configure and Write using GWLogger with log4j

~~~~
import org.geekwisdom.GWLogger;

 public static void main()
        {
                GWLogger myLogger = GWLogger.getInstance(5);
                myLogger.WriteLog(2,GWLogger.LogType.Error,"just a error message");
                return;
        }

~~~~
Sample log4j2.xml (write to console standard output (stdout))
~~~~
<Configuration status="WARN">
      <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
          <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>

        </Console>
      </Appenders>
      <Loggers>
        <Root level="error">
          <AppenderRef ref="Console"/>
        </Root>
      </Loggers>
</Configuration>

~~~~

Sample log4j2.xml (write to a file appender "error.log")
~~~~
<Configuration status="WARN">

      <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
          <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>

        </Console>
         <File name="ErrorLogger" fileName="error.log">
          <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
         </File>
      </Appenders>
      <Loggers>
        <Root level="error">
          <AppenderRef ref="ErrorLogger"/>
        </Root>
      </Loggers>
</Configuration>

~~~~

### References

Note: log4.. config files are specific to the language, see links below for your logging configuration

* [Log4j2 appenders from Myyong](https://mkyong.com/logging/log4j2-xml-example/)
* [Log4net appenders from Apache(https://logging.apache.org/log4net/release/config-examples.html)
* [Log4php appenders from Apache](https://logging.apache.org/log4php/docs/configuration.html)

[Back to Main](README.md)
