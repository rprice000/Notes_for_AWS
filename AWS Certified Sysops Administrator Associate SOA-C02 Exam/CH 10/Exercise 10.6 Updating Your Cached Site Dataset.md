Exercise 10.6 Updating Your Cached Site Dataset

***NOTE:  You must have completed 10.4 and 10.5 Exercise

1. Go to S3 Dashboard
2. Go to the bucket you created in 10.4 and delete the images
3. Type in permanently delete to remove the images
4. Copy the CloudFront Distribution name
    - See how the website still peforms even though the images are deleted
    - CloudFront will hold steady for 24 hours
5. To force the change you will need to invalidate the deleted objects
6. Go to CloudFront Dashboard
7. Click on the distribution
8. Click Invalidations tab
9. Click Create Invalidation
10. Add the images names with a preceeding /
    - /football1
    - /football2
11. Click Create Invalidation button
12. Once the invalidation is complet go to the CloudFront Distribution name in the browser to see the change
