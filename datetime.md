# Java DateTime Examples

This document contains 100 comprehensive examples demonstrating Java's modern  
datetime API from the `java.time` package, introduced in Java 8. These classes  
provide a robust, immutable, and thread-safe way to work with dates, times,  
timezones, and durations. The API replaces the legacy `Date` and `Calendar`  
classes with a cleaner design based on ISO-8601 standards.  

## Current date
This example shows how to get the current date using LocalDate.

```java
void main() {

    var today = java.time.LocalDate.now();
    IO.println("Today: " + today);
}
```

The `LocalDate.now` method returns the current date from the system clock in  
the default timezone. `LocalDate` represents a date without time or timezone  
information, making it ideal for birthdays, anniversaries, and calendar dates.  

## Specific date
This example demonstrates creating a date with specific year, month, and day.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 12, 25);
    IO.println("Date: " + date);
}
```

The `LocalDate.of` method creates a date from integer values for year, month,  
and day. The month can be specified as an integer (1-12) or using the `Month`  
enum for better readability and type safety.  

## Date from string
This example shows how to parse a date from a string.

```java
void main() {

    var date = java.time.LocalDate.parse("2024-03-15");
    IO.println("Parsed date: " + date);
}
```

The `parse` method accepts an ISO-8601 formatted string (yyyy-MM-dd) and  
converts it to a `LocalDate` object. This is useful when reading dates from  
configuration files, user input, or external APIs.  

## Current time
This example demonstrates getting the current time.

```java
void main() {

    var now = java.time.LocalTime.now();
    IO.println("Current time: " + now);
}
```

The `LocalTime.now` method returns the current time from the system clock.  
`LocalTime` represents time without date or timezone, suitable for events  
that occur daily at the same time, like alarm clocks or schedules.  

## Specific time
This example shows creating a time with specific hour, minute, and second.

```java
void main() {

    var time = java.time.LocalTime.of(14, 30, 45);
    IO.println("Time: " + time);
}
```

The `LocalTime.of` method creates a time from hour, minute, and second values.  
An optional nanosecond parameter is also available for precise timing. This  
method uses 24-hour format for hours (0-23).  

## Time from string
This example demonstrates parsing time from a string.

```java
void main() {

    var time = java.time.LocalTime.parse("09:30:00");
    IO.println("Parsed time: " + time);
}
```

The `parse` method converts an ISO-8601 time string (HH:mm:ss) into a  
`LocalTime` object. The seconds can be omitted if they are zero, and  
fractional seconds are supported using a decimal point.  

## Current datetime
This example shows getting the current date and time.

```java
void main() {

    var now = java.time.LocalDateTime.now();
    IO.println("Now: " + now);
}
```

The `LocalDateTime.now` method combines date and time from the system clock.  
`LocalDateTime` represents a datetime without timezone information, ideal for  
events that are timezone-independent or in a single location.  

## Specific datetime
This example demonstrates creating a specific date and time.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 10, 30, 0);
    IO.println("DateTime: " + datetime);
}
```

The `LocalDateTime.of` method creates a datetime from year, month, day, hour,  
minute, and second values. You can also create it by combining a `LocalDate`  
and `LocalTime` using the `atTime` and `atDate` methods.  

## Datetime from string
This example shows parsing datetime from a string.

```java
void main() {

    var datetime = java.time.LocalDateTime.parse("2024-03-15T14:30:00");
    IO.println("Parsed: " + datetime);
}
```

The `parse` method accepts an ISO-8601 datetime string with a 'T' separator  
between the date and time parts. This format is widely used in APIs and  
data interchange formats like JSON.  

## Add days to date
This example demonstrates adding days to a date.

```java
void main() {

    var today = java.time.LocalDate.now();
    var nextWeek = today.plusDays(7);
    IO.println("Today: " + today);
    IO.println("Next week: " + nextWeek);
}
```

The `plusDays` method returns a new `LocalDate` with the specified number of  
days added. All datetime classes are immutable, so operations always return  
new instances rather than modifying the original object.  

## Subtract days from date
This example shows subtracting days from a date.

```java
void main() {

    var today = java.time.LocalDate.now();
    var lastWeek = today.minusDays(7);
    IO.println("Today: " + today);
    IO.println("Last week: " + lastWeek);
}
```

The `minusDays` method returns a new `LocalDate` with the specified number of  
days subtracted. Similar methods exist for other units like weeks, months,  
and years, providing flexible date arithmetic.  

## Add months to date
This example demonstrates adding months to a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 1, 31);
    var nextMonth = date.plusMonths(1);
    IO.println("Original: " + date);
    IO.println("Plus 1 month: " + nextMonth);
}
```

The `plusMonths` method adds the specified number of months. If the resulting  
day doesn't exist in the target month (like February 31st), the date is  
adjusted to the last valid day of that month (February 29th or 28th).  

## Add years to date
This example shows adding years to a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 2, 29);
    var nextYear = date.plusYears(1);
    IO.println("Original: " + date);
    IO.println("Plus 1 year: " + nextYear);
}
```

The `plusYears` method adds years to a date. Leap year dates like February  
29th are automatically adjusted when moved to non-leap years, becoming  
February 28th to maintain validity.  

## Add hours to time
This example demonstrates adding hours to a time.

```java
void main() {

    var time = java.time.LocalTime.of(14, 30);
    var later = time.plusHours(3);
    IO.println("Original: " + time);
    IO.println("Plus 3 hours: " + later);
}
```

The `plusHours` method adds hours to a time. Time arithmetic automatically  
wraps around midnight, so adding hours to 23:00 will correctly move into  
the next day's hours without changing the date (since LocalTime has no date).  

## Add minutes to time
This example shows adding minutes to a time.

```java
void main() {

    var time = java.time.LocalTime.of(10, 15);
    var later = time.plusMinutes(45);
    IO.println("Original: " + time);
    IO.println("Plus 45 minutes: " + later);
}
```

