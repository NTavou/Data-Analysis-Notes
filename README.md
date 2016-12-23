# Data Analysis Notes

##Index

1. [Parsing XML in Python](#parsing-xml-in-python)
	- [Very short Intro on XML](#very-short-intro-on-xml)
	- [Few words about XPath](#few-words-about-xpath)
	- [XML parsing using Python](#xml-parsing-using-python)  


2. [Using Regular Expressions in Python](#using-regular-expressions-in-python)

<a name="parsing-xml-in-python"></a>
## Parsing XML in Python 
<a name="very-short-intro-on-xml"></a>
###Very short Intro on XML 

Sources: [www.w3schools](http://www.w3schools.com/xml/default.asp), [xml.silmaril.ie/](http://xml.silmaril.ie/)

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
<a name="few-words-about-xpath"></a>
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
<a name="xml-parsing-using-python"></a>
###XML parsing using Python

Source: [xml.etree.ElementTree ](https://docs.python.org/2/library/xml.etree.elementtree.html)




Using the following XML document as our sample data:


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

As an Element, root has a **tag** and **a dictionary of attributes**:
	
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


**text** or **tail** are attributes that can be used to hold additional data associated with the element. Their values are usually strings but may be any application-specific object.

We can use  **find(match)**  to find the first subelement matching match (match may be a tag name or path). Returns an element instance or None.


    >>> root.find('./country/rank').text
    '1'

    >>> root.find('./country/rank').attrib['name']
    'Liechtenstein'

But what if we wanted to find all the matching rank elements in our specific example? We can use **findall(match)** which finds all matching subelements, by tag name or path. It **returns a list** containing all matching elements in document order. So we need to iterate over the list to achieve the desired result:

    >>> my_findings = root.findall('./country/rank')
    >>> for my_finding in my_findings:
    ... print my_finding.text
    1
    4
    68

     >>> all_countries = root.findall('./country')
     >>> for attribute in all_countries:
    ...      print attribute.attrib['name']
	Liechtenstein
	Singapore
	Panama

It is possible to check all the Elements of our XML document along with its attributes (if any) by using the **iterparse** function:

    >>> for event,element in ET.iterparse('test.xml'):
    ...     print element.tag, element.attrib
    rank {}
    year {}
    gdppc {}
    neighbor {'direction': 'E', 'name': 'Austria'}
    neighbor {'direction': 'W', 'name': 'Switzerland'}
    country {'name': 'Liechtenstein'}
    rank {}
    year {}
    gdppc {}
    neighbor {'direction': 'N', 'name': 'Malaysia'}
    country {'name': 'Singapore'}
    rank {}
    year {}
    gdppc {}
    neighbor {'direction': 'W', 'name': 'Costa Rica'}
    neighbor {'direction': 'E', 'name': 'Colombia'}
    country {'name': 'Panama'}
    data {}




We can **iterate** recursively **over all the sub-tree** below an Element (its children, their children, and so on):

    >>> for neighbor in root.iter('neighbor'):
    ... print neighbor.attrib
    ...
    {'name': 'Austria', 'direction': 'E'}
    {'name': 'Switzerland', 'direction': 'W'}
    {'name': 'Malaysia', 'direction': 'N'}
    {'name': 'Costa Rica', 'direction': 'W'}
    {'name': 'Colombia', 'direction': 'E'}

In this case the element neighbor had two attributes: `name` and `direction`

----------
<a name="using-regular-expressions-in-python"></a>
## Using Regular Expressions in Python

Sources:   
[Learn Python the Hard Way](https://learnpythonthehardway.org/book/ex10.html),  
[Regular Expression HOWTO](https://docs.python.org/2/howto/regex.html),  
[Automate the Boring Stuff with Python](https://automatetheboringstuff.com/chapter7/),   
[re — Regular expression operations](https://docs.python.org/2/library/re.html)  

Before diving into regular expressions we need to have in mind the **escape sequences** that Python supports.

|Escape    | 	What it does  
|-------------  |-------------
| \\| Backslash (\) 
|\' | Single-quote (')
|\" | Double-quote (")
|\a	|ASCII bell (BEL)
|\b	|ASCII backspace (BS)
|\f	|ASCII formfeed (FF)
|\n	|ASCII linefeed (LF)
|\N{name}	|Character named name in the Unicode database (Unicode only)
|\r	|Carriage Return (CR)
|\t	|Horizontal Tab (TAB)
|\uxxxx	|Character with 16-bit hex value xxxx (u'' string only)
|\Uxxxxxxxx	|Character with 32-bit hex value xxxxxxxx (u'' string only)
|\v	|ASCII vertical tab (VT)
|\ooo|Character with octal value ooo
|\xhh|Character with hex value hh  


**Regular expressions** (called REs, or regexes, or regex patterns) are essentially a tiny, highly specialized programming language embedded inside Python and made available through the re module. Using this little language, you specify the rules for the set of possible strings that you want to match; this set might contain English sentences, or e-mail addresses, or TeX commands, or anything you like. You can then ask questions such as “Does this string match the pattern?”, or “Is there a match for the pattern anywhere in this string?”. You can also use REs to modify a string or to split it apart in various ways.

All the **regex** functions in Python are in the **re** module:

    >>> import re

As a first step we need to create a **Regex object** with the re.compile() function i.e.(find a phone number in a string with the pattern: three numbers, a hyphen, three numbers, a hyphen, and four numbers):
    
    >>> phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')

Pass the string you want to search into the Regex object’s **search() method**. This returns a Match object:

    >>> mo = phoneNumRegex.search('My number is 415-555-4242.')

The search() method will return None if the regex pattern is not found in the string. If the pattern is found, the search() method returns a **Match object**. In our case the pattern was found and a Match object was returned.

Call the Match object’s **group() method** to return a string of the actual matched text:

    >>> print('Phone number found: ' + mo.group())
    ... Phone number found: 415-555-4242 
 
Documentation about group:  
group([group1, ...]) 

Returns one or more subgroups of the match. If there is a single argument, the result is a single string; if there are multiple arguments, the result is a tuple with one item per argument. Without arguments, group1 defaults to zero (the whole match is returned)