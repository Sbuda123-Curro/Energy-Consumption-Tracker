
# Energy Consumption Tracker

An Android app that estimates the monthly electricity use and cost of a household appliance, rates the result, gives a short energy-saving tip, and saves every report to a local SQLite database. Built in Java as a coursework project for the ITMBA module at Eduvos (Mobile App Development).

## Features
- **Appliance input** with name, power rating (W), daily usage (hours), tariff (R/kWh) and a category (Kitchen, Entertainment, Lighting, Heating, Cooling)
- **Input validation**: required fields, numeric checks, positive values, and usage between 0 and 24 hours
- **Calculation** of daily consumption, monthly consumption and monthly cost
- **Energy rating and recommendation** based on monthly kWh
- **Saved reports**: every calculation is stored in SQLite and can be viewed later from the home screen

## How it calculates

```
daily kWh   = (power in watts x hours per day) / 1000
monthly kWh = daily kWh x 30
monthly cost = monthly kWh x tariff (R per kWh)
```

| Monthly use | Rating | Recommendation |
|---|---|---|
| under 150 kWh | Excellent | Keep your current usage |
| 150 to under 300 kWh | Good | Consider LED lighting |
| 300 to under 500 kWh | Average | Reduce use during peak hours |
| 500 to under 700 kWh | High Consumption | Replace old appliances with efficient models |
| 700 kWh and above | Very High Consumption | Immediate action recommended |

## Screens and flow

```
MainActivity (home)
 |- Start Calculation -> InputActivity -> Calculate & Save -> ResultsActivity
 |- View Saved Reports -> HistoryActivity (reads from SQLite)
 '- Exit

ResultsActivity
 |- Calculate Again -> InputActivity
 |- Home -> MainActivity
 '- Exit
```

## Project structure

```
app/src/main/java/com/example/energytracker/
  MainActivity.java            Home screen
  InputActivity.java           Appliance form, validation, save
  ResultsActivity.java         Shows the saved report with rating and advice
  HistoryActivity.java         Lists all saved reports
  Appliance.java               Model class
  ElectricityCalculator.java   Consumption and cost maths
  Recommendation.java          Rating and advice logic
  DatabaseHelper.java          SQLite storage (SQLiteOpenHelper)
app/src/main/res/layout/       XML layouts for each screen
```

## Tech
- Java 11, Android Gradle Plugin 8.2.2
- `minSdk 24`, `compileSdk` and `targetSdk` 34
- AndroidX AppCompat, SQLite (`SQLiteOpenHelper`)

## Run it
1. Install [Android Studio](https://developer.android.com/studio).
2. Clone this repo and choose **File > Open** on the project folder.
3. Let Gradle sync (Android Studio creates the Gradle wrapper if it's missing).
4. Run on an emulator or a device running Android 7.0 (API 24) or higher.

## Improvements after submission
Changes made after the original coursework submission:
- Decimal input now accepts a comma (`2,50`) as well as a dot, for phones with South African keyboard layouts
- Energy rating and recommendation are calculated before saving, so every stored report is complete
- Removed the always-on notification dot, which did not link to any feature
- Removed the unnecessary `System.exit(0)` call and relied on `finishAffinity()` to close the app
- Documented why `onUpgrade` recreates the table, and added the missing `proguard-rules.pro` file

## Notes
This is a personal portfolio record of my own coursework. Please don't reuse it for your own submissions.
