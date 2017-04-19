# Project 10 - Fortress Globitek_CTF

Time spent: **5** hours spent in total

> Objective: Create an intentionally vulnerable version of the Globitek application with a secret that can be stolen.

### Requirements

- [x] All source code and assets necessary for running app
- [x] `/globitek.sql` containing all required SQL, including the `secrets` table
- [x] GIF Walkthrough of compromise
<img src='./ctfDemonstration.gif' title='Video Walkthrough' width='' alt='Video Walkthrough CTF Demonstration' />
- [x] Brief writeup about the vulnerabilities introduced below
---html
<dl>
	<img src='./IDOR.PNG' alt='IDOR demonstration' />
	<dt>Vulnerability #1: Insecure Direct Object Reference (IDOR)</dt>
	<dd>There is a IDOR vulnerability in the show.php for the public's 
	"find a salesperson" page. You can access the salesperson that has 
	id=11, a hidden account, to obtain a first name and a password for
	one of the account holder.</dd>

	<img src='./sqli.PNG' alt='SQL Injection demonstration' />
	<dt>Vulnerability #2: SQL Injection (SQLi)</dt>
	<dd>We now know the first name and the password of an account, but
	we don't know the username. Luckily, username input box in the login
	page has a SQL Injection vulnerability. Thus, instead of figuring out
	the username, we can write a SQL command that directly queries it.
	In the username box, input: <em>x' OR first_name='Jinwoo</em>.</dd>

	<img src='./burp.PNG' alt='Field manipulation demonstration' />
	<dt>Vulnerability #3: Post request field manipulation using Burp</dt>
	<dd>Once we are logged in, we can go to a show.php page for countries
	where it has some post fields that are vulnerable to be manipulated
	using burp. There, you can define which table you want query from, 
	which entry you want to view, and which field you want to veiw. In 
	order to view the secret code, you need to modify the fields to match 
	the following:<em>id=1&table=secrets&field=secret&submit=Submit</em></dd>
</dl>
---

### Vulnerabilities
- Vulnerability #1: Insecure Direct Object Reference (IDOR)
- Vulnerability #2: SQL 
- Vulnerability #3: Post request field manipulation using Burp