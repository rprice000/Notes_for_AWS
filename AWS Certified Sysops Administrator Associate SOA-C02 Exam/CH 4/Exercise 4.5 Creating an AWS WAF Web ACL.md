Exercise 4.5 Creating an AWS WAF Web ACL


1. Go to AWS WAF & Shield service
2. Click Create web ACL
3. Select the region you want
    - US East (Ohio)
4. Type a Name
    - DemoACL
5. Type in a Description
6. Click Next button
7. Click Add rules drop down menu
8. Click Add managed rule groups
9. Select drop down AWS managed rule groups
10. Scroll to Free rule groups
11. Select Admin protection
***NOTE:  There may be other selections here
12. Click Add rules
13. Under Default web ACL action for requests that don't match any rules
    - Select Allow
14. Click Next Button
15. Next page shows how to set rule priority
    - NOTE:  In the real world you will need to do this
16. Click Next Button
17. Leave CloudWatch metrics as is
    - NOTE: In the real world you may need to change this
18. Click Next
19. Review your selection
20. Click Create web ACL Button

To Associate Resources to the Web ACL
21. Click on the Web ACL you just created
22. Click on Associated AWS resources tab
23. Click Add AWS resources