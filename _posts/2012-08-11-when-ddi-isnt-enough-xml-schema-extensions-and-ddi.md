---
id: 547
title: 'When DDI isn&#8217;t enough Part 1 &#8211; XML Schema Extensions and DDI'
date: 2012-08-11T00:12:54+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=547
permalink: /2012/08/when-ddi-isnt-enough-xml-schema-extensions-and-ddi/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Metadata
  - Programming
tags:
  - DDI
  - DDIX
  - "I'll make my own specification with blackjack..."
  - SQDX
  - XML Schema
---
No standard is perfect &#8211; in fact the DDI specification made this quite clear through the inclusion of the &#8216;[Note](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/reusable_xsd/elements/Note.html "DDI Note Element")&#8216; object to support extensions and to hold additional information. However, DDI Notes are usually seen as a mechanism of last resort for describing structured content as they are by their very nature _un_structured. There is however an intermediate solution between the implementation of Notes and leaving out vital information or using less optimal modeling to document everything. The way that I&#8217;ll demonstrate here is through the use of XML Schema substitution groups.

From the [XML Schema Documentation on substitution groups](http://www.w3.org/TR/2001/REC-xmlschema-0-20010502/#SubsGroups):

> XML Schema provides a mechanism, called substitution groups, that allows elements to be substituted for other elements. More specifically, elements can be assigned to a special group of elements that are said to be substitutable for a particular named element called the head element.

In essense, this allows for a schema designer to specific what classes of element can validly exist within an XML tree, before designing more complex child elements. Similarly, it allows for extensibility by third-party designers.

Within DDI Lifecycle there are a number of Substitution groups that can support these kinds of extensions.

For example, the [ControlConstruct](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/ControlConstruct.html) and [ControlConstructScheme](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/ControlConstructScheme.html) are used in this manner to support the inclusion of complex questionnaire logic.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:complexType</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"ControlConstructSchemeType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>A set of control constructs maintained by an agency, and used in the instrument. <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:complexContent<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:extension</span> <span style="color: #000066;">base</span>=<span style="color: #ff0000;">"r:MaintainableType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:sequence<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #808080; font-style: italic;">&lt;!-- Elements removed --&gt;</span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">ref</span>=<span style="color: #ff0000;">"ControlConstruct"</span> <span style="color: #000066;">maxOccurs</span>=<span style="color: #ff0000;">"unbounded"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #808080; font-style: italic;">&lt;!-- Elements removed --&gt;</span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:element<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:sequence<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:extension<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:complexContent<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:complexType<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"ControlConstruct"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"ControlConstructType"</span> <span style="color: #000066;">abstract</span>=<span style="color: #ff0000;">"true"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #808080; font-style: italic;">&lt;!-- Elements removed --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:element<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"IfThenElse"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"IfThenElseType"</span> <span style="color: #000066;">substitutionGroup</span>=<span style="color: #ff0000;">"ControlConstruct"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span></pre>
      </td>
    </tr>
  </table>
</div>

Here the ControlConstructScheme declares the existance of a ControlConstruct child element, while the ControlConstruct acts as the Head Element for the substitution group by declaring it to be an abstract, which supports the declaration of the [IfThenElse](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/IfThenElse.html) element as a part of this substitution group.

To extend this we can create a new element, and declare it as an extension of the ControlConstruct, to support a new metadata object. A trivial example is below:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"Foo"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"FooType"</span> <span style="color: #000066;">substitutionGroup</span>=<span style="color: #ff0000;">"d:ControlConstruct"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:complexType</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"FooType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:complexContent<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:extension</span> <span style="color: #000066;">base</span>=<span style="color: #ff0000;">"d:ControlConstructType"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:complexContent<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:complexType<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Here the Foo Element is defined as a part of the ControlConstruct group, of the complex FooType, which has ComplexContent based on the [ControlConstructType](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/complexTypes/ControlConstructType.html) as defined in the head element. Provided that the XSD that defined this new element was included correctly within the final DDI Instance, this would be valid DDI 3.1 XML. This means that the following fragment with the correct imported schemas would validate as DDI:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:ControlConstructScheme</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">"FooBar"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;sqdx:Foo</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">"Bar"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:ControlConstructScheme<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

Now, lets look at this in practice. The [ConditionalText](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/ConditionalText.html) element in DDI is used to document the existence of dynamic text in a survey instrument &#8211; be it as part of a question, statement or instruction. A conditional text exists as a part of the substitution group Text in the [DataCollection](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/namespaces/ddi_datacollection_3_1/namespace-summary.html) Module. One issue with this element as it exists, is although it defines how it should display the dynamic text, there is no declaration of what the default text may be, or what to display in a static environment. We can however, improve this through the creation of an extension of this using the above techniques, as shown below.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"ExtendedConditionalText"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"ExtendedConditionalTextType"</span> <span style="color: #000066;">substitutionGroup</span>=<span style="color: #ff0000;">"d:Text"</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:complexType</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"ExtendedConditionalTextType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Text which has a changeable value, based on a condition expressed in Code. This is an extension of the standard DDI ConditionalText in the DataCollection Module, that provides support for default values for conditional text and text for static environments.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:complexContent<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:extension</span> <span style="color: #000066;">base</span>=<span style="color: #ff0000;">"d:ConditionalTextType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:sequence<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"Default"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"r:StructuredStringType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>The text to display prior to a dynamic change of text in an electronic environment.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:element<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:element</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"Static"</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">"r:StructuredStringType"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>The text to display when dynamic changes of text are not available. For example, on paper forms or non-dynamic electronic forms - such as javascript less environments.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:documentation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:annotation<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:element<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:sequence<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:extension<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:complexContent<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/xs:complexType<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

In the above XML fragement, the ExtendedConditionalText is defined as an extension of the standard DDI [ConditionalTextType](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/complexTypes/ConditionalTextType.html), with additional elements defined as necessary.

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:QuestionText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:LiteralText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:Text<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You told me your dog likes to play fetch, what does <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:Text<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:LiteralText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;sqdx:ExtendedConditionalText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;r:Code</span> <span style="color: #000066;">programmingLanguage</span>=<span style="color: #ff0000;">"Pseudocode"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>if sex == 'Male' {return 'he'} else if sex == 'Female' {return 'she'} else {return 'they'}<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/r:Code<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:Expression<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;sqdx:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>...<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/sqdx:Default<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;sqdx:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>he/she<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/sqdx:Static<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/sqdx:ExtendedConditionalText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/d:QuestionText<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre>
      </td>
    </tr>
  </table>
</div>

This use of XML Schema extensions then means, that not only is the data ctructure properly defined and sharable using standard XML technologies, it also provides an easy way for defining possible advancements for future versions of the standard.

So, where can these extensions be used in DDI &#8211; here is a list of some of the substitution groups that exist in DDI 3.1:

  * [BaseLogicalProduct](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/logicalproduct_xsd/elements/BaseLogicalProduct.html)
  * [ValueRepresentation](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/logicalproduct_xsd/elements/ValueRepresentation.html) (Base of ResponseDomains, Variables, etc&#8230;)
  * [BaseRecordLayout](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/physicaldataproduct_xsd/elements/BaseRecordLayout.html)
  * [ControlConstruct](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/ControlConstruct.html)
  * [d:Text](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/Text.html) (only in the data collection module)
  * [ResponseDomain](http://www.ddialliance.org/sites/default/files/documentation/ddi3.1/schemas/datacollection_xsd/elements/ResponseDomain.html)

So where any of these substitution groups exist, a newly defined object could take their place. However, there are a few place where substitution groups would be advantages for future versions, the two main ones being a substitution group for Questions for incusion in QuestionSchemes, and as a replace for the reusable Code element to allow for more defined, system-independant and reusable logic within DDI.

Lastly, the [example Schema for the above ExtendedConditionalText is available on Pastebin](http://pastebin.com/0QiLAh4t), with a more indepth example showing how a Case/Switch control construct could be created to define higher-order questionnaire logic.
  
There is also an [example DDI instance on Pastebin that has concrete examples of all of the extensions](http://pastebin.com/srn4SXfr) listed.