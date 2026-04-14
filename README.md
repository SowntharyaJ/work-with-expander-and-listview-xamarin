# Work with Expander and ListView Xamarin
This example demonstrates how to work with Expander and ListView Xamarin.

## Sample

```xaml
<StackLayout>
    <expander:SfExpander DynamicSizeMode="Content" HeaderIconPosition="End" IconColor="WhiteSmoke" HeaderBackgroundColor="#03506f" >
        <expander:SfExpander.Header>
            <Grid HeightRequest="50">
                <Label Text="InBox" TextColor="White" HorizontalOptions="CenterAndExpand" VerticalOptions="CenterAndExpand"/>
            </Grid>
        </expander:SfExpander.Header>
        <expander:SfExpander.Content>
            <extListView:ExtendedListView x:Name="listView" ItemsSource="{Binding InboxInfo}" ItemSpacing="1" ItemSize="70">
                <extListView:ExtendedListView.ItemTemplate>
                    <DataTemplate>
                        <code>
                        . . .
                        . . .
                        <code>
                    </DataTemplate>
                </extListView:ExtendedListView.ItemTemplate>
            </extListView:ExtendedListView>
        </expander:SfExpander.Content>
    </expander:SfExpander>
</StackLayout>

C#:
public class ExtendedListView : SfListView
{
    VisualContainer container;

    public ExtendedListView()
    {
        container = this.GetVisualContainer();
        container.PropertyChanged += Container_PropertyChanged;
    }

    private void Container_PropertyChanged(object sender, System.ComponentModel.PropertyChangedEventArgs e)
    {
        Device.BeginInvokeOnMainThread(async() =>
        {
            var extent = (double)container.GetType().GetRuntimeProperties().FirstOrDefault(container => container.Name == "TotalExtent").GetValue(container);
            await Task.Delay(250);

            if (e.PropertyName == "Height")
                this.HeightRequest = extent;
        });
    }
}
```

**[View document in Syncfusion Xamarin Knowledge base](https://www.syncfusion.com/kb/12143/how-to-work-with-listview-sflistview-and-expander-sfexpander-in-xamarin-forms)**

## Requirements to run the demo

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) or [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/)
* Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting

### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
