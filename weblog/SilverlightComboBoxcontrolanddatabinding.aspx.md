---
title: Silverlight ComboBox control and data binding
postDate: 2009-03-25T11:01:05.414-05:00
abstract: 
postStatus: publish
---
25 March 2009

Google tells me that issues with the Silverlight ComboBox control are widespread and well known. It also tells me that there are few solid solutions out there if you want data binding to work with the Silverlight ComboBox in a simple, reliable manner.

Perhaps the best post on the topic is [this one](http://www.engineserver.com/silverlightcombobox/), but this particular code example doesn’t work in all cases (specifically not inside a DataTemplate, and as a form loads and gets async data).

After wasting more time than I care to consider, I believe I have a more complete solution. Though it isn’t perfect either, it does appear to work nicely with [CSLA .NET](http://www.lhotka.net/cslalight) NameValueListBase objects, and inside DataTemplate elements, which is really what I was after.

As others have pointed out, the solution is to subclass ComboBox and add SelectedValue and ValueMemberPath properties to the control. The trick is to catch all the edge cases where these new properties, and the pre-existing SelectedItem and Items properties, might change. I may not have them all either, but I think I handle most of them :)

To use the new control, you need to bring in the namespace containing the control, and then use XAML like this:


> &lt;this:ComboBox Name="ProductCategoryComboBox"
>                ItemsSource="{Binding Source={StaticResource ProductCategories},Path=Data}"
>                SelectedValue="{Binding Path=CategoryId, Mode=TwoWay}"
>                ValueMemberPath="Key"
>                DisplayMemberPath="Value"/&gt;


At least in my code, you *must* set the ValueMemberPath, though I’m sure the code could be enhanced to avoid that requirement. The bigger thing is that the SelectedValue binding *must* have Mode=TwoWay or the binding won’t work reliably. Even if you are using the ComboBox for display-only purposes, the Mode must be TwoWay.

Also I should point out that this XAML is using the CslaDataProvider control to get the data for the ItemsSource property. You could use other techniques as well, but I like the data provider model because it shifts all the work into XAML, so there’s no code required in the presentation layer. The ProductCategories resource is a CslaDataProvider control that retrieves a NameValueListBase object containing a list of items with Key and Value properties.

Here’s the control code:


> public class ComboBox : System.Windows.Controls.ComboBox
> {
>   public ComboBox()
>   {
>     this.Loaded += new RoutedEventHandler(ComboBox\_Loaded);
>     this.SelectionChanged += new SelectionChangedEventHandler(ComboBox\_SelectionChanged);
>   }
>
> void ComboBox\_Loaded(object sender, RoutedEventArgs e)
>   {
>     SetSelectionFromValue();
>   }
>
> private object \_selection;
>
> void ComboBox\_SelectionChanged(object sender, SelectionChangedEventArgs e)
>   {
>     if (e.AddedItems.Count &gt; 0)
>     {
>       \_selection = e.AddedItems[0];
>       SelectedValue = GetMemberValue(\_selection);
>     }
>     else
>     {
>       \_selection = null;
>       SelectedValue = null;
>     }
>   }
>
> private object GetMemberValue(object item)
>   {
>     return item.GetType().GetProperty(ValueMemberPath).GetValue(item, null);
>   }
>
> public static DependencyProperty ValueMemberPathProperty =
>     DependencyProperty.Register("ValueMemberPath", typeof(string), typeof(InventoryDemo.ComboBox), null);
>
> public string ValueMemberPath
>   {
>     get
>     {
>       return ((string)(base.GetValue(ComboBox.ValueMemberPathProperty)));
>     }
>     set
>     {
>       base.SetValue(ComboBox.ValueMemberPathProperty, value);
>     }
>   }
>
> public static DependencyProperty SelectedValueProperty =
>     DependencyProperty.Register("SelectedValue", typeof(object), typeof(InventoryDemo.ComboBox),
>     new PropertyMetadata((o, e) =&gt;
>     {
>       ((ComboBox)o).SetSelectionFromValue();
>     }));
>
> public object SelectedValue
>   {
>     get
>     {
>       return ((object)(base.GetValue(ComboBox.SelectedValueProperty)));
>     }
>     set
>     {
>       base.SetValue(ComboBox.SelectedValueProperty, value);
>     }
>   }
>
> private void SetSelectionFromValue()
>   {
>     var value = SelectedValue;
>     if (Items.Count &gt; 0 && value != null)
>     {
>       var sel = (from item in Items
>                  where GetMemberValue(item).Equals(value)
>                  select item).Single();
>       \_selection = sel;
>       SelectedItem = sel;
>     }
>   }
>
> protected override void OnItemsChanged(System.Collections.Specialized.NotifyCollectionChangedEventArgs e)
>   {
>     base.OnItemsChanged(e);
>     SetSelectionFromValue();
>   }
> }


It seems strange that the standard control doesn’t just do the right thing – but we must live in the world that is, not the world we would like to see…
