# Database Tuning

### Index

#### Bitmap

- significant space and performance advantage over other structures for query
- Bitmap indexes use [bit arrays](https://en.wikipedia.org/wiki/Bit_array) (commonly called bitmaps) and answer queries by performing [bitwise logical operations](https://en.wikipedia.org/wiki/Bitwise_operation) on these bitmaps
- work well for *low-[cardinality](https://en.wikipedia.org/wiki/Cardinality) [columns](https://en.wikipedia.org/wiki/Column_(database))*, which have a modest number of distinct values, either absolutely, or relative to the number of records that contain the data
  - The extreme case of low cardinality is [Boolean data](https://en.wikipedia.org/wiki/Boolean_data)
- unsuitable for [online transaction processing](https://en.wikipedia.org/wiki/Online_transaction_processing) applications
- requirements
  - low card
  - read only

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200103102503683.png" alt="image-20200103102503683" style="zoom:33%;" />



#### BRIN

- A BRIN is applicable to an index on a table that is large and where the index key value is easily sorted and evaluated with a [MinMax function](https://en.wikipedia.org/w/index.php?title=MinMax_function&action=edit&redlink=1)
- search by block

