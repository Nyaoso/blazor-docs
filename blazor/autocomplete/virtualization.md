---
layout: post
title: Virtualization in Blazor AutoComplete Component | Syncfusion
description: Checkout and learn here all about Virtualization in Syncfusion Blazor AutoComplete component and much more.
platform: Blazor
control: AutoComplete
documentation: ug
---

# Virtualization in Blazor AutoComplete Component

The AutoComplete has been provided virtualization to improve the UI performance for a large amount of data when [EnableVirtualization](https://help.syncfusion.com/cr/blazor/Syncfusion.Blazor.DropDowns.SfDropDownList-2.html#Syncfusion_Blazor_DropDowns_SfDropDownList_2_EnableVirtualization) is true. This feature doesn’t render out the entire data source on initial component rendering. It loads the N number of items in the popup on initial rendering and the remaining set number of items will load on each scrolling action in the popup. It can work with both local and remote data.

In the following code 150 items bound to the component, but only 6 items will load to the popup when you open the popup. Remaining set number of items will load on each scrolling action in the popup.

```cshtml

@using Syncfusion.Blazor.DropDowns
@using Syncfusion.Blazor.Data

<SfAutoComplete TValue="string" TItem="Record" Placeholder="Select an item" DataSource="@Records" Query="@LocalDataQuery" PopupHeight="130px" EnableVirtualization="true" ShowPopupButton="true">
    <AutoCompleteFieldSettings Value="Text"></AutoCompleteFieldSettings>
</SfAutoComplete>

@code{
    public Query LocalDataQuery = new Query().Take(6);
    public class Record
    {
        public string ID { get; set; }
        public string Text { get; set; }
    }
    public List<Record> Records { get; set; }
    protected override void OnInitialized()
    {
        this.Records = Enumerable.Range(1, 150).Select(i => new Record()
        {
            ID = i.ToString(),
            Text = "Item " + i,
        }).ToList();
    }
}
```


![Blazor AutoComplete with virtualization](./images/blazor_autocomplete_virtualization.gif)