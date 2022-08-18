# Chinook-Data
Find all customers that are not in the US.
1.SELECT * FROM customers WHERE Country <> 'USA';

Find all customers in Brazil.
2.SELECT * FROM customers WHERE Country = 'Brazil';

Find the invoices of the customers in Brazil.
3.SELECT customers.Firstname, customers.Lastname, customers.CustomerId, invoices.CustomerId, invoices.InvoiceId, invoices.InvoiceDate, invoices.BillingCountry
FROM customers
INNER JOIN invoices ON customers.CustomerId = invoices.CustomerId;

Find information about all employees.
4.SELECT * FROM employees;

Find the employees that are sales agents.
5.SELECT * FROM employees WHERE Title = 'Sales Support Agent';

Find a unique list of billing countries.
6.SELECT DISTINCT Country FROM employees;

Show invoices associated with all Sales support agents.
7.SELECT emp.Lastname, emp.Firstname, inv.InvoiceId
FROM employees emp
JOIN Customers cust ON cust.SupportRepId = emp.EmployeeId
JOIN Invoices Inv ON Inv.CustomerId = cust.CustomerId;

Show the Invoice Total, Customer name, Country, and Sales Agent name for all invoices and customers.
8.SELECT emp.Lastname, emp.Firstname, cust.Firstname, cust.Lastname, cust.Country, inv.total
FROM employees emp
JOIN customers cust ON cust.SupportRepId = emp.EmployeeId
JOIN Invoices inv ON Inv.CustomerId = cust.CustomerId;

Show all invoices from 2009.
9.SELECT COUNT (*) FROM invoices WHERE InvoiceDate BETWEEN '2009-01-01' AND '2009-12-31';

Show all sales from 2009.
10.SELECT SUM (Total) FROM invoices WHERE InvoiceDate BETWEEN '2009-01-01' AND '2009-12-31';
 
Show all the playlist tracks.
11.SELECT * FROM playlist_track;

Show all playlists.
12.SELECT * FROM playlists;

Write a query that includes the purchased track name with each invoice line item.
13.SELECT t.Name, i.InvoiceLineId
FROM Invoice_items i
JOIN Tracks t ON i.TrackId = t.TrackId;

Write a query that includes the purchased track name AND artist name with each invoice line item.
14.SELECT t.name, t.composer, i.InvoiceLineId
FROM Invoice_items i
JOIN Tracks t ON i.TrackId = t.TrackId;

Provide a query that shows all the Tracks, and include the Album name, Media type, and Genre.
15.SELECT t.name AS 'Track Name', a.Title AS 'Album Title', m.Name AS 'Media Type', g.Name AS 'Genre'
FROM Tracks t
JOIN Albums a ON a.AlbumId =t.AlbumId
JOIN Media_Types m ON m.MediaTypeId = t.MediaTypeId
JOIN Genres g ON g.GenreId = t.GenreId;

Show the total sales made by each sales agent.
16.SELECT emp.Firstname, emp.Lastname,
ROUND(SUM(Inv.Total), 2) AS 'Total Sales'
FROM employees emp
JOIN customers cust
ON cust.SupportRepId = emp.EmployeeId
JOIN invoices inv
ON Inv.customerId = cust.CustomerId
WHERE emp.Title = "Sales Support Agent"
GROUP BY emp.Firstname;

Which sales agent made the most in sales in 2009?
17.SELECT emp.Firstname, emp.Lastname,
ROUND(SUM(Inv.Total),2) AS 'Total Sales'
FROM employees emp
JOIN Customers cust
ON cust.SupportRepId = emp.EmployeeId
JOIN Invoices Inv
ON Inv.CustomerId = cust.CustomerId
WHERE emp.Title = 'Sales Support Agent'
AND Inv.InvoiceDate LIKE '2009%'
GROUP BY emp.Firstname
ORDER BY (ROUND(SUM(Inv.Total),2)) DESC LIMIT 1
