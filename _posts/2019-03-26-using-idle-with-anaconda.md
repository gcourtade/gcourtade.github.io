---
layout: post
title:  How to use IDLE with Anaconda
category: Conferences 
comments: true
description:
---

As a Windows user, I really like IDLE (Python's Integrated Development and Learning Enviornment) for Python programming. Some of its very nice features include the ability to select several lines and use `Alt+3` for commenting multiple lines (and `Alt+4` to uncomment them) as well as being able to run your code (in an interactive console) by pressing `F5`.

Using IDLE is straight-forward when uing a system-wide installation of Python, but things become a bit more tricky when using [Anaconda](https://www.anaconda.com/), since every environment you install will create its own version of IDLE integrated within the Python installation. So, here's how to make IDLE your default Python editor with Anaconda on Windows.

####  1. Making a custom conda activate command
It is simple to type `conda activate <environment name>` when using the Anaconda prompt, but here we want to activate our enviornment whenever we run IDLE. For this, we need to create a new batch file that activates our enviornment. In this example, I am using an environment called `py37`.

1. Go to your `condabin` directory. In my case it is `C:\Users\courtade\AppData\Local\Continuum\anaconda3\condabin`
2. Create a copy of `activate.bat` and rename it to `activate_py37.bat`
3. Edit the last line in `activate_py37.bat` so that the file looks like this:
```
@REM Copyright (C) 2012 Anaconda, Inc
@REM SPDX-License-Identifier: BSD-3-Clause
@CALL "%~dp0..\condabin\conda_hook.bat"
conda.bat activate py37
``` 

####  2. Editing idle.bat
`idle.bat` is the batch script used to run IDLE. You can find yours in the directory tree for the Anaconda environment. In this example, my `idle.bat` file is in `C:\Users\courtade\AppData\Local\Continuum\anaconda3\envs\py37\Lib\idlelib`.

Here, you should edit `idle.bat` to call the `activate_py37.bat`. My file looks like this:

```
@echo off
call "C:\Users\courtade\AppData\Local\Continuum\anaconda3\condabin\activate_py37.bat"
rem Start IDLE using the appropriate Python interpreter
set CURRDIR=%~dp0
start "IDLE" "%CURRDIR%..\..\pythonw.exe" "%CURRDIR%idle.pyw" %1 %2 %3 %4 %5 %6 %7 %8 %9
```

####  3. Making IDLE your default Python editor
Now go to your Desktop (or anywhere else) and create a `test.py` file. then `Right click > Open with > Choose another app > More Apps > Look for another app on this PC`. Now navigate to `C:\Users\courtade\AppData\Local\Continuum\anaconda3\envs\py37\Lib\idlelib` and choose `idle.bat` as the app.
Remember to check the box `Always use this app to open .py files` and click OK.
Now you can double click `test.py` to open it with IDLE and all the modules/packages you install on `py37` will also be available.

Happy coding with IDLE and Anaconda on Windows!