1. **可下拉编辑模式**

```xml
<dxg:GridColumn  FieldName="Type" Header="Type">
    <dxg:GridColumn.EditSettings>
        <dxe:ComboBoxEditSettings ItemsSource="{Binding TypeList}" DisplayMember="Name" ValueMember="Value"/>
    </dxg:GridColumn.EditSettings>
</dxg:GridColumn>
```

2. **不可下拉只读模式**

```xml
<dxg:GridColumn  FieldName="Type" Header="Type"  ReadOnly="False">
    <dxg:GridColumn.EditSettings>
        <dxe:ComboBoxEditSettings ItemsSource="{Binding TypeList}" DisplayMember="Name" ValueMember="Value" AllowDefaultButton="False"/>
    </dxg:GridColumn.EditSettings>
</dxg:GridColumn>
```