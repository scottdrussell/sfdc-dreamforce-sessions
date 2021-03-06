sfdc-dreamforce-sessions
========================

This document details how I went about creating the unofficial Excel export of Dreamforce 2014 sessions posted on the [Success Community](https://success.salesforce.com/06930000003yys0).

I'm preparing for my first Dreamforce conference and as of the time of this writing the official Agenda Builder has not been released. To review the 1,000+ sessions and begin to plan out which I want to attend, I have to use the paginated browser experience at http://www.salesforce.com/dreamforce/DF14/sessions.jsp. Not ideal. I'd rather slice and dice the data and plan out my sessions in Excel for now until I see how the official Agenda Builder app operates.

But how to get the list of all the Dreamforce sessions so I can put them into Excel?

Getting Started
===============

1. I viewed the source of the http://www.salesforce.com/dreamforce/DF14/sessions.jsp page with my browser and noticed they included this script towards the top `<script type="text/javascript" src="http://www.sfdcstatic.com/common/assets/js/min/df14-sessions-min.js"></script>`
2. It was minified, so I used http://www.jspretty.com/ to format the code for easier reading. Although the code had also been somewhat obfuscated when minified so I couldn't decipher variable names. Further inspection of the html source code showed this line `<div class="ng-scope" ng-controller="MainCtrl" ng-app="app">` so I began hunting for **MainCtrl** angular controller definition within the `df14-sessions-min.js` file
3. Once I found the **MainCtrl** controller, I read down a few lines and noticed a URL invocation to `/assets/js/filterSessions.jsp?eventId=a1Q30000002aJu6EAE` so in my browser I went to http://www.salesforce.com/assets/js/filterSessions.jsp?eventId=a1Q30000002aJu6EAE and voila! All the dreamforce sessions in wonderful .json format ready for our consumption!
4. At this point, I sparked the idea that I could write a simple AngularJS app to build out an HTML table of all the Dreamforce session data important to me then I could copy & paste that output into Excel. That is the code in this repository under the `dreamforce` folder. I welcome improvements to the code, my wish list is on the [issues page](/../../issues)
5. Since I'm running my AngularJS app locally, my browser security blocks any ajax urls to download the session .json data identified in Step 3 due to Cross-Origin Request (CORS) so I resigned to just saving a copy of the session data to [local .json file](dreamforce/sessionData.json)
6. Next, I wrote a very simple [angular controller](dreamforce/controllers.js) that read the json file and bound the data to be rendered in the [index.html](dreamforce/index.html) page.
7. I added some bootstrap css to style the table just for fun, but not necessary since I'm copying the data out to Excel anyways!

Please note, since the official listing of Dreamforce sessions is subject to change at anytime, you may want to periodically download the latest session data .json file.
