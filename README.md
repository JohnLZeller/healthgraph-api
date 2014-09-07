healthgraph-api
===============

About
-----

Python Client Library for 
[Health Graph API](http://developer.runkeeper.com/healthgraph). 
The API can be used for accessing [RunKeeper](http://runkeeper.com) for retrieving, 
updating, deleting and uploading Fitness Activity and Health Measurement Information.

The Health Graph API uses OAuth 2.0 for security. Every application must be registered 
with the [Applications Portal of Health Graph](http://runkeeper.com/partner). 
Once registered, the application will be assigned a unique client identifier and 
client secret for use with the Health Graph API.

More detailed and updated information for the project is published in the 
[Health Graph API Project Web Page](http://aouyar.github.com/healthgraph-api/).

For information on other projects you can check 
my [GitHub Personal Page](http://aouyar.github.com)
and [GitHub Profile](https://github.com/aouyar).


Download
--------

New versions of the code are be published for download 
at [PyPI - the Python Package Index](http://pypi.python.org/pypi/healthgraph-api) 
periodically.

You can download the latest development version of this code that is hosted 
at [GitHub](https://github.com/{{ site.user }}/{{ page.prjname }}) either
in [ZIP](https://github.com/aouyar/healthgraph-api/zipball/master)
or [TAR](https://github.com/aouyar/healthgraph-api/tarball/master) 
format.

You can also get the latest development version of the code by cloning  
the [Git](http://git-scm.com) repository for the project by running:

	git clone git://github.com/aouyar/healthgraph-api


Installation
------------

The easiest way to install the code is to use [pip](http://www.pip-installer.org/).

Install the newest version from [PyPI](http://pypi.python.org/pypi/healthgraph-api):

	pip install healthgraph-api
	
Install the latest development version:

	pip install git+https://github.com/aouyar/healthgraph-api.git#egg=healthgraph-api
	

The other option is to download and uncompress the code manually and execute the 
included _setup.py_ script for installation:

	./setup.py install
	

Example
------------
This example serves to demonstrate basic functionality.

```python
python
>>> import healthgraph
>>> auth = healthgraph.authmgr.AuthManager('123456789abcdefghijklmnopqrstuvw', 'wvutsrqponmlkjihgfedcba987654321', 'http://www.example.com')
>>> auth.get_login_url()
'https://runkeeper.com/apps/authorize?redirect_uri=http%3A%2F%2Fwww.example.com&response_type=code&client_id=123456789abcdefghijklmnopqrstuvw'
```

Visit the link printed by the call to auth.get_login_url() in your Browser and allow access to your application. Once you are redirected, look for the code in the address bar. You should see something like 'http://www.example.com/?code=wvutsrqponml987654321kjihgfedcba'

```python
>>> access_token = auth.get_access_token('wvutsrqponml987654321kjihgfedcba')
>>> healthgraph.init_session(access_token)
>>> user = healthgraph.resources.User()
```

Your session is active and you have your User object, so now you can grab your data! For instance, let's say I wanted to see how many miles I have run this week.

```python
>>> user.get_records()._prop_dict['totals']['Running']['THIS_WEEK']
0.0
```

That's it for this short example!

Licensing
---------

_Healthgraph-API_ is copyrighted free software made available under the terms of the 
_GPL License Version 3_ or later.

See the _COPYING_ file that acompanies the code for full licensing information.
