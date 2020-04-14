---
layout: post
title:  PowerShell for Non System Administrators
date:   2020-04-13 21:07:15 -0500
image:  '/assets/img/PowerShell-Logo.png'
tags:   [PowerShell, blog]
---

You might had heard a lot about PowerShell, that you should learn it as it is going to level up your career or that it might help you ease your daily tasks. Even though you might agree with this, you haven't found any real world examples that relates to your roles since most of the examples are SysAdmin related. It is hard to learn something new if you can't tie it to what you already know.

I will try to give a few examples for non SysAdmins, but before we get our hands dirty we need to understand some PowerShell basics. How it is structured and what is all the buzz about.

## What is Powershell?

Is a scripting language, that will glue all your tools into one.

## Where can I use PowerShell?

Well it depends on the version we want to use, but long story short, Windows, Linux and Mac nowadays.

As of April 13th 2020 it looks as follows.

.Net Version | Name |  Version | Windows | Linux | Mac
--- | --- | --- | --- | --- | ---
.Net Core | PowerShell | 7.1 (Preview) | Yes | Yes | Yes
.Net Core | PowerShell | 7 | Yes | Yes | Yes
.Net Core | PowerShell Core | 6.2 | Yes | Yes | Yes
.Net Core | PowerShell Core | 6.1 | Yes | Yes | Yes
.Net Core | PowerShell Core | 6 | Yes | Yes | Yes
Full .Net | Windows PowerShell | 5.1 | Yes | No | No
Full .Net | Windows PowerShell | 5 | Yes | No | No
Full .Net | Windows PowerShell | 4 | Yes | No | No
Full .Net | Windows PowerShell | 3 | Yes | No | No
Full .Net | Windows PowerShell | 2 | Yes | No | No
Full .Net | Windows PowerShell | 1 | Yes | No | No
Full .Net | Windows PowerShell | Monad | Yes | No | No

## Why should I care?

* PowerShell cmdlets (PowerShell commands) names are **standardized**. They use a verb and noun pair, where the verbs are already predefined and the nouns is just a description of whatever we are trying to achieve. This is very important because it makes discovery very intuitive and minimizes the learning curve.

* It is going to make us **very** productive with very **minimal** lines of code, using pipelines.

* It is cross platform.

* We can build pretty much anything as it uses the .Net framework.

## How it works?

When I teach beginners how PowerShell works I like to divide it into three chunks.

* Getting the data
* Filtering the data
* Displaying the data

There is obviously more than just getting, filtering and displaying the data but for beginners this is the workflow I suggest beginners to start with. Some of the other categories are __setting__, __deleting__, __adding__ just to mention a few more.

## Pipeline

This is what allows PowerShell to pass the objects from one cmdlet to the other. It is represented with the pipe character. The following is an oversimplified example of how we can use the pipeline workflow using get, filter and displaying:

``` PowerShell

Gets Data | Filters Data | Displays Data

```

Since we are working with objects we can apply as many filters as we want. Until we get the desired information that we are looking for. Something like so:

``` Powershell

Gets Data | First Filter | Second Filter | Third Filter | Displays Data

```

You define the order of the pipeline, but for starters we are going to stick to this pipeline workflow as it is a good pattern for beginners. Plus to be honest, this is probably the pipeline pattern I use like 90% of the times when I am at the command line. If I am going to be modifying, deleting or creating something I probably write a script first, this way I add a little logic to the script and not modify or delete every single object. I probably just query the results in the command line, using the pipeline workflow above.

Another thing to keep in mind is that all of this could happen in one line of code. **In my personal opinion** PowerShell is the best at retrieving data, filtering it and displaying it in a simple and fast way.

## Getting Data

So what type of data is PowerShell able to retrieve?

* Log File
* Text File
* CSV File
* __Excel File__
* Server
* PC
* Data Bases
* __API__
* Web Server
* __PLC__
* __Camera__
* __Tesla__
* Windows
* Linux
* Mac
* __Temperature Sensor__
* __Motor__
* o365
* Azure
* AWS
* __On demand Input__
* __Firewall__
* __Switches__
* Sharepoint
* __PowerShell Custom GUI__
* ___The sky is the limit___

As you can see, we can retrieve data from devices that are not even SysAdmin related. This is why PowerShell is no longer a scripting language that SysAdmins should only use.

### Excel

So let's work with the first 3 bolded items from the list above, but before we begin one thing you need to know is that by default PowerShell is not able to retrieve all data. This is why there are modules, which you can look at them as applications that you install on your operating system. Where the application is the module and the operating system is PowerShell. So every time you install a new module, you are making PowerShell even more powerful.

Copy the table below and paste it in a blank excel worksheet, save it on your Downloads folder and name it SampleData.xlsx. This way we have something to work on.

