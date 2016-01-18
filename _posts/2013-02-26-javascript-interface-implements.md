---
author: bluishoul
comments: true
date: 2013-02-26 08:26:53+00:00
layout: post
slug: javascript-interface-implements
title: JavaScript Interface 简单实现
wordpress_id: 1126
categories:
- 一周一博
tags:
- javascript
- pomodoro-time
---

开发 Pomodoro Time App 时需要考虑到将来可移植的问题，比如移植到 PhoneGap上或者在桌面Chrome上运行，例如 对通知的处理可能就有所不同，PhoneGap 能够调用系统的声音以及震动来实现通知提醒功能，而在Chrome上可以利用弹窗和声音来实现，为了实现解耦合。
这样的场景太多了，所以简单的设计了一下 Interface（接口）概念：


