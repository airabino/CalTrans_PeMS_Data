# CalTrans_PeMS_Data
Code for pulling station level data from CalTrans PeMS

The goal is to automate pulling data from CalTrans's PeMS system

Pulling data requires authentication credentials which can be made at:

https://pems.dot.ca.gov/

An example request for pulling vehicle volume data from a single station is

https://pems.dot.ca.gov/?report_form=1&station_id=1114091&dnode=VDS&content=loops&tab=det_timeseries&export=text&s_time_id=1706659200&s_time_id_f=01%2F31%2F2024+00%3A00&e_time_id=1706705940&e_time_id_f=01%2F31%2F2024+12%3A59&tod=all&tod_from=0&tod_to=0&dow_0=on&dow_1=on&dow_2=on&dow_3=on&dow_4=on&dow_5=on&dow_6=on&holidays=on&q=vmt&q2=&gn=hour

Breaking the example down:

Endpoint:

https://pems.dot.ca.gov/?

Format of the output as text:
report_form=1

Station ID - find these can be found for a given region/freeway at https://pems.dot.ca.gov/?fwy=5&dir=N&dnode=Freeway or similar:

&station_id=1114091

Specifying the types of stations to look at
&dnode=VDS
&content=loops

Specifying report parameters:
&tab=det_timeseries
&export=text

Specifying start an end time - are both formats needed?
&s_time_id=1706659200
&s_time_id_f=01%2F31%2F2024+00%3A00
&e_time_id=1706705940
&e_time_id_f=01%2F31%2F2024+12%3A59

Scope - TOD and DOW to be considered
&tod=all
&tod_from=0
&tod_to=0
&dow_0=on
&dow_1=on
&dow_2=on
&dow_3=on
&dow_4=on
&dow_5=on
&dow_6=on
&holidays=on

Queried data - vmt is what we want but it should be optional - lets not do the second query
&q=vmt
&q2=

Time step - {hour, day, week, month}
&gn=hour

these options can be experimented with on the website at https://pems.dot.ca.gov/?dnode=Freeway&content=loops&tab=det_timeseries&fwy=5&dir=N

Note that session authentication is required!!!! - see notebook

To do:

make a library which allows for pulling this data. the base pulling function shoudl handle authentication with inputted user and pass and should allow for specifying the parameters. Higher level functions should allow for pulling for all stations from sets such as highways, regions, counties, etc. A dictionary containing these regions, loaded at startup would be good to have. Repo should be formatted for PyPI.