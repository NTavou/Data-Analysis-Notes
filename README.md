# Data Analysis Notes
## My Notes on XML
(Based on multiple sources:  
[www.w3schools](http://www.w3schools.com/xml/default.asp), [xml.silmaril.ie/](http://xml.silmaril.ie/))

[XML](https://en.wikipedia.org/wiki/XML) stands for eXtensible Markup Language




- XML was designed to **carry data** - with focus on what data is.  
    HTML was designed to display data - with focus on how data looks.  



- XML tags are not predefined like HTML tags are. XML is just information wrapped in tags.  



- With XML, the author must define **both** the **tags** and the **document structure**.



- XML stores data in plain text format. This provides a software- and hardware-independent way of storing, transporting, and sharing data.

An example of XML code:

``<note\>``  
&nbsp;&nbsp;``<to\>Myself</to\>``  
&nbsp;&nbsp;``<from\>Myself</from\>``  
&nbsp;&nbsp;``<heading\>Hopefully, these notes will provide a short quick reference about XML in the future</heading\>``   
``</note\>``

If you want to view or display the above code (don't use the word run, check [here](http://xml.silmaril.ie/execute.html) why) you can use for example [this online XML editor](http://xmlgrid.net/).   



- XML documents form a [tree structure](http://www.w3schools.com/xml/xml_tree.asp) that starts at "the root" and branches to "the leaves". 
- An XML document [starts with](http://xml.silmaril.ie/internals.html) an optional **Prolog**, which can have two (optional) parts:
  
1.) The XML Declaration:  
``<?xml version="1.0" encoding="utf-8"?>``  

2.) A Document Type Declaration: 
``<!DOCTYPE report SYSTEM "http://sales.acme.corp/dtds/salesrep.dtd">``  
which identifies the type of document (here, ‘report’) and says where the Document Type Description (DTD) is stored;

The Prolog is followed by the **Document Instance** which has:  
1.) A **root element**, which is the outermost (top level) element (start-tag plus end-tag) which encloses everything else

``<?xml version="1.0" standalone="yes"?>``  
``<conversation>`` *<-- The root element*  
&nbsp;&nbsp;``<greeting>Hello, world!</greeting>``  
&nbsp;&nbsp;``<response>Stop the planet, I want to get off!</response>``  
``</conversation>`` *<-- The root element* 

 2.) A structured mix of descriptive or prescriptive **elements** enclosing the **character data content** (text), and optionally any **attributes** (‘name="value"’ pairs) inside some start-tags.






On a side note if you want to present XML code in a markdown format check these questions/answers in stackoverflow:  
[How do I ensure that whitespace is preserved in Markdown?](http://stackoverflow.com/questions/15721373/how-do-i-ensure-that-whitespace-is-preserved-in-markdown) 

Other Sources:

[Official XML Origin and Goals](https://www.w3.org/TR/xml/#sec-origin-goals)