The `plusMinutes` method adds the specified number of minutes. Similar to  
hours, minutes wrap around at 60, and the calculation correctly handles  
overflow into hours and potentially across midnight.  

## Compare dates
This example demonstrates comparing two dates.

```java
void main() {

    var date1 = java.time.LocalDate.of(2024, 6, 15);
    var date2 = java.time.LocalDate.of(2024, 8, 20);
    
    IO.println("date1 before date2: " + date1.isBefore(date2));
    IO.println("date1 after date2: " + date1.isAfter(date2));
    IO.println("dates equal: " + date1.isEqual(date2));
}
```

The `isBefore`, `isAfter`, and `isEqual` methods provide clear, readable date  
comparisons. These methods are preferred over using `compareTo` when you only  
need to check ordering relationships.  

## Check if date is in past
This example shows checking if a date is in the past.

```java
void main() {

    var past = java.time.LocalDate.of(2020, 1, 1);
    var today = java.time.LocalDate.now();
    
    IO.println("Date is in past: " + past.isBefore(today));
}
```

Comparing a date against `LocalDate.now` determines if it's in the past. This  
pattern is commonly used for validating expiration dates, checking if events  
have occurred, or filtering historical data.  

## Check if date is in future
This example demonstrates checking if a date is in the future.

```java
void main() {

    var future = java.time.LocalDate.of(2030, 12, 31);
    var today = java.time.LocalDate.now();
    
    IO.println("Date is in future: " + future.isAfter(today));
}
```

The `isAfter` method compares against the current date to determine if an  
event is upcoming. This is useful for scheduling, planning applications,  
and validating future-dated transactions.  

## Get year from date
This example shows extracting the year from a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var year = date.getYear();
    IO.println("Year: " + year);
}
```

The `getYear` method returns the year as an integer. Individual components  
of a date can be extracted using similar methods like `getMonthValue`,  
`getDayOfMonth`, `getDayOfWeek`, and `getDayOfYear`.  

## Get month from date
This example demonstrates extracting the month from a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var month = date.getMonth();
    var monthValue = date.getMonthValue();
    
    IO.println("Month: " + month);
    IO.println("Month value: " + monthValue);
}
```

The `getMonth` method returns a `Month` enum value, while `getMonthValue`  
returns an integer (1-12). The enum provides additional methods for month  
manipulation and is more type-safe than raw integers.  

## Get day of month
This example shows getting the day of the month.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var day = date.getDayOfMonth();
    IO.println("Day of month: " + day);
}
```

The `getDayOfMonth` method returns the day as an integer from 1 to 31. This  
is distinct from `getDayOfWeek` which returns the weekday, and `getDayOfYear`  
which returns the day number within the year (1-365 or 366).  

## Get day of week
This example demonstrates getting the day of the week.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var dayOfWeek = date.getDayOfWeek();
    IO.println("Day of week: " + dayOfWeek);
}
```

The `getDayOfWeek` method returns a `DayOfWeek` enum value (MONDAY, TUESDAY,  
etc.). The enum provides utility methods like `getValue` to get the ISO day  
number (1=Monday, 7=Sunday) and methods for day arithmetic.  

## Get day of year
This example shows getting the day number within the year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var dayOfYear = date.getDayOfYear();
    IO.println("Day of year: " + dayOfYear);
}
```

The `getDayOfYear` method returns an integer from 1 to 365 (or 366 in leap  
years). This is useful for calculations involving Julian dates or tracking  
progress through the year.  

## Check if leap year
This example demonstrates checking if a year is a leap year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 1, 1);
    var isLeap = date.isLeapYear();
    IO.println("2024 is leap year: " + isLeap);
}
```

The `isLeapYear` method returns true if the year follows leap year rules  
(divisible by 4, except centuries unless divisible by 400). This affects  
the number of days in February and the year.  

## Length of month
This example shows getting the number of days in a month.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 2, 15);
    var length = date.lengthOfMonth();
    IO.println("Days in February 2024: " + length);
}
```

The `lengthOfMonth` method returns 28, 29, 30, or 31 depending on the month  
and whether it's a leap year. This is useful for iterating through all days  
in a month or validating date ranges.  

## Length of year
This example demonstrates getting the number of days in a year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 1, 1);
    var length = date.lengthOfYear();
    IO.println("Days in 2024: " + length);
}
```

The `lengthOfYear` method returns 365 or 366 depending on whether it's a  
leap year. This is particularly useful for calculations involving annual  
periods or pro-rating values across a year.  

## Format date with pattern
This example shows formatting a date with a custom pattern.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var formatter = java.time.format.DateTimeFormatter.ofPattern("dd/MM/yyyy");
    var formatted = date.format(formatter);
    IO.println("Formatted: " + formatted);
}
```

The `DateTimeFormatter.ofPattern` method creates a formatter with a custom  
pattern using symbols like 'dd' for day, 'MM' for month, and 'yyyy' for year.  
The `format` method then applies this pattern to produce a string.  

## Format date with style
This example demonstrates formatting a date with predefined styles.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var short = date.format(java.time.format.DateTimeFormatter.ofLocalizedDate(
        java.time.format.FormatStyle.SHORT));
    var medium = date.format(java.time.format.DateTimeFormatter.ofLocalizedDate(
        java.time.format.FormatStyle.MEDIUM));
    var long = date.format(java.time.format.DateTimeFormatter.ofLocalizedDate(
        java.time.format.FormatStyle.LONG));
    
    IO.println("Short: " + short);
    IO.println("Medium: " + medium);
    IO.println("Long: " + long);
}
```

Predefined format styles (SHORT, MEDIUM, LONG, FULL) automatically adapt to  
the default locale, producing culturally appropriate date representations.  
This is essential for internationalized applications.  

## Format time with pattern
This example shows formatting time with a custom pattern.

```java
void main() {

    var time = java.time.LocalTime.of(14, 30, 45);
    var formatter = java.time.format.DateTimeFormatter.ofPattern("HH:mm:ss");
    var formatted = time.format(formatter);
    IO.println("Formatted: " + formatted);
}
```

