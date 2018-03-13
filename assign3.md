#### Assignment 3 [ Saydullo Toshtanov ] <br>

**Exersize 1** 

*task1*

<hr>

<pre>
Invoice table - when the user buys something, invoice will be created 
   id - invoice number  
   order_id - order number  
   amount - amount of payment (number)  
   issued - invoice created date (date)  
   due - invoice expired date (date)  
</pre>

<pre>
Invoice ( id, order_id, amount, issued, due ) : 
  id - > ( order_id, amount, issued, due) 
  order_id is foreign key  
 </pre>
 
 It's in **First Normal Form**:  
  * It has single valued columns
  * All columns have unique names
  * And order doesn't matter
  
  It's in **Second Normal Form**:
  * It's in 1NF
  * It's has no particial dependency
  
  It's in **BCNF** because it's satisfies 3NF and it doesn't have multiple overlapping candidate key. 
  
  
  <hr>
  
  <pre>
  Payment table - purchaser makes a payment based on invoice number:   
    pay_id - payment id
    timestamp - payment date and time (date and time)  
    amount - amount of payment (number)  
    invoice_id - number of invoice  
</pre>
  pay_id -> (timestamp,amount,inv_id)  
  It's in __BCNF__ because there no other overlapping candidate key. 
  
  
  <hr>
 <pre> 
  Orders table - contains all the orders made on the system.   
     Id - order number. Orders have unique ID  
     cust_name - customer name (string)   
     cust_country - country abbreviations (string)  
     order_date - date of the order (date)  
     product_name - name of the product ordered (string)  
     product_desc - textual description of the product ordered (string) 
     product_price - price of the ordered product (number) 
     quantity - amount of the product ordered (number)

 </pre>
 
 <pre>
   Id -> (cust_name,cust_country, order_date, product_name, product-desc, product_price, quantity)  
   cust_name -> country
   product_name -> product_desc, product_price
   id -> order_date, quantity
   id -> cust_name, product_name
   
   </pre>
   
   It's in **First Normal Form** :
    * It has single valued columns
    * All columns have unique names
    * And order doesn't matter  
But it doesn't satisfy 2NF, because it has partical dependencies. So we have to normalize this table to the __BCNF__ .




*task 2,3*
  <pre>
  In Orders table, we have these dependencies:   
    Id -> (cust_name,cust_country, order_date, product_name, product-desc, product_price, quantity)  
    cust_name -> country  
    product_name -> product_desc, product_price  
    id -> order_date, quantity  
    id -> cust_name, product_name  
   </pre>
   
   In __BCNF__ there're should not be  overlapping candidate keys. So we have split table into different tables with single candidate keys. 
   
   
   <pre>
      Customer :    
        cust_id  - customer id (int) PK
        cust_name - customer name ( varchar(45))
        cut_country - customer country ( varchar(45))
        
      Product : 
        product_id - product id (int) PK 
        product_name - product name (varchar(45))
        product_desc - product description (varchar(45))
        product_price - product price (double(10,2))
        
      Order_info :
        order_id - order id (int) PK
        order_date - date of order (date)
        order_quantity - quantity of ordered product
   
      Order_mapping :
        order_id - order id (int) PK FK (Order_info)
        cust_id -  customer id (int) PK FK (Customer)
        product_id - product id (int) PK FK (Product)
   
        Primary key (order_id, cust_id, product_id)
       
       </pre>
