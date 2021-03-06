Outlook Web Access Export Tools
===============================

- The POP daemon should be usable in the current version, I've tested it with Evolution Mail on Ubuntu 10.10 and GMail Mail Fetcher</li> 
- `gmail.py` should be usable if you call the append() function manually after fetching the data using `scraper.py`

Auto-download New Emails to GMail's Mail Fetcher from Outlook Web Access
------------------------------------------------------------------------

1. Open port `2221` on the machine you're going to run `popdaemon.py` on so Google's servers can access it
2. `python popdaemon.py --unread --owa-server='https://webaccess.corp-domain.com'`
3. Follow Google's instructions for Mail Fetcher, give it your IP address for the POP server, and 2221 as the port

Origin Documentation from [weboutlook](http://code.google.com/p/weboutlook/)
----------------------------------------------------------------------------

weboutlook is a Python module that retrieves full, raw e-mails from Microsoft Outlook Web Access by screen scraping. It can do the following:

- Log into a Microsoft Outlook Web Access account with a given username and password.
- Retrieve all e-mail IDs from the first page of your Inbox.
- Retrieve the full, raw source of the e-mail with a given ID.
- Delete an e-mail with a given ID (technically, move it to the 'Deleted Items' folder).

#### Using scraper.py directly

	>>> from scaper import OutlookWebScraper

	# Throws InvalidLogin exception for invalid username/password. 
	>>> s = OutlookWebScraper('https://webmaildomain.com', 'username', 'invalid password') 
	>>> s.login() Traceback (most recent call last):
	...
	scraper.InvalidLogin
	
	>>> s = OutlookWebScraper('https://webmaildomain.com', 'username', 'correct password') 
	>>> s.login()

	# Display IDs of messages in the inbox. 
	>>> s.inbox() '/Inbox/test-3.EML'

	# Display IDs of messages in the 'sent items' folder. 
	>>> s.get_folder('sent items') '/Sent%20Items/test-2.EML'

	# Display the raw source of a particular message. 
	>>> print s.get_message('/Inbox/Hey%20there.EML') ...

	# Delete a message. 
	>>> s.delete_message('/Inbox/Hey%20there.EML')
