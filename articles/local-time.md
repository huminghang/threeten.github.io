---
layout: article
title: LocalTime
subtitle: User guide for the LocalTime class
categories:
- articles
tags: local time hour minute second nano schedule
---

The `LocalTime` class represents the time and has got no representation of the date. 

It is ideal for representing time on a wall clock such as 10:15:30. For example when we say "Time is ten past three", it can be represented using 'LocalTime' as 3:10:00.
LocalTime supports nanosecond precision. The minimum value for LocalTime is midnight (00:00:00.0) at start of the day and maximum value is one nanosecond before midnight(23:59:59.999999999) at end of day. 
 

The "local" part of the name refers to the local time-line.
Specifically, a `LocalTime` has no reference to a time-zone or offset from UTC/Greewich. 

#### Creating a LocalTime

There are a number of ways to create a `LocalTime`.

##### Current Time

Creating the current time can be created using the following `now` methods:

{% highlight java %}
LocalTime a = LocalTime.now();
LocalTime b = LocalTime.now(ZoneId.of("Europe/Paris"));
LocalTime c = LocalTime.now(aClock);
{% endhighlight %}

The key point is that determining current time requires knowledge of the time-zone.
The first method (a) uses the Java default time-zone, as per `TimeZone.getDefault()`.
The second method (b) allows the time-zone to be explicitly controlled.
The third method (c) uses a `Clock` object, which provides further control over the current instant and time-zone. This will come handy in testing scenarios as we can provide an alternate clock. 

##### Using fields

If you want to hard code the creation of time, or have fields available, these factory
methods can be used:

{% highlight java %}

LocalTime a = LocalTime.of(12,30); 				// 12:30:00
LocalTime b = LocalTime.of(12,30,40);			  	// 12:30:40 	
LocalTime c = LocalTime.of(12, 30, 40, 987654321);		// 12:30:40.987654321	
LocalTime d = LocalTime.ofSecondOfDay(2); 			// 00:00:02
LocalTime e = LocalTime.ofSecondOfDay(2, 987654321);	        // 00:00:02.987654321
LocalTime f = LocalTime.ofNanoOfDay(2 * 1000000000L + 17); 	// 00:00:02.000000017

{% endhighlight %}

The first one, (a) , creates time from hour and minutes. In this case the seconds and nanoseconds are considered as zero. 

The second one, (b), creates time from hour, minutes and seconds. In this case the nanoseconds are considered as zero.
 
The third one, (c), creates time from hour, minutes, seconds and nanoseconds. 

The fourth one, (d), creates time from second of day which is calculated from midnight 00:00.

The fifth one, (e), creates time from second of day and nanoseconds after that which is calculated from midnight 00:00.

The sixth one, (f), creates time from nanosecond of day which is calculated from midnight 00:00:00. Remember that nanosecond is billionth of a second. ie 1 second =  1000,000,000 nanoseconds.


Valid value for an hour is 0 - 23 and for minutes/seconds is 0 - 59. If an invalid value is passed in, say 25 as value of hour, 61 as value of minute/second etc, then an exception is thrown. 


