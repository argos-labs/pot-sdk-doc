<<[Go to previous page](ARGOS_RPA_POT_SDK_on_Windows10.md)

# Install ARGOS POT SDK

Run below command in the Virtual Environment:

> pip install -U alabs.ppm alabs.icon --extra-index-url https://pypi-official.argos-labs.com/pypi

```bash
(py37) C:\work>pip install -U alabs.ppm alabs.icon --index https://pypi-official.argos-labs.com/pypi
Looking in indexes: https://pypi-official.argos-labs.com/pypi
Collecting alabs.ppm
  Downloading https://pypi-official.argos-labs.com/api/package/alabs-ppm/alabs.ppm-4.115.1700-py3-none-any.whl (101 kB)
     ---------------------------------------- 101.3/101.3 KB ? eta 0:00:00
Collecting alabs.icon
  Downloading https://pypi-official.argos-labs.com/api/package/alabs-icon/alabs.icon-1.711.2351-py3-none-any.whl (136 kB)
     ---------------------------------------- 136.7/136.7 KB ? eta 0:00:00
Collecting urllib3==1.25.8
  Downloading https://pypi-official.argos-labs.com/api/package/urllib3/urllib3-1.25.8-py2.py3-none-any.whl (125 kB)
     ---------------------------------------- 125.6/125.6 KB ? eta 0:00:00
Collecting beautifulsoup4
  Downloading https://pypi-official.argos-labs.com/api/package/beautifulsoup4/beautifulsoup4-4.9.3-py3-none-any.whl (115 kB)
     ---------------------------------------- 115.8/115.8 KB ? eta 0:00:00
Collecting alabs.common
  Downloading https://pypi-official.argos-labs.com/api/package/alabs-common/alabs.common-3.721.1350-py3-none-any.whl (43 kB)
     ---------------------------------------- 43.4/43.4 KB ? eta 0:00:00
Collecting requirements-parser
  Downloading https://pypi-official.argos-labs.com/api/package/requirements-parser/requirements-parser-0.2.0.tar.gz (6.3 kB)
  Preparing metadata (setup.py) ... done
Collecting requests
  Downloading https://pypi-official.argos-labs.com/api/package/requests/requests-2.26.0-py2.py3-none-any.whl (62 kB)
     ---------------------------------------- 62.3/62.3 KB 3.5 MB/s eta 0:00:00
Collecting wheel
  Downloading https://pypi-official.argos-labs.com/api/package/wheel/wheel-0.37.0-py2.py3-none-any.whl (35 kB)
Collecting PyYAML
  Downloading https://pypi-official.argos-labs.com/api/package/pyyaml/PyYAML-5.4.1-cp37-cp37m-win32.whl (193 kB)
     ---------------------------------------- 193.5/193.5 KB ? eta 0:00:00
Collecting idna==2.7
  Downloading https://pypi-official.argos-labs.com/api/package/idna/idna-2.7-py2.py3-none-any.whl (58 kB)
     ---------------------------------------- 58.2/58.2 KB ? eta 0:00:00
Collecting icon-font-to-png
  Downloading icon_font_to_png-0.4.1-py2.py3-none-any.whl (161 kB)
     ---------------------------------------- 161.4/161.4 KB 10.1 MB/s eta 0:00:00
Collecting chardet
  Downloading https://pypi-official.argos-labs.com/api/package/chardet/chardet-4.0.0-py2.py3-none-any.whl (178 kB)
     ---------------------------------------- 178.7/178.7 KB ? eta 0:00:00
Collecting charset-normalizer~=2.0.0
  Downloading https://pypi-official.argos-labs.com/api/package/charset-normalizer/charset_normalizer-2.0.4-py3-none-any.whl (36 kB)
Collecting certifi>=2017.4.17
  Downloading https://pypi-official.argos-labs.com/api/package/certifi/certifi-2021.5.30-py2.py3-none-any.whl (145 kB)
     ---------------------------------------- 145.5/145.5 KB ? eta 0:00:00
Collecting soupsieve>1.2
  Downloading https://pypi-official.argos-labs.com/api/package/soupsieve/soupsieve-2.2.1-py3-none-any.whl (33 kB)
Collecting tinycss>=0.4
  Downloading tinycss-0.4.tar.gz (87 kB)
     ---------------------------------------- 87.8/87.8 KB ? eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting Pillow>=4.0.0
  Downloading https://pypi-official.argos-labs.com/api/package/pillow/Pillow-8.3.1-cp37-cp37m-win32.whl (2.8 MB)
     ---------------------------------------- 2.8/2.8 MB 25.3 MB/s eta 0:00:00
Collecting six>=1.10.0
  Downloading https://pypi-official.argos-labs.com/api/package/six/six-1.16.0-py2.py3-none-any.whl (11 kB)
Using legacy 'setup.py install' for requirements-parser, since package 'wheel' is not installed.
Using legacy 'setup.py install' for tinycss, since package 'wheel' is not installed.
Installing collected packages: tinycss, requirements-parser, idna, certifi, wheel, urllib3, soupsieve, six, PyYAML, Pillow, charset-normalizer, chardet, requests, beautifulsoup4, icon-font-to-png, alabs.common, alabs.ppm, alabs.icon
  Running setup.py install for tinycss ... done
  Running setup.py install for requirements-parser ... done
Successfully installed Pillow-8.3.1 PyYAML-5.4.1 alabs.common-3.721.1350 alabs.icon-1.711.2351 alabs.ppm-4.115.1700 beautifulsoup4-4.9.3 certifi-2021.5.30 chardet-4.0.0 charset-normalizer-2.0.4 icon-font-to-png-0.4.1 idna-2.7 requests-2.26.0 requirements-parser-0.2.0 six-1.16.0 soupsieve-2.2.1 tinycss-0.4 urllib3-1.25.8 wheel-0.37.0

(py37) C:\work>
```

> * In above example you are in the `py37` virtual environment.
> * You can upgrade as well as install with `-U` option

## Check the version number

You can check the POT SDK related modules with `pip list` command at Virtual Env.

```bash
(py37) C:\work>pip list
Package             Version
------------------- ----------
alabs.common        4.323.1107
alabs.icon          1.711.2351
alabs.ppm           4.628.1925
beautifulsoup4      4.9.3
certifi             2021.5.30
chardet             4.0.0
charset-normalizer  2.0.4
icon-font-to-png    0.4.1
idna                2.7
Pillow              8.3.1
pip                 22.0.4
PyYAML              5.4.1
requests            2.26.0
requirements-parser 0.2.0
setuptools          40.8.0
six                 1.16.0
soupsieve           2.2.1
tinycss             0.4
urllib3             1.25.8
wheel               0.37.0

(py37) C:\work>
```

> Note: The versions may be upgraded.

### ARGOS POT SDK consists of three parts as follows:

| Item | Minimum version | Role | Description |
|---|---|---|---|
| [alabs.common](https://pypi-official.argos-labs.com/#/package/alabs-common) | 4.323.1107 | SDK library | Library for SDK |
| [alabs.icon](https://pypi-official.argos-labs.com/#/package/alabs-icon) | 1.711.2351 | icon utility | This utility make plugin icon |
| [alabs.ppm](https://pypi-official.argos-labs.com/#/package/alabs-ppm) | 4.628.1925 | POT utility | POT main utility |

> Above versions are for now, date 13 September, 2022

<<[Go to previous page](ARGOS_RPA_POT_SDK_on_Windows10.md)
