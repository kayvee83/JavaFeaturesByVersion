# Java Programming language features 

## Java 7

### Strings in switch statements

The comparison of String objects in switch statements is case sensitive

``` 
public String getTypeOfDayWithSwitchStatement(String dayOfWeekArg) {
     String typeOfDay;
     switch (dayOfWeekArg) {
         case "Monday":
             typeOfDay = "Start of work week";
             break;
         case "Tuesday":
         case "Wednesday":
         case "Thursday":
             typeOfDay = "Midweek";
             break;
         case "Friday":
             typeOfDay = "End of work week";
             break;
         case "Saturday":
         case "Sunday":
             typeOfDay = "Weekend";
             break;
         default:
             throw new IllegalArgumentException("Invalid day of the week: " + dayOfWeekArg);
     }
     return typeOfDay;
} 
```


### The try-with-resources Statement

##### Before Java 7

You can use a finally block to ensure that a resource is closed regardless of whether the try statement completes normally or abruptly

```
static String readFirstLineFromFileWithFinallyBlock(String path) throws IOException {
  BufferedReader br = new BufferedReader(new FileReader(path));
  try {
    return br.readLine();
  } finally {
    if (br != null) br.close();
  }
}
```

##### Java 7

You may declare one or more resources in a try-with-resources statement.

When the block of code that directly follows try block terminates, either normally or because of an exception, the close methods of the closed methods of the resources are automatically called in this reverse order of their creation

```
public static void writeToFileZipFileContents(String zipFileName, String outputFileName)
    throws java.io.IOException {

    java.nio.charset.Charset charset = java.nio.charset.Charset.forName("US-ASCII");
    java.nio.file.Path outputFilePath = java.nio.file.Paths.get(outputFileName);

    // Open zip file and create output file with try-with-resources statement

    try (
      java.util.zip.ZipFile zf = new java.util.zip.ZipFile(zipFileName);
      java.io.BufferedWriter writer = java.nio.file.Files.newBufferedWriter(outputFilePath, charset)
    ) {

      // Enumerate each entry

      for (java.util.Enumeration entries = zf.entries(); entries.hasMoreElements();) {

        // Get the entry name and write it to the output file

        String newLine = System.getProperty("line.separator");
        String zipEntryName = ((java.util.zip.ZipEntry)entries.nextElement()).getName() + newLine;
        writer.write(zipEntryName, 0, zipEntryName.length());
      }
    }
  } 
  ```

### Underscore in numeral literals

You can place underscores only between digit. 
This enables to separate groups of digits in numeric literals, which can improve the readability of your code.

```
long creditCardNumber = 1234_5678_9012_3456L;
long socialSecurityNumber = 999_99_9999L;
float pi = 	3.14_15F;
long hexBytes = 0xFF_EC_DE_5E;
long hexWords = 0xCAFE_BABE;
long maxLong = 0x7fff_ffff_ffff_ffffL;
byte nybbles = 0b0010_0101;
long bytes = 0b11010010_01101001_10010100_10010010;
```


### Catching Multiple Exception Types and Rethrowing Exceptions with Improved Type Checking

#### Handling More Than One Type of Exception

##### Before Java 7

``` 
catch (IOException ex) {
     logger.log(ex);
     throw ex;
catch (SQLException ex) {
     logger.log(ex);
     throw ex;
}
```

##### Java 7

The catch clause specifies the types of exceptions that the block can handle, and each exception type is separated with a vertical bar (|).

```
catch (IOException|SQLException ex) {
    logger.log(ex);
    throw ex;
}
```

#### Rethrowing Exceptions with More Inclusive Type Checking
This enables you to specify more specific exception types in the throws clause of a method declaration.

##### Before Java 7

You cannot throw an exception that is a supertype of one of the catch clause's exception parameters

##### Java 7
```
  public void rethrowException(String exceptionName)
  throws FirstException, SecondException {
    try {
      // ...
    }
    catch (Exception e) {
      throw e;
    }
  }
  ```


### Type Inference for Generic Instance Creation

##### Before Java 7
`Map<String, List<String>> myMap = new HashMap<String, List<String>>();`

##### Java 7
`Map<String, List<String>> myMap = new HashMap<>();`



