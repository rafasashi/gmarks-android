# Introduction #

There is no official Google Bookmarks API, but like most Google services, they use a REST-based API for their AJAX calls.  Hence, the calls can be reverse-engineered to access most of the core functionality with a minimal amount of HTML parsing.

The most likely reason for lack of an 'official' Bookmarks API is due to missing support for OAuth or AuthSub authentication which Google uses to allow third-parties to access content without the user explicitly supplying their credentials through a third-party interface.

Marcelino Martins first documented the Google Boomarks form POST and XML feed methods, which [can be found on his website](http://www.mmartins.com/mmartins/googlebookmarksapi/).


# Details #

This is messy because it's pasted from a text file.  Redacted values are filled with `_______`

```

AUTH REQUESTS ------------

GET https://www.google.com/accounts/ServiceLogin?

POST https://www.google.com/accounts/ServiceLoginAuth

?Email=_____&GALX=___________&Passwd&PersistentCookie=yes&asts=
 &continue=https%3A%2F%2Fwww.google.com%2Fbookmarks%2Fl&dsh=-4572327023467669697
 &followup=https%3A%2F%2Fwww.google.com%2Fbookmarks%2Fl&nui=1&rmShown=1&secTok=
 &service=bookmarks&signIn=Sign%20in&timeStmp=

## bunch of cookies created here

GET https://www.google.com/accounts/CheckCookie?continue=https%3A%2F%2Fwww.google.com%2Fbookmarks%2Fl
 &followup=https%3A%2F%2Fwww.google.com%2Fbookmarks%2Fl&service=bookmarks&chtml=LoginDoneHtml


BOOKMARKS API REQUESTS ------------------


GET https://www.google.com/bookmarks/api/threadsearch?q=&start=&fo=&g=

{"threadTitles":[{"sectionTitle":"","sectionContent":[{"labels":[".NET",
            "reference"],"url":
          "http://msdn2.microsoft.com/en-us/library/ms313865(msdn.10).aspx",
          "signedUrl":"....",
          "elementId":"_______","host":
          "msdn2.microsoft.com","threadId":"______","title":
          ".NET Framework SDK","titleHtml":".NET Framework SDK","titleShort":
          ".NET Framework SDK","description":"","descriptionHtml":"",
          "timestamp":1146749346703,"formattedTimestamp":"May 4, 2006",
          "modifiedTimestamp":1146749346703,"formattedModifiedTimestamp":
          "May 4, 2006","owner":{"photoUrl":
            "/s2/photos/public.....",
            "name":"Thomas Nichols","email":""},"isOwnedByUser":true,
          "isSharedWithUser":false,"isShared":false,"numSharees":0,
          "isPublished":false}, ... ]}],"start":0,"nr":329}


=== Meaning of query parameters: ===

g=Time|Title (sort order)
q=label%3A%22arduino%22 (sort by label)
start=1 (offset)
nr=25 (count) -- max=25 per query!
fo=Starred (Not sure what this is...)


 ALTERNATE LOOKUP method:
 /bookmarks/lookup?q=label:auto&hl=en




GET https://www.google.com/bookmarks/api/bookmark?xt=_________&op=LIST_LABELS

 RESPONSE
{"labels":[".NET","AJAX","arduino","art",___________,"^none"],"counts":[24,8,5,______,58]}


GET https://www.google.com/bookmarks/api/thread?op=FetchSummary

 RESPONSE
{"createdThreads":[],"sharedThreads":[],"starredItems":[]}


GET http://www.google.com/bookmarks/api/thread?op=ShowThread&threadID=


GET https://www.google.com/bookmarks/api/resultclick?la=17&tn=54&url&dt
 &xt=______%3A_______&mi=%20FILTER_OWNER%3A%20Starred%20GROUPING%3A%20Title

 RESPONSE
203 (no content)


POST https://www.google.com/bookmarks/api/thread?xt=______%3A_______&op=Star

 application/x-www-form-urlencoded
 td	{"results":[{"threadId":"_______","elementId":0,"authorId":0,
         "title":"My Blog","timestamp":0,"formattedTimestamp":0,
         "url":"http://blog.thomnichols.org","signedUrl":"",
         "previewUrl":"","snippet":"This is a test bookmark to sync to the mobile list.",
         "threadComments":[],"parentId":"_______","labels":["mobile"]}]}

 RESPONSE
)]}'
{"results":[{"threadresult":{"threadId":"_____","elementId":
        "__________","lastEditedBy":{"photoUrl":
          "/s2/photos/public/_____________",
          "name":"Thomas Nichols","email":""},"lastEditedByCurrentUser":
        true,"owner":{"photoUrl":
          "/s2/photos/public/_____________",
          "name":"Thomas Nichols","email":""},"isOwnedByUser":true,"title":
        "My Blog","timestamp":1294187376921,"formattedTimestamp":
        "\u003c 1 second ago","url":"http://blog.thomnichols.org/",
        "faviconUrl":"http://blog.thomnichols.org/favicon.ico","host":
        "blog.thomnichols.org","signedUrl":
        "http://www.google.com/url?q_________",
        "previewUrl":
        "https://www.google.com/webpagethumbnail?__________",
        "snippet":"This is a test bookmark to sync to the mobile list.",
        "parentId":"_______","isStarred":false,"labels":["mobile"]},
      "isUserFollowing":true,"localinfo":{}}]}
 
 

----------- ALTERNATE 'Create' method: -------------

GET https://www.google.com/bookmarks/mark?op=edit&output=popup

 Parse out of response: 
 <input type=hidden name=sig value="_____________">  <-- Needed in POST

POST https://www.google.com/bookmarks/mark?sig=______________=en&btnA

 Parameters application/x-www-form-urlencoded
	annotation	Test description.
	bkmk	https:www.google.com/bookmarks/l
	btnA	Add bookmark
	labels	test, mobile
	prev	/mark
	sig	Y6gx76mpQpVEfAWzrWP6Gw
	title	Anther test bookmark
 

 
POST https://www.google.com/bookmarks/api/thread?xt=______%3A_______&op=DeleteItems

 application/x-www-form-urlencoded
 td	{"deleteAllBookmarks":false,"deleteAllThreads":false,"urls":[],"ids":["_________"]}

 RESPONSE
)]}'
{"deletedIds":["______________"],"numDeletedBookmarks":
  1,"numDeletedThreads":0}



POST https://www.google.com/bookmarks/api/thread?xt=_____________&op=UpdateThreadElement

 application/x-www-form-urlencoded
 td	{"threads":[],"threadQueries":[],"threadResults":[{"threadId":"_____________",
         "elementId":"__________","authorId":0,"title":"___________",
         "timestamp":0,"formattedTimestamp":0,"url":"http://www.1up.com/do/feature?cId=3156339",
         "signedUrl":"","previewUrl":"","snippet":"bookmark description",
         "threadComments":[],"parentId":"","labels":["games"]}],"threadComments":[]}

 RESPONSE
)]}'
{"threads":[],"threadQueries":[],"threadResults":[{"threadId":
      "___________","elementId":"__________________",
      "lastEditedBy":{"photoUrl":
        "/s2/photos/public/_________",
        "name":"Thomas Nichols","email":""},"lastEditedByCurrentUser":true,
      "owner":{"photoUrl":
        "/s2/photos/public/______________p",
        "name":"Thomas Nichols","email":""},"isOwnedByUser":true,"title":
      "101 Free Games 2007 - The Best Free Games on the Web! from 1UP.com",
      "timestamp":1294187662692,"formattedTimestamp":"\u003c 1 second ago",
      "url":"http://www.1up.com/do/feature?cId\u003d3156339","faviconUrl":
      "http://www.1up.com/favicon.ico","host":"www.1up.com","signedUrl":
      "http://www.google.com/url?___________",
      "previewUrl":
      "https://www.google.com/webpagethumbnail?_______________",
      "snippet":"Your guide to the best free games on the Web. 2","parentId":
      "","isStarred":false,"labels":["games"]}],"threadComments":[]}


 DATE BASED SEARCH for Google.com (this does NOT work for bookmarks!)

Day/Month/Year:
	tbs=qdr:d
	tbs=qdr:m
	tbs=qdr:y

Custom date range:
	&tbs=cdr%3A1%2Ccd_min%3A12%2F26%2F2010%2Ccd_max%3A2%2F5%2F2011
       cdr:1,cd_min:12/26/2010,cd_max:2/5/2011


```