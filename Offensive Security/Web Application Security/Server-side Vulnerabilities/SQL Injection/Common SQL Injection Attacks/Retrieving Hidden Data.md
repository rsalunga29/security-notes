Imagine a shopping application that displays products in different categories. When the user clicks on the **Gifts** category, their browser requests the URL:
```txt
https://insecure-website.com/products?category=Gifts
```
This causes the application to make a SQL query to retrieve details of the relevant products from the database:
```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
The parameter `released = 1` is being used to hide products that are not yet released.

However, this application doesn't implement any defenses against SQL injection attacks. This means an attacker can construct the following to initiate an attack:
```txt
https://insecure-website.com/products?category=Gifts'--
```
This will result in a SQL query:
```sql
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```
Crucially, the `--` is a comment indicator which means the rest of the query is interpreted as a comment, effectively removing it. As a result, all products are displayed, including the ones that are yet to be released.

Additionally, you can use a similar attack to cause the application to display all products, regardless of any category, including categories they don't know about:
```txt
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```
This will result in a SQL query:
```sql
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```
The modified query returns all items where either the `category` is `Gifts`, or `1` is equal to `1`. As `1=1` is always true, the query returns all items.