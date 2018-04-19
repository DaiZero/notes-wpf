## 显示列号

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
                <TextBlock 
                Text="{Binding Path=RowHandle.Value,Converter={StaticResource RowHandleConverter}}" TextAlignment="Right" 
                Margin="0,0,10,0"/>
            </StackPanel>
        </DataTemplate>
    </ResourceDictionary>
</UserControl.Resources>
<!--方法2.1:TableView中的Indicator属性相关设置-->
<dxg:GridControl>
    <dxg:GridControl.View>
        <dxg:TableView  ShowIndicator="true" 
        IndicatorWidth="40" 
        RowIndicatorContentTemplate="{StaticResource rowIndicatorContentTemplate}"/>
    </dxg:GridControl.View>
</dxg:GridControl >
    
<!--方法2.2-->
<dxg:GridColumn Width="40">
    <dxg:GridColumn.CellTemplate>
        <DataTemplate>
            <TextBlock Width="40" 
            Text="{Binding Path = RowData.RowHandle.Value, Converter={StaticResource RowHandleConverter}}" 
                HorizontalAlignment="Center" VerticalAlignment="Center" TextAlignment="Center"/>
        </DataTemplate>
    </dxg:GridColumn.CellTemplate>
</dxg:GridColumn>
```

## 列表（时间类型）的格式化显示

1. **用EditSettings来实现**
```xml
<!--方式1-->
<dxg:GridColumn Header="时间" FieldName="ExDate">
      <dxg:GridColumn.EditSettings>
           <dxe:TextEditSettings Mask="yyyy-MM-dd" MaskType="DateTime" MaskUseAsDisplayFormat="True"/>
      </dxg:GridColumn.EditSettings>
</dxg:GridColumn>
<!--方式2-->
<dxg:GridColumn Header="时间" FieldName="ExDate">
    <dxg:GridColumn.EditSettings>
        <dxe:TextEditSettings DisplayFormat="yyyy-MM-dd"/>
    </dxg:GridColumn.EditSettings>
</dxg:GridColumn>
```

2. **用DataTemplate来实现**

```xml
<dxg:GridColumn Header="时间" FieldName="ExDate">
    <dxg:GridColumn.CellTemplate>
        <DataTemplate>
          <dxe:TextEdit Name="PART_Editor" DisplayFormatString="yyyy-MM-dd"/>
        </DataTemplate>
    </dxg:GridColumn.CellTemplate>
</dxg:GridColumn>
```

## 单选行数据的获取

>FocusedRow已经弃用，在Master Detail 下的Detail里的数据行用 TableView的FocusedRow取不到当前所选行数据，使用GridControl 下的CurrentItem或SelectedItem可取到。

## MasterDetail内容自动全部展开

 ```csharp
 private void FrameworkElement_OnLoaded(object sender, RoutedEventArgs e)
{
   var gctrl = (GridControl) sender;
   for (int i = 0; i < gctrl.VisibleRowCount; i++)
   {
      gctrl.ExpandMasterRow(gctrl.GetRowHandleByListIndex(i));
   }
 }
 ```