OrderDate | Region | Rep | Item | Units | UnitCost | Total
--- | --- | --- | --- | --- | --- | ---
1/6/2019 | East | Jones | Pencil | 95 | 1.99 | 189.05
1/23/2019 | Central | Kivell | Binder | 50 | 19.99 | 999.5
2/9/2019 | Central | Jardine | Pencil | 36 | 4.99 | 179.64
2/26/2019 | Central | Gill | Pen | 27 | 19.99 | 539.73
3/15/2019 | West | Sorvino | Pencil | 56 | 2.99 | 167.44
4/1/2019 | East | Jones | Binder | 60 | 4.99 | 299.4
4/18/2019 | Central | Andrews | Pencil | 75 | 1.99 | 149.25
5/5/2019 | Central | Jardine | Pencil | 90 | 4.99 | 449.1
5/22/2019 | West | Thompson | Pencil | 32 | 1.99 | 63.68

It should look something like this.

![Excel Sample Data]({{ site.baseurl }}/assets/img/ExcelSampleData.png)

First things first. Let's open a PowerShell window in admin mode and run the following code.

```Powershell
If(-not (Get-Module -Name ImportExcel -ListAvailable)){
    Install-Module -Name PSEverything -Scope CurrentUser
}
```

Inside the if statement we are going to check if the Excel module is installed or not. If it's not installed..., well you guessed it. We'll install it. If everything goes right you should now get some prompts asking you if you are sure if you trust and want to install the modules. So please accept them all to proceed.

Once it is installed we can finally retrieve the data inside an Excel file. Run __Import-Excel -Path '~\Downloads\SampleData.xlsx'__ in a PowerShell window and you should get the following output.

```PowerShell
Import-Excel -Path '~\Downloads\SampleData.xlsx'

OrderDate : 1/6/2019 12:00:00 AM
Region    : East
Rep       : Jones
Item      : Pencil
Units     : 95
UnitCost  : 1.99
Total     : 189.05

OrderDate : 1/23/2019 12:00:00 AM
Region    : Central
Rep       : Kivell
Item      : Binder
Units     : 50
UnitCost  : 19.99
Total     : 999.5

OrderDate : 2/9/2019 12:00:00 AM
Region    : Central
Rep       : Jardine
Item      : Pencil
Units     : 36
UnitCost  : 4.99
Total     : 179.64

OrderDate : 2/26/2019 12:00:00 AM
Region    : Central
Rep       : Gill
Item      : Pen
Units     : 27
UnitCost  : 19.99
Total     : 539.73

OrderDate : 3/15/2019 12:00:00 AM
Region    : West
Rep       : Sorvino
Item      : Pencil
Units     : 56
UnitCost  : 2.99
Total     : 167.44

OrderDate : 4/1/2019 12:00:00 AM
Region    : East
Rep       : Jones
Item      : Binder
Units     : 60
UnitCost  : 4.99
Total     : 299.4

OrderDate : 4/18/2019 12:00:00 AM
Region    : Central
Rep       : Andrews
Item      : Pencil
Units     : 75
UnitCost  : 1.99
Total     : 149.25

OrderDate : 5/5/2019 12:00:00 AM
Region    : Central
Rep       : Jardine
Item      : Pencil
Units     : 90
UnitCost  : 4.99
Total     : 449.1

OrderDate : 5/22/2019 12:00:00 AM
Region    : West
Rep       : Thompson
Item      : Pencil
Units     : 32
UnitCost  : 1.99
Total     : 63.68
```

* Import-Excel
  * Is the PowerShell function that is going to do the heavy lifting. It is going to retrieve the data inside the Excel file.
* -Path
  * Is the Path parameter
* '~\Downloads\SampleData.xlsx'
  * Is the file path to the excel file
  * ~ is the equivalent to my home directory, in my case C:\Users\Hector.

PowerShell should now display the excel file in an not easy to use format. But thats ok, we are currently not worried about how the data looks but that we are able to retrieve the data. As we are currently just getting our feet wet on how to retrieve some data.

### API

APIs are very easy to consume. Usually you just need the URL you are going to connect to, the method and in some cases the Token (long password) to access the data. I found an API that doesn't requires a token this way you can test it too without authenticating.

