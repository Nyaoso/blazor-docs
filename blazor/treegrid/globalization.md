---
layout: post
title: Globalization in Blazor TreeGrid Component | Syncfusion
description: Checkout and learn here all about Globalization in Syncfusion Blazor TreeGrid component and much more.
platform: Blazor
control: Tree Grid
documentation: ug
---

# Globalization in Blazor TreeGrid Component

Add **UseRequestLocalization** middle-ware in Configure method in **Startup.cs** file to get browser Culture Info.

Refer the following code to add configuration in Startup.cs file

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Localization;

namespace BlazorApplication
{
    public class Startup
    {
        ....
        ....

        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            app.UseRequestLocalization();
            ....
            ....
        }
    }
}
```

## Localization

The **Localization** library allows to localize default text content of the Tree Grid. The Tree Grid component has static text on some features (like pager information text, context menu options text, etc.) that can be changed to other cultures (Arabic, Deutsch, French, etc.).

### Blazor Server Side

In the following examples, demonstrate how to enable **Localization** for Tree Grid in server side Blazor samples. Here, the Resource file is used to translate the static text of the Tree Grid.

The Resource file is an XML file which contains the strings(key and value pairs) that has to be translated into different language. Refer [Localization](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-3.0) link to know more about how to configure and use localization in the ASP.NET Core application framework.

* Open the **Startup.cs** file and add the below configuration in the **ConfigureServices** function as follows.

```csharp
using Syncfusion.Blazor;
using System.Globalization;
using Microsoft.AspNetCore.Localization;

namespace BlazorApplication
{
    public class Startup
    {
        ....
        ....
        public void ConfigureServices(IServiceCollection services)
        {
            ....
            ....
            services.AddSyncfusionBlazor();
            services.AddLocalization(options => options.ResourcesPath = "Resources");
            services.Configure<RequestLocalizationOptions>(options =>
            {
                // define the list of cultures your app will support
                var supportedCultures = new List<CultureInfo>()
                {
                    new CultureInfo("de")
                };
                // set the default culture
                options.DefaultRequestCulture = new RequestCulture("de");
                options.SupportedCultures = supportedCultures;
                options.SupportedUICultures = supportedCultures;
                options.RequestCultureProviders = new List<IRequestCultureProvider>() {
                 new QueryStringRequestCultureProvider() // Here, You can also use other localization provider
                };
            });
            services.AddSingleton(typeof(ISyncfusionStringLocalizer), typeof(SampleLocalizer));
        }
    }
}
```

> Add [UseRequestLocalization()](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-3.0#localization-middleware) middle-ware in Configure method in **Startup.cs** file to get browser Culture Information.

* Then, write a **class** by inheriting **ISyncfusionStringLocalizer** interface and override the Manager property to get the resource file details from the application end.

```csharp
using Syncfusion.Blazor;

namespace BlazorApplication
{
     public class SampleLocalizer : ISyncfusionStringLocalizer
    {

        public string Get(string key)
        {
            return this.Manager.GetString(key);
        }

