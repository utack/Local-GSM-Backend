GSM LocationProvider backend for µg UnifiedNlp
==============================================

The µg Project at https://github.com/microg has a unified network location provider that accepts backends for the actual location lookup. This project implements a cell-tower based lookup for your current location.

This "GSM Location Backend" works without network connectivity and will
never post your data anywhere.

The database needed to lookup cell tower locations resides on the phone. A facility in the setting menu allows you to create a database using data from OpenCellID and/or Mozilla Location Services CSV files.

Alternatively, the on-phone database can be generated from scripts at https://github.com/n76/lacells-creator Those scripts gather tower information from OpenCellId http://opencellid.org and Mozilla Location Services https://location.services.mozilla.com

You can improve the quality of the data used by this location provider by contributing to either or both of those projects.

This software is licensed as "Apache License, Version 2.0" unless noted
otherwise.

This software is derived from LocalGSMLocationProvider at https://github.com/rtreffer/LocalGSMLocationProvider but differs as follows:

1. This software uses a sqlite database rather than the custom built one in LocalGSMLocationProvider.
2. This software does not ship with a built in database. Databases can be generated with the scripts at https://github.com/n76/lacells-creator
3. The database used by this software includes an estimated range of coverage for each cell tower. That information is used to provide a location estimate weighted by coverage area and to make an estimate of position accuracy. (The original LocalGSMLocationProvider assumes 800 meter range for all towers.)

Requirement for building
========================

1. Android development platform

Requirements on phone
=====================
1. This is a plug in for µg UnifiedNlp which can be installed from f-droid.

How to build and install
========================

1. ant debug
2. adb install bin/android_apps_gsmlp-debug.apk

Setup on phone
==============
1. Install a cell tower database. Either use the settings menu to select the data sources and mobile country codes (mcc) that you desire or use the scripts at https://github.com/n76/lacells-creator to build and install a database.
2. In the NLP Controller app (interface for µg UnifiedNlp) select the "GSM Location Backend".

Notes on generating the database
================================
The on-phone database can be created using this settings in the app or via scripts located at https://github.com/n76/lacells-creator in either case the following applies:

1. OpenCellID requires an API key to download its CSV file and limits downloads to one per day. Information on getting an API key can be found at http://wiki.opencellid.org/wiki/How_to_join
2. Mozilla publishes new CSV files once per day.

Both of these are large files and take time to transfer and process: The current OpenCellID gzip 152MB data file contains over 6.7 million records and Mozilla’s gzip 48MB data file contains over 2.2 million records. You are very likely to want to filter the data going into the on-phone database so that it only contains the Mobile Country Codes (MCCs) in your area of interest. For the United States (MCC codes of 310 and 311) the final on-phone database is about 96MB.

At least on a Google Galaxy Nexus (Maguro), download and creation of the database is much slower than using the scripts at https://github.com/n76/lacells-creator though with a decent data connection it can be done in a reasonable amount of time directly on the phone.
