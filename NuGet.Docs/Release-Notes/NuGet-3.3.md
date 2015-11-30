
# NuGet 3.3 Release Notes

[NuGet 3.2.1 Release Notes](nuget-3.2.1) 

NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.

## New Features

* Credential Providers have been introduced that allow all NuGet clients to be able to work seamlessly with an authenticated feed.  [Instructions on how to install the Visual Studio Online credential provider ](http://docs.nuget.org/Consume/Credential-Providers) and configure the NuGet clients to use it are available on NuGet Docs.

## New User Interface Features

* Separate Browse, Installed, and Updates Available tabs
* Updates Available badge indicating the number of packages with available updates
* Package badges in the package list to indicate if the package is installed or has an update available
* Download count and author added to the package list
* Highest available version number and currently installed version number on the package list 
* Action buttons to allow quick install, update, and uninstall from the package list
* Clearer action buttons on the package detail panel
* Package update date on the package detail panel
* Consolidate panel in Solution view
* Sortable grid of projects and installed version numbers on the solution view

## New Command-line Features

In this version we introduced the init and add commands to initialize [folder-based repositories](http://docs.nuget.org/Consume/Command-Line-Reference#folder-repository-commands).  Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog. 

## ContentFiles

Content is now supported in project.json managed projects through the new `contentFiles` folder and nuspec `contentFiles` element notation.  This content can be more directly specified by the package author for interactions with project systems.  More information about how to configure contentFiles in a NuSpec document can be found in the [NuSpec Reference](http://docs.nuget.org/Create/NuSpec-References#contentfiles-with-nuget-3.3-and-later).

## Credential Providers

Starting with NuGet 3.3 we are introducing support for third-party credential providers that allow seamless integration with feeds that maintain their own authentication scheme.  Learn more about [how to create a credential provider and use credential providers at docs.nuget.org](http://docs.nuget.org/Consume/Credential-Providers)  

## Fixed Issues

The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).  

The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## Known Issues

We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)
