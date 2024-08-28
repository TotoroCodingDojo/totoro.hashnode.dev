---
title: "Practical XML Manipulation with Groovy: Common Examples"
datePublished: Thu Aug 01 2024 09:17:04 GMT+0000 (Coordinated Universal Time)
cuid: clzb2axhf000109mnbgts6kkm
slug: practical-xml-manipulation-with-groovy-common-examples
tags: xml, groovy

---

## Introduction

To parse xml in groovy there are two options available

* `XmlParser` which returns a `Node` objects when parsing XML
    
* `XmlSlurper` which returns `GPathResult` instances when parsing XML. It evaluates the structure lazily. So if you update the xml you’ll have to evaluate the whole tree again.
    

When to use which one:

* **If you want to transform an existing document to another** then `XmlSlurper` will be the choice
    
* **If you want to update and read at the same time** then `XmlParser` is the choice.
    

Read more here - [https://groovy-lang.org/processing-xml.html](https://groovy-lang.org/processing-xml.html)

## Examples

### Copying a complete XML inside another XML node

* You have a xml and you want a **part** (it may consist nested nodes) **of that xml** inside some other xml structure you created.
    

You can get that part of xml using `XmlParser` as a `GPath` and then use the code given below.

```java
import groovy.xml.MarkupBuilder
import groovy.xml.XmlUtil

xml = '''
<records>
  <car name='HSV Maloo' make='Holden' year='2006'>
    <country>Australia</country>
    <record type='speed'>Production Pickup Truck with speed of 271kph</record>
  </car>
  <car name='P50' make='Peel' year='1962'>
    <country>Isle of Man</country>
    <record type='size'>Smallest Street-Legal Car at 99cm wide and 59 kg in weight</record>
  </car>
  <car name='Royale' make='Bugatti' year='1931'>
    <country>France</country>
    <record type='price'>Most Valuable Car at $15 million</record>
  </car>
</records>
'''

// records is a groovy.util.NodeList
def records = new XmlParser(false, false).parseText(xml).car
def writer = new StringWriter()
def xmlBuilder = new MarkupBuilder(writer)
xmlBuilder.mkp.xmlDeclaration(version: '1.0', encoding: 'UTF-8') // add xml declaration

xmlBuilder.'car-records'('id': '1') {
    // since we are using NodeList we have to iterate
    // in case it is Node you can directly use, mkp.yieldUnescaped()
    records.forEach { child ->
        mkp.yieldUnescaped(XmlUtil.serialize(child).replaceFirst(/<\?xml.*\?>/, ''))
    }
}

println(writer.toString())
```

In case there are you don't want to insert one but child elements of a particular element you can utilize this code snippet:

```java
import groovy.xml.MarkupBuilder
import groovy.xml.XmlUtil

xml = '''
<records>
  <car name='HSV Maloo' make='Holden' year='2006'>
    <country>Australia</country>
    <record type='speed'>Production Pickup Truck with speed of 271kph</record>
  </car>
  <car name='P50' make='Peel' year='1962'>
    <country>Isle of Man</country>
    <record type='size'>Smallest Street-Legal Car at 99cm wide and 59 kg in weight</record>
  </car>
  <car name='Royale' make='Bugatti' year='1931'>
    <country>France</country>
    <record type='price'>Most Valuable Car at $15 million</record>
  </car>
</records>
'''

def records = new XmlSlurper(false, false).parseText(xml).car
def writer = new StringWriter()
def xmlBuilder = new MarkupBuilder(writer)
xmlBuilder.mkp.xmlDeclaration(version: '1.0', encoding: 'UTF-8') // add xml declaration

xmlBuilder.'car-records'('id': '1') {
    records.forEach { child ->
        mkp.yieldUnescaped(XmlUtil.serialize(child).replaceFirst(/<\?xml.*\?>/, ''))
    }
}

println(writer.toString())
```

...more examples to come