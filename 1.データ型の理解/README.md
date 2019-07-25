# データ型の理解
- [データ型 (Transact-SQL)](https://docs.microsoft.com/ja-jp/sql/t-sql/data-types/data-types-transact-sql)
  - https://docs.microsoft.com/ja-jp/sql/t-sql/data-types/data-types-transact-sql

## 以下のデータ型について理解している
### BIT
- 1、0、または NULL の値をとる整数型です。
- 文字列値 TRUE および FALSE は bit 値に変換できます。TRUE は 1 に変換され、FALSE は 0 に変換されます。
- bit 型への変換において、0 以外の値はすべて 1 へと変換されます。

### DECIMAL
- 固定長の有効桁数と小数点以下保持桁数を持つ数値データ型です。
##### 引数
decimal[ (p[ ,s] )]
- 固定長の有効桁数と小数点以下保持桁数を指定します。
- 最大有効桁数を使用した場合、有効値は - 10^38 +1 から 10^38 - 1 です。 
- p (precision)：固定長の有効桁数
  - 格納される 10 進数の桁数の最大合計数。
  - この数には、小数点の左側と右側の両方が含まれます。
  - 有効桁数の値は、1 - 38 (最大有効桁数) にする必要があります。
  - 既定の有効桁数は 18 です。
- s (scale)：小数点以下保持桁数
  - 小数点の右側の保存される桁数です。
  - この数値が p から差し引かれ、小数点の左側の最大桁数が判別されます。
  - 小数点以下桁数は、0 から p の範囲の値である必要があり、有効桁数が指定されている場合にのみ指定できます。
  - 既定の小数点以下桁数は 0 です。したがって、0 <= s <= p になります。

### INT（int、bigint、smallint、tinyint）
- 整数データを使用する実数データ型です。
##### データ範囲
| データ型 | 範囲                                                                     | ストレージ |
|----------|--------------------------------------------------------------------------|------------|
| bigint   | -2^63 (-9,223,372,036,854,775,808) ～ 2^63-1 (9,223,372,036,854,775,807) | 8 バイト   |
| int      | -2^31 (-2,147,483,648) ～ 2^31-1 (2,147,483,647)                         | 4 バイト   |
| smallint | -2^15 (-32,768) ～ 2^15-1 (32,767)                                       | 2 バイト   |
| tinyint  | 0 ～ 255                                                                 | 1 バイト   |

### FLOAT/REAL
- 浮動小数点数値データで使用する概数型です。
- 浮動小数点データは概数であるため、データ型の範囲に含まれるすべての値を正確に表せるわけではありません。
-  real の ISO シノニムは、 float (24) であり、float (24) と同一の動作となります。
##### データ範囲
| データ型 | 範囲                                                        | ストレージ             |
|----------|-------------------------------------------------------------|------------------------|
| float    | - 1.79E+308 ～ -2.23E-308、0、および 2.23E-308 ～ 1.79E+308 | n の値により異なります |
| real     | - 3.40E+38 ～ -1.18E-38、0、および 1.18E-38 ～ 3.40E+38     | 4 バイト               |

##### 構文
float [ (n) ]
- n は、float 数の仮数部を格納するために使用されるビット数であるため、精度と格納サイズを指示します。
- n を指定する場合、1 から 53 までの値にする必要があります。
- n の既定値は 53 です

| n 値    | 有効桁数 | ストレージのサイズ |
|---------|----------|--------------------|
| 1 ～ 24 | 7 桁     | 4 バイト           |
| 25-53   | 15 桁    | 8 バイト           |

### DATETIME
- datetime と dattime2 があり、datetime2 は SQL 標準に準拠しています。
- datetime2 は、既存の datetime 型を拡張して、日付範囲と既定の有効桁数を増やし、ユーザーが必要に応じて有効桁数を指定できるようにしたものと考えることができます。
- 24 時間形式の時刻 (1 秒未満の秒を含む) と組み合わせた日付を定義します。
- なお、日付のみ保持する date 型もあり、日付範囲は datetime2 型と同様です。

| 項目                          | datetime                                             | datetime2
|-------------------------------|------------------------------------------------------|-----------|
| 日付範囲                      | 1753 年 1 月 1 日～ 9999 年 12 月 31 日              | 0001 年 1 月 1 日～ 9999 年 12 月 31 日 |
| 時間の範囲                    | 00:00:00 から 23:59:59.997                           | 00:00:00 から 23:59:59.9999999 |
| 精度                          | 値は、.000、.003、または .007 秒単位に丸められます。 | 100 ナノ秒 |
| 既定値                        | 1900-01-01 00:00:00                                  | 1900-01-01 00:00:00 |

### TEXT
- サイズの大きい非 Unicode 文字（text 型）、Unicode 文字（ntext 型）を格納する固定長データ型と可変長データ型を指定します。
　　- Unicode データは UNICODE UCS-2 文字セットを使用します。
- 文字列の最大長
  - text：2^31-1 (2,147,483,647)
  - ntext：2^30 - 1 (1,073,741,823)
##### 注意
- 今後のバージョンの SQL Server で削除される予定のため、text の代わりに [varchar(max)](#varchar)、ntext の代わりに [nvarchar(max)](#nvarchar) を使用すること。
  - 固定長の場合は [char](#char) もしくは [nchar](#nchar) を使用すること。

### IMAGE
- バイナリ データを格納する固定長データ型を指定します。
  - 0 ～ 2^31-1 (2,147,483,647) バイトの可変長のバイナリ データを指定します。 
##### 注意
- 今後のバージョンの SQL Server で削除される予定のため、image の代わりに [varbinary(max)](#BINARY/VARBINARY) を使用すること。

### CURSOR
- カーソルへの参照を格納している変数やストアド プロシージャの OUTPUT パラメーターを表すデータ型です。
- cursor 型の変数とパラメーターを参照できる操作は次のとおりです。
  - DECLARE *@local_variable* および SET *@local_variable* ステートメント。
  - OPEN、FETCH、CLOSE、および DEALLOCATE の各カーソル ステートメント
  - ストアド プロシージャ出力パラメーター
  - CURSOR_STATUS 関数
    - sp_cursor_list、sp_describe_cursor、sp_describe_cursor_tables、および sp_describe_cursor_columns の各システム ストアド プロシージャ
     - sp_cursor_list および sp_describe_cursor の cursor_name 出力列に、カーソル変数の名前が返されます。
- 作成された cursor 型の任意の変数は null を許容します。
- CREATE TABLE ステートメント内の列に cursor 型を使用することはできません。

##### 構文
- [DECLARE *@local_variable* ステートメント](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/declare-cursor-transact-sql)
    ```sql
    ISO Syntax  
    DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
        FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
    [;]  
    Transact-SQL Extended Syntax  
    DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
        [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
        FOR select_statement   
        [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
    [;]
    ```
- [SET *@local_variable* ステートメント](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/set-local-variable-transact-sql)
    ```sql
    SET   
    { @local_variable  
        [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
    }  
    |  
    { @SQLCLR_local_variable.mutator_method  
    }  
    |  
    { @local_variable  
        {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
    }  
    |   
    { @cursor_variable =   
        { @cursor_variable | cursor_name   
        | { CURSOR [ FORWARD_ONLY | SCROLL ]   
            [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
            [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
            [ TYPE_WARNING ]   
        FOR select_statement   
            [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
        }   
        }  
    }
    ```

### TABLE
- 後で処理できるように結果セットを格納するための特別なデータ型です。
- table 型は主に、テーブル値関数の結果セットとして返される行のセットの一時的な保存に使用します。
- テーブル変数（table 型の変数）は、関数、ストアド プロシージャ、およびバッチで使用できます。
- テーブル変数は、それが定義されている関数、ストアド プロシージャ、またはバッチの終了時に自動的に削除されます。
- テーブル変数を宣言するには、[DECLARE *@local_variable*](https://docs.microsoft.com/ja-jp/sql/t-sql/language-elements/declare-local-variable-transact-sql) を使用します。

##### 注意
- テーブル変数はクエリが効率的に処理するための統計情報を持たないため、参照する多数の行 (100 行を超える行) を使用する可能性がある場合はパフォーマンス問題に留意して慎重に使用する必要があります。このような場合、一時テーブルによってパフォーマンス問題が解決することがあります。
- テーブル変数を他のテーブルに結合するクエリの場合は、RECOMPILE ヒントを使用することで、クエリを効率的に処理するようになります。

##### 使用例
- テーブル変数の宣言
    ```sql
    DECLARE @Table TABLE(
    Id int NOT NULL,
    Name varchar(20) NOT NULL
    )
    ```

- テーブル変数を使った SELECT
    ```sql
    SELECT * FROM @Table
    ```

- テーブル変数への INSERT/INSERT/UPDATE/DELETE
    ```sql
    -- INSERT
    INSERT INTO @Table VALUES(1, 'Hoge')
    -- UPDATE
    UPDATE @Table SET name = name + '1'
    -- DELETE
    DELETE FROM @Table
    ```

- インラインテーブル値関数
  - RETURNS には TABLE とだけ書いて、ボディには BEGIN-END を書かず、RETURN に戻り値のクエリを書く。
    ```sql
    CREATE FUNCTION dbo.InlineTableValued()
    RETURNS TABLE
    AS
    RETURN
    SELECT 1 Id, 'Hoge' Name
    UNION ALL
    SELECT 2 Id, 'Fuga' Name
    UNION ALL
    SELECT 3 Id, 'Homu' Name
    GO
    ```
    ```sql
    SELECT * FROM dbo.InlineTableValued()
    ```
    | id | name |
    |----|------|
    | 1  | Hoge |
    | 2  | Fuga |
    | 3  | Homu |

- 複数ステートメントのテーブル値関数
  - RETURNS に戻り値として返すテーブル型変数を宣言して、ボディの最後には RETURN だけ書く。
    ```sql
    CREATE FUNCTION dbo.MultiStatementTableValued()
    RETURNS @Table TABLE (
    Id int NOT NULL,
    Name varchar(20) NOT NULL
    )
    AS
    BEGIN

    INSERT INTO @Table VALUES(1, 'Hoge')
    INSERT INTO @Table VALUES(2, 'Fuga')
    INSERT INTO @Table VALUES(3, 'Homu')

    RETURN

    END
    GO
    ```
    ```sql
    SELECT * FROM dbo.MultiStatementTableValued()
    ```
    | id | name |
    |----|------|
    | 1  | Hoge |
    | 2  | Fuga |
    | 3  | Homu |

### TIMESTAMP
- SQL Serverの timestamp はSQL標準とは異なり、日付または時刻のデータ型ではありません。
- [datetime または dattime2](#DATETIME) を使用すること。
#### 参考
- [日付と時刻のデータ型および関数 (Transact-SQL)](https://docs.microsoft.com/ja-jp/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)
  - https://docs.microsoft.com/ja-jp/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql


## 以下のデータ型について理解し、違いを説明できる
### CHAR/NCHAR
- char / nchar とも固定長の文字列データ型です。
- SQL Server 2017までは、char は非 Unicode 文字を格納し、nchar は Unicode 文字を格納する違いが特徴でしたが、SQL Server 2019 プレビュー 以降は、使用する照合順序によっては、char に UTF-8 のUnicode 文字を格納可能となりました。

#### char
- SQL Server 2019 プレビュー 以降、UTF-8 が有効になっている照合順序を使用する場合、これらのデータ型には Unicode 文字データの全範囲が格納され、UTF-8 文字エンコードが使用されます。
- UTF-8 が無効の照合順序を指定する場合、これらのデータ型には、対応するその照合順序のコード ページでサポートされている文字のサブセットのみが格納されます。
##### 構文
- char [ ( n ) ]
  - n によってバイト単位での文字列の長さが定義されます。1 から 8,000 までの値にする必要があります。
  - Latin などの 1 バイト エンコード文字セットの場合、ストレージのサイズは n バイトとなり、格納できる文字数もまた n となります。
  - マルチバイト エンコード文字セットの場合、ストレージのサイズは引き続き n バイトですが、格納できる文字数が n よりも少なくなる場合があります。
  - データ定義または変数宣言ステートメントで n を指定しないと、既定の長さは 1 になります。
  - CAST 関数および CONVERT 関数で n を指定しないと、既定の長さは 30 になります。

#### nchar
- SQL Server 2012 (11.x) 以降、補助文字 (SC) が有効になっている照合順序を使用する場合、これらのデータ型には Unicode 文字データの全範囲が格納され、UTF-16 文字エンコードが使用されます。
- SC が無効の照合順序を指定する場合、これらのデータ型には UCS-2 文字エンコードでサポートされている文字データのサブセットのみが格納されます。
##### 構文
- nchar [ ( n ) ]
  - n によってバイト ペアでの文字列の長さが定義されます。1 から 4,000 までの値にする必要があります。
  - ストレージのサイズは、n の 2 倍のバイト数です。
    - UCS-2 エンコードの場合、ストレージのサイズは n の 2 倍のバイト数となり、格納できる文字数もまた n となります。
    - UTF-16 エンコードの場合、ストレージのサイズは引き続き n の 2 倍のバイト数ですが、補助文字によって 2 つのバイト ペア (またはサロゲート ペア) が使用されるため、格納できる文字数は n よりも少なくなる場合があります。
  - データ定義または変数宣言ステートメントで n を指定しないと、既定の長さは 1 になります。
  - CAST 関数で n を指定しないと、既定の長さは 30 になります。

### VARCHAR/NVARCHAR
- varchar / nvarchar とも可変長の文字列データ型です。
- SQL Server 2017までは、char は非 Unicode 文字を格納し、nchar は Unicode 文字を格納する違いが特徴でしたが、SQL Server 2019 プレビュー 以降は、使用する照合順序によっては、char に UTF-8 のUnicode 文字を格納可能となりました。

#### varchar
- SQL Server 2019 プレビュー 以降、UTF-8 が有効になっている照合順序を使用する場合、これらのデータ型には Unicode 文字データの全範囲が格納され、UTF-8 文字エンコードが使用されます。
- UTF-8 が無効の照合順序を指定する場合、これらのデータ型には、対応するその照合順序のコード ページでサポートされている文字のサブセットのみが格納されます。 
##### 構文
- varchar [ ( n | max ) ] 
  - n によってバイト単位での文字列の長さが定義されます。1 から 8,000 までの値を指定できます。
  - max は最大格納サイズが 2^31-1 バイト (2 GB) であることを示します。
  - Latin などの 1 バイト エンコード文字セットの場合、ストレージのサイズは n バイト + 2 バイトとなり、格納できる文字数もまた n となります。
  - マルチバイト エンコード文字セットの場合、ストレージのサイズは引き続き n バイト + 2 バイトですが、格納できる文字数が n よりも少なくなる場合があります。
  - データ定義または変数宣言ステートメントで n を指定しないと、既定の長さは 1 になります。
  - CAST 関数および CONVERT 関数で n を指定しないと、既定の長さは 30 になります。

#### nvarchar
- SQL Server 2012 (11.x) 以降、補助文字 (SC) が有効になっている照合順序を使用する場合、これらのデータ型には Unicode 文字データの全範囲が格納され、UTF-16 文字エンコードが使用されます。
- SC が無効の照合順序を指定する場合、これらのデータ型には UCS-2 文字エンコードでサポートされている文字データのサブセットのみが格納されます。

##### 構文
- nvarchar [ ( n | max ) ]
  - 可変長の文字列データです。 n によってバイト ペアでの文字列の長さが定義されます。1 から 4,000 までの値を指定できます。
  - max は、ストレージの最大サイズが 2^30-1 文字 (2 GB) であることを示します。
  - ストレージのサイズは、n の 2 倍のバイト数 + 2 バイトです。
    - UCS-2 エンコードの場合、ストレージのサイズは n の 2 倍のバイト数 + 2 バイトとなり、格納できる文字数もまた n となります。
    - UTF-16 エンコードの場合、ストレージのサイズは引き続き n の 2 倍のバイト数 + 2 バイトですが、補助文字によって 2 つのバイト ペア (またはサロゲート ペア) が使用されるため、格納できる文字数は n よりも少なくなる場合があります。


### BINARY/VARBINARY

