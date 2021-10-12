---
title: Leveraging data annotation attributes in CSLA .NET
postDate: 2009-10-05T12:06:45.0728817-05:00
abstract: 
postStatus: publish
---
05 October 2009

One of the new features in CSLA .NET 3.8 is the ability to use the data annotation attributes from System.ComponentModel.DataAnnotations.

The DataAnnotations namespace was added in .NET 3.5 SP1, and includes a ValidationAttribute class that acts as the base class for validation attributes. An example of a validation attribute is Required, which is used to indicate that a property is a required value.

DataAnnotations are available in both .NET and Silverlight, though it turns out that their implementations aren’t quite the same. Still, their *usage* is the same, in that you decorate properties with data annotation attributes.

The idea behind DataAnnotations is that they are UI independent. If you put a Required attribute on a property, and then you build a UI using a technology that understands these ValidationAttribute subclasses, the UI will honor the attribute. The Silverlight DataForm is one example of a UI technology that does understand these attributes, and I suspect we’ll see many more UI technologies start to leverage them.

What’s interesting about this, is that the attribute object itself contains the validation rule logic. So the UI doesn’t actually implement the Required rule logic – it just asks the attribute object to do the evaluation. This is where things aren’t the same on .NET and Silverlight. On .NET ValidationAttribute subclasses override IsValid(), returning true if the rule is satisfied, false if not. On Silverlight ValidationAttribute subclasses override GetValidationResult() which returns null if the rule is satisfied, and a result object if the rule is broken. Either way the basic concept is the same, but the implementation code is different.

I wanted to support these attributes in CSLA .NET (for Windows and Silverlight). This is really a two-part process.

First, I needed to have a way to detect the attribute on a property, and attach a CSLA validation rule to that property so CSLA knows to execute the attribute’s rule when appropriate. CSLA .NET already has a business/validation rule subsystem that knows how to execute rules – I just needed to auto-add rules for data annotation attributes.

Second, I needed a way to execute any ValidationAttribute subclass, since that’s how one of these rules is evaluated. Again, CSLA .NET already has a validation rule subsystem that says validation rules are methods. So I just needed to create a CSLA-style rule method that knows how to invoke a ValidationAttribute to actually evaluate the rule’s condition.

I added a ValidationRules.AddDataAnnotations() method that you can call in your AddBusinessRules() override. This method reflects against your properties, detects any ValidationAttribute subclasses on any of your properties and adds a CSLA-style rule to link that property to the rule attribute. I also changed BusinessBase.AddBusinessRules() (this is the base method) so AddDataAnnotations() is called if you don’t override AddBusinessRules() – effectively making the use of data annotation attributes a default behavior.

Then I created a Csla.Validation.CommonRules.DataAnnotation() rule method. This is the rule method that is automatically associated with properties by AddDataAnnotations(). The DataAnnotation() rule method is pretty simple – it just executes the attribute object’s IsValid() or GetValidationResults() methods (depending on whether the code is running on .NET or Silverlight).

The end result is that when using CSLA .NET 3.8 you can apply data annotation attributes to your business class properties, and (assuming AddDataAnnotations() is called) they’ll be automatically linked into the normal CSLA .NET validation subsystem and executed like any other CSLA .NET business or validation rules.


> [Serializable]
> public class Data : BusinessBase&lt;Data&gt;
> {
>   private static PropertyInfo&lt;int&gt; IdProperty =
>     RegisterProperty&lt;int&gt;(c =&gt; c.Id);
>   [Range(0, 10, ErrorMessage = "Id must be between 0 and 10")]
>   public int Id
>   {
>     get { return GetProperty(IdProperty); }
>     set { SetProperty(IdProperty, value); }
>   }
>
> private static PropertyInfo&lt;string&gt; NameProperty =
>     RegisterProperty&lt;string&gt;(c =&gt; c.Name);
>   [Required(ErrorMessage = "Name is required")]
>   public string Name
>   {
>     get { return GetProperty(NameProperty); }
>     set { SetProperty(NameProperty, value); }
>   }
> }


Notice that this class doesn’t override AddBusinessRules(), so the base implementation is used, and the base implementation calls ValidationRules.AddDataAnnotations().

When AddDataAnnotations() is called, it detects the Range and Required attributes on the properties, and those attributes are automatically linked into the normal CSLA .NET business rule subsystem. This means the rules are automatically checked when a new instance of the object is created, and any time the property values are set – exactly the behavior you’d get with regular CSLA .NET rule methods.

But what’s nice about this is that these attributes are also honored by some UI technologies (like DataForm). This means that you automatically get the UI behaviors (if any) and yet you *know* that the rules will be run in the business layer regardless of whether the UI honors the attributes or not.

So this object will work nicely in the Silverlight DataForm, and will have the same business behavior in Windows Forms, behind a WCF service or anywhere else the object is used – even if the UI technology doesn’t honor the attributes.

You can also use this approach to create your own validation attributes by subclassing the ValidationAttribute base class in System.ComponentModel.DataAnnotations.

The only limitation I’ve found is that these attribute-based rules can only operate on a single property value. You can’t use this technique to do multi-property rules, or rules that operate on child collections or across other objects. You’ll need to use the normal CSLA .NET business/validation rule method approach to implement anything beyond simple single-property rules.
