# 単純なクエリ
## 以下のキーワードを用いたクエリを、それぞれ10個以上作成したことがある。
### [SELECT](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-transact-sql

### [UPDATE](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/update-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/update-transact-sql

### [INSERT](https://docs.microsoft.com/ja-jp/sql/t-sql/statements/insert-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/statements/insert-transact-sql

### [DELETE](https://docs.microsoft.com/ja-jp/sql/t-sql/statements/delete-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/statements/delete-transact-sql

### [WHERE](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/where-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/where-transact-sql

### [GROUP BY](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-group-by-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-group-by-transact-sql

### [ORDER BY](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-order-by-clause-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-order-by-clause-transact-sql

### [BETWEEN](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/between-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/between-transact-sql
  - サンプルの補足
  ```sql
  -- 従業員の氏名と時給を時給の昇順で取得
  SELECT e.FirstName, e.LastName, ep.Rate, ep.*  
  FROM HumanResources.vEmployee e   
  JOIN HumanResources.EmployeePayHistory ep   
      ON e.BusinessEntityID = ep.BusinessEntityID  
  ORDER BY ep.Rate;  
  GO

  -- BETWEENでは両端を含む範囲を取得する
  SELECT e.FirstName, e.LastName, ep.Rate  
  FROM HumanResources.vEmployee e   
  JOIN HumanResources.EmployeePayHistory ep   
      ON e.BusinessEntityID = ep.BusinessEntityID  
  WHERE ep.Rate BETWEEN 19 AND 22.5  
  ORDER BY ep.Rate;  
  GO

  -- 両端を含まない範囲を取得する場合は不等号を使用する
  SELECT e.FirstName, e.LastName, ep.Rate  
  FROM HumanResources.vEmployee e   
  JOIN HumanResources.EmployeePayHistory ep   
      ON e.BusinessEntityID = ep.BusinessEntityID  
  WHERE ep.Rate > 19 AND ep.Rate < 22.5  
  ORDER BY ep.Rate;  
  GO
  ```

### [TOP](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/top-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/top-transact-sql

### [IN](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/in-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/in-transact-sql

### [AS](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-transact-sql#a-using-select-to-retrieve-rows-and-columns)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/select-transact-sql#a-using-select-to-retrieve-rows-and-columns
    - SELECTの例にある「A. SELECT を使用して行および列を取得する」にて、テーブルの別名と列見出しの別名が例示されている。
  - 過去ドキュメントにテーブルの別名について記載あり
    - https://docs.microsoft.com/ja-jp/previous-versions/sql/sql-server-2008-r2/ms187455(v=sql.105)

### [IS NULL](https://docs.microsoft.com/ja-jp/sql/t-sql/queries/is-null-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/queries/is-null-transact-sql

### [NOT](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/not-transact-sql)/[OR](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/or-transact-sql)/[AND](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/and-transact-sql)
- MSドキュメント
  - NOT
    - https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/not-transact-sql
  - OR
    - https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/or-transact-sql
  - AND
    - https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/and-transact-sql

### [LIKE](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/like-transact-sql)
- MSドキュメント
  - https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/like-transact-sql
  

