---
title: "GetObjectOwner and SetObjectOwner Methods Example (VB)"
 
 
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
ms.topic: reference
  
localization_priority: Normal
ms.assetid: 0a30cce1-7626-8db3-4af4-84098c284db0
description: "This example demonstrates the GetObjectOwner and SetObjectOwner methods. This code assumes the existence of the group Accounting (see the Groups and Users Append, ChangePassword Methods Example (VB) to see how to add this group to the system). The owner of the Categories table is set to Accounting."
---

# GetObjectOwner and SetObjectOwner Methods Example (VB)

This example demonstrates the [GetObjectOwner](getobjectowner-method-adox.md) and [SetObjectOwner](http://msdn.microsoft.com/library/22c5d2d9-c7b2-3c3a-0b1f-a2e5bc46395c%28Office.15%29.aspx) methods. This code assumes the existence of the group Accounting (see the [Groups and Users Append, ChangePassword Methods Example (VB)](groups-and-users-append-changepassword-methods-example-vb.md) to see how to add this group to the system). The owner of the Categories table is set to Accounting. 
  
```
 
' BeginOwnersVB 
Sub Main() 
 On Error GoTo OwnersXError 
 
 Dim tblLoop As New ADOX.Table 
 Dim cat As New ADOX.Catalog 
 Dim strOwner As String 
 
 ' Open the Catalog. 
 cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" &amp; _ 
 "Data Source='c:\Program Files\" &amp; _ 
 "Microsoft Office\Office\Samples\Northwind.mdb';" &amp; _ 
 "jet oledb:system database=" &amp; _ 
 "'c:\Program Files\Microsoft Office\Office\system.mdw'" 
 
 ' Print the original owner of Categories 
 strOwner = cat.GetObjectOwner("Categories", adPermObjTable) 
 Debug.Print "Owner of Categories: " &amp; strOwner 
 
 ' Set the owner of Categories to Accounting 
 cat.SetObjectOwner "Categories", adPermObjTable, "Accounting" 
 
 ' List the owners of all tables and columns in the catalog. 
 For Each tblLoop In cat.Tables 
 Debug.Print "Table: " &amp; tblLoop.Name 
 Debug.Print " Owner: " &amp; _ 
 cat.GetObjectOwner(tblLoop.Name, adPermObjTable) 
 Next tblLoop 
 
 ' Restore the original owner of Categories 
 cat.SetObjectOwner "Categories", adPermObjTable, strOwner 
 
 'Clean up 
 Set cat.ActiveConnection = Nothing 
 Set cat = Nothing 
 Exit Sub 
 
OwnersXError: 
 
 Set cat = Nothing 
 
 If Err <> 0 Then 
 MsgBox Err.Source &amp; "-->" &amp; Err.Description, , "Error" 
 End If 
 
End Sub 
' EndOwnersVB 

```