Time formatting uses patterns with 'HH' for 24-hour format, 'hh' for 12-hour  
format, 'mm' for minutes, and 'ss' for seconds. Additional symbols like 'a'  
for AM/PM and 'SSS' for milliseconds provide fine-grained control.  

## Parse date with pattern
This example demonstrates parsing a date using a custom pattern.

```java
void main() {

    var dateString = "15/06/2024";
    var formatter = java.time.format.DateTimeFormatter.ofPattern("dd/MM/yyyy");
    var date = java.time.LocalDate.parse(dateString, formatter);
    IO.println("Parsed date: " + date);
}
```

When parsing dates not in ISO format, you must provide a `DateTimeFormatter`  
that matches the input string's pattern. The parser is strict by default,  
throwing exceptions for invalid dates.  

## Parse time with pattern
This example shows parsing time using a custom pattern.

```java
void main() {

    var timeString = "02:30:45 PM";
    var formatter = java.time.format.DateTimeFormatter.ofPattern("hh:mm:ss a");
    var time = java.time.LocalTime.parse(timeString, formatter);
    IO.println("Parsed time: " + time);
}
```

The 12-hour time format requires the 'a' pattern symbol for AM/PM markers.  
The parsed time is always stored internally in 24-hour format, regardless  
of the input format used.  

## With methods for date
This example demonstrates using with methods to change date components.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var newDate = date.withYear(2025).withMonth(12).withDayOfMonth(25);
    
    IO.println("Original: " + date);
    IO.println("Modified: " + newDate);
}
```

The `withYear`, `withMonth`, and `withDayOfMonth` methods create new dates  
with specific components changed. These are more readable than using plus/minus  
operations when you need to set rather than adjust values.  

## With methods for time
This example shows using with methods to change time components.

```java
void main() {

    var time = java.time.LocalTime.of(10, 30, 45);
    var newTime = time.withHour(14).withMinute(0).withSecond(0);
    
    IO.println("Original: " + time);
    IO.println("Modified: " + newTime);
}
```

Similar to dates, times can be modified using `withHour`, `withMinute`,  
`withSecond`, and `withNano` methods. Method chaining makes it convenient  
to change multiple components in a single expression.  

## Start of day
This example demonstrates getting the start of a day as a datetime.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var startOfDay = date.atStartOfDay();
    IO.println("Start of day: " + startOfDay);
}
```

The `atStartOfDay` method converts a `LocalDate` to a `LocalDateTime` with  
the time set to 00:00:00. This is useful for datetime range queries where  
you need the first moment of a day.  

## End of day
This example shows creating the end of a day as a datetime.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var endOfDay = date.atTime(23, 59, 59, 999999999);
    IO.println("End of day: " + endOfDay);
}
```

To get the last moment of a day, use `atTime` with maximum values for hours,  
minutes, seconds, and nanoseconds. This pattern is common for inclusive range  
queries that should capture all events on a specific date.  

## Combine date and time
This example demonstrates combining a date and time.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var time = java.time.LocalTime.of(14, 30);
    var datetime = date.atTime(time);
    
    IO.println("DateTime: " + datetime);
}
```

The `atTime` method on `LocalDate` accepts a `LocalTime` to create a  
`LocalDateTime`. Alternatively, `LocalTime.atDate` can be used. This  
separation allows flexible composition of date and time components.  

## Extract date from datetime
This example shows extracting the date part from a datetime.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 14, 30);
    var date = datetime.toLocalDate();
    IO.println("Date: " + date);
}
```

The `toLocalDate` method extracts just the date portion, discarding the time.  
This is useful when you need to group or compare events by date without  
considering the time of day.  

## Extract time from datetime
This example demonstrates extracting the time part from a datetime.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 14, 30);
    var time = datetime.toLocalTime();
    IO.println("Time: " + time);
}
```

The `toLocalTime` method extracts just the time portion, discarding the date.  
This is useful for analyzing patterns based solely on time of day, such as  
peak hours or daily schedules.  

## Duration between times
This example shows calculating duration between two times.

```java
void main() {

    var start = java.time.LocalTime.of(9, 0);
    var end = java.time.LocalTime.of(17, 30);
    var duration = java.time.Duration.between(start, end);
    
    IO.println("Duration: " + duration);
    IO.println("Hours: " + duration.toHours());
    IO.println("Minutes: " + duration.toMinutes());
}
```

`Duration.between` calculates the time-based amount between two temporal  
objects. It represents the duration in seconds and nanoseconds, with methods  
to convert to hours, minutes, or other units.  

## Duration between datetimes
This example demonstrates calculating duration between two datetimes.

```java
void main() {

    var start = java.time.LocalDateTime.of(2024, 6, 15, 9, 0);
    var end = java.time.LocalDateTime.of(2024, 6, 15, 17, 30);
    var duration = java.time.Duration.between(start, end);
    
    IO.println("Duration: " + duration);
    IO.println("Minutes: " + duration.toMinutes());
}
```

Duration works with any temporal types that include time information. It's  
ideal for measuring elapsed time in processes, calculating work hours, or  
determining time remaining until an event.  

## Period between dates
This example shows calculating the period between two dates.

```java
void main() {

    var start = java.time.LocalDate.of(2024, 1, 15);
    var end = java.time.LocalDate.of(2024, 6, 20);
    var period = java.time.Period.between(start, end);
    
    IO.println("Period: " + period);
    IO.println("Months: " + period.getMonths());
    IO.println("Days: " + period.getDays());
}
```

`Period.between` calculates the date-based amount between two dates in years,  
months, and days. Unlike `Duration` which measures precise time, `Period`  
handles calendar-based differences, accounting for varying month lengths.  

## Days between dates
This example demonstrates calculating the number of days between dates.

```java
void main() {

    var start = java.time.LocalDate.of(2024, 1, 1);
    var end = java.time.LocalDate.of(2024, 12, 31);
    var days = java.time.temporal.ChronoUnit.DAYS.between(start, end);
    
    IO.println("Days between: " + days);
}
```

