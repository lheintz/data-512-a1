# Readme
> __Set Up__  
> The tools used on this project were Anacoda 4.6.14, Python 3.6, VSCode 1.30.1, Jupyter Notebook 5.7.4, and linux terminal. Operating system was MacOSX Mojave 10.14.6

## Goal
The goal of this project is to pull data from wikipedia on the site traffic. There is a variety of data in a few different formats, ranging from mobile web, mobile app, and desktop view counts. Data will be pulled for all dates possible and brief time series analysis will be performed to assess traffic over time.

## Sources
The source of these data has been from the Wikimedia Foundation REST API: https://www.mediawiki.org/wiki/REST_API

The terms and conditions of the REST API are available here: https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions

The wikimedia REST API is licensed by [CC-BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) and [GFDL](https://www.gnu.org/licenses/fdl-1.3.html). 

## API Documentation
Legacy Pagecounts API documentation is available [here](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts).  
Pageviews API documentation is available [here](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews).


## Data Definition
The columns for the data pulled directly from the API are: 

__project__: Which is always 'en.wikipedia.org'  
__access-site__: indicates whether it is mobile, desktop, web, or app  
__granularity__: Indicates how granualar of data is pulled - in this case only monthly was pulled. More granular data is available in the new Pageviews API than old Pagecounts  
__start__: The start date for the requested data, in the format `YYYYMMDDHH`  
__end__: The end date for the requested data, in the format `YYYYMMDDHH`  

The data in my final output CSV file is:  
`month` - the month (int)  
`year` - the year YYYY (int)  
`pagecount_all_views` - the total number of views summing desktop and mobile views from legacy pagecount API  
`pagecount_desktop_views` - the total number of desktop views from the legacy pagecount API  
`pagecount_mobile_views` - the total number of mobile views from the legacy pagecount API  
`pageview_all_views` - the total number of views summing the desktop, mobile web, and mobile app views from the new pageview API, excluding spider traffic  
`pageview_desktop_views` - the total number of desktop views from the new pageview API, excluding spider traffic   
`pageview_mobile_views` - the total number of mobile views, summing the mobile app and mobile web views from the new pageview API, excluding spider traffic  

## Notes for Reuse / Special Considerations
For the purposes of this investigation, when possible, spiders (crawler views) were filtered. In the legacy API, there was no option to eliminate crawler traffic from the metrics. In the pageviews API, there is an option to choose from User or Spider traffic. In this case, only the user traffic was used which accounts for the drop that seemingly occurs in 2016. This is actually when the new API took effect. Therefore the views prior to this point may be erroneously high. The steep drop off accounts for the switch over in the APIs being used.