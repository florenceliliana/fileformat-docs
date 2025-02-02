---
title: Syncfusion Excel to PDF Conversion
description: In this section, you can learn how to convert Excel Workbook to PDF & Worksheet to PDF file; how to print Excel file and how to convert Excel chart to image
platform: file-formats
control: XlsIO
documentation: UG
---

# Excel to PDF Conversion

[XlsIO](https://www.syncfusion.com/document-processing/excel-framework/net/excel-to-pdf-conversion) supports converting an entire workbook or a single worksheet into PDF document. Refer the following links for assemblies/nuget packages required based on platforms to convert Excel document into PDF.

* [Assemblies Information](https://help.syncfusion.com/file-formats/xlsio/assemblies-required#converting-excel-document-to-pdf) 
* [NuGet Information](https://help.syncfusion.com/file-formats/xlsio/nuget-packages-required#converting-excel-document-into-pdf)

N> Worksheet To Image conversion can be performed by referring [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) NuGet package in UWP platform.

## Workbook to PDF

The following code illustrates how to convert an entire Excel workbook to PDF.

{% tabs %} 
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
   IApplication application = excelEngine.Excel;
   application.DefaultVersion = ExcelVersion.Xlsx;
   FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
   IWorkbook workbook = application.Workbooks.Open(excelStream);

   //Initialize XlsIO renderer.
   XlsIORenderer renderer = new XlsIORenderer();

   //Convert Excel document into PDF document 
   PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

   Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
   pdfDocument.Save(stream);

   excelStream.Dispose();
   stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Open the Excel document to Convert
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the PDF document
  Dim pdfDocument As PdfDocument = New PdfDocument()

  'Convert Excel document into PDF document
  pdfDocument = converter.Convert()

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example for converting entire Excel workbook to PDF in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/Workbook%20to%20PDF).    

To learn more about different conversion settings in Excel To PDF conversion, refer the [Excel to PDF conversion settings](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-converter-settings). 

## Worksheet to PDF

The following code shows how to convert a particular worksheet to PDF document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(worksheet);

  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  excelStream.Dispose();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //convert the sheet to PDF
  ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

  PdfDocument pdfDocument= new PdfDocument();
  pdfDocument = converter.Convert();
  pdfDocument.Save("ExcelToPDF.pdf");     
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx

  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Converts the particular sheet 
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(sheet)

  Dim pdfDocument As PdfDocument = New PdfDocument()
  pdfDocument = converter.Convert()

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}  

A complete working example for converting particular worksheet to PDF in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/Worksheet%20to%20PDF). 

### Creating individual PDF document for each worksheet

The following code snippet shows how to create an individual PDF document for each worksheet in a workbook.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  applicatin.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();
  PdfDocument pdfDocument = new PdfDocument();   

  foreach (IWorksheet sheet in workbook.Worksheets)
  {
    pdfDocument = renderer.ConvertToPDF(sheet);
    //Save the PDF file
    Stream stream = new FileStream(sheet.Name+".pdf", FileMode.Create, FileAccess.ReadWrite);
    pdfDocument.Save(stream);
    stream.Dispose();
  }
  excelStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  PdfDocument pdfDocument = new PdfDocument();     

  foreach (IWorksheet sheet in workbook.Worksheets)
  {
    ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);
    pdfDocument = converter.Convert();

    //Save the PDF file
    pdfDocument.Save(sheet.Name+".pdf");
    converter.Dispose();
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  Dim pdfDocument As New PdfDocument()

  For Each sheet As IWorksheet In workbook.Worksheets
    Dim converter As New ExcelToPdfConverter(sheet)
    PdfDocument = converter.Convert()

    'Save the PDF file
    PdfDocument.Save(sheet.Name + ".pdf")
    converter.Dispose()
  Next
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to convert each worksheet into individual PDF in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/Each%20Worksheet%20to%20PDF).
  
## Excel with chart to PDF

XlsIO supports to convert a workbook/worksheet with charts or a single chart into PDF document.

