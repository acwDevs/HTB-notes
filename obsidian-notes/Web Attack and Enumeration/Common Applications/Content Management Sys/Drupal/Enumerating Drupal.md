
searching for drupal strings
```shell-session
curl -s http://drupal.inlanefreight.local | grep Drupal
```

Drupal supports three types of users by default:

1. `Administrator`: This user has complete control over the Drupal website.
2. `Authenticated User`: These users can log in to the website and perform operations such as adding and editing articles based on their permissions.
3. `Anonymous`: All website visitors are designated as anonymous. By default, these users are only allowed to read posts.

finding version information in changelog.txt
```shell-session
curl -s http://drupal-acc.inlanefreight.local/CHANGELOG.txt | grep -m2 ""
```

using droopescan to get site information (versions, login portals, directories)
```shell-session
droopescan scan drupal -u http://drupal.inlanefreight.local
```
