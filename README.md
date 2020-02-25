# Add Province code list in UI

• **References:**

ContentCertification.docx






• **Go ECCnet Testing Environment:**

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image1.jpg)

• **Go ProSYNC BC:**

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image2.jpg)

• **Search GTIN:**

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image3.jpg)

• **Check Code List Value:**

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image4.jpg)

• **Run Service on QA server:**

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image5.jpg)

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image6.jpg)


• **Run Nutrition Sync on Cloud:**

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image7.jpg)

• **Check Walkthrough:**

Check 'Tracker' table

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image11.jpg)

Check 'Business Process' table

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image9.jpg)

Check 'Validation' table

![repo1](https://github.com/JongkukJayLee/ProdCertTasks/blob/master/images/image12.jpg)


• **Required SQL:**


```sql

SELECT TOP (1000) [OutputProcess]
      ,[ItemID]
      ,[DateUpdated]
      ,[DateProcessed]
FROM [EEV1_NextGen].[dbo].[Tracker] 
WHERE OutputProcess = 176
AND itemid = 247988

```

```sql

SELECT 
	s.DateUpdated, tk.gtin, tbp.BusinessProcessID, s.data, s.DateUpdated
FROM eev1_nextgen.dbo.tradeitemkey tk 
INNER join  eev1_nextgen.dbo.TradeItemInBusinessProcess tbp 
ON tk.itemid = tbp.itemid   and tbp.BusinessProcessID in ( 146, 176, 32)
INNER join eev1_nextgen.dbo.TradeItemDataSnapshot s 
ON tbp.id = s.id
WHERE tk.gtin='00079118958619'--tk.itemid = 247988
ORDER BY s.dateupdated DESC 

```

```sql

SELECT TOP (1000) 
       [ItemID]
      ,[OutputProcess]
      ,[Message]
      ,[DateProcessed]
      ,[AdditionalId]
FROM [EEV1_NextGen].[dbo].[ValidationMessages] 
WHERE itemid = 247988  
ORDER BY DateProcessed DESC 
```
