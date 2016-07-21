### 1. File Operations

### 2. User Environments

### 3. Network Operations

#### 3.1 SSH

SSH Secure Shell Client (homepage, [download](https://it.wm.edu/software/public/ssh/sshsecureshellclient-3.2.9.exe))

#### 3.2 RTMP

rtmpdump ([download](http://rtmpdump.mplayerhq.hu/download/))

#### 3.3 Synchonize

FullSync ([homepage](http://fullsync.sourceforge.net/index.php))

![](http://fullsync.sourceforge.net/screenshots/0.10.0/Profile_Details_dst.png)

### 4. Process

```powershell
# list process
tasklist

# kill prcess
taskkill /im chrome.exe /F
```


### 5. System Information

```powershell
# get architecture
wmic os get osarchitecture
#: OSArchitecture
#: 64-bit
```

<div style="display:none">
Download Windows 7 Professional 64 bit: https://drive.google.com/folderview?id=0B3PWckYm7eLkZS1pVHloNzdrTFk&usp=sharing#list
</div>

# Windows Shell

[Batsh - A language that compiles to Bash and Windows Batch](http://batsh.org/)

### Print

```
# print HELLO WORLD
echo HELLO WORLD

# print blank line
echo.
```

### Arguments [^3]

```powershell
echo %1
```

> $ test.bat helloworld
> helloworld

### Sleep

Sleep for 5 seconds [^1]

```powershell
timeout 5 > NUL

# deprecated
ping 127.0.0.1 -n 6 > nul
```

### Conditional [^4]

```powershell
if exist input.dat goto handle_input_file
    echo The file input.dat does not exist
    pause
    exit /b
:handle_input_file
```

### Loop [^2]

```
:while1
echo forever loop
goto :while1
```

> $ test.bat
> forever loop
> forever loop
> forever loop
> ...

[^1]: [How to sleep for 5 seconds in Windows's Command Prompt? (or DOS)](http://stackoverflow.com/questions/1672338/how-to-sleep-for-5-seconds-in-windowss-command-prompt-or-dos)
[^2]: [While loop in batch](http://stackoverflow.com/questions/1788473/while-loop-in-batch)
[^3]: [Command line parameters](http://www.robvanderwoude.com/parameters.php)
[^4]: [Windows Batch Files for Fun and Profit](http://www.quepublishing.com/articles/article.aspx?p=1154761&seqNum=7)

# Windows: How to fix MBR

Fix MBR with command prompt and installation DVD. Fix MBR with command prompt requires the original Windows 8 or 8.1 installation DVD. The instructions are [^1]

1.Boot from the original installation DVD.
2.At the Welcome screen, click "Repair your computer".
3.Choose" Troubleshoot > Advanced options > Command Prompt".
4.When the Command Prompt loads, type the following commands in order:

```
bootrec /FixMbr
bootrec /FixBoot
bootrec /ScanOs
bootrec /RebuildBcd
```

Remember to press "Enter" after each command and wait for each operation to finish.

5.Remove the DVD from the disk tray.
6.Type exit and Hit "Enter".
7.Restart your computer and check if Windows 8/8.1 can boot now.

[^1]: [Windows MBR fix](https://www.partitionwizard.com/partitionmagic/windows-8-mbr-fix.html)

# Installing Theano on Windows 8.1

Getting theano works in Windows 8.1 is not easy but possible. The important is use the right receipts. I found the right receipts and nice tutorial <a href="https://my6266blog.wordpress.com/2015/01/21/installing-theano-pylearn2-and-even-gpu-on-windows/" target="_blank">here</a>

<strong>Receipts</strong>

<ul>
<li>Windows 8.1 64-bit</li>
<li>CUDA 64-bit 7</li>
<li>Visual Studio 2013 (compiler 12.0) Ultimate</li>
<li><a href="https://repo.continuum.io/archive/Anaconda-2.1.0-Windows-x86_64.exe" target="_blank">Anaconda 64-bit 2.1.0</a></li>
<li><a href="https://git-scm.com/" target="_blank">Git-scm</a></li>
</ul>

I'm very happy getting things done.

<pre><code>PS C:Usersrain&gt; python
Python 2.7.8 |Anaconda 2.1.0 (64-bit)| (default, Jul 2 2014, 15:12:11) [MSC v.1500 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
Anaconda is brought to you by Continuum Analytics.
Please check out: http://continuum.io/thanks and https://binstar.org
&gt;&gt;&gt; import theano
DEBUG: nvcc STDOUT mod.cu
Creating library C:/Users/rain/AppData/Local/Theano/compiledir_Windows-8-6.2.9200-Intel64_Family_6_Model_60_Stepping_
3_GenuineIntel-2.7.8-64/cuda_ndarray/cuda_ndarray.lib and object C:/Users/rain/AppData/Local/Theano/compiledir_Windows-8
-6.2.9200-Intel64_Family_6_Model_60_Stepping_3_GenuineIntel-2.7.8-64/cuda_ndarray/cuda_ndarray.exp

Using gpu device 0: GeForce GTX 980
DEBUG: nvcc STDOUT mod.cu
Creating library C:/Users/rain/AppData/Local/Theano/compiledir_Windows-8-6.2.9200-Intel64_Family_6_Model_60_Stepping_
3_GenuineIntel-2.7.8-64/tmpgt3iqm/c8d7bd33dfef61705c2854dd1f0cb7ce.lib and object C:/Users/rain/AppData/Local/Theano/com
piledir_Windows-8-6.2.9200-Intel64_Family_6_Model_60_Stepping_3_GenuineIntel-2.7.8-64/tmpgt3iqm/c8d7bd33dfef61705c2854dd
1f0cb7ce.exp

DEBUG: nvcc STDOUT mod.cu
Creating library C:/Users/rain/AppData/Local/Theano/compiledir_Windows-8-6.2.9200-Intel64_Family_6_Model_60_Stepping_
3_GenuineIntel-2.7.8-64/tmpfab1so/0fc80e98cce631ecaa526b69dd28dae1.lib and object C:/Users/rain/AppData/Local/Theano/com
piledir_Windows-8-6.2.9200-Intel64_Family_6_Model_60_Stepping_3_GenuineIntel-2.7.8-64/tmpfab1so/0fc80e98cce631ecaa526b69
dd28dae1.exp</code></pre>