To preserve the charts during Excel To PDF conversion in .NET Framework, initialize the [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html#Syncfusion_XlsIO_IApplication_ChartToImageConverter) of [IApplication](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html) interface. Otherwise the charts present in worksheet gets skipped.

The following code illustrates how to convert an Excel with chart to PDF document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  FileStream excelStream = new FileStream("chart.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Convert Excel document with charts into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);
  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  excelStream.Dispose();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application
  application.ChartToImageConverter = new ChartToImageConverter();

  //Tuning chart image quality
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best;
  IWorkbook workbook = application.Workbooks.Open("chart.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);
  PdfDocument pdfDocument = new PdfDocument();
  pdfDocument = converter.Convert();
  pdfDocument.Save("ExcelToPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx

  'Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application
  application.ChartToImageConverter = New ChartToImageConverter()

  'Tuning chart image quality
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best

  Dim workbook As IWorkbook = application.Workbooks.Open("chart.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  Dim converter As New ExcelToPdfConverter(workbook)  
  Dim pdfDocument As New PdfDocument()
  pdfDocument = converter.Convert()
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}  

A complete working example to convert Excel chart to PDF in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/Chart%20to%20PDF).

## Excel with comments (notes) to PDF

XlsIO supports to convert a workbook or a worksheet with comments (notes) to PDF documents. By default, comments (notes) will not get converted. To convert the comments in worksheets of an Excel workbook, it is a must to set the print options through [ExcelPrintLocation](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelPrintLocation.html) enumeration. This option helps to convert,

* comments as displayed in place,
* comments at the end of the sheet, and
* without comments.

### Convert comments as displayed in place
Comments (notes) will be rendered in the output PDF document as displayed in the Excel file, if the **PrintInPlace** option is selected. The following code illustrates this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintInPlace;

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(worksheet);

  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  excelStream.Dispose();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintInPlace;
  ExcelToPdfConverter converter = new ExcelToPdfConverter(worksheet);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf");
  System.Diagnostics.Process.Start("ExcelToPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintInPlace

  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the PDF document
  Dim pdfDocument As PdfDocument = New PdfDocument()

  'Convert Excel document into PDF document
  pdfDocument = converter.Convert()

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel with comments to PDF and render comments in place in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/Comments%20in%20Place%20to%20PDF).

The following screenshot represents the input Excel file with notes

![Input excel file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img2.png)

The following screenshot represents the output pdf file generated by the XlsIO using **PrintInPlace** option

![Output pdf file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img3.png)

### Convert comments at the end of the sheet
Comments (notes) will be rendered in the output PDF document at the end of the each sheet which contains the comments (notes), when the **PrintSheetEnd** option is selected. The following code illustrates this. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintSheetEnd;

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(worksheet);
  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  excelStream.Dispose();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintSheetEnd;
  ExcelToPdfConverter converter = new ExcelToPdfConverter(worksheet);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf");
  System.Diagnostics.Process.Start("ExcelToPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintSheetEnd

  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the PDF document
  Dim pdfDocument As PdfDocument = New PdfDocument()

  'Convert Excel document into PDF document
  pdfDocument = converter.Convert()

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel with comments to PDF and render comments at the end in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/Comments%20to%20PDF%20at%20End).

The following screenshot represents the input Excel file with notes

![Input excel file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img4.png)

The following screenshot represents the output pdf file generated by the XlsIO using **PrintSheetEnd** option

![Output pdf file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img5.png)
![Output pdf file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img6.png)

### Convert without comments
Comments (notes) will not be displayed in the output PDF document, if the **PrintNoComments** option is selected. The following code illustrates this. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintNoComments;

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(worksheet);
  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  excelStream.Dispose();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintNoComments;
  ExcelToPdfConverter converter = new ExcelToPdfConverter(worksheet);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf");
  System.Diagnostics.Process.Start("ExcelToPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set print location to comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintNoComments

  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the PDF document
  Dim pdfDocument As PdfDocument = New PdfDocument()

  'Convert Excel document into PDF document
  pdfDocument = converter.Convert()

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel with comments to PDF ignoring the comments in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20to%20PDF/No%20Comments%20in%20PDF).

The following screenshot represents the input Excel file with notes

![Input excel file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img2.png)

The following screenshot represents the output pdf file generated by the XlsIO using **PrintNoComments** option

![Output pdf file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img7.png)

## Excel with threaded comments to PDF

XlsIO supports converting threaded comments conversation in Excel document to PDF. To convert the threaded comments to PDF, the print options should be set through [ExcelPrintLocation](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelPrintLocation.html) enumeration.

### Convert threaded comments at the end of the sheet

Threaded comments will be rendered in the PDF document at the end of the each sheet, when the **PrintSheetEnd** option is selected. The following code illustrates how to set print options to convert threaded comments.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream inputStream = new FileStream("CommentsTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add threaded comment
  IThreadedComment threadedComment = worksheet.Range["H16"].AddThreadedComment("What is the reason for the higher total amount of \"desk\"  in the west region?", "User1", DateTime.Now);
  
  //Add reply to the threaded comement
  threadedComment.AddReply("The unit cost of desk is higher compared to other items in the west region. As a result, the total amount is elevated.", "User2", DateTime.Now);
  threadedComment.AddReply("Additionally, Wilson sold 31 desks in the west region, which is also a contributing factor to the increased total amount.", "User3", DateTime.Now);

  //Set print location to threaded comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintSheetEnd;

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(worksheet);
  Stream stream = new FileStream("ExcelComments.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("CommentsTemplate.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add threaded comment
  IThreadedComment threadedComment = worksheet.Range["H16"].AddThreadedComment("What is the reason for the higher total amount of \"desk\"  in the west region?", "User1", DateTime.Now);
  
  //Add reply to the threaded comement
  threadedComment.AddReply("The unit cost of desk is higher compared to other items in the west region. As a result, the total amount is elevated.", "User2", DateTime.Now);
  threadedComment.AddReply("Additionally, Wilson sold 31 desks in the west region, which is also a contributing factor to the increased total amount.", "User3", DateTime.Now);
  
  //Set print location to threaded comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintSheetEnd;
  ExcelToPdfConverter converter = new ExcelToPdfConverter(worksheet);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the PDF document
  pdfDocument.Save("ExcelComments.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("CommentsTemplate.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Add threaded comment
  Dim threadedComment As IThreadedComment = worksheet.Range("H16").AddThreadedComment("What is the reason for the higher total amount of ""desk""  in the west region?", "User1", DateTime.Now)

  'Add reply to the threaded comement
  threadedComment.AddReply("The unit cost of desk is higher compared to other items in the west region. As a result, the total amount is elevated.", "User2", DateTime.Now)
  threadedComment.AddReply("Additionally, Wilson sold 31 desks in the west region, which is also a contributing factor to the increased total amount.", "User3", DateTime.Now)
  
  'Set print location to threaded comments
  worksheet.PageSetup.PrintComments = ExcelPrintLocation.PrintSheetEnd

  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the PDF document
  Dim pdfDocument As PdfDocument = New PdfDocument()

  'Convert Excel document into PDF document
  pdfDocument = converter.Convert()

  'Save the PDF document
  pdfDocument.Save("ExcelComments.pdf")
End Using
{% endhighlight %}
{% endtabs %}

The following screenshot represents the input Excel document with threaded comments

![Input excel file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img8.png)

The following screenshot represents the output pdf document generated by the XlsIO using **PrintSheetEnd** option

![Output pdf file](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img9.png)

## Substitute Font in Excel-to-PDF Conversion

By default, XlsIO substitutes unsupported fonts to **Microsoft Sans Serif** in Excel-to-PDF conversion. However, there might be a requirement for substituting a different font or the same font for the unsupported font during the conversion. XlsIO supports substituting unsupported or missing fonts through the event [SubstituteFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html#Syncfusion_XlsIO_IApplication_SubstituteFont). The event has the below arguments:

**AlternateFontName** – Substitutes an available font in the machine for the [OriginalFontName](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.SubstituteFontEventArgs.html#Syncfusion_XlsIO_Implementation_SubstituteFontEventArgs_OriginalFontName).
**AlternateFontStream** – Substitutes a font from stream that is added as embedded resource for the [OriginalFontName](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.SubstituteFontEventArgs.html#Syncfusion_XlsIO_Implementation_SubstituteFontEventArgs_OriginalFontName).	

The following code illustrates how to perform Excel-to-PDF conversion by substituting unsupported fonts in the machine.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using System;
using System.IO;
using Syncfusion.XlsIO;
using Syncfusion.XlsIORenderer;
using Syncfusion.Pdf;
using System.Reflection;

namespace FontSubstitution
{
  class Program
  {
    static void Main(string[] args)
    {
      using (ExcelEngine excelEngine = new ExcelEngine())
      {
        IApplication application = excelEngine.Excel;
        application.DefaultVersion = ExcelVersion.Xlsx;
        //Initializes the SubstituteFont event to perform font substitution during Excel-to-PDF conversion
        application.SubstituteFont += new SubstituteFontEventHandler(SubstituteFont);

        //Initialize XlsIO renderer.
        XlsIORenderer renderer = new XlsIORenderer();

        FileStream excelStream = new FileStream("Template.xlsx", FileMode.Open, FileAccess.Read);
        IWorkbook workbook = application.Workbooks.Open(excelStream);

        //Convert Excel document with charts into PDF document 
        PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

        Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
        pdfDocument.Save(stream);

        excelStream.Dispose();
        stream.Dispose();
      }
    }

    private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
    {
      //Substitute a font if the specified font is not installed in the machine.
      if (args.OriginalFontName == "Arial Unicode MS")
        args.AlternateFontName = "Arial";
      else if (args.OriginalFontName == "Homizio")
      {
        //Substitute by font stream.
        var assembly = Assembly.GetExecutingAssembly();
        var resourceName = "ExceltoPDF.Fonts.Homizio.ttf";
        Stream fileStream = assembly.GetManifestResourceStream(resourceName);
        MemoryStream memoryStream = new MemoryStream();
        fileStream.CopyTo(memoryStream);
        fileStream.Close();
        args.AlternateFontStream = memoryStream;
      }
    }
  }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using Syncfusion.ExcelToPdfConverter;
using Syncfusion.Pdf;
using Syncfusion.XlsIO;
using Syncfusion.XlsIO.Implementation;
using System.IO;
using System.Reflection;

namespace FontSubstitution
{
  class Program
  {
    static void Main(string[] args)
    {
      using (ExcelEngine excelEngine = new ExcelEngine())
      {
        IApplication application = excelEngine.Excel;
        application.DefaultVersion = ExcelVersion.Xlsx;

        //Initializes the SubstituteFont event to perform font substitution in Excel-to-PDF conversion.
        application.SubstituteFont += new SubstituteFontEventHandler(SubstituteFont);

        IWorkbook workbook = application.Workbooks.Open("Template.xlsx");
        IWorksheet worksheet = workbook.Worksheets[0];
        ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

        PdfDocument pdfDocument = new PdfDocument();
        pdfDocument = converter.Convert();
        pdfDocument.Save("ExcelToPDF.pdf");
      }
    }

    private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
    {
      //Substitute a font if the specified font is not installed in the machine.
      if (args.OriginalFontName == "Arial Unicode MS")
      {
        //Substitute by font name.
        args.AlternateFontName = "Arial";
      }
      else if (args.OriginalFontName == "Homizio")
      {
        //Substitute by font stream.
        var assembly = Assembly.GetExecutingAssembly();
        var resourceName = "ExceltoPDF.Fonts.Homizio.ttf";
        Stream fileStream = assembly.GetManifestResourceStream(resourceName);
        MemoryStream memoryStream = new MemoryStream();
        fileStream.CopyTo(memoryStream);
        fileStream.Close();
        args.AlternateFontStream = memoryStream;
      }
    }
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Imports Syncfusion.ExcelToPdfConverter
Imports Syncfusion.Pdf
Imports Syncfusion.XlsIO
Imports Syncfusion.XlsIO.Implementation
Imports System.IO
Imports System.Reflection

Namespace FontSubstitution
  
  Class Program
    
    Private Shared Sub Main(ByVal args() As String)
      Dim excelEngine As ExcelEngine = New ExcelEngine
      Dim application As IApplication = excelEngine.Excel
      application.DefaultVersion = ExcelVersion.Xlsx

      'Initializes the SubstituteFont event to perform font substitution in Excel-to-PDF conversion.
      AddHandler application.SubstituteFont, AddressOf Me.SubstituteFont

      Dim workbook As IWorkbook = application.Workbooks.Open("Template.xlsx")
      Dim worksheet As IWorksheet = workbook.Worksheets(0)
      Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)
      Dim pdfDocument As PdfDocument = New PdfDocument
      pdfDocument = converter.Convert
      pdfDocument.Save("ExcelToPDF.pdf")
    End Sub
    
    Private Shared Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
      'Substitute a font if the specified font is not installed in the machine.
      If (args.OriginalFontName = "Arial Unicode MS") Then
        'Substitute by font name.
        args.AlternateFontName = "Arial"
      ElseIf (args.OriginalFontName = "Homizio") Then
        'Substitute by font stream.
        Dim assembly = Assembly.GetExecutingAssembly
        Dim resourceName = "ExceltoPDF.Fonts.Homizio.ttf"
        Dim fileStream As Stream = assembly.GetManifestResourceStream(resourceName)
        Dim memoryStream As MemoryStream = New MemoryStream
        fileStream.CopyTo(memoryStream)
        fileStream.Close
        args.AlternateFontStream = memoryStream
      End If
      
    End Sub
  End Class
End Namespace
{% endhighlight %}
{% endtabs %}  

## Excel to PDF conversion in Linux OS

In Linux OS, the Excel to PDF conversion can be performed using .NET Core (Targeting .netcoreapp) application. Please refer [Excel to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/xlsio/nuget-packages-required#converting-excel-document-into-pdf) to know about the packages required to deploy .NET Core (Targeting .netcoreapp) application with Excel to PDF conversion capabilities.

In addition to the previous NuGet packages, SkiaSharp.Linux helper NuGet package is required, that can be generated by the following steps: 

1. Download libSkiaSharp.so [here](https://github.com/mono/SkiaSharp/releases/tag/v1.59.3#).
2. Create a folder and name it as SkiaSharp.Linux and place the downloaded file in the folder structure "SkiaSharp.Linux\runtimes\linux-x64\native"
3. Create a nuspec file with name SkiaSharp.Linux.nuspec using the following metadata information and place it inside SkiaSharp.Linux folder. The nuspec file can be customized.

{% tabs %}
{% highlight XML %}
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <id>SkiaSharp.Linux</id>
    <version>1.59.3</version>
    <title>SkiaSharp for Linux</title>
    <authors>Syncfusion Inc.</authors>
    <owners>Syncfusion Inc.</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>SkiaSharp for Linux is a supporting package for Linux platforms.</description>
    <tags>linux,cross-platform,skiasharp,net-standard,net-core,excel-to-pdf</tags>
    <dependencies>
      <group targetFramework=".NETStandard1.4">
        <dependency id="SkiaSharp" version="1.59.3" />
      </group>
    </dependencies>
  </metadata>
</package>
{% endhighlight %}
{% endtabs %}

4. Make sure that the nuget.exe file is present along with SkiaSharp.Linux folder (in the parent folder of SkiaSharp.Linux folder). If not, download it from [here](https://www.nuget.org/downloads#).
5. Open a command prompt and navigate to SkiaSharp.Linux folder.
6. Execute the following command.

~~~
nuget pack SkiaSharp.Linux\SkiaSharp.Linux.nuspec -outputdirectory "C:\NuGet" 
~~~

The output directory can be customized as per your need.

Now, SkiaSharp.Linux NuGet will be generated in the mentioned output directory and add the generated NuGet as additional reference. SkiaSharp.Linux NuGet package can also be downloaded from [here](https://www.syncfusion.com/downloads/support/directtrac/general/ze/SkiaSharp.Linux.1.59.3-2103435070#).

## Print Excel document

XlsIO supports Excel printing option by converting Excel To PDF and printing that PDF document. The Excel can be printed with specified page setup and printer settings in XlsIO.

The following printer settings can be applied to print Excel in XlsIO. 

![Printer settings](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img1.jpg)
 
### Print Excel document 

The following code snippet illustrates how to print the Excel document in XlsIO.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  // Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  // Print the converted PDF document
  converter.Print();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Print the converted PDF document
  converter.Print()
End Using
{% endhighlight %}
{% endtabs %}

### Print with printer settings

The following code snippet illustrates how to print the Excel document with printer settings in XlsIO.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  //Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize the printer settings
  PrinterSettings printerSettings = new PrinterSettings();

  //customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS";
  printerSettings.Copies = 2;
  printerSettings.FromPage = 2;
  printerSettings.ToPage = 3;
  printerSettings.DefaultPageSettings.Color = false;
  printerSettings.Duplex = Duplex.Vertical;

  //Print the converted PDF document with printer settings
  converter.Print(printerSettings);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the printer settings
  Dim printerSettings As PrinterSettings = New PrinterSettings

  'customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS"
  printerSettings.Copies = 2
  printerSettings.FromPage = 2
  printerSettings.ToPage = 3
  printerSettings.DefaultPageSettings.Color = false
  printerSettings.Duplex = Duplex.Vertical

  'Print the converted PDF document with printer settings
  converter.Print(printerSettings)
End Using
{% endhighlight %}
{% endtabs %}

### Print with Excel To PDF converter settings

The following code snippet illustrates how to print the Excel document with Excel To PDF converter settings in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx");

  //Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initializes the Excel To PDF converter setting class
  ExcelToPdfConverterSettings converterSettings = new ExcelToPdfConverterSettings();

  //Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible;
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Print the converted PDF document with converter settings
  converter.Print(converterSettings);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the Excel To PDF converter setting class
  Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

  'Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Print the converted PDF document with converter settings
  converter.Print(converterSettings)
End Using
{% endhighlight %}
{% endtabs %}

### Print with Excel To PDF converter and printer settings

The following code snippet illustrates how to print the Excel document with Excel To PDF converter settings and printer settings in XlsIO.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize the printer settings
  PrinterSettings printerSettings = new PrinterSettings();

  //customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS";
  printerSettings.Copies = 2;
  printerSettings.FromPage = 2;
  printerSettings.ToPage = 3;
  printerSettings.DefaultPageSettings.Color = true;
  printerSettings.Duplex = Duplex.Vertical;
  printerSettings.Collate = true;

  //Initializes the Excel To PDF converter setting class
  ExcelToPdfConverterSettings converterSettings = new ExcelToPdfConverterSettings();

  //Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible;
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Print the converted PDF document with printer settings and converter settings
  converter.Print(printerSettings, converterSettings);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the printer settings
  Dim printerSettings As PrinterSettings = New PrinterSettings

  'customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS"
  printerSettings.Copies = 2
  printerSettings.FromPage = 2
  printerSettings.ToPage = 3
  printerSettings.DefaultPageSettings.Color = true
  printerSettings.Duplex = Duplex.Vertical
  printerSettings.Collate = true

  'Initialize the Excel To PDF converter setting class
  Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

  'Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Print the converted PDF document with printer settings and converter settings
  converter.Print(printerSettings, converterSettings)
End Using
{% endhighlight %}
{% endtabs %}

  
N> Printing is supported only in Windows Forms and WPF platforms.

## Font fallback in Excel to PDF

This feature allows the use of substitute fonts when the fonts provided for the cell text cannot render the text properly in Excel to PDF conversion.

This feature allows the following options.

* Allow to fallback the unsupported fonts automatically with predefined fallback fonts.
* Replace the predefined fallback font with a custom font.

The following code illustrates how to use font fallback in the Excel to PDF Conversion.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(fileStream);              
    IWorksheet sheet = workbook.Worksheets[0];            
    application.XlsIORenderer = new XlsIORenderer();

    //Initialize fallback Font
    application.FallbackFonts.InitializeDefault();
    //Add customized fallback font with script type
    application.FallbackFonts.Add(ScriptType.Chinese, "SimSun");                              
           
    XlsIORenderer renderer = new XlsIORenderer();            
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);               
    Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
    pdfDocument.Save(stream);                       

    //Close and Dispose             
    workbook.Close();
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
    IWorksheet sheet = workbook.Worksheets[0];

    //Convert the sheet to PDF
    ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

    //Initialize fallback font
    application.FallbackFonts.InitializeDefault();
    //Add customized fallback font with script type
    application.FallbackFonts.Add(ScriptType.Chinese, "SimSun");

    PdfDocument pdfDocument = new PdfDocument();
    pdfDocument = converter.Convert();
    pdfDocument.Save("ExcelToPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
    Dim sheet As IWorksheet = workbook.Worksheets(0)
    Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(sheet)
    application.FallbackFonts.InitializeDefault()
    application.FallbackFonts.Add(ScriptType.Chinese, "SimSun")
    Dim pdfDocument As PdfDocument = New PdfDocument()
    pdfDocument = converter.Convert()
    pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}
{% endtabs %}

## Supported elements

This feature supports the following elements:

* Styles
* Rich-text formatting
* Headers and footers
* Images
* Picture recolor
	* Black and white
	* Color change
	* DuoTone
	* Gray scale
* Text boxes
* Hyperlinks
* Document properties
* Table styles
* Text rotations
* Excel page setup options
* Unicode
* Print titles
* Page breaks
* Print area
* Print order
* 2D charts
* 3D charts
* AutoShapes
* Group shapes
* Conditional formats
* Pivot tables
* Comments
* Form controls
	* Check box
	* Combo box
	* Option button
* Linear and Radial Gradient fill
	* Cells
	* Shapes

## Unsupported elements

The following list contains unsupported elements that presently not preserved in the generated PDF document: 

* Sparklines
* Pivot charts
* SmartArt graphics
* Different first page headers
* Different odd and even pages
* Tables
	* Custom styles
* Row and column headings
* ActiveX controls
* OLE objects


N> Explore our [.NET Excel Library](https://www.syncfusion.com/document-processing/excel-framework/net) Feature Tour page and [.Net Excel Framework demo](https://www.syncfusion.com/demos/fileformats/excel-library) that shows how to create and modify Excel files from C# with 5 lines of code on different platforms.
