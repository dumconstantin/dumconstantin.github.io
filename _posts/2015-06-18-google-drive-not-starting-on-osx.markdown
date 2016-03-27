---
layout: post
title: "Google Drive not starting on OSX"
comments: true
date: 2015-06-18 09:00:00
categories: productivity
---
Symptoms:

* Google Drive icon does not show in the top bar
* When trying to launch the Google Drive app from the Application folder it crashes silently
* After deleting and reinstalling the same behaviour occurs

The solution that worked for me was to delete the “~/Library/Application Support/Google/Drive” folder and then restart Google Drive – my Google Drive files were not harmed during the process :)
