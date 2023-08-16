---
title: "Virtual Vanguard: Mastering Django's Virtual Environments"
seoTitle: "Django, virtualenv, django virtual environment, virtual environment"
datePublished: Wed Apr 06 2022 07:04:28 GMT+0000 (Coordinated Universal Time)
cuid: cl1na0u0n02mv4wnv20x417o2
slug: virtual-vanguard-mastering-djangos-virtual-environments
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/BI465ksrlWs/upload/v1649228467024/UQEGLU5Ql.jpeg
tags: software-development, python, django, developer, software-engineering

---

## What is a virtual environment?

A virtual environment is a set of version or local settings that is specific to a particular project, instance or any entity which uses that environment. In simple terms, you create an environment that satisfies the needs of different scenarios without interfering with other project settings.

To better understand this, assume you created a project where you want to install a specific version of Django or any other package that you already have installed on your local machine. Not only that, that package comes with dependencies of another package demanding a specific version of it. So once you try installing that package it will send a package version conflict response and if you go about changing packages versions it will create a domino effect which will force you to change another dependent package version and another and another ........

To resolve the above-mentioned issue, virtual environment is used.

## My Settings

* OS:- `macOS montery`
    
* Python Version:- `Python 3.9.5`
    

## Setting up a virtual environment

So to set up a virtual environment, there are various ways of achieving this, through venv, virtualenv, pipenv etc. The way I like to go about this is using `virtualenv` hence I will be covering that but if you still need to know more about venv and other ways to go about this, you can comment down and I will write a separate blog about it.

### Through virtualenv

So one of the packages that help us with this task is virtualenv. To install virtualenv you can run the following command:-

```bash
pip install virtualenv
```

Before creating our very first environment, first check what all packages you already have in your global settings by running the following command:-

```bash
pip list
```

As for me it gives me a long list of all the packages that is present in my global setting

```bash
(base) ➜  virtualenv_blog pip list
Package                       Version
----------------------------- -------------------
asgiref                       3.5.0
backports.zoneinfo            0.2.1
brotlipy                      0.7.0
cachetools                    4.2.4
certifi                       2021.10.8
cffi                          1.15.0
chardet                       4.0.0
charset-normalizer            2.0.12
conda                         4.10.3
conda-package-handling        1.7.3
configparser                  5.2.0
coreapi                       2.3.3
coreschema                    0.0.4
cryptography                  36.0.2
defusedxml                    0.7.1
distlib                       0.3.4
dj-database-url               0.5.0
dj-rest-auth                  2.2.4
Django                        4.0.3
django-allauth                0.50.0
django-filter                 21.1
django-heroku                 0.3.1
django-rest-auth              0.9.5
django-rest-swagger           2.0.7
djangorestframework           3.13.1
djangorestframework-jwt       1.11.0
djangorestframework-simplejwt 5.1.0
filelock                      3.6.0
google-api-core               1.22.2
google-api-python-client      1.12.1
google-auth                   1.21.2
google-auth-httplib2          0.0.4
googleapis-common-protos      1.52.0
gunicorn                      19.9.0
```

Now to create a virtual environment you can simply run the command:-

```plaintext
virtualenv example_environment
```

On running the above command a `example_environment` folder will be created like this:-

```plaintext
(base) ➜  virtualenv_blog virtualenv example_environment
created virtual environment CPython3.9.5.final.0-64 in 260ms
  creator CPython3Posix(dest=/Users/ayoushchourasia/Work/WAL/upaway/python_basics/virtualenv_blog/example_environment, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/ayoushchourasia/Library/Application Support/virtualenv)
    added seed packages: pip==22.0.4, setuptools==61.0.0, wheel==0.37.1
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator
(base) ➜  virtualenv_blog ls
example_environment
(base) ➜  virtualenv_blog cd  example_environment/
(base) ➜  example_environment ls
bin        lib        pyvenv.cfg
```

So now that you have finally created your first virtual environment. Its time to activate the same and start working on it.

You can activate your virtual environment by simply calling the below command:-

```plaintext
(base) ➜  virtualenv_blog source example_environment/bin/activate
(example_environment) (base) ➜  virtualenv_blog
```

Notice that extra `(example_environment)` part before base, that's a confirmation that our virtual environment is up and now if you do pip list you won't get the packages from your global settings but rather from your local settings.

```plaintext
(example_environment) (base) ➜  virtualenv_blog pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 61.0.0
wheel      0.37.1
```

Now you are good to go and you can install and play with whatever version of a particular package you want to work with.

Now that you are here you can store this environment settings for future references using the following command:-

```plaintext
pip freeze --local > requirements.txt
```

And all of your local packages with their versions will be stored in the `requirements.txt` file and later on if you want to install the same in some another machine you can simply run:-

```plaintext
pip install -r requirements.txt
```

To get out of this virtual environment you can simply run:-

```plaintext
deactivate
```

If you delete the folder of `example_environment`, your virtual environment is gone so do take note of this.

To set a specific python version you can do that by simply mentioning the path before creating a virtual environment like this:-

```plaintext
virtualenv -p usr/bin/python2.7 python2.7_environment
```

You can find the path by simply running `which python`