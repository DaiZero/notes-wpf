1. **勾选框的显示**

```xml
<dxg:GridControl SelectionMode="Row">
<dxg:GridControl.View>
<dxg:TableView ShowCheckBoxSelectorColumn="True"/>
</dxg:GridControl.View>
</dxg:GridControl>
```

2. **单击数据行勾选框联动模式**

```xml
<dxg:GridControl SelectionMode="MultipleRow">
<dxg:GridControl.View>
<dxg:TableView ShowCheckBoxSelectorColumn="True" RetainSelectionOnClickOutsideCheckBoxSelector="False"/>
</dxg:GridControl.View>
</dxg:GridControl>
```