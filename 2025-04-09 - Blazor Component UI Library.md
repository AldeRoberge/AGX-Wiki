

Looking at the solutions : 

| 📚 Library                                                                  | ⭐ Stars | 📝 Commits | 📄 License                | ⏳ Expected Longevity      | 🎨 Aesthetic             | 📖 Quality of Documentation |     |
| --------------------------------------------------------------------------- | ------- | ---------- | ------------------------- | ------------------------- | ------------------------ | --------------------------- | --- |
| [Radzen Blazor](https://github.com/radzenhq/radzen-blazor)                  | 3900    | 4598       | 🟢 Free (MIT)             | 🟢 Popular                | 🟢 Choose your theme     | 🟢 Awesome                  |     |
| [Fluent UI](https://github.com/microsoft/fluentui-blazor)                   | 4200    | 3271       | 🟢 Free (MIT)             | 🟢 Used by Microsoft      | 🟡  Looks like Microsoft | 🟢 Awesome                  |     |
| [Ant Design Blazor](https://github.com/ant-design-blazor/ant-design-blazor) | 6000    | 2194       | 🟢 Free (MIT)             | 🟢 Very popular           | 🟢 Ant Design            | 🟡  Meh                     |     |
| [MudBlazor](https://github.com/MudBlazor/MudBlazor)                         | 8900    | 6612       | 🟢 Free (MIT)             | 🟢 Very popular           | 🔴 Material Design       | 🟢 Awesome                  |     |
| [Blazorise](https://github.com/Megabit/Blazorise)                           | 3400    | 4805       | 🔴 Paid                   | 🔴 I don't care it's paid | 🟡 Okay                  | 🟡 Okay                     |     |
| [Sysinfocus](https://github.com/Sysinfocus/simple-ui/)                      | 100     | 25         | 🔴 Free but closed-source | 🔴 Very unpopular         | 🟢 Shadcn                | 🟡 Okay                     |     |


| Library               | Website & Repository Links                                                                                              | UI Design / Framework                                                 | Key Features                                                                                                                  | License            |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| **Blazorise**         | [Documentation](https://blazorise.com/docs/) <br> [GitHub](https://github.com/Megabit/Blazorise)                        | Multiple CSS frameworks (Bootstrap, Bulma, Material, AntDesign, etc.) | Flexible and responsive design; rich component collection; supports several CSS frameworks                                    | Proprietary        |
| **Fluent UI Blazor**  | [GitHub](https://github.com/microsoft/fluentui-blazor)                                                                  | Fluent UI (Microsoft design system)                                   | Integrates Microsoft’s Fluent UI design language; ideal for enterprise applications                                           | MIT License        |
| **MudBlazor**         | [Overview & Docs](https://mudblazor.com/docs/overview) <br> [GitHub](https://github.com/MudBlazor/MudBlazor)            | Material Design                                                       | Elegant Material Design components; customizable themes; highly active community and regular updates                          | MIT License        |
| **Ant Design Blazor** | [GitHub](https://github.com/ant-design-blazor/ant-design-blazor)                                                        | Ant Design                                                            | Robust set of components inspired by Ant Design; enterprise-ready; consistency in UI behavior and design                      | MIT License        |
| **Radzen Blazor**     | [Live Demo & Docs](https://blazor.radzen.com/?theme=material3) <br> [GitHub](https://github.com/radzenhq/radzen-blazor) | Material (with additional theming options)                            | Wide variety of UI components (grids, charts, forms, etc.); productivity tools integrated; dual licensing (free & commercial) | Apache License 2.0 |



Looking at the discussions : 

| Link                                                                                                             | Takaways                                                                                                                                                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Fluent UI vs MudBlazor](https://www.reddit.com/r/Blazor/comments/1ax6o8n/fluent_ui_vs_mudblazor/) on Reddit     | A user states painful experience with FluentUI<br>A user states FluentUI is inferior to MudBlazor<br>A user states MudBlazor is working well<br>A user states FluentUI is limited, reeks of Microsoft                                                               |
| [Fluent UI Blazor Vs MudBlazor](https://www.restack.io/p/fluent-ui-blazor-vs-mudblazor-answer-cat-ai) on Restack | Fluent UI uses the Microsoft Fluent Design System<br>MudBlazor adopts the Material Design approach<br>MudBlazor is simple to use<br>MudBlazor has limited theming                                                                                                   |
| [8 Free and Open Source Blazor UI Libraries](https://www.youtube.com/watch?v=bsu0cCjeVaw) on YouTube             | MudBlazor contains more than 50 controls, has theming support, most popular control librairies.<br>Microsoft has many components. Popular. Active.<br>Ant Design Blazor, Ant group is a subsidiary of Alibaba Group. <br>Comments mention liking MudBlazor, Radzen. |


## Closing in

So it seems like there aren't really any clear winner. It's a game of compromise, as usual 🤪!

| **Criteria**       | **MudBlazor**                                                       | **Fluent UI (BlazorFluentUI)**                                                | **Ant Design (AntBlazor)**                                                         | **Sysinfocus**                                                      |
| ------------------ | ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Community Size** | 🟢 Very active and growing                                          | 🟡 Moderately active                                                          | 🔴 Smaller community                                                               | 🔴 Very small community                                             |
| **Documentation**  | 🟢 Excellent, detailed, and frequently updated                      | 🟡 Good overall but can vary between versions                                 | 🟡 Satisfactory; may require additional community resources                        | 🟡 Satisfactory; may require additional community resources         |
| **Aesthetic**      | 🟢 Modern Material Design; clean and familiar                       | 🟢 Microsoft Fluent design; enterprise-ready                                  | 🟢 Elegant and polished with a distinct international flair                        | 🟢 Shadcn                                                           |
| **Charts**         | 🟡 Basic chart components; often extended via third-party libraries | 🔴 Limited native chart support; external libraries usually required          | 🟡 Some chart support is available; typically supplemented with external libraries | 🟡 Basic chart components; often extended via third-party libraries |
| **Data Grids**     | 🟢 Robust grid/table components with many features                  | 🟡 Provides basic table components; advanced features may require custom work | 🟡 Offers some built-in grid features, though not as mature or customizable        |                                                                     |

At this point I dropped SysInfocus because it's closed-source and very unpopular.

Let's evaluate the quality of the documentation with the following components : 

### Breadcrumbs

| Link                                                               | Aesthetic               | Clarity of documentation             | Winner(s) |
| ------------------------------------------------------------------ | ----------------------- | ------------------------------------ | --------- |
| [Mudblazor](https://mudblazor.com/components/breadcrumbs)          | 🟢 Looks awesome        | 🟢 Very clear, lots of customization | ✅         |
| [FluentUI](https://www.fluentui-blazor.net/Breadcrumb)             | 🟡 Looks like Microsoft | 🟡 A bit fugly, but functional       | 🟡        |
| [AntBlazor](https://antblazor.com/en-US/components/breadcrumb)     | 🟢 Looks awesome        | 🟢 Awesome                           | 🟡        |
### Buttons

| Link                                                       | Aesthetic               | Clarity of documentation             | Winner(s) |
| ---------------------------------------------------------- | ----------------------- | ------------------------------------ | --------- |
| [Mudblazor](https://mudblazor.com/components/button#api)   | 🔴 Looks like shit      | 🟢 Very clear, lots of customization | 🟡        |
| [FluentUI](https://www.fluentui-blazor.net/Button)         | 🟡 Looks like Microsoft | 🟢 Clear                             | 🟡        |
| [AntBlazor](https://antblazor.com/en-US/components/button) | 🟢 Looks awesome        | 🟢 Very awesome                      | ✅         |
### Data Grid

| Link                                                                     | Aesthetic        | Clarity of documentation | Winner(s) |
| ------------------------------------------------------------------------ | ---------------- | ------------------------ | --------- |
| [Mudblazor](https://mudblazor.com/components/datagrid#default-data-grid) | 🟢 Looks awesome | 🟢 Very complete         | ✅         |
| [FluentUI](https://www.fluentui-blazor.net/datagrid-get-started)         | 🟢 Looks awesome | 🟢 Very complete         | ✅         |
| [AntBlazor](https://antblazor.com/en-US/components/table)                | 🟢 Looks awesome | 🟢 Complete              | 🟡        |

### Dialogs


| Link                                                                      | Aesthetic     | Clarity of documentation | Winner(s) |
| ------------------------------------------------------------------------- | ------------- | ------------------------ | --------- |
| [Mudblazor](https://mudblazor.com/components/form#simple-form-validation) | 🟡 Looks meh  | 🟢 Complete              | 🟡        |
| [FluentUI](https://www.fluentui-blazor.net/Dialog)                        | 🟡 Looks okay | 🟢 Complete              | 🟡        |
| [AntBlazor](https://antblazor.com/en-US/components/modal)                 | 🟡 Looks okay | 🟢 Complete              | 🟡        |

I think I don't like dialog boxes in general... lol

Let's take a look at the code.

#### Mudblazor 

```csharp
@inject IDialogService DialogService

<MudButton @onclick="OpenDialogAsync" Variant="Variant.Filled" Color="Color.Primary">
    Open Simple Dialog
</MudButton>

@code {

    private Task OpenDialogAsync()
    {
        var options = new DialogOptions { CloseOnEscapeKey = true };

        return DialogService.ShowAsync<DialogUsageExample_Dialog>("Simple Dialog", options);
    }
}
```

#### FluentUI

```csharp
@inject IDialogService _dialogService

<FluentButton OnClick="OpenDialog" Appearance="Appearance.Accent">Open dialog</FluentButton>

@code {
    private async Task OpenDialog()
    {
        var text = string.Empty;
        var dialogInstance = await _dialogService.ShowDialogAsync(@<div>
        <FluentTextField @bind-Value=text Label="Enter a value:" />
    </div>
    , new DialogParameters
    {
        Title = "Render Fragment Content",
    });

        var result = await dialogInstance.Result;
        if (!result.Cancelled)
        {
            await _dialogService.ShowSuccessAsync($"You entered: {text}", "Success");
        }
    }
}
```

#### AntBlazor

```csharp


<Button Type="ButtonType.Primary" OnClick="@(()=>{ _visible = true; })">

    Open Modal

</Button>

<Modal Title="BasicModal"

       @bind-Visible="@_visible">

    <p>Some contents...</p>

    <p>Some contents...</p>

    <p>Some contents...</p>

</Modal>

@code{

  

    bool _visible = false;

  

}
```


---



### Finalists

| Solution  | Aesthetic                    | Documentation quality | Code examples quality |
| --------- | ---------------------------- | --------------------- | --------------------- |
| MudBlazor | 🔴 Worst (Google Material)   | 🟢 Awesome            | 🟢 Best               |
| FluentUI  | 🟡 Okay (Microsoft Fluent)   | 🟢 Great              | 🟢 Awesome            |
| AntDesign | 🟢 Best (Alibaba Ant Design) | 🟡 Okay               | 🟡 Okay               |


A user reached out and told me I should look into [Syncfusion](https://blazor.syncfusion.com/demos/chart/multi-colored-line?theme=bootstrap5).

Turns out that it's free if we make below 1 000 000$ in revenue. 