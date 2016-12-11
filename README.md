# Data Analysis Notes
## My Notes on XML

###Very short Intro on XML

(Sources: [www.w3schools](http://www.w3schools.com/xml/default.asp), [xml.silmaril.ie/](http://xml.silmaril.ie/))

[XML](https://en.wikipedia.org/wiki/XML) stands for eXtensible Markup Language




- XML was designed to **carry data** - with focus on what data is.  
    (On the other hand,  HTML was designed to display data - with focus on how data looks.)  



- XML tags are not predefined like HTML tags are. XML is just information wrapped in tags.  



- With XML, the author must define **both** the **tags** and the **document structure**.



- XML stores data in plain text format. This provides a software- and hardware-independent way of storing, transporting, and sharing data.

An example of XML code:

``<note>``  
&nbsp;&nbsp;``<to>Myself</to>``  
&nbsp;&nbsp;``<from>Myself</from>``  
&nbsp;&nbsp;``<heading>Hopefully, these notes will provide a short quick reference about XML in the future</heading>``   
``</note>``

If you want to view or display the above code (don't use the word run, check [here](http://xml.silmaril.ie/execute.html) why) you can use for example [this online XML editor](http://xmlgrid.net/).   



- XML documents form a [tree structure](http://www.w3schools.com/xml/xml_tree.asp) that starts at "the root" and branches to "the leaves". 
- An XML document [starts with](http://xml.silmaril.ie/internals.html) an optional **Prolog**, which can have two (optional) parts:
  
1.) The XML Declaration:  
``<?xml version="1.0" encoding="utf-8"?>``  

2.) A Document Type Declaration:  
``<!DOCTYPE report SYSTEM "http://sales.acme.corp/dtds/salesrep.dtd">``    

which identifies the type of document (here, ‘report’) and says where the Document Type Description (DTD) is stored.

The Prolog is followed by the **Document Instance** which has:    

1.) A **root element**, which is the outermost (top level) element (start-tag plus end-tag) which encloses everything else. The root element is the **parent** of all other elements. An XML element is everything from (including) the element's start tag to (including) the element's end tag.

``<?xml version="1.0" encoding="utf-8"?>``  
``<!DOCTYPE report SYSTEM "http://sales.acme.corp/dtds/salesrep.dtd">``   
``<conversation>``  
&nbsp;&nbsp;``<greeting>Hello, world!</greeting>``  
&nbsp;&nbsp;``<response>Stop the planet, I want to get off!</response>``  
``</conversation>``  

In the above lines of XML code ``<conversation>``  is the root element. 

 2.) A structured mix of descriptive or prescriptive **elements** enclosing the **character data content** (text), and optionally any **attributes** (‘name="value"’ pairs) inside some start-tags. 

- All elements can have sub elements (**child elements**)  
``<root>``  
&nbsp;&nbsp;``<child>``  
&nbsp;&nbsp;&nbsp;&nbsp;``<subchild>.....</subchild>``  
&nbsp;&nbsp;``</child>``  
``</root>``  


- An element with no content is said to be empty:  
`<element></element>`  
or otherwise (called **self-closing tag**):  
`<element />`

- Element names are case-sensitive, must start with a letter or underscore, cannot start with the letters xml (or XML, or Xml, etc), can contain letters, digits, hyphens, underscores, and periods but they cannot contain spaces.
- XML elements can be extended to carry more information.  

- XML elements can have **attributes**, just like HTML. **Attributes** are designed to **contain data related to a specific element**. Attribute values must always be quoted. Either single or double quotes can be used:  

    `<person gender="female">`   

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;or like this:  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<person gender='female'>`    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Keep in mind that attributes cannot contain multiple values, tree structures and they are not easily expandable
