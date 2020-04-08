---
layout: post
title:  PowerShell the Big Picture
date:   2020-03-07 19:07:15 -0500
image:  '/assets/img/PowerShell-Logo.png'
tags:   [PowerShell, Big Picture, blog]
---

## What is Powershell?
---

Is a Scripting Language built on top of .Net framework and in later releases on top of .Net Core.

## How it works?
---

In a nutshell you work with .Net objects that you are able to *GET*, *SET*, *DELETE*, *FILTER*, *FORMAT*, etc. Using the pipeline allows you to massage the objects to display the output as you like.

The following is an oversimplified example of how the pipeline works:

```

Gets Data | Filters it | Displays it

```

You define the order:
* Get
* Set
* Delete
* Filter
* Display - Always at the end
* etc.

All this could happen in one line of code

**In my personal opinion** PowerShell is the best at retrieving data, filtering it and displaying it in a simple and logical way.

## Where can I use PowerShell?
---

Windows, Linux and Mac.

## Why should I care?
---

```
> Because it is **STANDARIZED** which makes it very simple to digest as far as discovery.

> Syntax is a verb followed by a noun (**VERB**-**NOUN**), which you already have a big advantage compared to non-english speaking countries.

> It is going to make you **VERY** productive with very **MINIMAL** lines of code.
```

Let me show you the light at the end of the tunnel.

```powershell
cd 'C:\Users\hector.andrade\OneDrive - UGN, Inc\IT\Training\PowerShell\1_Showcase'
code '.\2 - Get.ps1'
```

## Recap
---

 Get Data | Filter | Display
 --- | --- | ---
Log file | Filter | PowerShell (Raw)
Text file | No Filter | Out-GridView
Server | | CSV
PC | | TSV
Data Base | | Excel
Web server | | Diagram
PLC | | Graph
Camera | | Windows Forms
Tesla | | WPF
Windows | | Web Page
Linux | | Chat Bot
Mac | | Azure Functions
Temperature sensor | | AWS Lambda
Motor | | PaaS
o365 | | SaaS
Azure | | FaaS
AWS | | etc.
On demand Input | |
Firewall | |
Switches | |
Sharepoint | |
etc. | |


* Now that you understand the big picture the question is
* Where does your data lives and where do you want to display it

#### A picture is worth a thousand words

![](https://media-exp1.licdn.com/dms/image/C4E12AQENK2dORDbjLg/article-cover_image-shrink_720_1280/0?e=1586390400&v=beta&t=EA6w7gAgvaeFJEP_tVRXO0l4LiHc145jmBm7DYYIDuA)

#### PowerShell is the most powerful application installed on your computer.

#### One tool to glue them all. Bye middlewares, welcome PowerShell