`ChronoUnit.DAYS.between` provides a precise count of days between two dates.  
The `ChronoUnit` enum offers similar methods for other units like WEEKS,  
MONTHS, and YEARS, giving flexible temporal arithmetic.  

## Create duration
This example shows creating a duration with specific values.

```java
void main() {

    var duration1 = java.time.Duration.ofHours(2);
    var duration2 = java.time.Duration.ofMinutes(90);
    var duration3 = java.time.Duration.ofSeconds(3600);
    
    IO.println("2 hours: " + duration1);
    IO.println("90 minutes: " + duration2);
    IO.println("3600 seconds: " + duration3);
}
```

Duration can be created from hours, minutes, seconds, or nanoseconds using  
static factory methods. Multiple durations can be added or subtracted to  
build complex time periods.  

## Create period
This example demonstrates creating a period with specific values.

```java
void main() {

    var period1 = java.time.Period.ofDays(10);
    var period2 = java.time.Period.ofWeeks(2);
    var period3 = java.time.Period.of(1, 6, 15);
    
    IO.println("10 days: " + period1);
    IO.println("2 weeks: " + period2);
    IO.println("1 year, 6 months, 15 days: " + period3);
}
```

Period factory methods create date-based amounts. The `of` method accepts  
years, months, and days together, while individual methods create periods  
of single units like days or weeks.  

## Add duration to time
This example shows adding a duration to a time.

```java
void main() {

    var time = java.time.LocalTime.of(10, 30);
    var duration = java.time.Duration.ofMinutes(45);
    var newTime = time.plus(duration);
    
    IO.println("Original: " + time);
    IO.println("After adding duration: " + newTime);
}
```

The `plus` method accepts a `Duration` and adds it to the time. This is more  
flexible than using specific methods like `plusMinutes` when the duration is  
calculated dynamically or represents multiple units.  

## Add period to date
This example demonstrates adding a period to a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 1, 15);
    var period = java.time.Period.ofMonths(3);
    var newDate = date.plus(period);
    
    IO.println("Original: " + date);
    IO.println("After adding period: " + newDate);
}
```

The `plus` method with a `Period` adds the date-based amount to the date.  
Periods handle calendar arithmetic correctly, adjusting for varying month  
lengths and leap years automatically.  

## ZonedDateTime creation
This example shows creating a datetime with timezone information.

```java
void main() {

    var zoneId = java.time.ZoneId.of("America/New_York");
    var zonedDateTime = java.time.ZonedDateTime.of(2024, 6, 15, 14, 30, 0, 0, zoneId);
    
    IO.println("Zoned DateTime: " + zonedDateTime);
}
```

`ZonedDateTime` represents a datetime with timezone and offset information.  
It's essential for applications that need timezone-aware operations like  
scheduling across regions or displaying times in local timezones.  

## Current ZonedDateTime
This example demonstrates getting the current datetime with timezone.

```java
void main() {

    var now = java.time.ZonedDateTime.now();
    var nyc = java.time.ZonedDateTime.now(java.time.ZoneId.of("America/New_York"));
    
    IO.println("Local: " + now);
    IO.println("NYC: " + nyc);
}
```

`ZonedDateTime.now` returns the current datetime in the system's default  
timezone, or in a specified timezone when provided. This shows how the same  
moment appears differently across timezones.  

## Convert between timezones
This example shows converting a datetime between timezones.

```java
void main() {

    var paris = java.time.ZonedDateTime.of(2024, 6, 15, 14, 30, 0, 0,
        java.time.ZoneId.of("Europe/Paris"));
    var tokyo = paris.withZoneSameInstant(java.time.ZoneId.of("Asia/Tokyo"));
    
    IO.println("Paris: " + paris);
    IO.println("Tokyo: " + tokyo);
}
```

The `withZoneSameInstant` method converts to a different timezone while  
preserving the absolute instant in time. The displayed time changes to  
reflect the local time in the new timezone.  

## Get timezone offset
This example demonstrates getting the UTC offset for a timezone.

```java
void main() {

    var zonedDateTime = java.time.ZonedDateTime.now(
        java.time.ZoneId.of("America/New_York"));
    var offset = zonedDateTime.getOffset();
    
    IO.println("Offset: " + offset);
}
```

The `getOffset` method returns the UTC offset as a `ZoneOffset` object. The  
offset can vary throughout the year due to daylight saving time transitions,  
making timezone-aware types essential for accurate time calculations.  

## List available timezones
This example shows getting all available timezone IDs.

```java
void main() {

    var zones = java.time.ZoneId.getAvailableZoneIds();
    var count = 0;
    
    for (var zone : zones) {
        IO.println(zone);
        count++;
        if (count >= 10) break;
    }
    IO.println("... (showing first 10 of " + zones.size() + " zones)");
}
```

The `getAvailableZoneIds` method returns all timezone identifiers recognized  
by the system. These follow the IANA timezone database format like  
"America/New_York" or "Europe/London".  

## Instant creation
This example demonstrates creating an instant representing a point in time.

```java
void main() {

    var instant = java.time.Instant.now();
    IO.println("Current instant: " + instant);
}
```

`Instant` represents a point on the timeline in UTC, measured in seconds and  
nanoseconds from the Unix epoch (1970-01-01T00:00:00Z). It's ideal for  
timestamps and measuring machine time.  

## Instant from epoch
This example shows creating an instant from epoch seconds.

```java
void main() {

    var instant = java.time.Instant.ofEpochSecond(1717257600);
    IO.println("Instant: " + instant);
}
```

The `ofEpochSecond` method creates an `Instant` from the number of seconds  
since the Unix epoch. An optional nanosecond adjustment parameter provides  
sub-second precision when needed.  

## Convert instant to datetime
This example demonstrates converting an instant to a local datetime.

```java
void main() {

    var instant = java.time.Instant.now();
    var zoneId = java.time.ZoneId.systemDefault();
    var datetime = java.time.LocalDateTime.ofInstant(instant, zoneId);
    
    IO.println("Instant: " + instant);
    IO.println("LocalDateTime: " + datetime);
}
```

Converting an `Instant` to `LocalDateTime` requires a timezone because the  
instant is UTC-based while local datetime depends on the timezone. The  
`ofInstant` method performs this conversion.  

## Convert datetime to instant
This example shows converting a datetime to an instant.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 14, 30);
    var zoneId = java.time.ZoneId.systemDefault();
    var instant = datetime.atZone(zoneId).toInstant();
    
    IO.println("LocalDateTime: " + datetime);
    IO.println("Instant: " + instant);
}
```

