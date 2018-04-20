记录使用WPF的Dev控件开发过程中的实现相关功能的方法以及遇到的问题

## 功能实现
- [显示行号](wpf-dev-gridcontrol-show-row-index.md)
- [列表（时间类型）的格式化显示](wpf-dev-gridcontrol-datetime-type-row-custom-display.md)
- [MasterDetail内容自动全部展开](wpf-dev-gridcontrol-masterdetail-expand-all.md)

## 单选行数据的获取

>FocusedRow已经弃用，在Master Detail 下的Detail里的数据行用 TableView的FocusedRow取不到当前所选行数据，使用GridControl 下的CurrentItem或SelectedItem可取到。