        public System.Resources.ResourceManager Manager
        {
            get
            {
                return TreeGridBlazor.Resources.SyncfusionBlazorLocale.ResourceManager;
            }
        }
    }
}
```

* Add **.resx** file to [Resource](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-3.0#resource-files) folder and enter the key value (Locale Keywords) in the **Name** column and the translated string in the **Value** column as follows.

Name |Value (in Deutsch culture)
-----|-----
Grid_Add | Hinzufügen.
Grid_AddFormTitle | Neuen Datensatz hinzufügen.
Grid_AND | UND.
Grid_AutoFit | Diese Spalte automatisch anpassen.
Grid_AutoFitAll | Automatisch alle Spalten anpassen.
Grid_BatchSaveConfirm | Möchten Sie die Änderungen wirklich speichern?.
Grid_BatchSaveLostChanges | Nicht gespeicherte Änderungen gehen verloren. Sind Sie sicher, dass Sie fortfahren wollen?
Grid_Between | Zwischen
Grid_Blanks| Leerzeichen
Grid_Cancel| Stornieren
Grid_CancelButton| Stornieren
Grid_CancelEdit | Möchten Sie die Änderungen wirklich abbrechen?
Grid_ChooseColumns | Spalte auswählen
Grid_ChooseDate | Wählen Sie ein Datum
Grid_ClearButton | klar
Grid_ClearFilter | Filter löschen
Grid_Columnchooser | Säulen
Grid_ConfirmDelete | Möchten Sie den Datensatz wirklich löschen?
Grid_Contains | Enthält
Grid_Copy | Kopieren
Grid_Csvexport | CSV-Export
Grid_CustomFilter | Benutzerdefinierte Filter
Grid_CustomFilterDatePlaceHolder | Wählen Sie ein Datum
Grid_CustomFilterPlaceHolder | Geben Sie den Wert ein
Grid_DateFilter | Datumsfilter
Grid_DateTimeFilter | DateTime-Filter
Grid_Delete | Löschen
Grid_DeleteOperationAlert | Keine Datensätze zum Löschen ausgewählt
Grid_DeleteRecord | Aufzeichnung löschen
Grid_Edit | Bearbeiten
Grid_EditFormTitle | Details von
Grid_EditOperationAlert | Keine Datensätze zum Bearbeiten ausgewählt
Grid_EditRecord | Datensatz bearbeiten
Grid_EmptyDataSourceError | DataSource darf beim ersten Laden nicht leer sein, da Spalten aus dataSource in AutoGenerate Column Grid generiert werden
Grid_EmptyRecord | Keine Datensätze zum Anzeigen
Grid_EndsWith | Endet mit
Grid_EnterValue | Geben Sie den Wert ein
Grid_Equal | Gleich
Grid_Excelexport | Excel-Export
Grid_Export | Export
Grid_False | falsch
Grid_FilterbarTitle | Filterbalkenzelle
Grid_FilterButton | Filter
Grid_FilterFalse | Falsch
Grid_FilterMenu | Filter
Grid_FilterTrue | Wahr
Grid_FirstPage | Erste Seite
Grid_GreaterThan | Größer als
Grid_GreaterThanOrEqual | Größer als oder gleich
Grid_InvalidFilterMessage | Ungültige Filterdaten
Grid_Item | Artikel
Grid_Items | Artikel
Grid_LastPage | Letzte Seite
Grid_LessThan | Weniger als
Grid_LessThanOrEqual | Weniger als oder gleich
Grid_MatchCase | Match-Fall
Grid_Matchs | Keine Treffer gefunden
Grid_NextPage | Nächste Seite
Grid_NoResult | Keine Treffer gefunden
Grid_NotEqual | Nicht gleich
Grid_NumberFilter | Anzahl Filter
Grid_OKButton | in Ordnung
Grid_OR | ODER
Grid_Pdfexport | PDF-Export
Grid_PreviousPage | Vorherige Seite
Grid_Print | Drucken
Grid_Save | speichern
Grid_SaveButton | speichern
Grid_Search | Suche
Grid_SearchColumns | Spalten durchsuchen
Grid_SelectAll | Wählen Sie Alle
Grid_ShowRowsWhere | Zeilen anzeigen, in denen:
Grid_SortAscending | Aufsteigend sortieren
Grid_SortDescending | Absteigend sortieren
Grid_StartsWith | Beginnt mit
Grid_TextFilter | Textfilter
Grid_True | wahr
Grid_Update | Aktualisieren
Grid_Wordexport | Word-Export
Pager_All | Alle
Pager_CurrentPageInfo | {0} von {1} Seiten
Pager_FirstPageTooltip | Gehe zur ersten Seite
Pager_LastPageTooltip | Gehe zur letzten Seite
Pager_NextPagerTooltip | Zum nächsten Pager gehen
Pager_NextPageTooltip | Gehe zur nächsten Seite
Pager_PagerAllDropDown | Artikel
Pager_PagerDropDown | Objekte pro Seite
Pager_PreviousPagerTooltip | Zum vorherigen Pager wechseln
Pager_PreviousPageTooltip |Zurück zur letzten Seite
Pager_TotalItemsInfo |({0} Artikel)

* Finally, Specify the culture for Tree Grid using [locale](https://help.syncfusion.com/cr/blazor/Syncfusion.Blazor~Syncfusion.Blazor.TreeGrid.SfTreeGrid%601~Locale.html) property.

{% tabs %}

{% highlight razor %}

@using TreeGridComponent.Data;
@using Syncfusion.Blazor.TreeGrid;

<SfTreeGrid DataSource="@TreeGridData" AllowPaging="true" Locale="de-DE" IdMapping="TaskId" AllowSelection="true" ParentIdMapping="ParentId" TreeColumnIndex="1"
             Toolbar="@(new List<string>() { "Print", "ExpandAll", "CollapseAll" })">
    <TreeGridPageSettings PageSize="1"></TreeGridPageSettings>
    <TreeGridColumns>
        <TreeGridColumn Field="TaskId" HeaderText="Task ID" Width="80" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="TaskName" HeaderText="Task Name" Width="160"></TreeGridColumn>
        <TreeGridColumn Field="Duration" HeaderText="Duration" Width="100" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="Progress" HeaderText="Progress" Width="100" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="Priority" HeaderText="Priority" Width="80"></TreeGridColumn>
    </TreeGridColumns>
</SfTreeGrid>

@code{
    [Inject]
    IJSRuntime JsRuntime { get; set; }

    public List<TreeData> TreeGridData { get; set; }

    protected override void OnInitialized()
    {
        this.TreeGridData = TreeData.GetSelfDataSource().ToList();
    }

    protected override void OnAfterRender(bool firstRender)
    {
        if (firstRender)
        {
            this.JsRuntime.Sf().LoadLocaleData("locale.json").SetCulture("de-DE");
        }
    }
}

{% endhighlight %}

{% highlight c# %}

namespace TreeGridComponent.Data {

public class TreeData
    {
       
            public int TaskId { get; set;}
            public string TaskName { get; set;}
            public int? Duration { get; set;}
            public int? Progress { get; set;}
            public string Priority { get; set;}
            public int? ParentId { get; set;}
      
        public static List<TreeData> GetSelfDataSource()
        {
            List<TreeData> BusinessObjectCollection = new List<TreeData>();
            BusinessObjectCollection.Add(new TreeData() { TaskId = 1,TaskName = "Parent Task 1",Duration = 10,Progress = 70,Priority = "Critical",ParentId = null });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 2,TaskName = "Child task 1",Progress = 80,Priority = "Low",ParentId = 1 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 3,TaskName = "Child Task 2",Duration = 5,Progress = 65,Priority = "Critical",ParentId = 2 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 4,TaskName = "Child task 3",Duration = 6,Priority = "High",Progress = 77,ParentId = 2 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 5,TaskName = "Parent Task 2",Duration = 10,Progress = 70,Priority = "Critical",ParentId = null});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 6,TaskName = "Child task 1",Duration = 4,Progress = 80,Priority = "Critical",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 7,TaskName = "Child Task 2",Duration = 5,Progress = 65,Priority = "Low",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 8,TaskName = "Child task 3",Duration = 6,Progress = 77,Priority = "High",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 9,TaskName = "Child task 4",Duration = 6,Progress = 77,Priority = "Low",ParentId = 5});
            return BusinessObjectCollection;
        }
    }
}

{% endhighlight %}

{% endtabs %}

### Blazor WebAssembly

For Blazor WebAssembly, use **JSON** file which contains translated text of the culture.

The following list of properties and its values are used in the Tree Grid.

Locale keywords |Text
-----|-----
EmptyRecord |No records to display.
True |true
False |false
InvalidFilterMessage |Invalid filter data.
GroupDropArea |Drag a column header here to group its column.
UnGroup |Click here to ungroup.
GroupDisable |Grouping is disabled for this column.
FilterbarTitle |\s filter bar cell.
EmptyDataSourceError |DataSource must not be empty at initial load as columns are generated from the dataSource in AutoGenerate Column Tree Grid.
Add | Add
Edit| Edit
Cancel| Cancel
Update| Update
Delete | Delete
Print | Print
Pdfexport | PDF Export
Excelexport | Excel Export
Wordexport | Word Export
Csvexport | CSV Export
Search | Search
Column chooser | Columns
Save | Save
Item | item
Items | items
EditOperationAlert | No records selected for edit operation
DeleteOperationAlert | No records selected for delete operation
SaveButton | Save
OKButton | OK
CancelButton | Cancel
EditFormTitle | Details of
AddFormTitle | Add New Record
BatchSaveConfirm | Are you sure you want to save changes?
BatchSaveLostChanges | Unsaved changes will be lost. Are you sure you want to continue?
ConfirmDelete | Are you sure you want to Delete Record?
CancelEdit | Are you sure you want to Cancel the changes?
ChooseColumns | Choose Column
SearchColumns | Search columns
Matchs | No Matches Found
FilterButton | Filter
ClearButton | Clear
StartsWith | Starts With
EndsWith | Ends With
Contains | Contains
Equal | Equal
NotEqual | Not Equal
LessThan | Less Than
LessThanOrEqual | Less Than Or Equal
GreaterThan | Greater Than
GreaterThanOrEqual | Greater Than Or Equal
ChooseDate | Choose a Date
EnterValue | Enter the value
Copy | Copy
Group | Group by this column
Ungroup | Ungroup by this column
autoFitAll | AutoFit all columns
AutoFit | AutoFit this column
Export | Export
FirstPage | First Page
LastPage | Last Page
PreviousPage | Previous Page
NextPage | Next Page
SortAscending | Sort Ascending
SortDescending | Sort Descending
EditRecord | Edit Record
DeleteRecord | Delete Record
FilterMenu | Filter
SelectAll | Select All
Blanks | Blanks
FilterTrue | True
FilterFalse | False
NoResult | No Matches Found
ClearFilter | Clear Filter
NumberFilter | Number Filters
TextFilter | Text Filters
DateFilter | Date Filters
MatchCase | Match Case
Between | Between
CustomFilter | Custom Filter
CustomFilterPlaceHolder | Enter the value
CustomFilterDatePlaceHolder | Choose a date
AND | AND
OR | OR
ShowRowsWhere | Show rows where
currentPageInfo | {0} of {1} pages
totalItemsInfo | ({0} items)
firstPageTooltip | Go to first page
lastPageTooltip | Go to last page
nextPageTooltip | Go to next page
previousPageTooltip | Go to previous page
nextPagerTooltip | Go to next pager
previousPagerTooltip | Go to previous pager
pagerDropDown | Items per page
pagerAllDropDown | Items
All | All

### Loading translations

The following example demonstrates the Tree Grid in **Deutsch** culture. Here use **LoadLocaleData** method to load the **locale.json** file and **SetCulture** method to set the culture of the Tree Grid.

{% tabs %}

{% highlight razor %}

@using TreeGridComponent.Data;
@using Syncfusion.Blazor.TreeGrid;

<SfTreeGrid DataSource="@TreeGridData" AllowPaging="true" Locale="de-DE" IdMapping="TaskId" AllowSelection="true" ParentIdMapping="ParentId" TreeColumnIndex="1"
             Toolbar="@(new List<string>() { "Print", "ExpandAll", "CollapseAll" })">
    <TreeGridPageSettings PageSize="1"></TreeGridPageSettings>
    <TreeGridColumns>
        <TreeGridColumn Field="TaskId" HeaderText="Task ID" Width="80" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="TaskName" HeaderText="Task Name" Width="160"></TreeGridColumn>
        <TreeGridColumn Field="Duration" HeaderText="Duration" Width="100" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="Progress" HeaderText="Progress" Width="100" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="Priority" HeaderText="Priority" Width="80"></TreeGridColumn>
    </TreeGridColumns>
</SfTreeGrid>

@code{
    [Inject]
    IJSRuntime JsRuntime { get; set; }

    public List<TreeData> TreeGridData { get; set; }

    protected override void OnInitialized()
    {
        this.TreeGridData = TreeData.GetSelfDataSource().ToList();
    }

    protected override void OnAfterRender(bool firstRender)
    {
        if (firstRender)
        {
            this.JsRuntime.Sf().LoadLocaleData("locale.json").SetCulture("de-DE");
        }
    }
}



{% endhighlight %}

{% highlight c# %}

namespace TreeGridComponent.Data {

public class TreeData
    {
       
            public int TaskId { get; set;}
            public string TaskName { get; set;}
            public int? Duration { get; set;}
            public int? Progress { get; set;}
            public string Priority { get; set;}
            public int? ParentId { get; set;}
      
        public static List<TreeData> GetSelfDataSource()
        {
            List<TreeData> BusinessObjectCollection = new List<TreeData>();
            BusinessObjectCollection.Add(new TreeData() { TaskId = 1,TaskName = "Parent Task 1",Duration = 10,Progress = 70,Priority = "Critical",ParentId = null });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 2,TaskName = "Child task 1",Progress = 80,Priority = "Low",ParentId = 1 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 3,TaskName = "Child Task 2",Duration = 5,Progress = 65,Priority = "Critical",ParentId = 2 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 4,TaskName = "Child task 3",Duration = 6,Priority = "High",Progress = 77,ParentId = 2 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 5,TaskName = "Parent Task 2",Duration = 10,Progress = 70,Priority = "Critical",ParentId = null});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 6,TaskName = "Child task 1",Duration = 4,Progress = 80,Priority = "Critical",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 7,TaskName = "Child Task 2",Duration = 5,Progress = 65,Priority = "Low",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 8,TaskName = "Child task 3",Duration = 6,Progress = 77,Priority = "High",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 9,TaskName = "Child task 4",Duration = 6,Progress = 77,Priority = "Low",ParentId = 5});
            return BusinessObjectCollection;
        }
    }
}

{% endhighlight %}

{% highlight json %}

{
    "de-DE": {
            "treegrid": {
                "EmptyRecord": "Keine Aufzeichnungen angezeigt",
                "ExpandAll": "Alle erweitern",
                "CollapseAll": "Alles einklappen",
                "Print": "Drucken",
                "Pdfexport": "PDF-Export",
                "Excelexport": "Excel-Export",
                "Wordexport": "Word-Export",
                "FilterButton": "Filter",
                "ClearButton": "klar",
                "StartsWith": "Beginnt mit",
                "EndsWith": "Endet mit",
                "Contains": "Enthält",
                "Equal": "Gleich",
                "NotEqual": "Nicht gleich",
                "LessThan": "Weniger als",
                "LessThanOrEqual": "Weniger als oder gleich",
                "GreaterThan": "Größer als",
                "GreaterThanOrEqual": "Größer als oder gleich",
                "EnterValue": "Geben Sie den Wert ein",
                "FilterMenu": "Filter"
            },
            "pager": {
                "currentPageInfo": "{0} von {1} Seiten",
                "totalItemsInfo": "({0} Beiträge)",
                "firstPageTooltip": "Zur ersten Seite",
                "lastPageTooltip": "Zur letzten Seite",
                "nextPageTooltip": "Zur nächsten Seite",
                "previousPageTooltip": "Zurück zur letzten Seit",
                "nextPagerTooltip": "Zum nächsten Pager",
                "previousPagerTooltip": "Zum vorherigen Pager"
            },
            "dropdowns": {
                "noRecordsTemplate": "Keine Aufzeichnungen gefunden"
            },
            "datepicker": {
                "placeholder": "Wählen Sie ein Datum",
                "today": "heute"
            }
        }	
    }

{% endhighlight %}

{% endtabs %}


![Localization in Blazor TreeGrid](images/blazor-treegrid-localization.png)

## Internationalization

The **Internationalization** library is used to globalize number, date, and time values in Tree Grid component using format strings in the **Format**. In the below sample we set the culture and currency using the **SetCulture** and **SetCurrencyCode** methods.

{% tabs %}

{% highlight razor %}

@using TreeGridComponent.Data;
@using Microsoft.JSInterop
@using Syncfusion.Blazor.TreeGrid;

<SfTreeGrid DataSource="@TreeGridData" AllowPaging="true" Locale="de-DE" IdMapping="TaskId" AllowSelection="true" ParentIdMapping="ParentId" TreeColumnIndex="1"
             Toolbar="@(new List<string>() { "Print", "ExpandAll", "CollapseAll" })">
    <TreeGridPageSettings PageSize="1"></TreeGridPageSettings>
    <TreeGridColumns>
        <TreeGridColumn Field="TaskId" HeaderText="Task ID" Width="80" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="TaskName" HeaderText="Task Name" Width="160"></TreeGridColumn>
        <TreeGridColumn Field="Duration" HeaderText="Duration" Width="100" Format="C2" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="StartDate" HeaderText=" Start Date" Format="yMd" Type="Syncfusion.Blazor.Grids.ColumnType.Date" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right" Width="100"></TreeGridColumn>
        <TreeGridColumn Field="Priority" HeaderText="Priority" Width="80"></TreeGridColumn>
    </TreeGridColumns>
</SfTreeGrid>

@code{
    [Inject]
    IJSRuntime JsRuntime { get; set; }

    public List<TreeData> TreeGridData { get; set; }

    protected override void OnInitialized()
    {
        this.TreeGridData = TreeData.GetSelfDataSource().ToList();
    }

    protected override void OnAfterRender(bool firstRender)
    {
        if (firstRender)
        {
            this.JsRuntime.Sf().SetCulture("de-DE").SetCurrencyCode("EUR");
        }
    }
}

{% endhighlight %}

{% highlight c# %}

namespace TreeGridComponent.Data {

public class TreeData
    {
       
            public int TaskId { get; set;}
            public string TaskName { get; set;}
            public int? Duration { get; set;}
            public int? Progress { get; set;}
            public string Priority { get; set;}
            public int? ParentId { get; set;}
      
        public static List<TreeData> GetSelfDataSource()
        {
            List<TreeData> TreeDataCollection = new List<TreeData>();
            TreeDataCollection.Add(new TreeData() { TaskId = 1, TaskName = "Parent Task 1", StartDate = new DateTime(2017, 10, 23), Duration = 10, Progress = 70, Priority = "Critical", ParentId = null });
            TreeDataCollection.Add(new TreeData() { TaskId = 2, TaskName = "Child task 1", StartDate = new DateTime(2017, 10, 24), Progress = 80, Priority = "Low", Duration = 50, ParentId = 1 });
            TreeDataCollection.Add(new TreeData() { TaskId = 3, TaskName = "Child Task 2", StartDate = new DateTime(2017, 10, 25), Duration = 5, Progress = 65, Priority = "Critical", ParentId = 2 });
            TreeDataCollection.Add(new TreeData() { TaskId = 4, TaskName = "Child task 3", StartDate = new DateTime(2017, 10, 26), Duration = 6, Priority = "High", Progress = 77, ParentId = 2 });
            TreeDataCollection.Add(new TreeData() { TaskId = 5, TaskName = "Parent Task 2", StartDate = new DateTime(2017, 10, 27), Duration = 10, Progress = 70, Priority = "Critical", ParentId = null });
            TreeDataCollection.Add(new TreeData() { TaskId = 6, TaskName = "Child task 1", StartDate = new DateTime(2017, 10, 28), Duration = 4, Progress = 80, Priority = "Critical", ParentId = 5 });
            TreeDataCollection.Add(new TreeData() { TaskId = 7, TaskName = "Child Task 2", StartDate = new DateTime(2017, 10, 11), Duration = 5, Progress = 65, Priority = "Low", ParentId = 5 });
            TreeDataCollection.Add(new TreeData() { TaskId = 8, TaskName = "Child task 3", StartDate = new DateTime(2017, 10, 14), Duration = 6, Progress = 77, Priority = "High", ParentId = 5 });
            TreeDataCollection.Add(new TreeData() { TaskId = 9, TaskName = "Child task 4", StartDate = new DateTime(2017, 10, 17), Duration = 6, Progress = 77, Priority = "Low", ParentId = 5 });
            return TreeDataCollection;
        }
    }
}

{% endhighlight %}

{% highlight json %}

{
    "de-DE": {
            "treegrid": {
                "EmptyRecord": "Keine Aufzeichnungen angezeigt",
                "ExpandAll": "Alle erweitern",
                "CollapseAll": "Alles einklappen",
                "Print": "Drucken",
                "Pdfexport": "PDF-Export",
                "Excelexport": "Excel-Export",
                "Wordexport": "Word-Export",
                "FilterButton": "Filter",
                "ClearButton": "klar",
                "StartsWith": "Beginnt mit",
                "EndsWith": "Endet mit",
                "Contains": "Enthält",
                "Equal": "Gleich",
                "NotEqual": "Nicht gleich",
                "LessThan": "Weniger als",
                "LessThanOrEqual": "Weniger als oder gleich",
                "GreaterThan": "Größer als",
                "GreaterThanOrEqual": "Größer als oder gleich",
                "EnterValue": "Geben Sie den Wert ein",
                "FilterMenu": "Filter"
            },
            "pager": {
                "currentPageInfo": "{0} von {1} Seiten",
                "totalItemsInfo": "({0} Beiträge)",
                "firstPageTooltip": "Zur ersten Seite",
                "lastPageTooltip": "Zur letzten Seite",
                "nextPageTooltip": "Zur nächsten Seite",
                "previousPageTooltip": "Zurück zur letzten Seit",
                "nextPagerTooltip": "Zum nächsten Pager",
                "previousPagerTooltip": "Zum vorherigen Pager"
            },
            "dropdowns": {
                "noRecordsTemplate": "Keine Aufzeichnungen gefunden"
            },
            "datepicker": {
                "placeholder": "Wählen Sie ein Datum",
                "today": "heute"
            }
        }	
    }
    

{% endhighlight %}

{% highlight json %}

{
  "main": {
    "de": {
      "identity": {
        "version": {
          "_number": "$Revision: 14842 $",
          "_cldrVersion": "35.1"
        },
        "language": "de"
      },
      "numbers": {
        "defaultNumberingSystem": "latn",
        "otherNumberingSystems": {
          "native": "latn"
        },
        "minimumGroupingDigits": "1",
        "symbols-numberSystem-latn": {
          "decimal": ",",
          "group": ".",
          "list": ";",
          "percentSign": "%",
          "plusSign": "+",
          "minusSign": "-",
          "exponential": "E",
          "superscriptingExponent": "·",
          "perMille": "‰",
          "infinity": "∞",
          "nan": "NaN",
          "timeSeparator": ":"
        },
        "decimalFormats-numberSystem-latn": {
          "standard": "#,##0.###",
          "long": {
            "decimalFormat": {
              "1000-count-one": "0 Tausend",
              "1000-count-other": "0 Tausend",
              "10000-count-one": "00 Tausend",
              "10000-count-other": "00 Tausend",
              "100000-count-one": "000 Tausend",
              "100000-count-other": "000 Tausend",
              "1000000-count-one": "0 Million",
              "1000000-count-other": "0 Millionen",
              "10000000-count-one": "00 Millionen",
              "10000000-count-other": "00 Millionen",
              "100000000-count-one": "000 Millionen",
              "100000000-count-other": "000 Millionen",
              "1000000000-count-one": "0 Milliarde",
              "1000000000-count-other": "0 Milliarden",
              "10000000000-count-one": "00 Milliarden",
              "10000000000-count-other": "00 Milliarden",
              "100000000000-count-one": "000 Milliarden",
              "100000000000-count-other": "000 Milliarden",
              "1000000000000-count-one": "0 Billion",
              "1000000000000-count-other": "0 Billionen",
              "10000000000000-count-one": "00 Billionen",
              "10000000000000-count-other": "00 Billionen",
              "100000000000000-count-one": "000 Billionen",
              "100000000000000-count-other": "000 Billionen"
            }
          },
          "short": {
            "decimalFormat": {
              "1000-count-one": "0",
              "1000-count-other": "0",
              "10000-count-one": "0",
              "10000-count-other": "0",
              "100000-count-one": "0",
              "100000-count-other": "0",
              "1000000-count-one": "0 Mio'.'",
              "1000000-count-other": "0 Mio'.'",
              "10000000-count-one": "00 Mio'.'",
              "10000000-count-other": "00 Mio'.'",
              "100000000-count-one": "000 Mio'.'",
              "100000000-count-other": "000 Mio'.'",
              "1000000000-count-one": "0 Mrd'.'",
              "1000000000-count-other": "0 Mrd'.'",
              "10000000000-count-one": "00 Mrd'.'",
              "10000000000-count-other": "00 Mrd'.'",
              "100000000000-count-one": "000 Mrd'.'",
              "100000000000-count-other": "000 Mrd'.'",
              "1000000000000-count-one": "0 Bio'.'",
              "1000000000000-count-other": "0 Bio'.'",
              "10000000000000-count-one": "00 Bio'.'",
              "10000000000000-count-other": "00 Bio'.'",
              "100000000000000-count-one": "000 Bio'.'",
              "100000000000000-count-other": "000 Bio'.'"
            }
          }
        },
        "scientificFormats-numberSystem-latn": {
          "standard": "#E0"
        },
        "percentFormats-numberSystem-latn": {
          "standard": "#,##0 %"
        },
        "currencyFormats-numberSystem-latn": {
          "currencySpacing": {
            "beforeCurrency": {
              "currencyMatch": "[:^S:]",
              "surroundingMatch": "[:digit:]",
              "insertBetween": " "
            },
            "afterCurrency": {
              "currencyMatch": "[:^S:]",
              "surroundingMatch": "[:digit:]",
              "insertBetween": " "
            }
          },
          "standard": "#,##0.00 ¤",
          "accounting": "#,##0.00 ¤",
          "short": {
            "standard": {
              "1000-count-one": "0",
              "1000-count-other": "0",
              "10000-count-one": "0",
              "10000-count-other": "0",
              "100000-count-one": "0",
              "100000-count-other": "0",
              "1000000-count-one": "0 Mio'.' ¤",
              "1000000-count-other": "0 Mio'.' ¤",
              "10000000-count-one": "00 Mio'.' ¤",
              "10000000-count-other": "00 Mio'.' ¤",
              "100000000-count-one": "000 Mio'.' ¤",
              "100000000-count-other": "000 Mio'.' ¤",
              "1000000000-count-one": "0 Mrd'.' ¤",
              "1000000000-count-other": "0 Mrd'.' ¤",
              "10000000000-count-one": "00 Mrd'.' ¤",
              "10000000000-count-other": "00 Mrd'.' ¤",
              "100000000000-count-one": "000 Mrd'.' ¤",
              "100000000000-count-other": "000 Mrd'.' ¤",
              "1000000000000-count-one": "0 Bio'.' ¤",
              "1000000000000-count-other": "0 Bio'.' ¤",
              "10000000000000-count-one": "00 Bio'.' ¤",
              "10000000000000-count-other": "00 Bio'.' ¤",
              "100000000000000-count-one": "000 Bio'.' ¤",
              "100000000000000-count-other": "000 Bio'.' ¤"
            }
          },
          "unitPattern-count-one": "{0} {1}",
          "unitPattern-count-other": "{0} {1}"
        },
        "miscPatterns-numberSystem-latn": {
          "approximately": "≈{0}",
          "atLeast": "{0}+",
          "atMost": "≤{0}",
          "range": "{0}–{1}"
        },
        "minimalPairs": {
          "pluralMinimalPairs-count-one": "{0} Tag",
          "pluralMinimalPairs-count-other": "{0} Tage",
          "other": "{0}. Abzweigung nach rechts nehmen"
        }
      }
    }
  }
}


{% endhighlight %}

{% highlight json %}

{
  "main": {
    "de": {
      "identity": {
        "version": {
          "_number": "$Revision: 14842 $",
          "_cldrVersion": "35.1"
        },
        "language": "de"
      },
      "numbers": {
        "currencies": {
          "ADP": {
            "displayName": "Andorranische Pesete",
            "displayName-count-one": "Andorranische Pesete",
            "displayName-count-other": "Andorranische Peseten",
            "symbol": "ADP"
          },
          "AED": {
            "displayName": "VAE-Dirham",
            "displayName-count-one": "VAE-Dirham",
            "displayName-count-other": "VAE-Dirham",
            "symbol": "AED"
          },
          "AFA": {
            "displayName": "Afghanische Afghani (1927–2002)",
            "displayName-count-one": "Afghanische Afghani (1927–2002)",
            "displayName-count-other": "Afghanische Afghani (1927–2002)",
            "symbol": "AFA"
          },
          "AFN": {
            "displayName": "Afghanischer Afghani",
            "displayName-count-one": "Afghanischer Afghani",
            "displayName-count-other": "Afghanische Afghani",
            "symbol": "AFN"
          },
          "ALK": {
            "displayName": "Albanischer Lek (1946–1965)",
            "displayName-count-one": "Albanischer Lek (1946–1965)",
            "displayName-count-other": "Albanische Lek (1946–1965)",
            "symbol": "ALK"
          },
          "ALL": {
            "displayName": "Albanischer Lek",
            "displayName-count-one": "Albanischer Lek",
            "displayName-count-other": "Albanische Lek",
            "symbol": "ALL"
          },
          "AMD": {
            "displayName": "Armenischer Dram",
            "displayName-count-one": "Armenischer Dram",
            "displayName-count-other": "Armenische Dram",
            "symbol": "AMD"
          },
          "ANG": {
            "displayName": "Niederländische-Antillen-Gulden",
            "displayName-count-one": "Niederländische-Antillen-Gulden",
            "displayName-count-other": "Niederländische-Antillen-Gulden",
            "symbol": "ANG"
          },
          "AOA": {
            "displayName": "Angolanischer Kwanza",
            "displayName-count-one": "Angolanischer Kwanza",
            "displayName-count-other": "Angolanische Kwanza",
            "symbol": "AOA",
            "symbol-alt-narrow": "Kz"
          },
          "AOK": {
            "displayName": "Angolanischer Kwanza (1977–1990)",
            "displayName-count-one": "Angolanischer Kwanza (1977–1990)",
            "displayName-count-other": "Angolanische Kwanza (1977–1990)",
            "symbol": "AOK"
          },
          "AON": {
            "displayName": "Angolanischer Neuer Kwanza (1990–2000)",
            "displayName-count-one": "Angolanischer Neuer Kwanza (1990–2000)",
            "displayName-count-other": "Angolanische Neue Kwanza (1990–2000)",
            "symbol": "AON"
          },
          "AOR": {
            "displayName": "Angolanischer Kwanza Reajustado (1995–1999)",
            "displayName-count-one": "Angolanischer Kwanza Reajustado (1995–1999)",
            "displayName-count-other": "Angolanische Kwanza Reajustado (1995–1999)",
            "symbol": "AOR"
          },
          "ARA": {
            "displayName": "Argentinischer Austral",
            "displayName-count-one": "Argentinischer Austral",
            "displayName-count-other": "Argentinische Austral",
            "symbol": "ARA"
          },
          "ARL": {
            "displayName": "Argentinischer Peso Ley (1970–1983)",
            "displayName-count-one": "Argentinischer Peso Ley (1970–1983)",
            "displayName-count-other": "Argentinische Pesos Ley (1970–1983)",
            "symbol": "ARL"
          },
          "ARM": {
            "displayName": "Argentinischer Peso (1881–1970)",
            "displayName-count-one": "Argentinischer Peso (1881–1970)",
            "displayName-count-other": "Argentinische Pesos (1881–1970)",
            "symbol": "ARM"
          },
          "ARP": {
            "displayName": "Argentinischer Peso (1983–1985)",
            "displayName-count-one": "Argentinischer Peso (1983–1985)",
            "displayName-count-other": "Argentinische Peso (1983–1985)",
            "symbol": "ARP"
          },
          "ARS": {
            "displayName": "Argentinischer Peso",
            "displayName-count-one": "Argentinischer Peso",
            "displayName-count-other": "Argentinische Pesos",
            "symbol": "ARS",
            "symbol-alt-narrow": "$"
          },
          "ATS": {
            "displayName": "Österreichischer Schilling",
            "displayName-count-one": "Österreichischer Schilling",
            "displayName-count-other": "Österreichische Schilling",
            "symbol": "öS"
          },
          "AUD": {
            "displayName": "Australischer Dollar",
            "displayName-count-one": "Australischer Dollar",
            "displayName-count-other": "Australische Dollar",
            "symbol": "AU$",
            "symbol-alt-narrow": "$"
          },
          "AWG": {
            "displayName": "Aruba-Florin",
            "displayName-count-one": "Aruba-Florin",
            "displayName-count-other": "Aruba-Florin",
            "symbol": "AWG"
          },
          "AZM": {
            "displayName": "Aserbaidschan-Manat (1993–2006)",
            "displayName-count-one": "Aserbaidschan-Manat (1993–2006)",
            "displayName-count-other": "Aserbaidschan-Manat (1993–2006)",
            "symbol": "AZM"
          },
          "AZN": {
            "displayName": "Aserbaidschan-Manat",
            "displayName-count-one": "Aserbaidschan-Manat",
            "displayName-count-other": "Aserbaidschan-Manat",
            "symbol": "AZN"
          },
          "BAD": {
            "displayName": "Bosnien und Herzegowina Dinar (1992–1994)",
            "displayName-count-one": "Bosnien und Herzegowina Dinar (1992–1994)",
            "displayName-count-other": "Bosnien und Herzegowina Dinar (1992–1994)",
            "symbol": "BAD"
          },
          "BAM": {
            "displayName": "Bosnien und Herzegowina Konvertierbare Mark",
            "displayName-count-one": "Bosnien und Herzegowina Konvertierbare Mark",
            "displayName-count-other": "Bosnien und Herzegowina Konvertierbare Mark",
            "symbol": "BAM",
            "symbol-alt-narrow": "KM"
          },
          "BAN": {
            "displayName": "Bosnien und Herzegowina Neuer Dinar (1994–1997)",
            "displayName-count-one": "Bosnien und Herzegowina Neuer Dinar (1994–1997)",
            "displayName-count-other": "Bosnien und Herzegowina Neue Dinar (1994–1997)",
            "symbol": "BAN"
          },
          "BBD": {
            "displayName": "Barbados-Dollar",
            "displayName-count-one": "Barbados-Dollar",
            "displayName-count-other": "Barbados-Dollar",
            "symbol": "BBD",
            "symbol-alt-narrow": "$"
          },
          "BDT": {
            "displayName": "Bangladesch-Taka",
            "displayName-count-one": "Bangladesch-Taka",
            "displayName-count-other": "Bangladesch-Taka",
            "symbol": "BDT",
            "symbol-alt-narrow": "৳"
          },
          "BEC": {
            "displayName": "Belgischer Franc (konvertibel)",
            "displayName-count-one": "Belgischer Franc (konvertibel)",
            "displayName-count-other": "Belgische Franc (konvertibel)",
            "symbol": "BEC"
          },
          "BEF": {
            "displayName": "Belgischer Franc",
            "displayName-count-one": "Belgischer Franc",
            "displayName-count-other": "Belgische Franc",
            "symbol": "BEF"
          },
          "BEL": {
            "displayName": "Belgischer Finanz-Franc",
            "displayName-count-one": "Belgischer Finanz-Franc",
            "displayName-count-other": "Belgische Finanz-Franc",
            "symbol": "BEL"
          },
          "BGL": {
            "displayName": "Bulgarische Lew (1962–1999)",
            "displayName-count-one": "Bulgarische Lew (1962–1999)",
            "displayName-count-other": "Bulgarische Lew (1962–1999)",
            "symbol": "BGL"
          },
          "BGM": {
            "displayName": "Bulgarischer Lew (1952–1962)",
            "displayName-count-one": "Bulgarischer Lew (1952–1962)",
            "displayName-count-other": "Bulgarische Lew (1952–1962)",
            "symbol": "BGK"
          },
          "BGN": {
            "displayName": "Bulgarischer Lew",
            "displayName-count-one": "Bulgarischer Lew",
            "displayName-count-other": "Bulgarische Lew",
            "symbol": "BGN"
          },
          "BGO": {
            "displayName": "Bulgarischer Lew (1879–1952)",
            "displayName-count-one": "Bulgarischer Lew (1879–1952)",
            "displayName-count-other": "Bulgarische Lew (1879–1952)",
            "symbol": "BGJ"
          },
          "BHD": {
            "displayName": "Bahrain-Dinar",
            "displayName-count-one": "Bahrain-Dinar",
            "displayName-count-other": "Bahrain-Dinar",
            "symbol": "BHD"
          },
          "BIF": {
            "displayName": "Burundi-Franc",
            "displayName-count-one": "Burundi-Franc",
            "displayName-count-other": "Burundi-Francs",
            "symbol": "BIF"
          },
          "BMD": {
            "displayName": "Bermuda-Dollar",
            "displayName-count-one": "Bermuda-Dollar",
            "displayName-count-other": "Bermuda-Dollar",
            "symbol": "BMD",
            "symbol-alt-narrow": "$"
          },
          "BND": {
            "displayName": "Brunei-Dollar",
            "displayName-count-one": "Brunei-Dollar",
            "displayName-count-other": "Brunei-Dollar",
            "symbol": "BND",
            "symbol-alt-narrow": "$"
          },
          "BOB": {
            "displayName": "Bolivianischer Boliviano",
            "displayName-count-one": "Bolivianischer Boliviano",
            "displayName-count-other": "Bolivianische Bolivianos",
            "symbol": "BOB",
            "symbol-alt-narrow": "Bs"
          },
          "BOL": {
            "displayName": "Bolivianischer Boliviano (1863–1963)",
            "displayName-count-one": "Bolivianischer Boliviano (1863–1963)",
            "displayName-count-other": "Bolivianische Bolivianos (1863–1963)",
            "symbol": "BOL"
          },
          "BOP": {
            "displayName": "Bolivianischer Peso",
            "displayName-count-one": "Bolivianischer Peso",
            "displayName-count-other": "Bolivianische Peso",
            "symbol": "BOP"
          },
          "BOV": {
            "displayName": "Boliviansiche Mvdol",
            "displayName-count-one": "Boliviansiche Mvdol",
            "displayName-count-other": "Bolivianische Mvdol",
            "symbol": "BOV"
          },
          "BRB": {
            "displayName": "Brasilianischer Cruzeiro Novo (1967–1986)",
            "displayName-count-one": "Brasilianischer Cruzeiro Novo (1967–1986)",
            "displayName-count-other": "Brasilianische Cruzeiro Novo (1967–1986)",
            "symbol": "BRB"
          },
          "BRC": {
            "displayName": "Brasilianischer Cruzado (1986–1989)",
            "displayName-count-one": "Brasilianischer Cruzado (1986–1989)",
            "displayName-count-other": "Brasilianische Cruzado (1986–1989)",
            "symbol": "BRC"
          },
          "BRE": {
            "displayName": "Brasilianischer Cruzeiro (1990–1993)",
            "displayName-count-one": "Brasilianischer Cruzeiro (1990–1993)",
            "displayName-count-other": "Brasilianische Cruzeiro (1990–1993)",
            "symbol": "BRE"
          },
          "BRL": {
            "displayName": "Brasilianischer Real",
            "displayName-count-one": "Brasilianischer Real",
            "displayName-count-other": "Brasilianische Real",
            "symbol": "R$",
            "symbol-alt-narrow": "R$"
          },
          "BRN": {
            "displayName": "Brasilianischer Cruzado Novo (1989–1990)",
            "displayName-count-one": "Brasilianischer Cruzado Novo (1989–1990)",
            "displayName-count-other": "Brasilianische Cruzado Novo (1989–1990)",
            "symbol": "BRN"
          },
          "BRR": {
            "displayName": "Brasilianischer Cruzeiro (1993–1994)",
            "displayName-count-one": "Brasilianischer Cruzeiro (1993–1994)",
            "displayName-count-other": "Brasilianische Cruzeiro (1993–1994)",
            "symbol": "BRR"
          },
          "BRZ": {
            "displayName": "Brasilianischer Cruzeiro (1942–1967)",
            "displayName-count-one": "Brasilianischer Cruzeiro (1942–1967)",
            "displayName-count-other": "Brasilianischer Cruzeiro (1942–1967)",
            "symbol": "BRZ"
          },
          "BSD": {
            "displayName": "Bahamas-Dollar",
            "displayName-count-one": "Bahamas-Dollar",
            "displayName-count-other": "Bahamas-Dollar",
            "symbol": "BSD",
            "symbol-alt-narrow": "$"
          },
          "BTN": {
            "displayName": "Bhutan-Ngultrum",
            "displayName-count-one": "Bhutan-Ngultrum",
            "displayName-count-other": "Bhutan-Ngultrum",
            "symbol": "BTN"
          },
          "BUK": {
            "displayName": "Birmanischer Kyat",
            "displayName-count-one": "Birmanischer Kyat",
            "displayName-count-other": "Birmanische Kyat",
            "symbol": "BUK"
          },
          "BWP": {
            "displayName": "Botswanischer Pula",
            "displayName-count-one": "Botswanischer Pula",
            "displayName-count-other": "Botswanische Pula",
            "symbol": "BWP",
            "symbol-alt-narrow": "P"
          },
          "BYB": {
            "displayName": "Belarus-Rubel (1994–1999)",
            "displayName-count-one": "Belarus-Rubel (1994–1999)",
            "displayName-count-other": "Belarus-Rubel (1994–1999)",
            "symbol": "BYB"
          },
          "BYN": {
            "displayName": "Weißrussischer Rubel",
            "displayName-count-one": "Weißrussischer Rubel",
            "displayName-count-other": "Weißrussische Rubel",
            "symbol": "BYN",
            "symbol-alt-narrow": "р."
          },
          "BYR": {
            "displayName": "Weißrussischer Rubel (2000–2016)",
            "displayName-count-one": "Weißrussischer Rubel (2000–2016)",
            "displayName-count-other": "Weißrussische Rubel (2000–2016)",
            "symbol": "BYR"
          },
          "BZD": {
            "displayName": "Belize-Dollar",
            "displayName-count-one": "Belize-Dollar",
            "displayName-count-other": "Belize-Dollar",
            "symbol": "BZD",
            "symbol-alt-narrow": "$"
          },
          "CAD": {
            "displayName": "Kanadischer Dollar",
            "displayName-count-one": "Kanadischer Dollar",
            "displayName-count-other": "Kanadische Dollar",
            "symbol": "CA$",
            "symbol-alt-narrow": "$"
          },
          "CDF": {
            "displayName": "Kongo-Franc",
            "displayName-count-one": "Kongo-Franc",
            "displayName-count-other": "Kongo-Francs",
            "symbol": "CDF"
          },
          "CHE": {
            "displayName": "WIR-Euro",
            "displayName-count-one": "WIR-Euro",
            "displayName-count-other": "WIR-Euro",
            "symbol": "CHE"
          },
          "CHF": {
            "displayName": "Schweizer Franken",
            "displayName-count-one": "Schweizer Franken",
            "displayName-count-other": "Schweizer Franken",
            "symbol": "CHF"
          },
          "CHW": {
            "displayName": "WIR Franken",
            "displayName-count-one": "WIR Franken",
            "displayName-count-other": "WIR Franken",
            "symbol": "CHW"
          },
          "CLE": {
            "displayName": "Chilenischer Escudo",
            "displayName-count-one": "Chilenischer Escudo",
            "displayName-count-other": "Chilenische Escudo",
            "symbol": "CLE"
          },
          "CLF": {
            "displayName": "Chilenische Unidades de Fomento",
            "displayName-count-one": "Chilenische Unidades de Fomento",
            "displayName-count-other": "Chilenische Unidades de Fomento",
            "symbol": "CLF"
          },
          "CLP": {
            "displayName": "Chilenischer Peso",
            "displayName-count-one": "Chilenischer Peso",
            "displayName-count-other": "Chilenische Pesos",
            "symbol": "CLP",
            "symbol-alt-narrow": "$"
          },
          "CNH": {
            "displayName": "Renminbi Yuan (Off–Shore)",
            "displayName-count-one": "Renminbi Yuan (Off–Shore)",
            "displayName-count-other": "Renminbi Yuan (Off–Shore)",
            "symbol": "CNH"
          },
          "CNX": {
            "displayName": "Dollar der Chinesischen Volksbank",
            "displayName-count-one": "Dollar der Chinesischen Volksbank",
            "displayName-count-other": "Dollar der Chinesischen Volksbank",
            "symbol": "CNX"
          },
          "CNY": {
            "displayName": "Renminbi Yuan",
            "displayName-count-one": "Chinesischer Yuan",
            "displayName-count-other": "Renminbi Yuan",
            "symbol": "CN¥",
            "symbol-alt-narrow": "¥"
          },
          "COP": {
            "displayName": "Kolumbianischer Peso",
            "displayName-count-one": "Kolumbianischer Peso",
            "displayName-count-other": "Kolumbianische Pesos",
            "symbol": "COP",
            "symbol-alt-narrow": "$"
          },
          "COU": {
            "displayName": "Kolumbianische Unidades de valor real",
            "displayName-count-one": "Kolumbianische Unidad de valor real",
            "displayName-count-other": "Kolumbianische Unidades de valor real",
            "symbol": "COU"
          },
          "CRC": {
            "displayName": "Costa-Rica-Colón",
            "displayName-count-one": "Costa-Rica-Colón",
            "displayName-count-other": "Costa-Rica-Colón",
            "symbol": "CRC",
            "symbol-alt-narrow": "₡"
          },
          "CSD": {
            "displayName": "Serbischer Dinar (2002–2006)",
            "displayName-count-one": "Serbischer Dinar (2002–2006)",
            "displayName-count-other": "Serbische Dinar (2002–2006)",
            "symbol": "CSD"
          },
          "CSK": {
            "displayName": "Tschechoslowakische Krone",
            "displayName-count-one": "Tschechoslowakische Kronen",
            "displayName-count-other": "Tschechoslowakische Kronen",
            "symbol": "CSK"
          },
          "CUC": {
            "displayName": "Kubanischer Peso (konvertibel)",
            "displayName-count-one": "Kubanischer Peso (konvertibel)",
            "displayName-count-other": "Kubanische Pesos (konvertibel)",
            "symbol": "CUC",
            "symbol-alt-narrow": "Cub$"
          },
          "CUP": {
            "displayName": "Kubanischer Peso",
            "displayName-count-one": "Kubanischer Peso",
            "displayName-count-other": "Kubanische Pesos",
            "symbol": "CUP",
            "symbol-alt-narrow": "$"
          },
          "CVE": {
            "displayName": "Cabo-Verde-Escudo",
            "displayName-count-one": "Cabo-Verde-Escudo",
            "displayName-count-other": "Cabo-Verde-Escudos",
            "symbol": "CVE"
          },
          "CYP": {
            "displayName": "Zypern-Pfund",
            "displayName-count-one": "Zypern Pfund",
            "displayName-count-other": "Zypern Pfund",
            "symbol": "CYP"
          },
          "CZK": {
            "displayName": "Tschechische Krone",
            "displayName-count-one": "Tschechische Krone",
            "displayName-count-other": "Tschechische Kronen",
            "symbol": "CZK",
            "symbol-alt-narrow": "Kč"
          },
          "DDM": {
            "displayName": "Mark der DDR",
            "displayName-count-one": "Mark der DDR",
            "displayName-count-other": "Mark der DDR",
            "symbol": "DDM"
          },
          "DEM": {
            "displayName": "Deutsche Mark",
            "displayName-count-one": "Deutsche Mark",
            "displayName-count-other": "Deutsche Mark",
            "symbol": "DM"
          },
          "DJF": {
            "displayName": "Dschibuti-Franc",
            "displayName-count-one": "Dschibuti-Franc",
            "displayName-count-other": "Dschibuti-Franc",
            "symbol": "DJF"
          },
          "DKK": {
            "displayName": "Dänische Krone",
            "displayName-count-one": "Dänische Krone",
            "displayName-count-other": "Dänische Kronen",
            "symbol": "DKK",
            "symbol-alt-narrow": "kr"
          },
          "DOP": {
            "displayName": "Dominikanischer Peso",
            "displayName-count-one": "Dominikanischer Peso",
            "displayName-count-other": "Dominikanische Pesos",
            "symbol": "DOP",
            "symbol-alt-narrow": "$"
          },
          "DZD": {
            "displayName": "Algerischer Dinar",
            "displayName-count-one": "Algerischer Dinar",
            "displayName-count-other": "Algerische Dinar",
            "symbol": "DZD"
          },
          "ECS": {
            "displayName": "Ecuadorianischer Sucre",
            "displayName-count-one": "Ecuadorianischer Sucre",
            "displayName-count-other": "Ecuadorianische Sucre",
            "symbol": "ECS"
          },
          "ECV": {
            "displayName": "Verrechnungseinheit für Ecuador",
            "displayName-count-one": "Verrechnungseinheiten für Ecuador",
            "displayName-count-other": "Verrechnungseinheiten für Ecuador",
            "symbol": "ECV"
          },
          "EEK": {
            "displayName": "Estnische Krone",
            "displayName-count-one": "Estnische Krone",
            "displayName-count-other": "Estnische Kronen",
            "symbol": "EEK"
          },
          "EGP": {
            "displayName": "Ägyptisches Pfund",
            "displayName-count-one": "Ägyptisches Pfund",
            "displayName-count-other": "Ägyptische Pfund",
            "symbol": "EGP",
            "symbol-alt-narrow": "E£"
          },
          "ERN": {
            "displayName": "Eritreischer Nakfa",
            "displayName-count-one": "Eritreischer Nakfa",
            "displayName-count-other": "Eritreische Nakfa",
            "symbol": "ERN"
          },
          "ESA": {
            "displayName": "Spanische Peseta (A–Konten)",
            "displayName-count-one": "Spanische Peseta (A–Konten)",
            "displayName-count-other": "Spanische Peseten (A–Konten)",
            "symbol": "ESA"
          },
          "ESB": {
            "displayName": "Spanische Peseta (konvertibel)",
            "displayName-count-one": "Spanische Peseta (konvertibel)",
            "displayName-count-other": "Spanische Peseten (konvertibel)",
            "symbol": "ESB"
          },
          "ESP": {
            "displayName": "Spanische Peseta",
            "displayName-count-one": "Spanische Peseta",
            "displayName-count-other": "Spanische Peseten",
            "symbol": "ESP",
            "symbol-alt-narrow": "₧"
          },
          "ETB": {
            "displayName": "Äthiopischer Birr",
            "displayName-count-one": "Äthiopischer Birr",
            "displayName-count-other": "Äthiopische Birr",
            "symbol": "ETB"
          },
          "EUR": {
            "displayName": "Euro",
            "displayName-count-one": "Euro",
            "displayName-count-other": "Euro",
            "symbol": "€",
            "symbol-alt-narrow": "€"
          },
          "FIM": {
            "displayName": "Finnische Mark",
            "displayName-count-one": "Finnische Mark",
            "displayName-count-other": "Finnische Mark",
            "symbol": "FIM"
          },
          "FJD": {
            "displayName": "Fidschi-Dollar",
            "displayName-count-one": "Fidschi-Dollar",
            "displayName-count-other": "Fidschi-Dollar",
            "symbol": "FJD",
            "symbol-alt-narrow": "$"
          },
          "FKP": {
            "displayName": "Falkland-Pfund",
            "displayName-count-one": "Falkland-Pfund",
            "displayName-count-other": "Falkland-Pfund",
            "symbol": "FKP",
            "symbol-alt-narrow": "Fl£"
          },
          "FRF": {
            "displayName": "Französischer Franc",
            "displayName-count-one": "Französischer Franc",
            "displayName-count-other": "Französische Franc",
            "symbol": "FRF"
          },
          "GBP": {
            "displayName": "Britisches Pfund",
            "displayName-count-one": "Britisches Pfund",
            "displayName-count-other": "Britische Pfund",
            "symbol": "£",
            "symbol-alt-narrow": "£"
          },
          "GEK": {
            "displayName": "Georgischer Kupon Larit",
            "displayName-count-one": "Georgischer Kupon Larit",
            "displayName-count-other": "Georgische Kupon Larit",
            "symbol": "GEK"
          },
          "GEL": {
            "displayName": "Georgischer Lari",
            "displayName-count-one": "Georgischer Lari",
            "displayName-count-other": "Georgische Lari",
            "symbol": "GEL",
            "symbol-alt-narrow": "₾",
            "symbol-alt-variant": "₾"
          },
          "GHC": {
            "displayName": "Ghanaischer Cedi (1979–2007)",
            "displayName-count-one": "Ghanaischer Cedi (1979–2007)",
            "displayName-count-other": "Ghanaische Cedi (1979–2007)",
            "symbol": "GHC"
          },
          "GHS": {
            "displayName": "Ghanaischer Cedi",
            "displayName-count-one": "Ghanaischer Cedi",
            "displayName-count-other": "Ghanaische Cedi",
            "symbol": "GHS"
          },
          "GIP": {
            "displayName": "Gibraltar-Pfund",
            "displayName-count-one": "Gibraltar-Pfund",
            "displayName-count-other": "Gibraltar-Pfund",
            "symbol": "GIP",
            "symbol-alt-narrow": "£"
          },
          "GMD": {
            "displayName": "Gambia-Dalasi",
            "displayName-count-one": "Gambia-Dalasi",
            "displayName-count-other": "Gambia-Dalasi",
            "symbol": "GMD"
          },
          "GNF": {
            "displayName": "Guinea-Franc",
            "displayName-count-one": "Guinea-Franc",
            "displayName-count-other": "Guinea-Franc",
            "symbol": "GNF",
            "symbol-alt-narrow": "F.G."
          },
          "GNS": {
            "displayName": "Guineischer Syli",
            "displayName-count-one": "Guineischer Syli",
            "displayName-count-other": "Guineische Syli",
            "symbol": "GNS"
          },
          "GQE": {
            "displayName": "Äquatorialguinea-Ekwele",
            "displayName-count-one": "Äquatorialguinea-Ekwele",
            "displayName-count-other": "Äquatorialguinea-Ekwele",
            "symbol": "GQE"
          },
          "GRD": {
            "displayName": "Griechische Drachme",
            "displayName-count-one": "Griechische Drachme",
            "displayName-count-other": "Griechische Drachmen",
            "symbol": "GRD"
          },
          "GTQ": {
            "displayName": "Guatemaltekischer Quetzal",
            "displayName-count-one": "Guatemaltekischer Quetzal",
            "displayName-count-other": "Guatemaltekische Quetzales",
            "symbol": "GTQ",
            "symbol-alt-narrow": "Q"
          },
          "GWE": {
            "displayName": "Portugiesisch Guinea Escudo",
            "displayName-count-one": "Portugiesisch Guinea Escudo",
            "displayName-count-other": "Portugiesisch Guinea Escudo",
            "symbol": "GWE"
          },
          "GWP": {
            "displayName": "Guinea-Bissau Peso",
            "displayName-count-one": "Guinea-Bissau Peso",
            "displayName-count-other": "Guinea-Bissau Pesos",
            "symbol": "GWP"
          },
          "GYD": {
            "displayName": "Guyana-Dollar",
            "displayName-count-one": "Guyana-Dollar",
            "displayName-count-other": "Guyana-Dollar",
            "symbol": "GYD",
            "symbol-alt-narrow": "$"
          },
          "HKD": {
            "displayName": "Hongkong-Dollar",
            "displayName-count-one": "Hongkong-Dollar",
            "displayName-count-other": "Hongkong-Dollar",
            "symbol": "HK$",
            "symbol-alt-narrow": "$"
          },
          "HNL": {
            "displayName": "Honduras-Lempira",
            "displayName-count-one": "Honduras-Lempira",
            "displayName-count-other": "Honduras-Lempira",
            "symbol": "HNL",
            "symbol-alt-narrow": "L"
          },
          "HRD": {
            "displayName": "Kroatischer Dinar",
            "displayName-count-one": "Kroatischer Dinar",
            "displayName-count-other": "Kroatische Dinar",
            "symbol": "HRD"
          },
          "HRK": {
            "displayName": "Kroatischer Kuna",
            "displayName-count-one": "Kroatischer Kuna",
            "displayName-count-other": "Kroatische Kuna",
            "symbol": "HRK",
            "symbol-alt-narrow": "kn"
          },
          "HTG": {
            "displayName": "Haitianische Gourde",
            "displayName-count-one": "Haitianische Gourde",
            "displayName-count-other": "Haitianische Gourdes",
            "symbol": "HTG"
          },
          "HUF": {
            "displayName": "Ungarischer Forint",
            "displayName-count-one": "Ungarischer Forint",
            "displayName-count-other": "Ungarische Forint",
            "symbol": "HUF",
            "symbol-alt-narrow": "Ft"
          },
          "IDR": {
            "displayName": "Indonesische Rupiah",
            "displayName-count-one": "Indonesische Rupiah",
            "displayName-count-other": "Indonesische Rupiah",
            "symbol": "IDR",
            "symbol-alt-narrow": "Rp"
          },
          "IEP": {
            "displayName": "Irisches Pfund",
            "displayName-count-one": "Irisches Pfund",
            "displayName-count-other": "Irische Pfund",
            "symbol": "IEP"
          },
          "ILP": {
            "displayName": "Israelisches Pfund",
            "displayName-count-one": "Israelisches Pfund",
            "displayName-count-other": "Israelische Pfund",
            "symbol": "ILP"
          },
          "ILR": {
            "displayName": "Israelischer Schekel (1980–1985)",
            "displayName-count-one": "Israelischer Schekel (1980–1985)",
            "displayName-count-other": "Israelische Schekel (1980–1985)",
            "symbol": "ILR"
          },
          "ILS": {
            "displayName": "Israelischer Neuer Schekel",
            "displayName-count-one": "Israelischer Neuer Schekel",
            "displayName-count-other": "Israelische Neue Schekel",
            "symbol": "₪",
            "symbol-alt-narrow": "₪"
          },
          "INR": {
            "displayName": "Indische Rupie",
            "displayName-count-one": "Indische Rupie",
            "displayName-count-other": "Indische Rupien",
            "symbol": "₹",
            "symbol-alt-narrow": "₹"
          },
          "IQD": {
            "displayName": "Irakischer Dinar",
            "displayName-count-one": "Irakischer Dinar",
            "displayName-count-other": "Irakische Dinar",
            "symbol": "IQD"
          },
          "IRR": {
            "displayName": "Iranischer Rial",
            "displayName-count-one": "Iranischer Rial",
            "displayName-count-other": "Iranische Rial",
            "symbol": "IRR"
          },
          "ISJ": {
            "displayName": "Isländische Krone (1918–1981)",
            "displayName-count-one": "Isländische Krone (1918–1981)",
            "displayName-count-other": "Isländische Kronen (1918–1981)",
            "symbol": "ISJ"
          },
          "ISK": {
            "displayName": "Isländische Krone",
            "displayName-count-one": "Isländische Krone",
            "displayName-count-other": "Isländische Kronen",
            "symbol": "ISK",
            "symbol-alt-narrow": "kr"
          },
          "ITL": {
            "displayName": "Italienische Lira",
            "displayName-count-one": "Italienische Lira",
            "displayName-count-other": "Italienische Lire",
            "symbol": "ITL"
          },
          "JMD": {
            "displayName": "Jamaika-Dollar",
            "displayName-count-one": "Jamaika-Dollar",
            "displayName-count-other": "Jamaika-Dollar",
            "symbol": "JMD",
            "symbol-alt-narrow": "$"
          },
          "JOD": {
            "displayName": "Jordanischer Dinar",
            "displayName-count-one": "Jordanischer Dinar",
            "displayName-count-other": "Jordanische Dinar",
            "symbol": "JOD"
          },
          "JPY": {
            "displayName": "Japanischer Yen",
            "displayName-count-one": "Japanischer Yen",
            "displayName-count-other": "Japanische Yen",
            "symbol": "¥",
            "symbol-alt-narrow": "¥"
          },
          "KES": {
            "displayName": "Kenia-Schilling",
            "displayName-count-one": "Kenia-Schilling",
            "displayName-count-other": "Kenia-Schilling",
            "symbol": "KES"
          },
          "KGS": {
            "displayName": "Kirgisischer Som",
            "displayName-count-one": "Kirgisischer Som",
            "displayName-count-other": "Kirgisische Som",
            "symbol": "KGS"
          },
          "KHR": {
            "displayName": "Kambodschanischer Riel",
            "displayName-count-one": "Kambodschanischer Riel",
            "displayName-count-other": "Kambodschanische Riel",
            "symbol": "KHR",
            "symbol-alt-narrow": "៛"
          },
          "KMF": {
            "displayName": "Komoren-Franc",
            "displayName-count-one": "Komoren-Franc",
            "displayName-count-other": "Komoren-Francs",
            "symbol": "KMF",
            "symbol-alt-narrow": "FC"
          },
          "KPW": {
            "displayName": "Nordkoreanischer Won",
            "displayName-count-one": "Nordkoreanischer Won",
            "displayName-count-other": "Nordkoreanische Won",
            "symbol": "KPW",
            "symbol-alt-narrow": "₩"
          },
          "KRH": {
            "displayName": "Südkoreanischer Hwan (1953–1962)",
            "displayName-count-one": "Südkoreanischer Hwan (1953–1962)",
            "displayName-count-other": "Südkoreanischer Hwan (1953–1962)",
            "symbol": "KRH"
          },
          "KRO": {
            "displayName": "Südkoreanischer Won (1945–1953)",
            "displayName-count-one": "Südkoreanischer Won (1945–1953)",
            "displayName-count-other": "Südkoreanischer Won (1945–1953)",
            "symbol": "KRO"
          },
          "KRW": {
            "displayName": "Südkoreanischer Won",
            "displayName-count-one": "Südkoreanischer Won",
            "displayName-count-other": "Südkoreanische Won",
            "symbol": "₩",
            "symbol-alt-narrow": "₩"
          },
          "KWD": {
            "displayName": "Kuwait-Dinar",
            "displayName-count-one": "Kuwait-Dinar",
            "displayName-count-other": "Kuwait-Dinar",
            "symbol": "KWD"
          },
          "KYD": {
            "displayName": "Kaiman-Dollar",
            "displayName-count-one": "Kaiman-Dollar",
            "displayName-count-other": "Kaiman-Dollar",
            "symbol": "KYD",
            "symbol-alt-narrow": "$"
          },
          "KZT": {
            "displayName": "Kasachischer Tenge",
            "displayName-count-one": "Kasachischer Tenge",
            "displayName-count-other": "Kasachische Tenge",
            "symbol": "KZT",
            "symbol-alt-narrow": "₸"
          },
          "LAK": {
            "displayName": "Laotischer Kip",
            "displayName-count-one": "Laotischer Kip",
            "displayName-count-other": "Laotische Kip",
            "symbol": "LAK",
            "symbol-alt-narrow": "₭"
          },
          "LBP": {
            "displayName": "Libanesisches Pfund",
            "displayName-count-one": "Libanesisches Pfund",
            "displayName-count-other": "Libanesische Pfund",
            "symbol": "LBP",
            "symbol-alt-narrow": "L£"
          },
          "LKR": {
            "displayName": "Sri-Lanka-Rupie",
            "displayName-count-one": "Sri-Lanka-Rupie",
            "displayName-count-other": "Sri-Lanka-Rupien",
            "symbol": "LKR",
            "symbol-alt-narrow": "Rs"
          },
          "LRD": {
            "displayName": "Liberianischer Dollar",
            "displayName-count-one": "Liberianischer Dollar",
            "displayName-count-other": "Liberianische Dollar",
            "symbol": "LRD",
            "symbol-alt-narrow": "$"
          },
          "LSL": {
            "displayName": "Loti",
            "displayName-count-one": "Loti",
            "displayName-count-other": "Loti",
            "symbol": "LSL"
          },
          "LTL": {
            "displayName": "Litauischer Litas",
            "displayName-count-one": "Litauischer Litas",
            "displayName-count-other": "Litauische Litas",
            "symbol": "LTL",
            "symbol-alt-narrow": "Lt"
          },
          "LTT": {
            "displayName": "Litauischer Talonas",
            "displayName-count-one": "Litauische Talonas",
            "displayName-count-other": "Litauische Talonas",
            "symbol": "LTT"
          },
          "LUC": {
            "displayName": "Luxemburgischer Franc (konvertibel)",
            "displayName-count-one": "Luxemburgische Franc (konvertibel)",
            "displayName-count-other": "Luxemburgische Franc (konvertibel)",
            "symbol": "LUC"
          },
          "LUF": {
            "displayName": "Luxemburgischer Franc",
            "displayName-count-one": "Luxemburgische Franc",
            "displayName-count-other": "Luxemburgische Franc",
            "symbol": "LUF"
          },
          "LUL": {
            "displayName": "Luxemburgischer Finanz-Franc",
            "displayName-count-one": "Luxemburgische Finanz-Franc",
            "displayName-count-other": "Luxemburgische Finanz-Franc",
            "symbol": "LUL"
          },
          "LVL": {
            "displayName": "Lettischer Lats",
            "displayName-count-one": "Lettischer Lats",
            "displayName-count-other": "Lettische Lats",
            "symbol": "LVL",
            "symbol-alt-narrow": "Ls"
          },
          "LVR": {
            "displayName": "Lettischer Rubel",
            "displayName-count-one": "Lettische Rubel",
            "displayName-count-other": "Lettische Rubel",
            "symbol": "LVR"
          },
          "LYD": {
            "displayName": "Libyscher Dinar",
            "displayName-count-one": "Libyscher Dinar",
            "displayName-count-other": "Libysche Dinar",
            "symbol": "LYD"
          },
          "MAD": {
            "displayName": "Marokkanischer Dirham",
            "displayName-count-one": "Marokkanischer Dirham",
            "displayName-count-other": "Marokkanische Dirham",
            "symbol": "MAD"
          },
          "MAF": {
            "displayName": "Marokkanischer Franc",
            "displayName-count-one": "Marokkanische Franc",
            "displayName-count-other": "Marokkanische Franc",
            "symbol": "MAF"
          },
          "MCF": {
            "displayName": "Monegassischer Franc",
            "displayName-count-one": "Monegassischer Franc",
            "displayName-count-other": "Monegassische Franc",
            "symbol": "MCF"
          },
          "MDC": {
            "displayName": "Moldau-Cupon",
            "displayName-count-one": "Moldau-Cupon",
            "displayName-count-other": "Moldau-Cupon",
            "symbol": "MDC"
          },
          "MDL": {
            "displayName": "Moldau-Leu",
            "displayName-count-one": "Moldau-Leu",
            "displayName-count-other": "Moldau-Leu",
            "symbol": "MDL"
          },
          "MGA": {
            "displayName": "Madagaskar-Ariary",
            "displayName-count-one": "Madagaskar-Ariary",
            "displayName-count-other": "Madagaskar-Ariary",
            "symbol": "MGA",
            "symbol-alt-narrow": "Ar"
          },
          "MGF": {
            "displayName": "Madagaskar-Franc",
            "displayName-count-one": "Madagaskar-Franc",
            "displayName-count-other": "Madagaskar-Franc",
            "symbol": "MGF"
          },
          "MKD": {
            "displayName": "Mazedonischer Denar",
            "displayName-count-one": "Mazedonischer Denar",
            "displayName-count-other": "Mazedonische Denari",
            "symbol": "MKD"
          },
          "MKN": {
            "displayName": "Mazedonischer Denar (1992–1993)",
            "displayName-count-one": "Mazedonischer Denar (1992–1993)",
            "displayName-count-other": "Mazedonische Denar (1992–1993)",
            "symbol": "MKN"
          },
          "MLF": {
            "displayName": "Malischer Franc",
            "displayName-count-one": "Malische Franc",
            "displayName-count-other": "Malische Franc",
            "symbol": "MLF"
          },
          "MMK": {
            "displayName": "Myanmarischer Kyat",
            "displayName-count-one": "Myanmarischer Kyat",
            "displayName-count-other": "Myanmarische Kyat",
            "symbol": "MMK",
            "symbol-alt-narrow": "K"
          },
          "MNT": {
            "displayName": "Mongolischer Tögrög",
            "displayName-count-one": "Mongolischer Tögrög",
            "displayName-count-other": "Mongolische Tögrög",
            "symbol": "MNT",
            "symbol-alt-narrow": "₮"
          },
          "MOP": {
            "displayName": "Macao-Pataca",
            "displayName-count-one": "Macao-Pataca",
            "displayName-count-other": "Macao-Pataca",
            "symbol": "MOP"
          },
          "MRO": {
            "displayName": "Mauretanischer Ouguiya (1973–2017)",
            "displayName-count-one": "Mauretanischer Ouguiya (1973–2017)",
            "displayName-count-other": "Mauretanische Ouguiya (1973–2017)",
            "symbol": "MRO"
          },
          "MRU": {
            "displayName": "Mauretanischer Ouguiya",
            "displayName-count-one": "Mauretanischer Ouguiya",
            "displayName-count-other": "Mauretanische Ouguiya",
            "symbol": "MRU"
          },
          "MTL": {
            "displayName": "Maltesische Lira",
            "displayName-count-one": "Maltesische Lira",
            "displayName-count-other": "Maltesische Lira",
            "symbol": "MTL"
          },
          "MTP": {
            "displayName": "Maltesisches Pfund",
            "displayName-count-one": "Maltesische Pfund",
            "displayName-count-other": "Maltesische Pfund",
            "symbol": "MTP"
          },
          "MUR": {
            "displayName": "Mauritius-Rupie",
            "displayName-count-one": "Mauritius-Rupie",
            "displayName-count-other": "Mauritius-Rupien",
            "symbol": "MUR",
            "symbol-alt-narrow": "Rs"
          },
          "MVP": {
            "displayName": "Malediven-Rupie (alt)",
            "displayName-count-one": "Malediven-Rupie (alt)",
            "displayName-count-other": "Malediven-Rupien (alt)",
            "symbol": "MVP"
          },
          "MVR": {
            "displayName": "Malediven-Rufiyaa",
            "displayName-count-one": "Malediven-Rufiyaa",
            "displayName-count-other": "Malediven-Rupien",
            "symbol": "MVR"
          },
          "MWK": {
            "displayName": "Malawi-Kwacha",
            "displayName-count-one": "Malawi-Kwacha",
            "displayName-count-other": "Malawi-Kwacha",
            "symbol": "MWK"
          },
          "MXN": {
            "displayName": "Mexikanischer Peso",
            "displayName-count-one": "Mexikanischer Peso",
            "displayName-count-other": "Mexikanische Pesos",
            "symbol": "MX$",
            "symbol-alt-narrow": "$"
          },
          "MXP": {
            "displayName": "Mexikanischer Silber-Peso (1861–1992)",
            "displayName-count-one": "Mexikanische Silber-Peso (1861–1992)",
            "displayName-count-other": "Mexikanische Silber-Pesos (1861–1992)",
            "symbol": "MXP"
          },
          "MXV": {
            "displayName": "Mexicanischer Unidad de Inversion (UDI)",
            "displayName-count-one": "Mexicanischer Unidad de Inversion (UDI)",
            "displayName-count-other": "Mexikanische Unidad de Inversion (UDI)",
            "symbol": "MXV"
          },
          "MYR": {
            "displayName": "Malaysischer Ringgit",
            "displayName-count-one": "Malaysischer Ringgit",
            "displayName-count-other": "Malaysische Ringgit",
            "symbol": "MYR",
            "symbol-alt-narrow": "RM"
          },
          "MZE": {
            "displayName": "Mosambikanischer Escudo",
            "displayName-count-one": "Mozambikanische Escudo",
            "displayName-count-other": "Mozambikanische Escudo",
            "symbol": "MZE"
          },
          "MZM": {
            "displayName": "Mosambikanischer Metical (1980–2006)",
            "displayName-count-one": "Mosambikanischer Metical (1980–2006)",
            "displayName-count-other": "Mosambikanische Meticais (1980–2006)",
            "symbol": "MZM"
          },
          "MZN": {
            "displayName": "Mosambikanischer Metical",
            "displayName-count-one": "Mosambikanischer Metical",
            "displayName-count-other": "Mosambikanische Meticais",
            "symbol": "MZN"
          },
          "NAD": {
            "displayName": "Namibia-Dollar",
            "displayName-count-one": "Namibia-Dollar",
            "displayName-count-other": "Namibia-Dollar",
            "symbol": "NAD",
            "symbol-alt-narrow": "$"
          },
          "NGN": {
            "displayName": "Nigerianischer Naira",
            "displayName-count-one": "Nigerianischer Naira",
            "displayName-count-other": "Nigerianische Naira",
            "symbol": "NGN",
            "symbol-alt-narrow": "₦"
          },
          "NIC": {
            "displayName": "Nicaraguanischer Córdoba (1988–1991)",
            "displayName-count-one": "Nicaraguanischer Córdoba (1988–1991)",
            "displayName-count-other": "Nicaraguanische Córdoba (1988–1991)",
            "symbol": "NIC"
          },
          "NIO": {
            "displayName": "Nicaragua-Córdoba",
            "displayName-count-one": "Nicaragua-Córdoba",
            "displayName-count-other": "Nicaragua-Córdobas",
            "symbol": "NIO",
            "symbol-alt-narrow": "C$"
          },
          "NLG": {
            "displayName": "Niederländischer Gulden",
            "displayName-count-one": "Niederländischer Gulden",
            "displayName-count-other": "Niederländische Gulden",
            "symbol": "NLG"
          },
          "NOK": {
            "displayName": "Norwegische Krone",
            "displayName-count-one": "Norwegische Krone",
            "displayName-count-other": "Norwegische Kronen",
            "symbol": "NOK",
            "symbol-alt-narrow": "kr"
          },
          "NPR": {
            "displayName": "Nepalesische Rupie",
            "displayName-count-one": "Nepalesische Rupie",
            "displayName-count-other": "Nepalesische Rupien",
            "symbol": "NPR",
            "symbol-alt-narrow": "Rs"
          },
          "NZD": {
            "displayName": "Neuseeland-Dollar",
            "displayName-count-one": "Neuseeland-Dollar",
            "displayName-count-other": "Neuseeland-Dollar",
            "symbol": "NZ$",
            "symbol-alt-narrow": "$"
          },
          "OMR": {
            "displayName": "Omanischer Rial",
            "displayName-count-one": "Omanischer Rial",
            "displayName-count-other": "Omanische Rials",
            "symbol": "OMR"
          },
          "PAB": {
            "displayName": "Panamaischer Balboa",
            "displayName-count-one": "Panamaischer Balboa",
            "displayName-count-other": "Panamaische Balboas",
            "symbol": "PAB"
          },
          "PEI": {
            "displayName": "Peruanischer Inti",
            "displayName-count-one": "Peruanische Inti",
            "displayName-count-other": "Peruanische Inti",
            "symbol": "PEI"
          },
          "PEN": {
            "displayName": "Peruanischer Sol",
            "displayName-count-one": "Peruanischer Sol",
            "displayName-count-other": "Peruanische Sol",
            "symbol": "PEN"
          },
          "PES": {
            "displayName": "Peruanischer Sol (1863–1965)",
            "displayName-count-one": "Peruanischer Sol (1863–1965)",
            "displayName-count-other": "Peruanische Sol (1863–1965)",
            "symbol": "PES"
          },
          "PGK": {
            "displayName": "Papua-Neuguineischer Kina",
            "displayName-count-one": "Papua-Neuguineischer Kina",
            "displayName-count-other": "Papua-Neuguineische Kina",
            "symbol": "PGK"
          },
          "PHP": {
            "displayName": "Philippinischer Peso",
            "displayName-count-one": "Philippinischer Peso",
            "displayName-count-other": "Philippinische Pesos",
            "symbol": "PHP",
            "symbol-alt-narrow": "₱"
          },
          "PKR": {
            "displayName": "Pakistanische Rupie",
            "displayName-count-one": "Pakistanische Rupie",
            "displayName-count-other": "Pakistanische Rupien",
            "symbol": "PKR",
            "symbol-alt-narrow": "Rs"
          },
          "PLN": {
            "displayName": "Polnischer Złoty",
            "displayName-count-one": "Polnischer Złoty",
            "displayName-count-other": "Polnische Złoty",
            "symbol": "PLN",
            "symbol-alt-narrow": "zł"
          },
          "PLZ": {
            "displayName": "Polnischer Zloty (1950–1995)",
            "displayName-count-one": "Polnischer Zloty (1950–1995)",
            "displayName-count-other": "Polnische Zloty (1950–1995)",
            "symbol": "PLZ"
          },
          "PTE": {
            "displayName": "Portugiesischer Escudo",
            "displayName-count-one": "Portugiesische Escudo",
            "displayName-count-other": "Portugiesische Escudo",
            "symbol": "PTE"
          },
          "PYG": {
            "displayName": "Paraguayischer Guaraní",
            "displayName-count-one": "Paraguayischer Guaraní",
            "displayName-count-other": "Paraguayische Guaraníes",
            "symbol": "PYG",
            "symbol-alt-narrow": "₲"
          },
          "QAR": {
            "displayName": "Katar-Riyal",
            "displayName-count-one": "Katar-Riyal",
            "displayName-count-other": "Katar-Riyal",
            "symbol": "QAR"
          },
          "RHD": {
            "displayName": "Rhodesischer Dollar",
            "displayName-count-one": "Rhodesische Dollar",
            "displayName-count-other": "Rhodesische Dollar",
            "symbol": "RHD"
          },
          "ROL": {
            "displayName": "Rumänischer Leu (1952–2006)",
            "displayName-count-one": "Rumänischer Leu (1952–2006)",
            "displayName-count-other": "Rumänische Leu (1952–2006)",
            "symbol": "ROL"
          },
          "RON": {
            "displayName": "Rumänischer Leu",
            "displayName-count-one": "Rumänischer Leu",
            "displayName-count-other": "Rumänische Leu",
            "symbol": "RON",
            "symbol-alt-narrow": "L"
          },
          "RSD": {
            "displayName": "Serbischer Dinar",
            "displayName-count-one": "Serbischer Dinar",
            "displayName-count-other": "Serbische Dinaren",
            "symbol": "RSD"
          },
          "RUB": {
            "displayName": "Russischer Rubel",
            "displayName-count-one": "Russischer Rubel",
            "displayName-count-other": "Russische Rubel",
            "symbol": "RUB",
            "symbol-alt-narrow": "₽"
          },
          "RUR": {
            "displayName": "Russischer Rubel (1991–1998)",
            "displayName-count-one": "Russischer Rubel (1991–1998)",
            "displayName-count-other": "Russische Rubel (1991–1998)",
            "symbol": "RUR",
            "symbol-alt-narrow": "р."
          },
          "RWF": {
            "displayName": "Ruanda-Franc",
            "displayName-count-one": "Ruanda-Franc",
            "displayName-count-other": "Ruanda-Francs",
            "symbol": "RWF",
            "symbol-alt-narrow": "F.Rw"
          },
          "SAR": {
            "displayName": "Saudi-Rial",
            "displayName-count-one": "Saudi-Rial",
            "displayName-count-other": "Saudi-Rial",
            "symbol": "SAR"
          },
          "SBD": {
            "displayName": "Salomonen-Dollar",
            "displayName-count-one": "Salomonen-Dollar",
            "displayName-count-other": "Salomonen-Dollar",
            "symbol": "SBD",
            "symbol-alt-narrow": "$"
          },
          "SCR": {
            "displayName": "Seychellen-Rupie",
            "displayName-count-one": "Seychellen-Rupie",
            "displayName-count-other": "Seychellen-Rupien",
            "symbol": "SCR"
          },
          "SDD": {
            "displayName": "Sudanesischer Dinar (1992–2007)",
            "displayName-count-one": "Sudanesischer Dinar (1992–2007)",
            "displayName-count-other": "Sudanesische Dinar (1992–2007)",
            "symbol": "SDD"
          },
          "SDG": {
            "displayName": "Sudanesisches Pfund",
            "displayName-count-one": "Sudanesisches Pfund",
            "displayName-count-other": "Sudanesische Pfund",
            "symbol": "SDG"
          },
          "SDP": {
            "displayName": "Sudanesisches Pfund (1957–1998)",
            "displayName-count-one": "Sudanesisches Pfund (1957–1998)",
            "displayName-count-other": "Sudanesische Pfund (1957–1998)",
            "symbol": "SDP"
          },
          "SEK": {
            "displayName": "Schwedische Krone",
            "displayName-count-one": "Schwedische Krone",
            "displayName-count-other": "Schwedische Kronen",
            "symbol": "SEK",
            "symbol-alt-narrow": "kr"
          },
          "SGD": {
            "displayName": "Singapur-Dollar",
            "displayName-count-one": "Singapur-Dollar",
            "displayName-count-other": "Singapur-Dollar",
            "symbol": "SGD",
            "symbol-alt-narrow": "$"
          },
          "SHP": {
            "displayName": "St. Helena-Pfund",
            "displayName-count-one": "St. Helena-Pfund",
            "displayName-count-other": "St. Helena-Pfund",
            "symbol": "SHP",
            "symbol-alt-narrow": "£"
          },
          "SIT": {
            "displayName": "Slowenischer Tolar",
            "displayName-count-one": "Slowenischer Tolar",
            "displayName-count-other": "Slowenische Tolar",
            "symbol": "SIT"
          },
          "SKK": {
            "displayName": "Slowakische Krone",
            "displayName-count-one": "Slowakische Kronen",
            "displayName-count-other": "Slowakische Kronen",
            "symbol": "SKK"
          },
          "SLL": {
            "displayName": "Sierra-leonischer Leone",
            "displayName-count-one": "Sierra-leonischer Leone",
            "displayName-count-other": "Sierra-leonische Leones",
            "symbol": "SLL"
          },
          "SOS": {
            "displayName": "Somalia-Schilling",
            "displayName-count-one": "Somalia-Schilling",
            "displayName-count-other": "Somalia-Schilling",
            "symbol": "SOS"
          },
          "SRD": {
            "displayName": "Suriname-Dollar",
            "displayName-count-one": "Suriname-Dollar",
            "displayName-count-other": "Suriname-Dollar",
            "symbol": "SRD",
            "symbol-alt-narrow": "$"
          },
          "SRG": {
            "displayName": "Suriname Gulden",
            "displayName-count-one": "Suriname-Gulden",
            "displayName-count-other": "Suriname-Gulden",
            "symbol": "SRG"
          },
          "SSP": {
            "displayName": "Südsudanesisches Pfund",
            "displayName-count-one": "Südsudanesisches Pfund",
            "displayName-count-other": "Südsudanesische Pfund",
            "symbol": "SSP",
            "symbol-alt-narrow": "£"
          },
          "STD": {
            "displayName": "São-toméischer Dobra (1977–2017)",
            "displayName-count-one": "São-toméischer Dobra (1977–2017)",
            "displayName-count-other": "São-toméische Dobra (1977–2017)",
            "symbol": "STD"
          },
          "STN": {
            "displayName": "São-toméischer Dobra",
            "displayName-count-one": "São-toméischer Dobra",
            "displayName-count-other": "São-toméische Dobras",
            "symbol": "STN",
            "symbol-alt-narrow": "Db"
          },
          "SUR": {
            "displayName": "Sowjetischer Rubel",
            "displayName-count-one": "Sowjetische Rubel",
            "displayName-count-other": "Sowjetische Rubel",
            "symbol": "SUR"
          },
          "SVC": {
            "displayName": "El Salvador Colon",
            "displayName-count-one": "El Salvador-Colon",
            "displayName-count-other": "El Salvador-Colon",
            "symbol": "SVC"
          },
          "SYP": {
            "displayName": "Syrisches Pfund",
            "displayName-count-one": "Syrisches Pfund",
            "displayName-count-other": "Syrische Pfund",
            "symbol": "SYP",
            "symbol-alt-narrow": "SYP"
          },
          "SZL": {
            "displayName": "Swasiländischer Lilangeni",
            "displayName-count-one": "Swasiländischer Lilangeni",
            "displayName-count-other": "Swasiländische Emalangeni",
            "symbol": "SZL"
          },
          "THB": {
            "displayName": "Thailändischer Baht",
            "displayName-count-one": "Thailändischer Baht",
            "displayName-count-other": "Thailändische Baht",
            "symbol": "฿",
            "symbol-alt-narrow": "฿"
          },
          "TJR": {
            "displayName": "Tadschikistan Rubel",
            "displayName-count-one": "Tadschikistan-Rubel",
            "displayName-count-other": "Tadschikistan-Rubel",
            "symbol": "TJR"
          },
          "TJS": {
            "displayName": "Tadschikistan-Somoni",
            "displayName-count-one": "Tadschikistan-Somoni",
            "displayName-count-other": "Tadschikistan-Somoni",
            "symbol": "TJS"
          },
          "TMM": {
            "displayName": "Turkmenistan-Manat (1993–2009)",
            "displayName-count-one": "Turkmenistan-Manat (1993–2009)",
            "displayName-count-other": "Turkmenistan-Manat (1993–2009)",
            "symbol": "TMM"
          },
          "TMT": {
            "displayName": "Turkmenistan-Manat",
            "displayName-count-one": "Turkmenistan-Manat",
            "displayName-count-other": "Turkmenistan-Manat",
            "symbol": "TMT"
          },
          "TND": {
            "displayName": "Tunesischer Dinar",
            "displayName-count-one": "Tunesischer Dinar",
            "displayName-count-other": "Tunesische Dinar",
            "symbol": "TND"
          },
          "TOP": {
            "displayName": "Tongaischer Paʻanga",
            "displayName-count-one": "Tongaischer Paʻanga",
            "displayName-count-other": "Tongaische Paʻanga",
            "symbol": "TOP",
            "symbol-alt-narrow": "T$"
          },
          "TPE": {
            "displayName": "Timor-Escudo",
            "displayName-count-one": "Timor-Escudo",
            "displayName-count-other": "Timor-Escudo",
            "symbol": "TPE"
          },
          "TRL": {
            "displayName": "Türkische Lira (1922–2005)",
            "displayName-count-one": "Türkische Lira (1922–2005)",
            "displayName-count-other": "Türkische Lira (1922–2005)",
            "symbol": "TRL"
          },
          "TRY": {
            "displayName": "Türkische Lira",
            "displayName-count-one": "Türkische Lira",
            "displayName-count-other": "Türkische Lira",
            "symbol": "TRY",
            "symbol-alt-narrow": "₺",
            "symbol-alt-variant": "TL"
          },
          "TTD": {
            "displayName": "Trinidad und Tobago-Dollar",
            "displayName-count-one": "Trinidad und Tobago-Dollar",
            "displayName-count-other": "Trinidad und Tobago-Dollar",
            "symbol": "TTD",
            "symbol-alt-narrow": "$"
          },
          "TWD": {
            "displayName": "Neuer Taiwan-Dollar",
            "displayName-count-one": "Neuer Taiwan-Dollar",
            "displayName-count-other": "Neue Taiwan-Dollar",
            "symbol": "NT$",
            "symbol-alt-narrow": "NT$"
          },
          "TZS": {
            "displayName": "Tansania-Schilling",
            "displayName-count-one": "Tansania-Schilling",
            "displayName-count-other": "Tansania-Schilling",
            "symbol": "TZS"
          },
          "UAH": {
            "displayName": "Ukrainische Hrywnja",
            "displayName-count-one": "Ukrainische Hrywnja",
            "displayName-count-other": "Ukrainische Hrywen",
            "symbol": "UAH",
            "symbol-alt-narrow": "₴"
          },
          "UAK": {
            "displayName": "Ukrainischer Karbovanetz",
            "displayName-count-one": "Ukrainische Karbovanetz",
            "displayName-count-other": "Ukrainische Karbovanetz",
            "symbol": "UAK"
          },
          "UGS": {
            "displayName": "Uganda-Schilling (1966–1987)",
            "displayName-count-one": "Uganda-Schilling (1966–1987)",
            "displayName-count-other": "Uganda-Schilling (1966–1987)",
            "symbol": "UGS"
          },
          "UGX": {
            "displayName": "Uganda-Schilling",
            "displayName-count-one": "Uganda-Schilling",
            "displayName-count-other": "Uganda-Schilling",
            "symbol": "UGX"
          },
          "USD": {
            "displayName": "US-Dollar",
            "displayName-count-one": "US-Dollar",
            "displayName-count-other": "US-Dollar",
            "symbol": "$",
            "symbol-alt-narrow": "$"
          },
          "USN": {
            "displayName": "US Dollar (Nächster Tag)",
            "displayName-count-one": "US-Dollar (Nächster Tag)",
            "displayName-count-other": "US-Dollar (Nächster Tag)",
            "symbol": "USN"
          },
          "USS": {
            "displayName": "US Dollar (Gleicher Tag)",
            "displayName-count-one": "US-Dollar (Gleicher Tag)",
            "displayName-count-other": "US-Dollar (Gleicher Tag)",
            "symbol": "USS"
          },
          "UYI": {
            "displayName": "Uruguayischer Peso (Indexierte Rechnungseinheiten)",
            "displayName-count-one": "Uruguayischer Peso (Indexierte Rechnungseinheiten)",
            "displayName-count-other": "Uruguayische Pesos (Indexierte Rechnungseinheiten)",
            "symbol": "UYI"
          },
          "UYP": {
            "displayName": "Uruguayischer Peso (1975–1993)",
            "displayName-count-one": "Uruguayischer Peso (1975–1993)",
            "displayName-count-other": "Uruguayische Pesos (1975–1993)",
            "symbol": "UYP"
          },
          "UYU": {
            "displayName": "Uruguayischer Peso",
            "displayName-count-one": "Uruguayischer Peso",
            "displayName-count-other": "Uruguayische Pesos",
            "symbol": "UYU",
            "symbol-alt-narrow": "$"
          },
          "UYW": {
            "displayName": "UYW",
            "symbol": "UYW"
          },
          "UZS": {
            "displayName": "Usbekistan-Sum",
            "displayName-count-one": "Usbekistan-Sum",
            "displayName-count-other": "Usbekistan-Sum",
            "symbol": "UZS"
          },
          "VEB": {
            "displayName": "Venezolanischer Bolívar (1871–2008)",
            "displayName-count-one": "Venezolanischer Bolívar (1871–2008)",
            "displayName-count-other": "Venezolanische Bolívares (1871–2008)",
            "symbol": "VEB"
          },
          "VEF": {
            "displayName": "Venezolanischer Bolívar (2008–2018)",
            "displayName-count-one": "Venezolanischer Bolívar (2008–2018)",
            "displayName-count-other": "Venezolanische Bolívares (2008–2018)",
            "symbol": "VEF",
            "symbol-alt-narrow": "Bs"
          },
          "VES": {
            "displayName": "Venezolanischer Bolívar",
            "displayName-count-one": "Venezolanischer Bolívar",
            "displayName-count-other": "Venezolanische Bolívares",
            "symbol": "VES"
          },
          "VND": {
            "displayName": "Vietnamesischer Dong",
            "displayName-count-one": "Vietnamesischer Dong",
            "displayName-count-other": "Vietnamesische Dong",
            "symbol": "₫",
            "symbol-alt-narrow": "₫"
          },
          "VNN": {
            "displayName": "Vietnamesischer Dong(1978–1985)",
            "displayName-count-one": "Vietnamesischer Dong(1978–1985)",
            "displayName-count-other": "Vietnamesische Dong(1978–1985)",
            "symbol": "VNN"
          },
          "VUV": {
            "displayName": "Vanuatu-Vatu",
            "displayName-count-one": "Vanuatu-Vatu",
            "displayName-count-other": "Vanuatu-Vatu",
            "symbol": "VUV"
          },
          "WST": {
            "displayName": "Samoanischer Tala",
            "displayName-count-one": "Samoanischer Tala",
            "displayName-count-other": "Samoanische Tala",
            "symbol": "WST"
          },
          "XAF": {
            "displayName": "CFA-Franc (BEAC)",
            "displayName-count-one": "CFA-Franc (BEAC)",
            "displayName-count-other": "CFA-Franc (BEAC)",
            "symbol": "FCFA"
          },
          "XAG": {
            "displayName": "Unze Silber",
            "displayName-count-one": "Unze Silber",
            "displayName-count-other": "Unzen Silber",
            "symbol": "XAG"
          },
          "XAU": {
            "displayName": "Unze Gold",
            "displayName-count-one": "Unze Gold",
            "displayName-count-other": "Unzen Gold",
            "symbol": "XAU"
          },
          "XBA": {
            "displayName": "Europäische Rechnungseinheit",
            "displayName-count-one": "Europäische Rechnungseinheiten",
            "displayName-count-other": "Europäische Rechnungseinheiten",
            "symbol": "XBA"
          },
          "XBB": {
            "displayName": "Europäische Währungseinheit (XBB)",
            "displayName-count-one": "Europäische Währungseinheiten (XBB)",
            "displayName-count-other": "Europäische Währungseinheiten (XBB)",
            "symbol": "XBB"
          },
          "XBC": {
            "displayName": "Europäische Rechnungseinheit (XBC)",
            "displayName-count-one": "Europäische Rechnungseinheiten (XBC)",
            "displayName-count-other": "Europäische Rechnungseinheiten (XBC)",
            "symbol": "XBC"
          },
          "XBD": {
            "displayName": "Europäische Rechnungseinheit (XBD)",
            "displayName-count-one": "Europäische Rechnungseinheiten (XBD)",
            "displayName-count-other": "Europäische Rechnungseinheiten (XBD)",
            "symbol": "XBD"
          },
          "XCD": {
            "displayName": "Ostkaribischer Dollar",
            "displayName-count-one": "Ostkaribischer Dollar",
            "displayName-count-other": "Ostkaribische Dollar",
            "symbol": "EC$",
            "symbol-alt-narrow": "$"
          },
          "XDR": {
            "displayName": "Sonderziehungsrechte",
            "displayName-count-one": "Sonderziehungsrechte",
            "displayName-count-other": "Sonderziehungsrechte",
            "symbol": "XDR"
          },
          "XEU": {
            "displayName": "Europäische Währungseinheit (XEU)",
            "displayName-count-one": "Europäische Währungseinheiten (XEU)",
            "displayName-count-other": "Europäische Währungseinheiten (XEU)",
            "symbol": "XEU"
          },
          "XFO": {
            "displayName": "Französischer Gold-Franc",
            "displayName-count-one": "Französische Gold-Franc",
            "displayName-count-other": "Französische Gold-Franc",
            "symbol": "XFO"
          },
          "XFU": {
            "displayName": "Französischer UIC-Franc",
            "displayName-count-one": "Französische UIC-Franc",
            "displayName-count-other": "Französische UIC-Franc",
            "symbol": "XFU"
          },
          "XOF": {
            "displayName": "CFA-Franc (BCEAO)",
            "displayName-count-one": "CFA-Franc (BCEAO)",
            "displayName-count-other": "CFA-Francs (BCEAO)",
            "symbol": "CFA"
          },
          "XPD": {
            "displayName": "Unze Palladium",
            "displayName-count-one": "Unze Palladium",
            "displayName-count-other": "Unzen Palladium",
            "symbol": "XPD"
          },
          "XPF": {
            "displayName": "CFP-Franc",
            "displayName-count-one": "CFP-Franc",
            "displayName-count-other": "CFP-Franc",
            "symbol": "CFPF"
          },
          "XPT": {
            "displayName": "Unze Platin",
            "displayName-count-one": "Unze Platin",
            "displayName-count-other": "Unzen Platin",
            "symbol": "XPT"
          },
          "XRE": {
            "displayName": "RINET Funds",
            "displayName-count-one": "RINET Funds",
            "displayName-count-other": "RINET Funds",
            "symbol": "XRE"
          },
          "XSU": {
            "displayName": "SUCRE",
            "displayName-count-one": "SUCRE",
            "displayName-count-other": "SUCRE",
            "symbol": "XSU"
          },
          "XTS": {
            "displayName": "Testwährung",
            "displayName-count-one": "Testwährung",
            "displayName-count-other": "Testwährung",
            "symbol": "XTS"
          },
          "XUA": {
            "displayName": "Rechnungseinheit der AfEB",
            "displayName-count-one": "Rechnungseinheit der AfEB",
            "displayName-count-other": "Rechnungseinheiten der AfEB",
            "symbol": "XUA"
          },
          "XXX": {
            "displayName": "Unbekannte Währung",
            "displayName-count-one": "(unbekannte Währung)",
            "displayName-count-other": "(unbekannte Währung)",
            "symbol": "XXX"
          },
          "YDD": {
            "displayName": "Jemen-Dinar",
            "displayName-count-one": "Jemen-Dinar",
            "displayName-count-other": "Jemen-Dinar",
            "symbol": "YDD"
          },
          "YER": {
            "displayName": "Jemen-Rial",
            "displayName-count-one": "Jemen-Rial",
            "displayName-count-other": "Jemen-Rial",
            "symbol": "YER"
          },
          "YUD": {
            "displayName": "Jugoslawischer Dinar (1966–1990)",
            "displayName-count-one": "Jugoslawischer Dinar (1966–1990)",
            "displayName-count-other": "Jugoslawische Dinar (1966–1990)",
            "symbol": "YUD"
          },
          "YUM": {
            "displayName": "Jugoslawischer Neuer Dinar (1994–2002)",
            "displayName-count-one": "Jugoslawischer Neuer Dinar (1994–2002)",
            "displayName-count-other": "Jugoslawische Neue Dinar (1994–2002)",
            "symbol": "YUM"
          },
          "YUN": {
            "displayName": "Jugoslawischer Dinar (konvertibel)",
            "displayName-count-one": "Jugoslawische Dinar (konvertibel)",
            "displayName-count-other": "Jugoslawische Dinar (konvertibel)",
            "symbol": "YUN"
          },
          "YUR": {
            "displayName": "Jugoslawischer reformierter Dinar (1992–1993)",
            "displayName-count-one": "Jugoslawischer reformierter Dinar (1992–1993)",
            "displayName-count-other": "Jugoslawische reformierte Dinar (1992–1993)",
            "symbol": "YUR"
          },
          "ZAL": {
            "displayName": "Südafrikanischer Rand (Finanz)",
            "displayName-count-one": "Südafrikanischer Rand (Finanz)",
            "displayName-count-other": "Südafrikanischer Rand (Finanz)",
            "symbol": "ZAL"
          },
          "ZAR": {
            "displayName": "Südafrikanischer Rand",
            "displayName-count-one": "Südafrikanischer Rand",
            "displayName-count-other": "Südafrikanische Rand",
            "symbol": "ZAR",
            "symbol-alt-narrow": "R"
          },
          "ZMK": {
            "displayName": "Kwacha (1968–2012)",
            "displayName-count-one": "Kwacha (1968–2012)",
            "displayName-count-other": "Kwacha (1968–2012)",
            "symbol": "ZMK"
          },
          "ZMW": {
            "displayName": "Kwacha",
            "displayName-count-one": "Kwacha",
            "displayName-count-other": "Kwacha",
            "symbol": "ZMW",
            "symbol-alt-narrow": "K"
          },
          "ZRN": {
            "displayName": "Zaire-Neuer Zaïre (1993–1998)",
            "displayName-count-one": "Zaire-Neuer Zaïre (1993–1998)",
            "displayName-count-other": "Zaire-Neue Zaïre (1993–1998)",
            "symbol": "ZRN"
          },
          "ZRZ": {
            "displayName": "Zaire-Zaïre (1971–1993)",
            "displayName-count-one": "Zaire-Zaïre (1971–1993)",
            "displayName-count-other": "Zaire-Zaïre (1971–1993)",
            "symbol": "ZRZ"
          },
          "ZWD": {
            "displayName": "Simbabwe-Dollar (1980–2008)",
            "displayName-count-one": "Simbabwe-Dollar (1980–2008)",
            "displayName-count-other": "Simbabwe-Dollar (1980–2008)",
            "symbol": "ZWD"
          },
          "ZWL": {
            "displayName": "Simbabwe-Dollar (2009)",
            "displayName-count-one": "Simbabwe-Dollar (2009)",
            "displayName-count-other": "Simbabwe-Dollar (2009)",
            "symbol": "ZWL"
          },
          "ZWR": {
            "displayName": "Simbabwe-Dollar (2008)",
            "displayName-count-one": "Simbabwe-Dollar (2008)",
            "displayName-count-other": "Simbabwe-Dollar (2008)",
            "symbol": "ZWR"
          }
        }
      }
    }
  }
}

{% endhighlight %}

{% endtabs %}

![Internationalization in Blazor TreeGrid](images/blazor-treegrid-internationalization.png)

> * In the above sample, **Duration** column is formatted by **NumberFormatOptions**.
> * By default, **locale** value is **en-US**. In order to change the **en-US** culture to a different culture, set the **SetCulture** method accordingly.

## Right to left (RTL)

RTL provides an option to switch the text direction and layout of the Tree Grid component from right to left. It improves the user experiences and accessibility for users who use right-to-left languages (Arabic, Farsi, Urdu, etc.). In the below sample **EnableRtl** method is used to enable RTL in the Tree Grid.

{% tabs %}

{% highlight razor %}

@using TreeGridComponent.Data;
@using Syncfusion.Blazor.TreeGrid;

<SfTreeGrid DataSource="@TreeGridData" AllowPaging="true" Locale="ar-AE" IdMapping="TaskId" AllowSelection="true" ParentIdMapping="ParentId" TreeColumnIndex="1"
             Toolbar="@(new List<string>() { "Print", "ExpandAll", "CollapseAll" })">
    <TreeGridPageSettings PageSize="1"></TreeGridPageSettings>
    <TreeGridColumns>
        <TreeGridColumn Field="TaskId" HeaderText="Task ID" Width="80" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="TaskName" HeaderText="Task Name" Width="160"></TreeGridColumn>
        <TreeGridColumn Field="Duration" HeaderText="Duration" Width="100" Format="C2" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right"></TreeGridColumn>
        <TreeGridColumn Field="StartDate" HeaderText=" Start Date" Format="yMd" Type="Syncfusion.Blazor.Grids.ColumnType.Date" TextAlign="Syncfusion.Blazor.Grids.TextAlign.Right" Width="100"></TreeGridColumn>
        <TreeGridColumn Field="Priority" HeaderText="Priority" Width="80"></TreeGridColumn>
    </TreeGridColumns>
</SfTreeGrid>

@code{
    [Inject]
    IJSRuntime JsRuntime { get; set; }

    public List<TreeData> TreeGridData { get; set; }

    protected override void OnInitialized()
    {
        this.TreeGridData = TreeData.GetSelfDataSource().ToList();
    }

    protected override void OnAfterRender(bool firstRender)
    {
        if (firstRender)
        {
            this.JsRuntime.Sf().EnableRtl(true);
        }
    }
}

{% endhighlight %}

{% highlight c# %}

namespace TreeGridComponent.Data {

public class TreeData
    {
       
            public int TaskId { get; set;}
            public string TaskName { get; set;}
            public int? Duration { get; set;}
            public int? Progress { get; set;}
            public string Priority { get; set;}
            public int? ParentId { get; set;}
      
        public static List<TreeData> GetSelfDataSource()
        {
            List<TreeData> BusinessObjectCollection = new List<TreeData>();
            BusinessObjectCollection.Add(new TreeData() { TaskId = 1,TaskName = "Parent Task 1",Duration = 10,Progress = 70,Priority = "Critical",ParentId = null });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 2,TaskName = "Child task 1",Progress = 80,Priority = "Low",ParentId = 1 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 3,TaskName = "Child Task 2",Duration = 5,Progress = 65,Priority = "Critical",ParentId = 2 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 4,TaskName = "Child task 3",Duration = 6,Priority = "High",Progress = 77,ParentId = 3 });
            BusinessObjectCollection.Add(new TreeData() { TaskId = 5,TaskName = "Parent Task 2",Duration = 10,Progress = 70,Priority = "Critical",ParentId = null});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 6,TaskName = "Child task 1",Duration = 4,Progress = 80,Priority = "Critical",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 7,TaskName = "Child Task 2",Duration = 5,Progress = 65,Priority = "Low",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 8,TaskName = "Child task 3",Duration = 6,Progress = 77,Priority = "High",ParentId = 5});
            BusinessObjectCollection.Add(new TreeData() { TaskId = 9,TaskName = "Child task 4",Duration = 6,Progress = 77,Priority = "Low",ParentId = 5});
            return BusinessObjectCollection;
        }
    }
}

{% endhighlight %}

{% highlight json %}

{
    "ar-AE": {
        "treegrid": {
            "EmptyRecord": "لا سجلات لعرضها",
            "Print": "طباعة",
            "ExpandAll": "توسيع الكل",
            "CollapseAll": "انهيار جميع",
            "FilterButton": "منقي",
            "ClearButton": "واضح",
            "StartsWith": "ابدا ب",
            "EndsWith": "ينتهي مع",
            "Contains": "يحتوي على",
            "Equal": "مساو",
            "NotEqual": "غير متساوي",
            "LessThan": "أقل من",
            "LessThanOrEqual": "اصغر من او يساوي",
            "GreaterThan": "أكثر من",
            "GreaterThanOrEqual": "أكبر من أو يساوي",
            "ChooseDate": "اختر تاريخا",
            "EnterValue": "أدخل القيمة",
            "FilterMenu": "منقي"
        },
        "pager": {
            "currentPageInfo": "{0} من {1} صفحة",
            "totalItemsInfo": "({0} العناصر)",
            "firstPageTooltip": "انتقل إلى الصفحة الأولى",
            "lastPageTooltip": "انتقل إلى الصفحة الأخيرة",
            "nextPageTooltip": "انتقل إلى الصفحة التالية",
            "previousPageTooltip": "انتقل إلى الصفحة السابقة",
            "nextPagerTooltip": "الذهاب إلى بيجر المقبل",
            "previousPagerTooltip": "الذهاب إلى بيجر السابقة"
        },
        "dropdowns": {
            "noRecordsTemplate": "لا توجد سجلات"
        },
        "datepicker": {
            "placeholder": "اختر تاريخا",
            "today": "اليوم"
        }
    }
}

{% endhighlight %}

{% endtabs %}


![Right to Left in Blazor TreeGrid](images/blazor-treegrid-right-to-left.png)