To convert `LocalDateTime` to `Instant`, you must first add timezone  
information using `atZone`, then call `toInstant`. This two-step process  
makes the timezone dependency explicit.  

## Instant arithmetic
This example demonstrates adding duration to an instant.

```java
void main() {

    var instant = java.time.Instant.now();
    var later = instant.plus(java.time.Duration.ofHours(2));
    
    IO.println("Now: " + instant);
    IO.println("2 hours later: " + later);
}
```

Instants support duration-based arithmetic using `plus` and `minus` methods.  
Since instants represent absolute time, only time-based durations (not  
date-based periods) can be added.  

## Compare instants
This example shows comparing two instants.

```java
void main() {

    var instant1 = java.time.Instant.now();
    var instant2 = instant1.plus(java.time.Duration.ofSeconds(1));
    
    IO.println("instant1 before instant2: " + instant1.isBefore(instant2));
    IO.println("instant1 after instant2: " + instant1.isAfter(instant2));
}
```

Instant comparison methods work like other temporal types. Since instants  
are absolute points in time, comparisons are unambiguous regardless of  
timezone considerations.  

## Get epoch milliseconds
This example demonstrates getting milliseconds since the epoch.

```java
void main() {

    var instant = java.time.Instant.now();
    var millis = instant.toEpochMilli();
    IO.println("Epoch milliseconds: " + millis);
}
```

The `toEpochMilli` method returns the timestamp as milliseconds since the  
Unix epoch. This format is commonly used in databases, APIs, and for  
interoperability with legacy Java date code.  

## Get epoch seconds
This example shows getting seconds since the epoch.

```java
void main() {

    var instant = java.time.Instant.now();
    var seconds = instant.getEpochSecond();
    IO.println("Epoch seconds: " + seconds);
}
```

The `getEpochSecond` method returns just the seconds component of the  
timestamp. The `getNano` method can be used to get the nanosecond part  
for full precision.  

## TemporalAdjuster first day of month
This example demonstrates using an adjuster to get the first day of a month.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var firstDay = date.with(java.time.temporal.TemporalAdjusters.firstDayOfMonth());
    IO.println("First day of month: " + firstDay);
}
```

`TemporalAdjusters` provide common date adjustments like finding the first  
or last day of a month or year. The `with` method applies these adjusters  
to modify dates in meaningful ways.  

## TemporalAdjuster last day of month
This example shows using an adjuster to get the last day of a month.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var lastDay = date.with(java.time.temporal.TemporalAdjusters.lastDayOfMonth());
    IO.println("Last day of month: " + lastDay);
}
```

The `lastDayOfMonth` adjuster correctly handles varying month lengths and  
leap years. This eliminates the need for manual calendar arithmetic when  
finding month boundaries.  

## TemporalAdjuster next weekday
This example demonstrates finding the next occurrence of a weekday.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var nextMonday = date.with(
        java.time.temporal.TemporalAdjusters.next(java.time.DayOfWeek.MONDAY));
    IO.println("Next Monday: " + nextMonday);
}
```

The `next` adjuster finds the next occurrence of a specified day of the week.  
Similar methods like `previous`, `nextOrSame`, and `previousOrSame` provide  
flexible weekday navigation.  

## TemporalAdjuster first day of year
This example shows getting the first day of the year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var firstDay = date.with(java.time.temporal.TemporalAdjusters.firstDayOfYear());
    IO.println("First day of year: " + firstDay);
}
```

The `firstDayOfYear` adjuster sets the date to January 1st of the same year.  
This is useful for year-to-date calculations or resetting dates to year  
boundaries.  

## TemporalAdjuster last day of year
This example demonstrates getting the last day of the year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var lastDay = date.with(java.time.temporal.TemporalAdjusters.lastDayOfYear());
    IO.println("Last day of year: " + lastDay);
}
```

The `lastDayOfYear` adjuster sets the date to December 31st of the same year.  
Combined with `atStartOfDay` or `atTime`, this creates year-end timestamps  
for reporting and analysis.  

## Clock for testing
This example shows using Clock for testable time-based code.

```java
void main() {

    var fixedClock = java.time.Clock.fixed(
        java.time.Instant.parse("2024-06-15T10:30:00Z"),
        java.time.ZoneId.of("UTC"));
    var date = java.time.LocalDate.now(fixedClock);
    
    IO.println("Fixed date: " + date);
}
```

`Clock` allows injecting custom time sources, making time-dependent code  
testable. A fixed clock always returns the same instant, while other  
implementations can offset or adjust the system clock.  

## Clock with offset
This example demonstrates creating a clock with an offset.

```java
void main() {

    var systemClock = java.time.Clock.systemDefaultZone();
    var offsetClock = java.time.Clock.offset(systemClock, 
        java.time.Duration.ofHours(2));
    
    var normalTime = java.time.LocalDateTime.now(systemClock);
    var offsetTime = java.time.LocalDateTime.now(offsetClock);
    
    IO.println("Normal: " + normalTime);
    IO.println("Offset: " + offsetTime);
}
```

An offset clock adds a fixed duration to another clock's time. This is useful  
for simulating future scenarios or testing time-sensitive logic without  
changing the system clock.  

## YearMonth creation
This example shows working with year-month combinations.

```java
void main() {

    var yearMonth = java.time.YearMonth.of(2024, 6);
    IO.println("Year-Month: " + yearMonth);
    IO.println("Length: " + yearMonth.lengthOfMonth() + " days");
}
```

`YearMonth` represents a year and month without a day component. It's useful  
for monthly billing periods, credit card expiration dates, or any scenario  
where you need month-level precision.  

## MonthDay creation
This example demonstrates working with month-day combinations.

```java
void main() {

    var birthday = java.time.MonthDay.of(6, 15);
    var today = java.time.MonthDay.now();
    
    IO.println("Birthday: " + birthday);
    IO.println("Is today the birthday: " + birthday.equals(today));
}
```

`MonthDay` represents a month and day without a year, ideal for recurring  
annual events like birthdays and holidays. It can be combined with a year  
to create a full date.  

## Year creation
This example shows working with just a year.

```java
void main() {

    var year = java.time.Year.of(2024);
    IO.println("Year: " + year);
    IO.println("Is leap: " + year.isLeap());
    IO.println("Length: " + year.length() + " days");
}
```

`Year` represents a single year and provides year-specific operations like  
leap year checking. It can be combined with month and day to create a full  
date when needed.  

## Format with locale
This example demonstrates formatting dates with different locales.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var usFormat = date.format(java.time.format.DateTimeFormatter.ofLocalizedDate(
        java.time.format.FormatStyle.LONG).withLocale(java.util.Locale.US));
    var frFormat = date.format(java.time.format.DateTimeFormatter.ofLocalizedDate(
        java.time.format.FormatStyle.LONG).withLocale(java.util.Locale.FRANCE));
    
    IO.println("US: " + usFormat);
    IO.println("France: " + frFormat);
}
```

