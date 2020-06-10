---
title: "How to: Write Queries with Complex Filtering"
ms.date: 07/20/2015
ms.assetid: bf286ffc-7990-4b00-a4eb-ee3d70129950
---
# How to: Write Queries with Complex Filtering (Visual Basic)
Sometimes you want to write LINQ to XML queries with complex filters. For example, you might have to find all elements that have a child element with a particular name and value. This topic gives an example of writing a query with complex filtering.  
  
## Example  
 This example shows how to find all `PurchaseOrder` elements that have a child `Address` element that has a `Type` attribute equal to "Shipping" and a child `State` element equal to "NY". It uses a nested query in the `Where` clause, and the `Any` operator returns `True` if the collection has any elements in it.  
  
 This example uses the following XML document: [Sample XML File: Multiple Purchase Orders (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
 For more information about the `Any` operator, see [Quantifier Operations (Visual Basic)](quantifier-operations.md).  
  
```vb  
Dim root As XElement = XElement.Load("PurchaseOrders.xml")  
Dim purchaseOrders As IEnumerable(Of XElement) = _  
    From el In root.<PurchaseOrder> _  
    Where _  
        (From add In el.<Address> _  
        Where _  
             add.@Type = "Shipping" And _  
             add.<State>.Value = "NY" _  
        Select add) _  
    .Any() _  
    Select el  
For Each el As XElement In purchaseOrders  
    Console.WriteLine(el.@PurchaseOrderNumber)  
Next  
```  
  
 This code produces the following output:  
  
```console  
99505  
```  
  
## Example  
 The following example shows the same query for XML that is in a namespace. For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).  
  
 This example uses the following XML document: [Sample XML File: Multiple Purchase Orders in a Namespace](sample-xml-file-multiple-purchase-orders-in-a-namespace.md).  
  
```vb  
Imports <xmlns:aw='http://www.adventure-works.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("PurchaseOrdersInNamespace.xml")  
        Dim purchaseOrders As IEnumerable(Of XElement) = _  
            From el In root.<aw:PurchaseOrder> _  
            Where _  
                (From add In el.<aw:Address> _  
                Where _  
                     add.@aw:Type = "Shipping" And _  
                     add.<aw:State>.Value = "NY" _  
                Select add) _  
            .Any() _  
            Select el  
        For Each el As XElement In purchaseOrders  
            Console.WriteLine(el.@aw:PurchaseOrderNumber)  
        Next  
    End Sub  
End Module  
```  
  
 This code produces the following output:  
  
```console  
99505  
```  
  
## See also

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [Basic Queries (LINQ to XML) (Visual Basic)](basic-queries-linq-to-xml.md)
- [XML Child Axis Property](../../../language-reference/xml-axis/xml-child-axis-property.md)
- [XML Attribute Axis Property](../../../language-reference/xml-axis/xml-attribute-axis-property.md)
- [XML Value Property](../../../language-reference/xml-axis/xml-value-property.md)
- [Projection Operations (Visual Basic)](projection-operations.md)
- [Quantifier Operations (Visual Basic)](quantifier-operations.md)