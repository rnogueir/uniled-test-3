# UniLED Technical Test 3

This is a solution for the database optimization problem.


## SoldItems table

The current table definition has a mixture of product description and sales history.

The following columns can be moved to a "reference" table called Products:
- name
- code
- ext_id
- maker
- barcode
- taxcode
- status_code
- visibility

The remaining columns can be maintained on a new table called Sales:
- ID
- product_code (previouly called `code`)
- sold_date



## Database size limit

In order to limit the database growth, the new Sales table can be divided into partitions, using the `sold_date` as sorting key; as the table grows, the partitions with older rows can be archived and deleted.

In case the older entries are needed frequently, it will be necessary to adapt the application in order to access the archived rows which might be kept in a different database/disk/machine.
