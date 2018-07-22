---
title: "iOS Localization Tool"
date: 2018-07-22T13:39:13+08:00
draft: false
categories: [iOS, Localization]
tags: [iOS, localization, tools, python]
author: rogermolas
---

Localization is simply the process of translating your app into multiple languages.

In situation like you need support multiple language, including API response messages and dynamic strings you need a list of localizable .strings file, and you need to localized it based on the Language you want  ( e.g ***English***, ***Chinese***, ***Japanese*** ). 

Xcode has a **built-in** localizable file generator that generate your localizable .strings for each language you supported.

In this format
```
en.lproj  // directory
   |- localizable.strings

zh.lproj  // directory
   |- localizable.strings

ja.lproj  // directory
   |- localizable.strings
```
Thats Cool!!

***But how about the contents?***

You need to copy and paste it base on it corresponding laguage. For Chinese stings you put it on **zh.lproj/ localizable.strings** and  for Japanese stings put it on **ja.lproj/ localizable.strings** and your good to go.

***Holy Shiiit, i have 400 stings that needs to be localized in 3 or more languages*** 400 x  3 = 1,200

Just copy and paste your 1,200 lines of string, Good Luck!
s
### To solve the pain of copy and pasting and save time.

you can use the tool called [**csv-localizer**](https://github.com/rogermolas/csv-localizer) [![GitHub stars](https://img.shields.io/github/stars/badges/shields.svg?style=social&label=Stars)](https://github.com/rogermolas/csv-localizer) available on Github.

Just instruct you translator or someone working on translations to put all translated strings into CSV file based on the format provided.

**csv-localizer** can be installed from homebrew via

```bash
$ brew tap rogermolas/csv-localizer
$ brew install csv-localizer
```

Convert using the following command

```bash
$ csv-localizer -p ios -i path/csv_files/ -o path/output
```
>*Input directory, CSV files directory path, should not include the .csv file*
>*"path/csv_files/*" **and not** "*~~path/csv_files/strings.csv~~*"

>**The reason for that is, csv-localizer can process multiple csv files, thats why its only accept  a directory path.**


Generated files
```
en.lproj  // directory
   |- localizable.strings

zh.lproj  // directory
   |- localizable.strings

ja.lproj  // directory
   |- localizable.strings
```
Thats it,  your ready to go. Easy Right?

It will generate the same format just like what Xcode did, but this time it has its localized contents in each corresponding laguage. :)