Locale-aware formatting produces region-specific date representations. The  
same date appears differently based on cultural conventions for date  
ordering and month names.  

## Custom formatter with symbols
This example shows creating formatters with custom symbols.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 14, 30, 45);
    var formatter = java.time.format.DateTimeFormatter.ofPattern(
        "yyyy-MM-dd'T'HH:mm:ss");
    var formatted = datetime.format(formatter);
    
    IO.println("Formatted: " + formatted);
}
```

Pattern symbols define how each datetime component appears. Single quotes  
escape literal characters in patterns. Common symbols include 'y' for year,  
'M' for month, 'd' for day, 'H' for hour, and 'm' for minute.  

## ISO formatters
This example demonstrates using predefined ISO formatters.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 14, 30, 45);
    
    IO.println("ISO_DATE: " + datetime.format(
        java.time.format.DateTimeFormatter.ISO_DATE));
    IO.println("ISO_TIME: " + datetime.format(
        java.time.format.DateTimeFormatter.ISO_TIME));
    IO.println("ISO_DATE_TIME: " + datetime.format(
        java.time.format.DateTimeFormatter.ISO_DATE_TIME));
}
```

ISO formatters produce standardized ISO-8601 strings. These formatters are  
ideal for APIs, data exchange, and persistence because they're unambiguous  
and widely supported.  

## Parse with strict resolver
This example shows using strict date parsing.

```java
void main() {

    try {
        var formatter = java.time.format.DateTimeFormatter.ofPattern("dd/MM/yyyy")
            .withResolverStyle(java.time.format.ResolverStyle.STRICT);
        var date = java.time.LocalDate.parse("31/02/2024", formatter);
        IO.println("Date: " + date);
    } catch (Exception e) {
        IO.println("Parse error: " + e.getMessage());
    }
}
```

The strict resolver style rejects invalid dates like February 31st. The smart  
resolver (default) would adjust such dates, while lenient accepts almost  
anything. Strict mode ensures data integrity.  

## Truncate to unit
This example demonstrates truncating datetime to a specific unit.

```java
void main() {

    var now = java.time.LocalDateTime.now();
    var truncated = now.truncatedTo(java.time.temporal.ChronoUnit.HOURS);
    
    IO.println("Original: " + now);
    IO.println("Truncated to hours: " + truncated);
}
```

The `truncatedTo` method zeros out all fields smaller than the specified  
unit. Truncating to hours sets minutes, seconds, and nanoseconds to zero,  
useful for grouping or comparing times by hour.  

## Between with ChronoUnit
This example shows calculating differences using ChronoUnit.

```java
void main() {

    var start = java.time.LocalDate.of(2024, 1, 1);
    var end = java.time.LocalDate.of(2024, 12, 31);
    
    var days = java.time.temporal.ChronoUnit.DAYS.between(start, end);
    var weeks = java.time.temporal.ChronoUnit.WEEKS.between(start, end);
    var months = java.time.temporal.ChronoUnit.MONTHS.between(start, end);
    
    IO.println("Days: " + days);
    IO.println("Weeks: " + weeks);
    IO.println("Months: " + months);
}
```

`ChronoUnit.between` calculates the difference between temporals in specific  
units. It provides an alternative to `Duration` and `Period` when you only  
need a single unit of measurement.  

## OffsetDateTime creation
This example demonstrates creating a datetime with UTC offset.

```java
void main() {

    var offset = java.time.ZoneOffset.ofHours(-5);
    var offsetDateTime = java.time.OffsetDateTime.of(
        2024, 6, 15, 14, 30, 0, 0, offset);
    
    IO.println("OffsetDateTime: " + offsetDateTime);
}
```

`OffsetDateTime` represents a datetime with a fixed UTC offset. Unlike  
`ZonedDateTime`, it doesn't include timezone rules, making it suitable for  
database storage or when offset is known but timezone is not.  

## OffsetTime creation
This example shows creating a time with UTC offset.

```java
void main() {

    var offset = java.time.ZoneOffset.ofHours(9);
    var offsetTime = java.time.OffsetTime.of(14, 30, 0, 0, offset);
    
    IO.println("OffsetTime: " + offsetTime);
}
```

`OffsetTime` combines time with a UTC offset. It's less common than  
`OffsetDateTime` but useful when you need to represent a time of day  
with timezone context but without a specific date.  

