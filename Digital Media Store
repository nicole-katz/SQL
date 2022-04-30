/* Show Customers (full names, customer ID and country) who are not in the US */
SELECT FirstName, LastName, CustomerId, Country 
FROM chinook.customers 
WHERE Country != "USA";

/* Show only Customers from Brazil*/
SELECT *
FROM chinook.customers
WHERE Country = "Brazil";

/* Show Customer's full name, Invoice ID, Date of the invoice and Billing Country for Customers from Brazil*/
SELECT cust.FirstName, cust.LastName, inv.InvoiceId, inv.InvoiceDate, inv.BillingCountry
FROM chinook.invoices as inv
LEFT JOIN chinook.customers as cust
ON inv.CustomerId = cust.CustomerId
WHERE inv.BillingCountry = "Brazil";

/* Show the Employees who are Sales Agents*/
SELECT *
FROM chinook.employees
WHERE title = "Sales Support Agent";

/* Find a unique list of billing countries from the Invoice table*/
SELECT DISTINCT BillingCountry
FROM chinook.invoices;

/* Show the invoices associated with each Sales Agent - include the Sales Agent's full name*/
SELECT emp.FirstName, emp.LastName, inv.InvoiceId
FROM chinook.employees as emp
JOIN chinook.Customers as cust ON cust.SupportRepId = emp.EmployeeId
JOIN chinook.Invoices as inv ON inv.CustomerId = cust.CustomerId;

/* Show the Invoice Total, Customer name, Country and Sales Agent name for all invoices and customers*/
SELECT inv.Total, cust.FirstName, cust.LastName, cust.Country, emp.FirstName, emp.LastName
FROM chinook.customers as cust
JOIN chinook.invoices as inv ON cust.CustomerId = inv.CustomerId
JOIN chinook.employees as emp ON emp.EmployeeId = cust.SupportRepId;

/* Show the number of Invoices there were in 2009*/
SELECT COUNT(*)
FROM chinook.invoices
WHERE InvoiceDate BETWEEN '2009-01-01' AND '2009-12-31';

/* Show total sales for 2009*/
SELECT SUM(Total)
FROM chinook.invoices
WHERE InvoiceDate BETWEEN '2009-01-01' AND '2009-12-31';

/* Show purchased track name with each invoice line item*/
SELECT t.name, i.invoicelineid
FROM chinook.invoice_items as i
JOIN chinook.tracks as t ON i.TrackId = t.TrackId;

/* Show purchased track name and artist name with each invoice line item*/
SELECT t.name, t.composer, i.invoicelineid
FROM chinook.invoice_items as i
JOIN chinook.tracks as t ON i.TrackId = t.TrackId;

/* Show all Tracks, Album name, Media Type, and Genre*/
SELECT t.name AS 'Track Name', m.Name AS 'Media Type', g.Name AS 'Genre', a.title AS 'Album Title'
FROM chinook.tracks as t
JOIN chinook.albums as a ON t.AlbumId = a.AlbumId
JOIN chinook.genres as g ON t.GenreId = g.GenreId
JOIN chinook.media_types as m ON t.MediaTypeId = m.MediaTypeId;

/* Show total sales made by each sales agent*/
SELECT e.FirstName, e.LastName,
ROUND(SUM(i.Total), 2) AS 'Total Sales'
FROM chinook.employees as e
JOIN chinook.customers as c ON c.SupportRepId = e.EmployeeId
JOIN chinook.invoices as i ON i.CustomerId = c.CustomerId
WHERE e.Title = 'Sales Support Agent'
GROUP BY e.FirstName;

# Show the Sales Agent that made the most in sales in 2009
SELECT e.FirstName, e.LastName,
ROUND(SUM(i.Total), 2) AS 'Total Sales'
FROM chinook.employees as e
JOIN chinook.customers as c on c.SupportRepId = e.EmployeeId
JOIN chinook.invoices as I on i.CustomerId = c.CustomerId
WHERE e.Title = 'Sales Support Agent'
AND i.InvoiceDate LIKE '2009%'
GROUP BY e.FirstName
ORDER BY (ROUND(SUM(i.Total), 2)) DESC LIMIT 1;
