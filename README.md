[![Build Status](https://dev.azure.com/qmfrederik/appium-docker-ios/_apis/build/status/quamotion.xcshim?branchName=master)](https://dev.azure.com/qmfrederik/appium-docker-ios/_build/latest?definitionId=20&branchName=master)

# Xcode shim for Appium on Linux

This repository contains a Xcode shim which simulates the Xcode commands used by
Appium and forwards them to [Quamotion xcuitrunner](http://docs.quamotion.mobi/docs/xcuitrunner/getting-started/).

You can use Appium to run tests on real, physical iOS devices using a Linux device
with this shim.

The shim relies on tools from [Quamotion](http://quamotion.mobi) which make it possible
to run Appium for iOS on Linux. These tools are available under a commercial license
from [Quamotion](http://quamotion.mobi).
