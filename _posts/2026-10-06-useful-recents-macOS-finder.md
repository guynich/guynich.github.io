---
layout: post
title: "After a long and puzzling wait, a more useful macOS Finder Recents view (WIP)"
date: 2026-10-06
---

> Updated since first post: adds scope; date added; list; sorting.

I switched to macOS when I joined Apple in late 2009.  I never missed Windows
since.  My new colleague Ruchir showed me some Finder tricks and I was sold.
Side story: Ruchir joined Apple two weeks before me but seemed to know
*everything*.

I've always been puzzled that sometime a newly created file is not shown in
Finder's Recents view.  Like when I use macOS' native Image Capture app to scan
a document to a Documents folder.  The scanned file never appears in Recents
until after I go find and *open* the file.  Not so useful...

Today, with Claude's help, I realized a Finder Smart Folder can do better, much
better, for me than Apple Finder's native Recents.  I'm testing these settings.

<img src="/images/finder_smart_search_scoped.png" alt="Custom Recents in macOS Finder"
width="100%"/>

* Scope: in Finder select `Documents` and hit `command + F` to generate a scoped
  smart folder list only for documents
  * This excludes files found in other folders such as `~/Library`
* Hold `option` key when clicking `+` to generate the `Any` (or `All` or `None`)
  option
  * In the example I include `Other` > `Date added` to assist finding new files
  * The `None` option with `Name` allows you to exclude specific file
    extensions from the search result, not shown here
* Sort the `list` results either by `Date added` or by `Date Last Opened`
* Save the search as a Favorite.  It reruns every time you open the view in Finder
* I added smart folder search for other scopes such as `Pictures`.

This is going to make working on my computer a little bit easier every day.
