# How to customize the style of tree nodes based on its level using converter in WPF TreeView

This repository describes how to customize the style of tree nodes based on its level using converter in [WPF TreeView](https://www.syncfusion.com/wpf-controls/treeview) (SfTreeView).

The TreeView allows you to customize the style of [TreeViewItem](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.TreeView.TreeViewItem.html) based on different levels by using [IValueConverter](https://docs.microsoft.com/en-us/dotnet/api/system.windows.data.ivalueconverter?view=netcore-3.1).

#### XAML

``` xml
<Window.Resources>
    <local:FontAttributeConverter x:Key="FontAttributeConverter"/>
</Window.Resources>
<Window.DataContext>
    <local:MailFolderViewModel x:Name="viewModel"/>
</Window.DataContext>

<Grid>
    <Syncfusion:SfTreeView HorizontalAlignment="Left" ItemTemplateDataContextType="Node"  ItemsSource="{Binding Folders}"  ChildPropertyName="SubFolder" >
        <Syncfusion:SfTreeView.ItemTemplate>
            <DataTemplate>
                <Label  Content="{Binding Content.FolderName}" FontWeight="{Binding Level, Converter={StaticResource FontAttributeConverter}}"
                FontSize="14"/>
            </DataTemplate>
        </Syncfusion:SfTreeView.ItemTemplate>
    </Syncfusion:SfTreeView>
</Grid>
```
#### C#

``` csharp
public class FontAttributeConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        var level = (int)value;
        return level == 0 ? FontWeights.Bold : FontWeights.Regular;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```