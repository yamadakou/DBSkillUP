# テーブル結合
## 以下のテーブル結合について違いを説明できる
- INNER JOIN
  - MSドキュメント（過去バージョンでのリファレンス）
    - https://docs.microsoft.com/ja-jp/previous-versions/sql/sql-server-2008-r2/ms190014(v=sql.105)
  - 複数のテーブルを結合し、条件が一致したもののみを取得する。
- OUTER JOIN（LEFT, RIGHT, FULL）
  - MSドキュメント（過去バージョンでのリファレンス）
    - https://docs.microsoft.com/ja-jp/previous-versions/sql/sql-server-2008-r2/ms187518(v=sql.105)
  - LEFT OUTER JOIN
    - 左側にあるテーブルを優先して全レコード取得する。
  - RIGHT OUTER JOIN
    - 右側にあるテーブルを優先して全レコード取得する。
  - FULL OUTER JOIN
    - 両方のテーブルどちらも優先で、結合条件で一致するレコードも一致しないレコードもすべて取得する。
  - 結合イメージの参考記事
    - https://sql55.com/t-sql/t-sql-join-1.php

## それぞれを用いたクエリを10個以上作成したことがある
- INNER JOIN
- OUTER JOIN（LEFT, RIGHT, FULL）

### [JOIN（FROM句内に記載）](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/from-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/from-transact-sql
  

### サンプルの補足
```sql
-- 製品ごとの仕入先の会社を取得（INNER JOIN）
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
INNER JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);

-- 製品ごとの仕入先の会社を取得（LEFT OUTER JOIN）
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
LEFT OUTER JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);

-- 製品ごとの仕入先の会社を取得（RIGHT OUTER JOIN）
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
RIGHT OUTER JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);

-- 製品ごとの仕入先の会社を取得（FULL OUTER JOIN）
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
FULL OUTER JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);


-- 製品ごとの仕入先の会社を取得（INNER JOINと同様）
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);

-- 製品ごとの仕入先の会社を取得（LEFT OUTER JOINを指定しているが実行計画は仕入先に対するRIGHT OUTER JOINで処理）
SELECT p.ProductID, v.BusinessEntityID  
FROM Purchasing.ProductVendor AS v  
LEFT OUTER JOIN Production.Product AS p   
ON (v.ProductID = p.ProductID);

-- 仕入先の会社ごとの製品を取得（RIGHT OUTER JOINを指定しているが実行計画は製品に対するLEFT OUTER JOINで処理）
SELECT v.BusinessEntityID, p.ProductID
FROM Purchasing.ProductVendor AS v  
RIGHT OUTER JOIN Production.Product AS p   
ON (v.ProductID = p.ProductID);

-- 製品ごとの仕入先の会社を取得（CROSS JOIN）
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
CROSS JOIN Purchasing.ProductVendor AS v
```