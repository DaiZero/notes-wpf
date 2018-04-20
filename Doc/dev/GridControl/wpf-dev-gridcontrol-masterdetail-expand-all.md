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