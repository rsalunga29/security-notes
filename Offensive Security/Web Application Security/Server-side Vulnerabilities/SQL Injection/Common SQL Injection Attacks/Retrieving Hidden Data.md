Imagine a shopping application that displays products in different categories. When the user clicks on the **Gifts** category, their browser requests the URL:
```txt
`https://insecure-website.com/products?category=Gifts`
```
This causes the application to make a SQL query to retrieve details of the relevant products from the database:
```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
The parameter `released = 1` is being used to hide products that are not yet released.