# Frequently Asked Questions #

### I get a 'Connection Error' whenever I try to sync! ###

Yup, as of 19 Dec 2011, Google has changed their Bookmarks API in a major way, which breaks GMarks.  I'm working quickly to create a fix!

### How do I Edit/ Delete a bookmark? ###

Long-press a bookmark from the list view.  It will let you edit tags, title, description, or delete the bookmark.

### Where's the search feature? ###

Press the 'Menu' key on your device.  If you don't see a search button, that probably means you have a hardware search button on your device.  This button will launch search within the GMarks app.

### How do I enable Global Search? ###

_i.e. Can I add GMarks to the search widget?_ <br />
_Can I search GMarks when I press the dedicated search key from the home screen on my device?_

To enable global search, go to your system 'Settings' (not GMarks settings) then choose "Search" -> "Searchable Items" and select "GMarks" from the list.

### I deleted a bookmark from the website, but I still see it in GMarks! ###

This is because GMarks only sync's **changed** bookmarks, and GMarks can't tell if a bookmark has been deleted or just hasn't been changed since the last sync.  You can fix this by using the "full sync" operation in GMarks settings.  This will refresh your entire GMarks list from the server, removing duplicates.


### I thought you said I didn't have to type my username and password?!?  I don't trust you! ###

Many apps that use an unofficial Google API will actually ask for and store your username and password directly in their app.  I'm doing a little better by letting you send your username and password **directly** to Google through the browser, and then using your session token to perform the Google Bookmarks requests in GMarks.  **Unfortunately, this is the best _anyone_ can do until Google releases a Bookmarks API that supports AuthSub or OAuth authentication.**  See also the PrivacyPolicy.

If this still bothers you, please tell Google by [voting for this issue](http://code.google.com/p/gdata-issues/issues/detail?id=120).

### It says I logged in successfully, but every time I try to sync it directs me back to the login page ###

It's possible you accidentally unchecked 'remember me' on the login page?  Under 'Settings,' tap 'Log Out' and then try to sync again which should let you re-enter your login.