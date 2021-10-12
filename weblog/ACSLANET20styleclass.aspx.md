---
title: A CSLA .NET 2.0 style class
postDate: 2005-10-06T15:18:16.281-05:00
abstract: A teaser showing the evolution of CSLA-style classes
postStatus: publish
---
06 October 2005

Here's a "basic" CSLA .NET 2.0 editable root class. It pretty much illustrates all the things you can do in a class under the upcoming version of the framework. In particular note the way validation rules are handled and all the transactional options in the DataPortal\_XYZ methods (presumably you'd pick one for your app :) ).

A CustomerTypes class is also included at the bottom, illustrating how to implement a name-value list that works with data binding.

Imports<font color="#000000"> CSLA<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&lt;Serializable()&gt; _<o:p></o:p></font>

Public<font color="#000000"> </font>Class<font color="#000000"> Customer<o:p></o:p></font>

<font color="#000000">&nbsp; </font>Inherits<font color="#000000"> BusinessBase(</font>Of<font color="#000000"> Customer)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Business Methods "<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> mID </font>As<font color="#000000"> </font>Integer<o:p></o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> mLastName </font>As<font color="#000000"> </font>String<font color="#000000"> = </font>""<o:p></o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> mFirstName </font>As<font color="#000000"> </font>String<font color="#000000"> = </font>""<o:p></o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> mLastActivity </font>As<font color="#000000"> SmartDate<o:p></o:p></font>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> mType </font>As<font color="#000000"> </font>Integer<o:p></o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> mCity </font>As<font color="#000000"> </font>String<font color="#000000"> = </font>""<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Shared<font color="#000000"> mCustomerTypes </font>As<font color="#000000"> CustomerTypes<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font><?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:place w:st="on"><st1:placename w:st="on"><span style="COLOR: blue">Public</span></st1:placename><font color="#000000"> </font><st1:placename w:st="on"><span style="COLOR: blue">Property</span></st1:placename><font color="#000000"> <st1:placetype w:st="on">City</st1:placetype></font></st1:place><font color="#000000">() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanReadProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mCity<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property read not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanWriteProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> </font>Not<font color="#000000"> mCity.Equals(value) </font>Then<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mCity = value<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged()<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property write not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Shared<font color="#000000"> </font>ReadOnly<font color="#000000"> </font>Property<font color="#000000"> CustomerTypes() </font>As<font color="#000000"> CustomerTypes<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> mCustomerTypes </font>Is<font color="#000000"> </font>Nothing<font color="#000000"> </font>Then<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mCustomerTypes = Library.CustomerTypes.GetCustomerTypes<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mCustomerTypes<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>ReadOnly<font color="#000000"> </font>Property<font color="#000000"> ID() </font>As<font color="#000000"> </font>Integer<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mID<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> LastName() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanReadProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mLastName<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property read not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanWriteProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> mLastName &lt;&gt; value </font>Then<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mLastName = value.ToUpper<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged()<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property write not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;</span></font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> FirstName() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanReadProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mFirstName<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property read not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanWriteProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> mFirstName &lt;&gt; value </font>Then<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mFirstName = value<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged()<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property write not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> LastActivity() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanReadProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mLastActivity.Text<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property read not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanWriteProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> mLastActivity &lt;&gt; value </font>Then<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mLastActivity.Text = value<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged()<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property write not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> CustomerType() </font>As<font color="#000000"> </font>Integer<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanReadProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mType<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property read not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>Integer<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanWriteProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> mType &lt;&gt; value </font>Then<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mType = value<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged()<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property write not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>ReadOnly<font color="#000000"> </font>Property<font color="#000000"> CustomerTypeText() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> CanReadProperty() </font>Then<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> CustomerTypes.Value(mType)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Else<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Throw<font color="#000000"> </font>New<font color="#000000"> System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"Property read not allowed"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Business Rules "<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> AddBusinessRules()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>AddRule(</font>AddressOf<font color="#000000"> Validation.CommonRules.StringRequired, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"FirstName"<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>AddRule(</font>AddressOf<font color="#000000"> Validation.CommonRules.StringRequired, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"LastName"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Object ID Value "<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Function<font color="#000000"> GetIdValue() </font>As<font color="#000000"> </font>Object<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mID<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Function<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Constructors "<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes">&nbsp; </span><span style="COLOR: blue">Private</span> <span style="COLOR: blue">Sub</span> <span style="COLOR: blue">New</span>()<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><o:p>&nbsp;</o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span><span style="COLOR: green">' don't allow a Guest to see or change city data<o:p></o:p></span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>AuthorizationRules.DenyRead(<span style="COLOR: maroon">"City"</span>, <span style="COLOR: maroon">"Guest"</span>)<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>AuthorizationRules.DenyWrite(<span style="COLOR: maroon">"City"</span>, <span style="COLOR: maroon">"Guest"</span>)<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><o:p>&nbsp;</o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes">&nbsp; </span><span style="COLOR: blue">End</span> <span style="COLOR: blue">Sub<o:p></o:p></span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"></p></font><o:p>&nbsp;</o:p>
<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Factory Methods "<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Shared<font color="#000000"> </font>Function<font color="#000000"> NewCustomer() </font>As<font color="#000000"> Customer<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> DataPortal.Create(</font>Of<font color="#000000"> Customer)(</font>Nothing<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Function<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Shared<font color="#000000"> </font>Function<font color="#000000"> GetCustomer(</font>ByVal<font color="#000000"> id </font>As<font color="#000000"> </font>Integer<font color="#000000">) </font>As<font color="#000000"> Customer<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> DataPortal.Fetch(</font>Of<font color="#000000"> Customer)(</font>New<font color="#000000"> Criteria(id))<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Function<o:p></o:p>

