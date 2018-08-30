## The Pack URI Scheme
Uniform resource identifiers (URIs) are used to identify and load files in many ways:
* Specifying the user interface (UI) to show when an application first starts
* Loading images
* Navigating to pages
* Loading non-executable data files

Furthermore, URIs can be used to identify and load files from a variety of locations:
* The current assembly
* A referenced assembly
* A location relative to an assembly
* The application's site of origin

Pack URI Scheme:
* Open Packaging Conventions (OPC) specification
* describes a model for organizing and identifying content
* key elements are packages and parts, where a package is a logical container for one or more logical parts

**Format of pack URI :`pack://authority/path`**   
The authority specifies the type of package that a part is contained by, while the path specifies the location of a part within a package.


## [Resource File Pack URIs](https://docs.microsoft.com/en-us/dotnet/framework/wpf/app-development/pack-uris-in-wpf#resource-file-pack-uris)
