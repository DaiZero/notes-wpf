# 显示列号

![showrowindex](/Img/dev/gridcontrol_showcolumindex.png)

方法1 代码(CodeBehind)：

```csharp
this.dataGrid.LoadingRow += new EventHandler<DataGridRowEventArgs>(this.DataGrid_LoadingRow);     
private void DataGrid_LoadingRow(object sender, DataGridRowEventArgs e)
{
    e.Row.Header = e.Row.GetIndex() + 1;
}
```

方法2 代码(MVVM)：
Convertor:
```csharp
 public class RowHandleToRowNumberConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            return value == null ? 0 : System.Convert.ToInt32(value) + 1;
        }

        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            return value == null ? 0 : System.Convert.ToInt32(value) - 1;
        }
    }
```

Xaml:
```xml
xmlns:dxg="http://schemas.devexpress.com/winfx/2008/xaml/grid"
xmlns:dxe="http://schemas.devexpress.com/winfx/2008/xaml/editors"
xmlns:cvt="clr-namespace:Converters"
    
<UserControl.Resources>
    <ResourceDictionary>
        <cvt:RowHandleToRowNumberConverter x:Key="RowHandleConverter"/>
        <DataTemplate x:Key="rowIndicatorContentTemplate">
            <StackPanel VerticalAlignment="Stretch" HorizontalAlignment="Stretch">
                <TextBlock Text="{Binding Path=RowHandle.Value,Converter={StaticResource RowHandleConverter}}" TextAlignment="Right" Margin="0,0,10,0"/>
            </StackPanel>
        </DataTemplate>
    </ResourceDictionary>
</UserControl.Resources>
<!--方法2.1:TableView中的Indicator属性相关设置-->
<dxg:GridControl>
    <dxg:GridControl.View>
        <dxg:TableView  ShowIndicator="true" IndicatorWidth="40" RowIndicatorContentTemplate="{StaticResource rowIndicatorContentTemplate}"/>
    </dxg:GridControl.View>
</dxg:GridControl >
    
<!--方法2.2-->
<dxg:GridColumn Width="40">
    <dxg:GridColumn.CellTemplate>
        <DataTemplate>
            <TextBlock Width="40" Text="{Binding Path = RowData.RowHandle.Value, Converter={StaticResource RowHandleConverter}}" 
                HorizontalAlignment="Center" VerticalAlignment="Center" TextAlignment="Center"/>
        </DataTemplate>
    </dxg:GridColumn.CellTemplate>
</dxg:GridColumn>
```