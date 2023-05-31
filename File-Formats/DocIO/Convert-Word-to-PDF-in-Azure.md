---
title: Convert Word document to PDF in Microsoft Azure | Syncfusion
description: Learn how to convert a Word document to a PDF in Azure services using Syncfusion .NET Word (DocIO) library in C#.
platform: file-formats
control: DocIO
documentation: UG
---


# Convert Word to PDF in Azure Platform 

Syncfusion Essential DocIO is a [.NET Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, **convert a Word document to a PDF in Azure services** within a few lines of code. 

N> If this is your first time working with Azure, please refer to the dedicated Azure development resources. This section explains how to convert Word documents to PDF in C# using the .NET Word (DocIO) library in Azure. 

## Prerequisites 
* An active **Microsoft Azure subscription** is required. If you don’t have one, please create a free account before starting.

## Nuget package required
<table>
<thead>
<tr>
<th>
Azure Services<br/></th><th>
NuGet package name<br/></th></tr></thead>
<tr>
<td>
App Service (Linux)<br/></td><td>
{{'[Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core)' | markdownify}}<br/>
{{'[SkiaSharp.NativeAssets.Linux v2.8.2.3](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux)' | markdownify}}<br/>{{'[HarfBuzzSharp.NativeAssets.Linux v2.88.3](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux)' |markdownify}} <br/></td></tr>
<tr>
<td>
Azure Functions v1 <br/></td><td>
{{'[Syncfusion.DocToPDFConverter.AspNet](https://www.nuget.org/packages/Syncfusion.DocToPDFConverter.AspNet)' |markdownify}} <br/></td></tr>
<tr>
<td>
Azure Functions v4 <br/></td><td>
{{'[Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core)' | markdownify }}<br/></td></tr>
</table>