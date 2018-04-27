---
title: "Optimize Property--Dynamic (ADO)"
 
 
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
ms.topic: reference
  
localization_priority: Normal
ms.assetid: 2253b052-2d8a-f6f0-f8b8-f56e79d243de

---

# Optimize Property--Dynamic (ADO)

Specifies whether an index should be created on a field.
  
## Settings and Return Values

Sets or returns a **Boolean** value that indicates whether an index should be created. 
  
## Remarks

An index can improve the performance of operations that find or sort values in a [Recordset](recordset-object-ado.md). The index is internal to ADO — you cannot explicitly access or use it in your application.
  
To create an index on a field, set the **Optimize** property to **True**. To delete the index, set this property to **False**. 
  
 **Optimize** is a dynamic property appended to the [Field](field-object-ado.md) object [Properties](properties-collection-ado.md) collection when the [CursorLocation](cursorlocation-property-ado.md) property is set to **adUseClient**. 
  
 **Usage**
  
```
Dim rs As New Recordset
Dim fld As Field
rs.CursorLocation = adUseClient      'Enable index creation
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable
rs.Open
Set fld = rs.Fields(0)
fld.Properties("Optimize") = True    'Create an index
fld.Properties("Optimize") = False   'Delete an index

```