## Date range check
This example demonstrates checking if a date falls within a range.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var start = java.time.LocalDate.of(2024, 6, 1);
    var end = java.time.LocalDate.of(2024, 6, 30);
    
    var inRange = !date.isBefore(start) && !date.isAfter(end);
    IO.println("Date in range: " + inRange);
}
```

Range checking combines `isBefore` and `isAfter` methods. The negation  
handles edge cases where the date equals the start or end boundaries,  
making the range inclusive on both ends.  

## Week of year
This example shows getting the week number of the year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var weekOfYear = date.get(java.time.temporal.IsoFields.WEEK_OF_WEEK_BASED_YEAR);
    IO.println("Week of year: " + weekOfYear);
}
```

The `IsoFields.WEEK_OF_WEEK_BASED_YEAR` field returns the ISO week number.  
ISO weeks start on Monday and the first week contains the year's first  
Thursday, which may differ from calendar weeks.  

## Quarter of year
This example demonstrates getting the quarter of the year.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var quarter = date.get(java.time.temporal.IsoFields.QUARTER_OF_YEAR);
    IO.println("Quarter: " + quarter);
}
```

The `IsoFields.QUARTER_OF_YEAR` field returns 1-4 representing the quarter.  
This is useful for financial reporting and business analytics that operate  
on quarterly periods.  

## Day of quarter
This example shows getting the day number within the quarter.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var dayOfQuarter = date.get(java.time.temporal.IsoFields.DAY_OF_QUARTER);
    IO.println("Day of quarter: " + dayOfQuarter);
}
```

The `IsoFields.DAY_OF_QUARTER` field returns the day number (1-92) within  
the current quarter. This helps track progress through quarterly periods  
or calculate quarter-to-date metrics.  

## Working with TemporalQuery
This example demonstrates using temporal queries for custom extractions.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var precision = date.query(java.time.temporal.TemporalQueries.precision());
    
    IO.println("Precision: " + precision);
}
```

`TemporalQuery` allows extracting information from temporal objects using  
a functional approach. Predefined queries like `precision`, `zoneId`, and  
`chronology` provide metadata about the temporal object.  

## Custom TemporalAdjuster
This example shows creating a custom temporal adjuster.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var nextWorkday = date.with(temporal -> {
        var result = (java.time.LocalDate) temporal;
        do {
            result = result.plusDays(1);
        } while (result.getDayOfWeek() == java.time.DayOfWeek.SATURDAY || 
                 result.getDayOfWeek() == java.time.DayOfWeek.SUNDAY);
        return result;
    });
    
    IO.println("Next workday: " + nextWorkday);
}
```

Custom adjusters implement business logic for date manipulation. This example  
skips weekends to find the next workday, demonstrating how complex calendar  
rules can be encapsulated in reusable adjusters.  

## Min and max dates
This example demonstrates finding the minimum and maximum of multiple dates.

```java
void main() {

    var date1 = java.time.LocalDate.of(2024, 6, 15);
    var date2 = java.time.LocalDate.of(2024, 3, 20);
    var date3 = java.time.LocalDate.of(2024, 9, 10);
    
    var min = date1;
    if (date2.isBefore(min)) min = date2;
    if (date3.isBefore(min)) min = date3;
    
    var max = date1;
    if (date2.isAfter(max)) max = date2;
    if (date3.isAfter(max)) max = date3;
    
    IO.println("Min: " + min);
    IO.println("Max: " + max);
}
```

Finding the earliest or latest date from a collection uses comparison methods.  
This pattern is common in scheduling, deadline tracking, and determining  
valid date ranges from multiple sources.  

## Until method for ranges
This example shows using until to calculate temporal amounts.

```java
void main() {

    var start = java.time.LocalDate.of(2024, 1, 1);
    var end = java.time.LocalDate.of(2024, 12, 31);
    
    var period = start.until(end);
    IO.println("Period: " + period);
    
    var days = start.until(end, java.time.temporal.ChronoUnit.DAYS);
    IO.println("Days: " + days);
}
```

The `until` method calculates the amount between two temporals. Without a  
unit parameter it returns a `Period`, with a unit it returns a long value  
in that specific unit, providing flexible temporal arithmetic.  

## Negative duration and period
This example demonstrates working with negative temporal amounts.

```java
void main() {

    var negativeDuration = java.time.Duration.ofHours(-5);
    var negativePeriod = java.time.Period.ofDays(-10);
    
    var time = java.time.LocalTime.of(12, 0);
    var date = java.time.LocalDate.of(2024, 6, 15);
    
    IO.println("Time minus 5 hours: " + time.plus(negativeDuration));
    IO.println("Date minus 10 days: " + date.plus(negativePeriod));
}
```

Negative durations and periods allow subtracting time by using the `plus`  
method. This provides an alternative to the `minus` method and is useful  
when the direction of adjustment is determined dynamically.  

## Convert ZonedDateTime to OffsetDateTime
This example shows converting between timezone-aware types.

```java
void main() {

    var zonedDateTime = java.time.ZonedDateTime.now(
        java.time.ZoneId.of("America/New_York"));
    var offsetDateTime = zonedDateTime.toOffsetDateTime();
    
    IO.println("ZonedDateTime: " + zonedDateTime);
    IO.println("OffsetDateTime: " + offsetDateTime);
}
```

The `toOffsetDateTime` method converts from `ZonedDateTime` to  
`OffsetDateTime`, discarding timezone rules while preserving the offset.  
This is useful for persistence or when timezone rules aren't needed.  

## Midnight detection
This example demonstrates checking if a time is midnight.

```java
void main() {

    var midnight = java.time.LocalTime.MIDNIGHT;
    var time = java.time.LocalTime.of(0, 0, 0);
    
    IO.println("Is midnight: " + time.equals(midnight));
    IO.println("Midnight: " + midnight);
}
```

The `LocalTime.MIDNIGHT` constant represents 00:00:00. Comparing times  
against this constant or checking hours/minutes/seconds for zero determines  
if a time represents the start of day.  

## Noon detection
This example shows checking if a time is noon.

