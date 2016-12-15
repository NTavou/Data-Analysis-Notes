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

    <note> 
       <to>Myself</to> 
       <from>Myself</from> 
       <heading>Reminder</heading> 
       <body>Hopefully, these notes will provide a short quick reference about XML in the future</body> 
    </note>
`
If you want to view or display the above code (don't use the word run, check [here](http://xml.silmaril.ie/execute.html) why) you can use for example [this online XML editor](http://xmlgrid.net/).   

- XML documents form a [tree structure](http://www.w3schools.com/xml/xml_tree.asp) that starts at "the root" and branches to "the leaves". 
- An XML document [starts with](http://xml.silmaril.ie/internals.html) an optional **Prolog**, which can have two (optional) parts:
  
1.) The XML Declaration: 
 
    <?xml version="1.0" encoding="utf-8"?>  

2.) A Document Type Declaration:
  
    <!DOCTYPE report SYSTEM "http://sales.acme.corp/dtds/salesrep.dtd">  `  

which identifies the type of document (here, ‘report’) and says where the Document Type Description (DTD) is stored.

The Prolog is followed by the **Document Instance** which has:    

1.) A **root element**, which is the outermost (top level) element (start-tag plus end-tag) which encloses everything else. The root element is the **parent** of all other elements. An XML element is everything from (including) the element's start tag to (including) the element's end tag.

    <?xml version="1.0" standalone="yes"?>
    <conversation>
      <greeting>Hello, world!</greeting>
      <response>Stop the planet, I want to get off!</response>
    </conversation>

In the above lines of XML code ``<conversation>``  is the root element. 

 2.) A structured mix of descriptive or prescriptive **elements** enclosing the **character data content** (text), and optionally any **attributes** (‘name="value"’ pairs) inside some start-tags. 

  All elements can have sub elements (**child elements**):  

    <root>
      <child>
        <subchild>.....</subchild>
      </child>
    </root>



An element with no content is said to be empty:  
    
    <element></element>
  
or otherwise (called **self-closing tag**):  

    <element />

- Element names are case-sensitive, must start with a letter or underscore, cannot start with the letters xml (or XML, or Xml, etc), can contain letters, digits, hyphens, underscores, and periods but they cannot contain spaces.
- XML elements can be extended to carry more information.  

- XML elements can have **attributes**, just like HTML. **Attributes** are designed to **contain data related to a specific element**. Attribute values must always be quoted. 

Either single or double quotes can be used:  

    <person gender="female">   

or like this:  

    <person gender='female'>    

Keep in mind that attributes cannot contain multiple values, tree structures and they are not easily expandable

----------

###Few words about XPath

(Source: [www.w3schools](http://www.w3schools.com/xml/xpath_intro.asp))

XPath can be used **to navigate through elements and attributes** in an **XML** document.

- XPath uses path expressions to select nodes or node-sets in an XML document.

- These path expressions look very much like the expressions you use with a traditional computer file system

- In XPath, there are seven kinds of nodes: element, attribute, text, namespace, processing-instruction, comment, and document nodes.

- XML documents are treated as trees of nodes. 
    
- XPath **uses path expressions to select nodes** in an XML document. The node is selected by following a path or steps.

| Expression    | 	Description  
|-------------  |-------------
| nodename| Selects all nodes with the name "nodename" | 
| /| Selects from the root node
| //	        | Selects nodes in the document from the current node that match the selection no matter where they are
|.	           |Selects the current node
|..	|Selects the parent of the current node
|@	|Selects attributes


----------

###Parsing XML in Python

(Source: [https://www.python.org/](https://docs.python.org/2/library/xml.etree.elementtree.html))


Using the following XML document as the sample data:

    <?xml version="1.0"?>
    <data>
        <country name="Liechtenstein">
            <rank>1</rank>
            <year>2008</year>
            <gdppc>141100</gdppc>
            <neighbor name="Austria" direction="E"/>
            <neighbor name="Switzerland" direction="W"/>
      </country>
      <country name="Singapore">
            <rank>4</rank>
            <year>2011</year>
            <gdppc>59900</gdppc>
            <neighbor name="Malaysia" direction="N"/>
      </country>
      <country name="Panama">
            <rank>68</rank>
            <year>2011</year>
            <gdppc>13600</gdppc>
            <neighbor name="Costa Rica" direction="W"/>
            <neighbor name="Colombia" direction="E"/>
      </country>
    </data>

Importing the data:

    import xml.etree.ElementTree as ET
    import pprint

	tree = ET.parse('country_data.xml')
    root = tree.getroot()

As an Element, root has a tag and a dictionary of attributes:
	
	>>> print root.tag, root.attrib
	data {}

It also has children nodes over which we can iterate:
	
	>>> for child in root:
	...     print child.tag, child.attrib
	country {'name': 'Liechtenstein'}
	country {'name': 'Singapore'}
	country {'name': 'Panama'}
    
Children are nested, and we can **access** specific child nodes by **index**:	
	
	>>> root[0][0].text
	'1'
	
	>>> root[0][1].text
	'2008'

**Iterating** recursively **over all the sub-tree** below an Element (its children, their children, and so on):

    >>> for neighbor in root.iter('neighbor'):
    ... print neighbor.attrib
    ...
    {'name': 'Austria', 'direction': 'E'}
    {'name': 'Switzerland', 'direction': 'W'}
    {'name': 'Malaysia', 'direction': 'N'}
    {'name': 'Costa Rica', 'direction': 'W'}
    {'name': 'Colombia', 'direction': 'E'}

In this case the element neighbor had two attributes: `name` and `direction`  