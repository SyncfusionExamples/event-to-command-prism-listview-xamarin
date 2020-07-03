# How to work with Prism using the EventToCommandBehavior in Xamarin.Forms ListView (SfListView)

You can pass the default event argument as parameter when using [Prism](https://prismlibrary.com/docs/index.html) Framework EventToCommandBehavior in Xamarin.Forms [SfListView](https://help.syncfusion.com/xamarin/listview/overview).

The prism [EventToCommandBehavior](https://prismlibrary.com/docs/xamarin-forms/behaviors/eventtocommandbehavior.html) will pass the parameter based on the [CommandParameter](https://prismlibrary.com/docs/xamarin-forms/behaviors/eventtocommandbehavior.html#commandparameter), [EventArgsParameterPath](https://prismlibrary.com/docs/xamarin-forms/behaviors/eventtocommandbehavior.html#eventargsparameterpath) and [EventArgsConverter](https://prismlibrary.com/docs/xamarin-forms/behaviors/eventtocommandbehavior.html#eventargsconverter). The parameter will be null in the [Command](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/commanding) execute method, if no value passed to these parameters.

You can also refer the following article
https://www.syncfusion.com/kb/11680/how-to-work-with-prism-using-the-eventtocommandbehavior-in-xamarin-forms-listview

**XAML**

Refer the Prism Framework **EventToCommandBehavior** for ListView. Use **EventArgsConverter** to pass the default EventArgs to the **Command**.
``` xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ListViewXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.ListView.XForms;assembly=Syncfusion.SfListView.XForms"
             xmlns:helper="clr-namespace:ListViewXamarin.Helper"
             xmlns:behavior="http://prismlibrary.com"
             x:Class="ListViewXamarin.MainPage">
  
    <ContentPage.Resources>
        <ResourceDictionary>
            <helper:Converter x:Key="EventArgsConverter"/>
        </ResourceDictionary>
    </ContentPage.Resources>
	 <ContentPage.Content>
        <StackLayout>
            <syncfusion:SfListView x:Name="listView" ItemSize="60" ItemsSource="{Binding ContactsInfo}">
                <syncfusion:SfListView.Behaviors>
                    <behavior:EventToCommandBehavior EventName="ItemDoubleTapped" Command="{Binding ItemDoubleTappedCommand}" EventArgsConverter="{StaticResource EventArgsConverter}"/>
                </syncfusion:SfListView.Behaviors>
                <syncfusion:SfListView.ItemTemplate>
                    <DataTemplate>
                        <Grid x:Name="grid">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="70" />
                                <ColumnDefinition Width="*" />
                            </Grid.ColumnDefinitions>
                            <Image Source="{Binding ContactImage}" VerticalOptions="Center" HorizontalOptions="Center" HeightRequest="50" WidthRequest="50"/>
                            <Grid Grid.Column="1" RowSpacing="1" Padding="10,0,0,0" VerticalOptions="Center">
                                <Label x:Name="label" LineBreakMode="NoWrap" TextColor="#474747" Text="{Binding ContactName}"/>
                                <Label Grid.Row="1" Grid.Column="0" TextColor="#474747" LineBreakMode="NoWrap" Text="{Binding ContactNumber}"/>
                            </Grid>
                        </Grid>
                    </DataTemplate>
                </syncfusion:SfListView.ItemTemplate>
            </syncfusion:SfListView>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```
**C#**

Return the value which is the actual parameter of the Event.
``` c#
namespace ListViewXamarin.Helper
{
    public class Converter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            return value;
        }

        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```