```java
void main() {

    var noon = java.time.LocalTime.NOON;
    var time = java.time.LocalTime.of(12, 0, 0);
    
    IO.println("Is noon: " + time.equals(noon));
    IO.println("Noon: " + noon);
}
```

The `LocalTime.NOON` constant represents 12:00:00. This constant simplifies  
code that needs to reference midday, common in scheduling and time-based  
business logic.  

## Era handling
This example demonstrates working with calendar eras.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var era = date.getEra();
    IO.println("Era: " + era);
}
```

The `getEra` method returns the calendar era, typically CE (Common Era) or  
BCE (Before Common Era) for the ISO calendar. Different chronologies may  
have different era systems.  

## Working with different chronologies
This example shows using non-ISO calendar systems.

```java
void main() {

    var isoDate = java.time.LocalDate.of(2024, 6, 15);
    var hijrahDate = java.time.chrono.HijrahDate.from(isoDate);
    
    IO.println("ISO date: " + isoDate);
    IO.println("Hijrah date: " + hijrahDate);
}
```

Java supports multiple calendar systems through the chronology API. The  
`HijrahDate` represents dates in the Islamic calendar, while other  
implementations support Japanese, Thai Buddhist, and other calendars.  

## Date equals with different types
This example demonstrates comparing dates across temporal types.

```java
void main() {

    var localDate = java.time.LocalDate.of(2024, 6, 15);
    var localDateTime = java.time.LocalDateTime.of(2024, 6, 15, 0, 0);
    var dateFromDateTime = localDateTime.toLocalDate();
    
    IO.println("Dates equal: " + localDate.equals(dateFromDateTime));
}
```

Direct comparison between different temporal types returns false even if they  
represent the same date. Extract the date component first for meaningful  
comparison across types like `LocalDate` and `LocalDateTime`.  

## Parse ISO instant
This example shows parsing an instant from an ISO-8601 string.

```java
void main() {

    var instantString = "2024-06-15T14:30:00Z";
    var instant = java.time.Instant.parse(instantString);
    IO.println("Parsed instant: " + instant);
}
```

The `Instant.parse` method accepts ISO-8601 formatted strings with a 'Z'  
suffix indicating UTC. This format is commonly used in APIs, logs, and  
database timestamps for its unambiguous representation.  

## Parse ZonedDateTime
This example demonstrates parsing a zoned datetime from a string.

```java
void main() {

    var zdt = java.time.ZonedDateTime.parse("2024-06-15T14:30:00+02:00[Europe/Paris]");
    IO.println("Parsed ZonedDateTime: " + zdt);
}
```

The parser handles both the offset (+02:00) and timezone identifier  
([Europe/Paris]) from the string. This comprehensive format ensures timezone  
information is preserved when serializing and deserializing datetimes.  

## Plus temporal amount
This example shows adding a temporal amount to a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var period = java.time.Period.ofMonths(3);
    var newDate = date.plus(period);
    
    IO.println("Original: " + date);
    IO.println("Plus 3 months: " + newDate);
}
```

The `plus` method accepts any `TemporalAmount` including `Period` and  
`Duration`. This polymorphic approach allows writing generic code that works  
with different temporal units without knowing the specific type.  

## Minus temporal amount
This example demonstrates subtracting a temporal amount from a datetime.

```java
void main() {

    var datetime = java.time.LocalDateTime.of(2024, 6, 15, 14, 30);
    var duration = java.time.Duration.ofHours(2);
    var earlier = datetime.minus(duration);
    
    IO.println("Original: " + datetime);
    IO.println("Minus 2 hours: " + earlier);
}
```

The `minus` method subtracts a `TemporalAmount` from the temporal object.  
Like `plus`, it works with both `Period` and `Duration`, providing flexible  
temporal arithmetic in a unified interface.  

## Range of date
This example shows getting the valid range for a date field.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var dayOfMonthRange = date.range(java.time.temporal.ChronoField.DAY_OF_MONTH);
    
    IO.println("Day of month range: " + dayOfMonthRange);
}
```

The `range` method returns the valid range of values for a temporal field.  
For DAY_OF_MONTH, this shows the valid days (1-30 or 1-31) based on the  
specific month and year, accounting for leap years.  

## Is supported field
This example demonstrates checking if a temporal field is supported.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var time = java.time.LocalTime.of(14, 30);
    
    IO.println("Date supports HOUR_OF_DAY: " + 
        date.isSupported(java.time.temporal.ChronoField.HOUR_OF_DAY));
    IO.println("Time supports HOUR_OF_DAY: " + 
        time.isSupported(java.time.temporal.ChronoField.HOUR_OF_DAY));
}
```

The `isSupported` method checks if a temporal object supports a specific  
field or unit. `LocalDate` doesn't support time fields, while `LocalTime`  
doesn't support date fields, making this check essential for generic code.  

## From temporal accessor
This example shows creating temporal objects from TemporalAccessor.

```java
void main() {

    var accessor = java.time.LocalDateTime.now();
    var date = java.time.LocalDate.from(accessor);
    var time = java.time.LocalTime.from(accessor);
    
    IO.println("Date: " + date);
    IO.println("Time: " + time);
}
```

The static `from` method extracts a temporal type from any `TemporalAccessor`  
that contains the required fields. This pattern enables converting between  
compatible temporal types in a type-safe manner.  

## Temporal unit operations
This example demonstrates adding temporal units to a date.

```java
void main() {

    var date = java.time.LocalDate.of(2024, 6, 15);
    var plusWeeks = date.plus(2, java.time.temporal.ChronoUnit.WEEKS);
    var plusYears = date.plus(5, java.time.temporal.ChronoUnit.YEARS);
    
    IO.println("Original: " + date);
    IO.println("Plus 2 weeks: " + plusWeeks);
    IO.println("Plus 5 years: " + plusYears);
}
```

The overloaded `plus` method accepts a long value and a `TemporalUnit`,  
providing an alternative to dedicated methods like `plusWeeks`. This approach  
is useful when the unit is determined dynamically at runtime.  

