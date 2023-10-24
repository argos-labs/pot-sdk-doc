<<[Go to previous page](ARGOS_RPA_POT_SDK_on_Windows10.md)

# Preparing private repository

After building a plugin you must upload the plugin to your private (test) repository for test with STU and PAM. You can then ask ARGOS LABS to publish it to the entire ARGOS Low-code community or to publish it to a designated repository for their private usage.

This section will guild you to set up your Python private repository. After setting it up you can coonfigure it at Supervisor so that your STU will see you plugin there fow showing at his toolbox.

## Installation of private repository using pypicloud

We are using normal Python repository scheme. We will simply use [pypicloud](https://pypicloud.readthedocs.io/en/latest/topics/getting_started.html#installation) for the following advantages:

* Web based user interface to manage plugins and users
* Simple local installation

### Making a new `pypi` Virtual Environment

You need to make a new VENV(Virtual Environment) to run pypicloud, your local Python repository.
> You can change any VENV name instead `pypi`

```sh
C:\work>
C:\work>C:\Python37-32\python.exe -m venv pypi

C:\work>pypi\Scripts\activate

(pypi) C:\work>dir
 Volume in drive C has no label.
 Volume Serial Number is C085-F9C0

 Directory of C:\work

03/20/2022  06:59 PM    <DIR>          .
03/20/2022  06:59 PM    <DIR>          ..
03/17/2022  12:08 AM    <DIR>          py37
03/20/2022  06:59 PM    <DIR>          pypi
               0 File(s)              0 bytes
               4 Dir(s)   9,551,917,056 bytes free

(pypi) C:\work>pip list
Package    Version
---------- -------
pip        19.0.3
setuptools 40.8.0
You are using pip version 19.0.3, however version 22.0.4 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.

(pypi) C:\work>python -m pip install --upgrade pip
Collecting pip
  Using cached https://files.pythonhosted.org/packages/4d/16/0a14ca596f30316efd412a60bdfac02a7259bf8673d4d917dc60b9a21812/pip-22.0.4-py3-none-any.whl
Installing collected packages: pip
  Found existing installation: pip 19.0.3
    Uninstalling pip-19.0.3:
      Successfully uninstalled pip-19.0.3
Successfully installed pip-22.0.4

(pypi) C:\work>pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 40.8.0
```
> versions may be different from the examples above.

### Installing pypicloud

Just two commands are required.

```
pip install SQLAlchemy==1.4.49
pip install pypicloud[server]
```

Below shows the actual example.
```sh
(pypi) C:\work>pip install SQLAlchemy==1.4.49
...
(pypi) C:\work>pip install pypicloud[server]
Collecting pypicloud[server]
  Downloading pypicloud-1.3.3-py3-none-any.whl (534 kB)
     ---------------------------------------- 534.0/534.0 KB 11.1 MB/s eta 0:00:00
Collecting transaction
  Downloading transaction-3.0.1-py2.py3-none-any.whl (47 kB)
     ---------------------------------------- 47.4/47.4 KB ? eta 0:00:00
Collecting cryptography
  Downloading cryptography-36.0.2-cp36-abi3-win32.whl (1.9 MB)
     ---------------------------------------- 1.9/1.9 MB 30.0 MB/s eta 0:00:00
Collecting pyramid-rpc
  Downloading pyramid_rpc-0.8-py2.py3-none-any.whl (24 kB)
Collecting passlib>=1.7
  Downloading passlib-1.7.4-py2.py3-none-any.whl (525 kB)
     ---------------------------------------- 525.6/525.6 KB 32.2 MB/s eta 0:00:00
Collecting pyramid>=2
  Downloading pyramid-2.0-py3-none-any.whl (246 kB)
     ---------------------------------------- 246.6/246.6 KB ? eta 0:00:00
Collecting pyramid-jinja2
  Downloading pyramid_jinja2-2.9.2-py3-none-any.whl (43 kB)
     ---------------------------------------- 43.1/43.1 KB 2.2 MB/s eta 0:00:00
Collecting paste
  Downloading Paste-3.5.0-py2.py3-none-any.whl (593 kB)
     ---------------------------------------- 593.2/593.2 KB 36.4 MB/s eta 0:00:00
Collecting pyramid-beaker
  Downloading pyramid_beaker-0.8.tar.gz (21 kB)
  Preparing metadata (setup.py) ... done
Collecting requests
  Using cached requests-2.27.1-py2.py3-none-any.whl (63 kB)
Collecting distlib
  Downloading distlib-0.3.4-py2.py3-none-any.whl (461 kB)
     ---------------------------------------- 461.2/461.2 KB 30.1 MB/s eta 0:00:00
Collecting boto3>=1.7.0
  Downloading boto3-1.21.22-py3-none-any.whl (132 kB)
     ---------------------------------------- 132.3/132.3 KB ? eta 0:00:00
Collecting zope.sqlalchemy
  Downloading zope.sqlalchemy-1.6-py2.py3-none-any.whl (22 kB)
Collecting pyramid-tm
  Downloading pyramid_tm-2.5-py2.py3-none-any.whl (6.5 kB)
Collecting pyramid-duh
  Downloading pyramid_duh-0.1.2-py2.py3-none-any.whl (13 kB)
Collecting waitress
  Downloading waitress-2.1.1-py3-none-any.whl (57 kB)
     ---------------------------------------- 57.3/57.3 KB 2.9 MB/s eta 0:00:00
Collecting jmespath<2.0.0,>=0.7.1
  Downloading jmespath-1.0.0-py3-none-any.whl (23 kB)
Collecting botocore<1.25.0,>=1.24.22
  Downloading botocore-1.24.22-py3-none-any.whl (8.6 MB)
     ---------------------------------------- 8.6/8.6 MB 36.7 MB/s eta 0:00:00
Collecting s3transfer<0.6.0,>=0.5.0
  Downloading s3transfer-0.5.2-py3-none-any.whl (79 kB)
     ---------------------------------------- 79.5/79.5 KB ? eta 0:00:00
Collecting hupper>=1.5
  Downloading hupper-1.10.3-py2.py3-none-any.whl (26 kB)
Collecting plaster-pastedeploy
  Downloading plaster_pastedeploy-0.7-py2.py3-none-any.whl (7.8 kB)
Collecting venusian>=1.0
  Downloading venusian-3.0.0-py3-none-any.whl (13 kB)
Requirement already satisfied: setuptools in c:\work\pypi\lib\site-packages (from pyramid>=2->pypicloud[server]) (40.8.0)
Collecting zope.interface>=3.8.0
  Downloading zope.interface-5.4.0-cp37-cp37m-win32.whl (208 kB)
     ---------------------------------------- 208.5/208.5 KB 12.4 MB/s eta 0:00:00
Collecting plaster
  Downloading plaster-1.0-py2.py3-none-any.whl (14 kB)
Collecting webob>=1.8.3
  Downloading WebOb-1.8.7-py2.py3-none-any.whl (114 kB)
     ---------------------------------------- 115.0/115.0 KB ? eta 0:00:00
Collecting translationstring>=0.4
  Downloading translationstring-1.4-py2.py3-none-any.whl (15 kB)
Collecting zope.deprecation>=3.5.0
  Downloading zope.deprecation-4.4.0-py2.py3-none-any.whl (10 kB)
Collecting cffi>=1.12
  Using cached cffi-1.15.0-cp37-cp37m-win32.whl (166 kB)
Collecting six>=1.4.0
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting beaker
  Downloading Beaker-1.11.0.tar.gz (40 kB)
     ---------------------------------------- 40.9/40.9 KB ? eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting markupsafe
  Downloading MarkupSafe-2.1.1-cp37-cp37m-win32.whl (14 kB)
Collecting jinja2!=2.11.0,!=2.11.1,!=2.11.2,>=2.5.0
  Using cached Jinja2-3.0.3-py3-none-any.whl (133 kB)
Collecting idna<4,>=2.5
  Using cached idna-3.3-py3-none-any.whl (61 kB)
Collecting certifi>=2017.4.17
  Using cached certifi-2021.10.8-py2.py3-none-any.whl (149 kB)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.9-py2.py3-none-any.whl (138 kB)
     ---------------------------------------- 139.0/139.0 KB 8.6 MB/s eta 0:00:00
Collecting charset-normalizer~=2.0.0
  Using cached charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Collecting SQLAlchemy!=1.4.0,!=1.4.1,!=1.4.2,!=1.4.3,!=1.4.4,!=1.4.5,!=1.4.6,>=0.9
  Downloading SQLAlchemy-1.4.32-cp37-cp37m-win32.whl (1.6 MB)
     ---------------------------------------- 1.6/1.6 MB 49.7 MB/s eta 0:00:00
Collecting python-dateutil<3.0.0,>=2.1
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pycparser
  Using cached pycparser-2.21-py2.py3-none-any.whl (118 kB)
Collecting importlib-metadata
  Downloading importlib_metadata-4.11.3-py3-none-any.whl (18 kB)
Collecting greenlet!=0.4.17
  Downloading greenlet-1.1.2-cp37-cp37m-win32.whl (98 kB)
     ---------------------------------------- 98.2/98.2 KB 5.9 MB/s eta 0:00:00
Collecting PasteDeploy>=2.0
  Downloading PasteDeploy-2.1.1-py2.py3-none-any.whl (17 kB)
Collecting typing-extensions>=3.6.4
  Using cached typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Collecting zipp>=0.5
  Using cached zipp-3.7.0-py3-none-any.whl (5.3 kB)
Using legacy 'setup.py install' for pyramid-beaker, since package 'wheel' is not installed.
Using legacy 'setup.py install' for beaker, since package 'wheel' is not installed.
Installing collected packages: translationstring, passlib, distlib, certifi, beaker, zope.interface, zope.deprecation, zipp, webob, waitress, venusian, urllib3, typing-extensions, six, pycparser, plaster, PasteDeploy, markupsafe, jmespath, idna, hupper, greenlet, charset-normalizer, transaction, requests, python-dateutil, plaster-pastedeploy, paste, jinja2, importlib-metadata, cffi, SQLAlchemy, pyramid, cryptography, botocore, zope.sqlalchemy, s3transfer, pyramid-tm, pyramid-rpc, pyramid-jinja2, pyramid-duh, pyramid-beaker, boto3, pypicloud
  Running setup.py install for beaker ... done
  Running setup.py install for pyramid-beaker ... done
Successfully installed PasteDeploy-2.1.1 SQLAlchemy-1.4.32 beaker-1.11.0 boto3-1.21.22 botocore-1.24.22 certifi-2021.10.8 cffi-1.15.0 charset-normalizer-2.0.12 cryptography-36.0.2 distlib-0.3.4 greenlet-1.1.2 hupper-1.10.3 idna-3.3 importlib-metadata-4.11.3 jinja2-3.0.3 jmespath-1.0.0 markupsafe-2.1.1 passlib-1.7.4 paste-3.5.0 plaster-1.0 plaster-pastedeploy-0.7 pycparser-2.21 pypicloud-1.3.3 pyramid-2.0 pyramid-beaker-0.8 pyramid-duh-0.1.2 pyramid-jinja2-2.9.2 pyramid-rpc-0.8 pyramid-tm-2.5 python-dateutil-2.8.2 requests-2.27.1 s3transfer-0.5.2 six-1.16.0 transaction-3.0.1 translationstring-1.4 typing-extensions-4.1.1 urllib3-1.26.9 venusian-3.0.0 waitress-2.1.1 webob-1.8.7 zipp-3.7.0 zope.deprecation-4.4.0 zope.interface-5.4.0 zope.sqlalchemy-1.6
```

### Configuration 
Although `pypicloud` is designed to work with AWS S3, GCS, AZure, and so on, for our example, let's configure it to work at the local environment.

```sh
(pypi) C:\work>pypicloud-make-config -t server.ini
[1] s3
[2] gcs
[3] filesystem
[4] azure-blob
Where do you want to store your packages? 3
Admin username? admin
Password:
Password:
Config file written to 'server.ini'

(pypi) C:\work>dir
 Volume in drive C has no label.
 Volume Serial Number is C085-F9C0

 Directory of C:\work

03/20/2022  07:00 PM    <DIR>          .
03/20/2022  07:00 PM    <DIR>          ..
03/17/2022  12:08 AM    <DIR>          py37
03/20/2022  06:59 PM    <DIR>          pypi
03/20/2022  07:00 PM             1,421 server.ini
               1 File(s)          1,421 bytes
               4 Dir(s)   9,418,104,832 bytes free
```

We are using `[3] filesystem`. 
After selecting store type you entered `admin` user id and password, keep in mind that later you can manage this site at web browser.

All configuration is saved in the file `server.ini`
Next is the generated contents of this `server.ini` file:

```ini
[app:main]
use = egg:pypicloud

pyramid.reload_templates = False
pyramid.debug_authorization = false
pyramid.debug_notfound = false
pyramid.debug_routematch = false
pyramid.default_locale_name = en

pypi.default_read =
    everyone
pypi.default_write =
    authenticated

pypi.storage = file
storage.dir = %(here)s/packages

db.url = sqlite:///%(here)s/db.sqlite

auth.admins =
  admin

user.admin = $5$rounds=16000$Q/WgE4r66PqVTa5E$4y/Ho9ya/N9keb5.ivLx5vBaotWR70mauC3zwYkpGd0

# For beaker
session.encrypt_key = Z0ldKdXSXowRnfs7u8d4+/Qyf8+VmQjZ2Hzb4pb78YQ=
session.validate_key = skuHsoAMDRMiFt5wMlO8Hpd8wbx//rhbyciDMimeUe8=
session.secure = False
session.invalidate_corrupt = true

###
# wsgi server configuration
###

[server:main]
use = egg:waitress#main
host = 0.0.0.0
port = 6543

###
# logging configuration
# http://docs.pylonsproject.org/projects/pyramid/en/latest/narr/logging.html
###

[loggers]
keys = root, botocore, pypicloud

[handlers]
keys = console

[formatters]
keys = generic

[logger_root]
level = INFO
handlers = console

[logger_pypicloud]
level = DEBUG
qualname = pypicloud
handlers =

[logger_botocore]
level = WARN
qualname = botocore
handlers =

[handler_console]
class = StreamHandler
args = (sys.stderr,)
level = NOTSET
formatter = generic

[formatter_generic]
format = %(levelname)s %(asctime)s [%(name)s] %(message)s
```

> Default port number is `6543`. You can change any port you want less than 65535.

## Running the private repository using pypicloud


```sh
(pypi) C:\work>pserve server.ini
INFO 2022-03-20 19:00:44,516 [pypicloud.cache.base] Cache is empty. Rebuilding from storage backend...
INFO 2022-03-20 19:00:44,516 [pypicloud.cache.base] Cache repopulated
Starting server in PID 804.
INFO 2022-03-20 19:00:44,625 [waitress] Serving on http://0.0.0.0:6543
```

## The Web interface

![01-pypiserver](https://raw.githubusercontent.com/argos-labs/pot-sdk-doc/main/Captures/03-Make_Plugin_PyCharm/08-pypicloud/01-pypiserver.png)

You can see above result at web browser with the address [http://localhost:6543](http://localhost:6543).

![02-pypiserver-login](https://raw.githubusercontent.com/argos-labs/pot-sdk-doc/main/Captures/03-Make_Plugin_PyCharm/08-pypicloud/02-pypiserver-login.png)

You can login with the `user id` and `password` which are created at Configuration.

![03-pypiserver-admin](https://raw.githubusercontent.com/argos-labs/pot-sdk-doc/main/Captures/03-Make_Plugin_PyCharm/08-pypicloud/03-pypiserver-admin.png)

At `Admin` top menu you can manage Users and Groups.
Once logined with `admin` user you can easily upload or delete modules.

> Refer to this link [manual](https://pypicloud.readthedocs.io/en/latest/index.html) for more detailed use.

## Setting your Supervisor account to activate the private repository with your STU and PAM

You can register your private repository at [Supervisor's private plugin menu](https://rpa.argos-labs.com/#/plugin/private-plugin).

![04-supervisor-add-private-plugin](https://raw.githubusercontent.com/argos-labs/pot-sdk-doc/main/Captures/03-Make_Plugin_PyCharm/08-pypicloud/04-supervisor-add-private-plugin.png)

If you click `+` icon on the top right side then `Add Private Plugin` dialog shows up. You can set thess informations:

* `Name` - Any unique name for private plugins, we are using `local-repository`
* `URL` - For the protocol `http://` and rest address will be `127.0.0.1:6543/simple/` (same meaning with `localhost:6543/simple/`)
* `User` - User id for private repository
* `Password` - User password for private repository
* `Enabled` - Must be checked to use this private repository

Click the `Save` button.

![05-supervisor-first-private-plugin](https://raw.githubusercontent.com/argos-labs/pot-sdk-doc/main/Captures/03-Make_Plugin_PyCharm/08-pypicloud/05-supervisor-first-private-plugin.png)

> **IMPORTANT** If you already have one or more private repositories then re-order your new private repository to the first position. (move it up to the top of the list) This is because the POT SDK has been designed to upload the new plugin to the ***FIRST private repository*** on the list.

<<[Go to previous page](ARGOS_RPA_POT_SDK_on_Windows10.md)
