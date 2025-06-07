# What is Prometheus?
<b>Simply open-source monitoring and alerting toolkit</b>. 
<li>It collects metrics. What is the fuck is metrics? Relax bro, it's time-series data. Ok give me some example of time-series data.</li>
## What is time-series data?
Imagine you're checking your body temperature every hour when you're sick:

- 9:00 AM: 98.6°F
- 10:00 AM: 99.1°F
- 11:00 AM: 100.3°F
- 12:00 PM: 101.0°F

## This is a sequence of data points. 
*Time-Series = Measurements + Timestamps**
In technology, it works exactly the same way. Some examples:

## Website Traffic:
<ul>
- Jan 1, 9:00: 120 visitors
- Jan 1, 9:05: 135 visitors
- Jan 1, 9:10: 158 visitors  
</ul>


## Server CPU Usage:
<ul>
- 2023-03-15 14:00: 45% usage
- 2023-03-15 14:01: 48% usage
- 2023-03-15 14:02: 52% usage
</ul>


## Stock Prices:
<ul>
- APL 10:00: $182.30
- AAPL 10:01: $182.15
- AAPL 10:02: $182.45 
</ul>


## Why "Time is the Primary Axis"?
This just means: The order matters (9:00 AM data comes before 10:00 AM). We care about how values change over time. The time between measurements is regular (every minute, every hour, etc.)

