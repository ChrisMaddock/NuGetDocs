# NuGet Frequently Asked Questions

## Getting started


**What is required to run NuGet?**

NuGet requires Visual Studio 2010 Pro/Premium/Ultimate (or newer), Visual Web Developer Express 2010, or any Express SKU of Visual Studio 2012 (or newer).
The NuGet Package Manager Console requires that [PowerShell 2.0](http://support.microsoft.com/kb/968929) be installed. 
Powershell 2.0 is already installed if you have the following operating systems:

* Windows 7 (or newer)
* Windows Server 2008 R2 (or newer)

If you have the following operating systems, you must [manually install Powershell 2.0](http://support.microsoft.com/kb/968929/en-us).

* Windows XP SP3 /Windows Vista SP1
* Windows Server 2003 SP2/ Windows Server 2008

**Are there any known issues with NuGet?
Please check out the [Known Issues](/Release-Notes/Known-Issues) page. 

**Does NuGet support Mono?**

The command-line application (*nuget.exe*) builds and runs under Mono (version 3.2 or later) and allows you to create packages in Mono.
This is especially true for Mono on Windows, but there are some known issues for Mono on Linux and OS X.  To review
the known issues, [search for Mono in our issue list](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono).

Also, [a graphical client is available as an add-in for MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin).

Details of the features that have currently been tested to work with Linux and OS X can be found under [compatibility](/consume/Compatibility)

**Is there a command-line tool for NuGet?**

**Yes there is!** See David Ebbo's Blog post entitled [Installing NuGet Packages directly from the command line](http://blog.davidebbo.com/2011/01/installing-nuget-packages-directly-from.html).

Keep in mind that the focus of NuGet is to let you modify your projects and add references to Visual Studio projects. 
The command line tool, NuGet.exe, will download and unpack packages, but it won't automate Visual Studio and 
modify your project files.
Within Visual Studio, there are two clients for NuGet: 
the PowerShell-based **Package Manager Console** and the **Manage NuGet Packages** dialog box. 
Both are wrappers around the NuGet API, which is written in managed code.
NuGet.exe is also used to create and publish packages.

## NuGet With Visual Studio

**How do I check the exact version of NuGet installed?**

In Visual Studio go to the _Help_ > _About Microsoft Visual Studio_ menu and look for NuGet Package Manager. The version is 
displayed next to that entry.

![NuGet Version in the Visual Studio Extension Manager](/images/consume/nuget-version.png)

Alternatively, you can launch the Package Manager Console and type in `$host` to output information about NuGet 
Powershell host including the version.

**What languages are supported by NuGet?**

The most recent version of NuGet supports C#, Visual Basic, F#, [WiX](http://wix.sourceforge.net/), and C++ Projects. For learning more about support for C++, check out our [blog post](http://blog.nuget.org/20130426/native-support.html) for more details.

**What project templates are supported by NuGet?**

NuGet has full support for a variety of project templates like Windows, Web, Silverlight, SharePoint, Wix and so on.  The support for LightSwitch and Cloud templates is minimal at this point of time.

**How do I update packages that are part of visual studio templates ?**

You can do an "Update All" from the "Manage NuGet Packages" dialog. More details [here](../Release-Notes/NuGet-2.5) or use the "Update-Package" command from NuGet Package Manager Console. This will get the latest version of all the packages that are part of the template.

However, if you want to update the template in one go, instead of doing it for every project, you will have to manually update the template repository. Check out [Xavier Decoster's blog on the same.](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)

Please be noted that manually updating the template repository should be done at your own risk. It might corrupt the template files or the latest version of the packages may not be compatible with each other.

## Can I use NuGet outside of Visual Studio?

**You sure can!** As discussed in the question on command line tools for NuGet, the primary focus 
of NuGet is Visual Studio, but the core NuGet API has no dependencies on Visual Studio. 
There are multiple NuGet clients that work completely outside of Visual Studio:

* [SharpDevelop Alpha](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx). (See a demo of this in [Phil Haack's MvcConf talk](http://bit.ly/fzrJDa).) 
* [NuGet.exe](http://blog.davidebbo.com/2011/01/installing-nuget-packages-directly-from.html) 
* [MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin) and Xamarin Studio add-in

## NuGet CommandLine

**How do I get the latest version of NuGet commandline?**

You can download NuGet.exe from [our distribution site](https://dist.nuget.org/index.html) or install the package from [nuget.org](http://www.nuget.org/packages/NuGet.CommandLine).

Once you have the command-line, use "NuGet.exe Update" to self update the exe to the latest version.

**Is it possible to extend NuGet commandline?**

Yes, it is possible to add custom commands to NuGet.exe.
Check out [this post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx) by Rob Reynolds for a quick walkthrough.

## NuGet Package Manager Console

**How do I get access to the DTE object in the Package Manager console?**

The console provides a variable named `$DTE` that returns the `DTE` object. See the `Get-Project` command in 
[Package Manager Console Powershell Reference](/Consume/Package-Manager-Console-PowerShell-Reference).

**Why does the Package Manager Console or the Manage NuGet Packages dialog box crash or show an exception?**

Check the [Known Issues](/Release-Notes/Known-Issues) page. Typically, the issue is due to having an older version of the Reflector add-in installed or not having PowerShell 2.0 installed (as in the case of Windows XP).

**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**

This is a known issue with how PowerShell interacts with a COM object. Try the following:
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
`Get-Interface` is a helper function added by the NuGet PowerShell host.


## Creating and Publishing packages

**How do I get my package in the feed?**

See the [Creating and publishing a package](/Create/creating-and-publishing-a-package) page.

**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**

See the section titled "Supporting Multiple .NET Framework Versions and Profiles" in [Creating a Package](/Create/Enforced-Package-Conventions#supporting-multiple-.net-framework-versions-and-profiles).

**How do I set up a local repository or feed?**

See [Hosting Your Own NuGet Feeds](/Create/Hosting-Your-Own-NuGet-Feeds).

**How can I bulk upload packages to my NuGet feed ?**

See [Bulk Publishing NuGet Packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx).
	
**How can I create package out of a project or solution ?**

You can use Nuget.exe [Pack command](/consume/command-line-reference#pack-command-examples) to create a NuGet package out a project.

This command will take care adding all the NuGet packages installed in the project as package dependencies and referenced projects as "Reference" assemblies in the package.
You can invoke this command in post build event to automate the build process.


## Working with Packages


**What is the difference between a project-level package and a solution-level package?**

A solution-level package has to be installed only once in a solution to be available for all projects in the solution. 
A project-level package must be installed separately in each project where you want to use it.
For solution-level packages, NuGet doesn't change anything in a project, whereas in a project-level package it does. 
Typically, a solution-level package installs new commands that can be called from within the **Package Manager Console** window.

**Is it possible to install NuGet package without internet ?**

**Yes you can!** See Scott Hanselman's Blog post entitled [How to access NuGet when NuGet.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx).

**How to install packages in a different location from the default "Packages" folder?**

This can be done by setting the "repositoryPath" settings in nuget.config.
More details [here.](/release-notes/nuget-2.1)

**How do I avoid checking in packages folder to source control?**

You can turn off source control integration for the Packages folder by setting the "disableSourceControlIntegration" propety in the nuget.config to "true".

This key works at the solution level and hence need to be added to the NuGet.config file present in the "$(SolutionDir)\.nuget directory". Enabling package restore from VS would add the .nuget\nuget.config file automatically.


**How do I turn off package restore?**

You can disable package restore at the machine wide using the package manager settings or by setting an environment variable "EnableNugetPackageRestore" to "false". 
However, to disable just at sln level, you would have to manually delete the .nuget folder from the Solution and the file system and revert the changes in the csproj file related to package restore.

**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**

**Select the *All* node when installing your local package.** The *all** node aggregates all the feeds. 
When you select a specific repository under the Online tab, that restricts installation to just that node. 
The reason for this behavior is that in many cases, users of a local repository don't want to accidentally 
install a remote package due to corporate polices.

## Managing Packages in NuGet.Org

**Is it possible to reserve names for packages that will be published in future?**

It is not possible to squat package names. If you feel that an existing package has taken the name which suits your package more, try [contacting the owner of the package](https://nuget.org/packages/[package ID]/ContactOwners?). If you didnt get response within a couple of weeks, you can contact support and the NuGet Gallery team will look in to it.

**How do I claim ownership for packages ?**

Check out [Managing Package Owners on nuget.org](/Create/Managing-Package-Owners) for details.

**How do I deal with a package owner who is violating my software license?**

We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.  We have crafted a [dispute resolution process](/Consume/Dispute-Resolution) that we ask you to follow before NuGet.org administrators intercede.


**Is it recommended to upload my test packages to NuGet.org ?**

For test purposes, you can use [staging.nuget.org](http://staging.nuget.org). Please note that the packages being uploaded to staging.nuget.org may not be preserved. More details can be found [here.](http://blog.nuget.org/20130419/goodbye-preview.html)


**Why can't I download / upload packages to NuGet.org?**

When downloading and uploading to NuGet does not work, it's best to [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information such as MTR or a Fiddler trace.

To capture MTR:

> 1. Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)
> 2. Enter `api.nuget.org` as the hostname and click *Start*.
> 3. Wait until the *Sent* column is >= 100.
> 
>    ![MTR](/images/consume/mtr.png)
> 
> 4. Copy text to clipboard and include the copied details in your support request. Also let us know your geographical area.

To capture Fiddler:

> 1. Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler). 
> 2. Start Fiddler and disable capturing traffic using the *File | Capture Traffic* menu.
> 3. Remove all sessions (select all items in the list, press the *Delete* key)
> 4. Configure Fiddler to capture HTTPS traffic by checking  *Decrypt HTTPS traffic* in the *HTTPS* tab of the *Tools | Fiddler Options...* menu.
> 5. Close Visual Studio.
> 6. Enable the *File | Capture Traffic* menu.
> 7. Start Visual Studio or NuGet.exe and perform the actions that are not working. The traffic generated by these actions should show up in Fiddler.
> 8. Once the actions have run, use the *File | Save | All Sessions* menu and store the captured sessions. Include the file in your support request.

Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler. If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).