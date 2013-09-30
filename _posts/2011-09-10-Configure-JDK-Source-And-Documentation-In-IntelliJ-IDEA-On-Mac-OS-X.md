---
layout: post
title: Configure JDK Source and Documentation in IntelliJ IDEA on Mac OS X
author: Milinda Pathirage
time: 2011-09-10
excerpt: This post describes steps necessary to download and configure JDK source files and documetation in IntelliJ IDEA on Mac OS X.
---

When you install IntelliJ IDEA on Mac OS X, it doesn't automatically pick the JDK source and documentation as it do in Linux. As I got to know this is because default Java installation in Mac OS X doesn't have those. You need to first download "*Java for Mac OS X <version> Developer Package*" from [Apple Developer Downloads](http://connect.apple.com/). You have to follow below steps to configure JDK source and documentation in IntelliJ IDEA.

1. Sign in to Apple’s [Developer Downloads](http://connect.apple.com/) using you Apple Developer account.  
2. Select “Downloads” under “Browse” and then “Java” under “Downloads”.
3. Download and install “Java for Mac OS X z.z Update z Developer Package” or "Developer Preview" package suitable for your system. 
4. Open the “Project Structure” dialog through “File” menu or through tool bar.
5. Click on “SDKs” under “Platform Settings” and look at the “Documentation Paths” tab.
6. Add the following paths (the path may be different based on which JDK you’re using):
	* /Library/Java/JavaVirtualMachines/**java.version**/Contents/Home/docs.jar!/docs/api
	* /Library/Java/JavaVirtualMachines/**java.version**/Contents/Home/appledocs.jar!/appledoc/api
7. Add the following path under the Sourcepath tab:
	* /Library/Java/JavaVirtualMachines/**java.version**/Contents/Home/src.jar!/src
	
After you done the above steps you should be able to go to JDK sources and your auto completion should show documentation for classes and methods. 