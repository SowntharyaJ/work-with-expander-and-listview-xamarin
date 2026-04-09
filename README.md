**[View document in Syncfusion Xamarin Knowledge base](https://www.syncfusion.com/kb/12143/how-to-work-with-listview-sflistview-and-expander-sfexpander-in-xamarin-forms)**

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
