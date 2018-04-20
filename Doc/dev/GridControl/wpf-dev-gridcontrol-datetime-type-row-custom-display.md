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