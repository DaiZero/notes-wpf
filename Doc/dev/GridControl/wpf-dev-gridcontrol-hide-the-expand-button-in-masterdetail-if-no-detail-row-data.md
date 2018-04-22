>如果MasterDetail中没有详细数据，如何隐藏主细节网格中的展开按钮

1. **数据转换器：数字转换为Visibility类型**
```csharp
public class NumberToVisibilityConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            if (value is int)
            {
                return (int)value>0? Visibility.Visible:Visibility.Hidden;
            }
            return Visibility.Hidden;
        }
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            return value;
        }
    }
```
2. **前台实现:**
```xml
<UserControl.Resources>
    <ResourceDictionary>
        <cvt:NumberToVisibilityConverter x:Key="cvt001" />
        <Style TargetType="{x:Type dxg:GridDetailExpandButton}">
            <Setter Property="Visibility"  
            Value="{Binding DataContext.Row.DetailList.Count, RelativeSource={RelativeSource Self}, Converter={StaticResource cvt001}}" />
        </Style>
    </ResourceDictionary>
</UserControl.Resources>
```
3. **参考文档**
https://www.devexpress.com/Support/Center/Example/Details/E4237/how-to-hide-the-expand-button-in-master-detail-grid-if-a-row-has-no-detail-data