<o:p></o:p>
<o:p><p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: blue">Public</span><font color="#000000"> </font><span style="COLOR: blue">Shared</span><font color="#000000"> </font><span style="COLOR: blue">Sub </span><font color="#000000">DeleteCustomer(</font><span style="COLOR: blue">ByVal</span><font color="#000000"> id </font><span style="COLOR: blue">As</span><font color="#000000"> </font><span style="COLOR: blue">Integer</span><font color="#000000">) </font></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp;&nbsp;&nbsp; </font></span><font color="#000000">DataPortal.Delete</font><font color="#000000">(</font><span style="COLOR: blue">New</span><font color="#000000"> Criteria(id))<o:p></o:p></font></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: blue">End</span><font color="#000000"> </font><span style="COLOR: blue">Sub</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none">&nbsp;</p></o:p>
<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Criteria "<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>&lt;Serializable()&gt; _<o:p></o:p></font>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Class<font color="#000000"> Criteria<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Public<font color="#000000"> ID </font>As<font color="#000000"> </font>Integer<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Public<font color="#000000"> </font>Sub<font color="#000000"> </font>New<font color="#000000">(</font>ByVal<font color="#000000"> id </font>As<font color="#000000"> </font>Integer<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Me<font color="#000000">.ID = id<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Class<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Data Access "<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><span style="mso-spacerun: yes">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: green">'&nbsp;Forced to run on client</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="COLOR: green"></span></span>&nbsp; </p></span>&lt;RunLocal()&gt; _<o:p></o:p></font>
<font color="#000000">&nbsp; </font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_Create(</font>ByVal<font color="#000000"> criteria </font>As<font color="#000000"> </font>Object<font color="#000000">)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' get default values from db<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' we get here via DataPortal.Create()<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mID = </font>New<font color="#000000"> System.Random().Next(100, 999)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mType = CustomerTypes.DefaultKey<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>CheckRules()<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: green">'&nbsp;Runs on client or server based on DataPortal config</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none">&nbsp; </p></font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_Fetch(</font>ByVal<font color="#000000"> criteria </font>As<font color="#000000"> </font>Object<font color="#000000">)<o:p></o:p></font>
<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' get data from db<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' we get here via DataPortal.Fetch()<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Dim<font color="#000000"> crit </font>As<font color="#000000"> Criteria = </font>DirectCast<font color="#000000">(criteria, Criteria)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mID = crit.ID<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mType = CustomerTypes.Key(</font>"Hybrid"<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mLastName = </font>"Lhotka"<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mFirstName = </font>"Rocky"<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>CheckRules()<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><span style="mso-spacerun: yes">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: green">'&nbsp;COM+&nbsp;transactions</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="COLOR: green"></span></span>&nbsp; </p></span>&lt;Transactional()&gt; _<o:p></o:p></font>
<font color="#000000">&nbsp; </font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_Insert()<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' insert data into db<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' we get here via obj.Save()<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: green">'&nbsp;System.Transactions namespace</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none">&nbsp; </p></font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_Update()<o:p></o:p></font>
<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' update data in db<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' we get here via obj.Save()<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Using<font color="#000000"> tr </font>As<font color="#000000"> </font>New<font color="#000000"> System.Transactions.TransactionScope<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>' do updates<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>tr.Complete()<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Using<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: green">'&nbsp;ADO.NET transactions</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none">&nbsp; </p></font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_DeleteSelf()<o:p></o:p></font>
<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' do deferred delete of self<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' we get here via obj.Save()<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Using<font color="#000000"> cn </font>As<font color="#000000"> </font>New<font color="#000000"> SqlClient.SqlConnection<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Using<font color="#000000"> tr </font>As<font color="#000000"> SqlClient.SqlTransaction = cn.BeginTransaction<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>' do delete<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Using<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Using<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>
<font color="#000000"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'; mso-no-proof: yes"><span style="mso-spacerun: yes"><font color="#000000">&nbsp; </font></span><span style="COLOR: green">'&nbsp;No transactions</span></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none">&nbsp; </p></font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_Delete(</font>ByVal<font color="#000000"> criteria </font>As<font color="#000000"> </font>Object<font color="#000000">)<o:p></o:p></font>
<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Dim<font color="#000000"> crit </font>As<font color="#000000"> Criteria = </font>DirectCast<font color="#000000">(criteria, Criteria)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' do immediate delete based on criteria<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>' we get here via DataPortal.Delete()<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

End<font color="#000000"> </font>Class<o:p></o:p>

<o:p><font face="Times New Roman" color="#000000">&nbsp;</font></o:p>



======================================================



Imports<font color="#000000"> CSLA<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

Public<font color="#000000"> </font>Class<font color="#000000"> CustomerTypes<o:p></o:p></font>

<font color="#000000">&nbsp; </font>Inherits<font color="#000000"> NameValueListBase(</font>Of<font color="#000000"> </font>Integer<font color="#000000">, </font>String<font color="#000000">)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Function<font color="#000000"> DefaultKey() </font>As<font color="#000000"> </font>Integer<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> 1<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Function<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Function<font color="#000000"> DefaultValue() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> Value(DefaultKey)<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Function<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Sub<font color="#000000"> </font>New<font color="#000000">()<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Shared<font color="#000000"> </font>Function<font color="#000000"> GetCustomerTypes() </font>As<font color="#000000"> CustomerTypes<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> DataPortal.Fetch(</font>Of<font color="#000000"> CustomerTypes) _</font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (</font>New<font color="#000000"> Criteria(</font>GetType<font color="#000000">(CustomerTypes)))<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Function<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Protected<font color="#000000"> </font>Overrides<font color="#000000"> </font>Sub<font color="#000000"> DataPortal_Fetch(</font>ByVal<font color="#000000"> criteria </font>As<font color="#000000"> </font>Object<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Me<font color="#000000">.IsReadOnly = </font>False<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Add(</font>New<font color="#000000"> NameValuePair(1, </font>"Domestic"<font color="#000000">))<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Add(</font>New<font color="#000000"> NameValuePair(2, </font>"International"<font color="#000000">))<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Add(</font>New<font color="#000000"> NameValuePair(3, </font>"Hybrid"<font color="#000000">))<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Me<font color="#000000">.IsReadOnly = </font>True<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

End<font color="#000000"> </font>Class<o:p></o:p>