Usually the documentation to access the API data is pretty straight forward. [Here](https://pokeapi.co/docs/v2.html/#pokemon) is Pokemon's API documentation in case you want to deep dive into Pokemon's API. We will be retrieving Snorlax information.

```PowerShell
Invoke-RestMethod -Uri https://pokeapi.co/api/v2/pokemon/snorlax/ -Method get

abilities                : {@{ability=; is_hidden=True; slot=3}, @{ability=; is_hidden=False; slot=2}, @{ability=; is_hidden=False; slot=1}}
base_experience          : 189
forms                    : {@{name=snorlax; url=https://pokeapi.co/api/v2/pokemon-form/143/}}
game_indices             : {@{game_index=143; version=}, @{game_index=143; version=}, @{game_index=143; version=}, @{game_index=143; version=}…}
height                   : 21
held_items               : {@{item=; version_details=System.Object[]}, @{item=; version_details=System.Object[]}}
id                       : 143
is_default               : True
location_area_encounters : https://pokeapi.co/api/v2/pokemon/143/encounters
moves                    : {@{move=; version_group_details=System.Object[]}, @{move=; version_group_details=System.Object[]}, @{move=; version_group_details=System.Object[]}, @{move=;
                           version_group_details=System.Object[]}…}
name                     : snorlax
order                    : 217
species                  : @{name=snorlax; url=https://pokeapi.co/api/v2/pokemon-species/143/}
sprites                  : @{back_default=https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/143.png; back_female=;
                           back_shiny=https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/shiny/143.png; back_shiny_female=;
                           front_default=https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/143.png; front_female=;
                           front_shiny=https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/143.png; front_shiny_female=}
stats                    : {@{base_stat=30; effort=0; stat=}, @{base_stat=110; effort=0; stat=}, @{base_stat=65; effort=0; stat=}, @{base_stat=65; effort=0; stat=}…}
types                    : {@{slot=1; type=}}
weight                   : 4600
```

* Invoke-RestMethod
  * THis is the PowerShell funtion
* -Uri
  * This is the URI parameter
* https://pokeapi.co/api/v2/pokemon/snorlax/
  * API to query
* -Method
  * This is the Method Parameter
* GET
  * This is the method we will be using to retrieve the API's information

You should of gotten some objects back in PowerShell. So you should now be able to see Snorlax height, weight, and even some pictures. Pretty cool, for a one liner.

Once again the data output is not the best, but that's ok we are not really concentrating on making the output beautiful, we just want to retrieve some data.

### PLC

PLC stands for programmable logic controller. PLCs are use pretty much by all the manufacturing businesses. They are used to automate their manufacturing processes. PLCs control all the edge devices inside presses, ovens, conveyors, WaterJets, mills, etc. Like the motors, sensors, cameras, etc. They are indispensable in a manufacturing business.

There are many PLC manufacturers. I created a PowerShell module that retrieves data from [Rockwell Allen-Bradley](https://ab.rockwellautomation.com/Programmable-Controllers) PLCs using [InGear Drivers](https://ingeardrivers.com/products/net-products/netlogix/). There are other PLC brands that you probably have heard of such as Siemens, Schneider Electric, ABB, Honeywell, Fanuc, etc. Some projects out in the wild that have managed to make arduinos and Raspberry PIs PLCs too.

So, let's see how I retrieve PLC information. First I connect to the PLC using __Connect-PLC__. After that I create a tag which in the programing world would be the equivalent of a variable using __New-Tag__. Next I read the tag which contains all the data using __Read-Tag__. Finally I disconnect from the PLC using __Disconnect-PLC__.

```PowerShell
$PLC = Connect-PLC -IPAddress 172.16.1.11 -CPUType 'LOGIX'
$Tag = New-Tag -Controller $PLC -Name 'MDT.NOCYCLEMIN' -DataType 'Int'
Read-Tag -Name $Tag

Name          : MDT.NOCYCLEMIN
DataType      : DINT
Value         : 24010
TimeStamp     : 4/13/2020 8:01:17 PM
QualityCode   : 192
Active        : True
Length        : 1
QualityString : QUALITY GOOD
AlignArray    : False
Controller    : Logix.Controller
Now           : 24016
MyObject      :
ErrorCode     : 0
ErrorString   : SUCCESS
NetType       : System.Int32

Disconnect-PLC -Controller $PLC
```

Obviously this was a little more elaborate, but we achieved the end result which was a way to retrieve data from a Rockwell Allen-Bradley PLC. The reason why I included this example was to show you that you can even develop your own PowerShell modules using third party DLLs. PowerShell is not __only for system administrators__ remember!

### Recap

So far we have talked about one of the three pipeline workflows. Which is how to retrieve the data from somewhere. It really doesn't matter where the data lives, as longest we know where it is stored. There are high chances to find a PowerShell way to retrieve it.

```PowerShell
**GETS DATA** | Filters Data | Displays Data
```

## Filtering Data

Filtering the data will allow you to be very granular with the output you will be displaying. For example, let's say you have an excel file that has thousands of rows, but first you want to get an idea of how the first 20 rows look. Or using our Excel example maybe you are just interested on the rows where the region equals West. Or maybe you want to group the records based on the month they were purchased. So knowing how to filter the data is very important to get what I call some free analytics.



## Conclusion

The take away is to understand that PowerShell will help you standardize the way you interact with any type of data. You no longer need to remember how to filter something in App1, how to filter this other thing in App2. Heck, you might not even be able to apply filter or sort things in the apps. Using PowerShell you can retrieve pretty much anything from anywhere and all the free analytics it gives you can be applied the same way to any application.
