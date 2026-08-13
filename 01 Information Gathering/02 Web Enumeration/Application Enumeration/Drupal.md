# Footprinting
```
curl -s http://drupal.inlanefreight.local | grep Drupal
#Another way to identify Drupal CMS - nodes
# /node/1
```
# Identify Drupal version
```
curl -s http://drupal-acc.inlanefreight.local/CHANGELOG.txt | grep -m2 ""
curl -s http://drupal.inlanefreight.local/CHANGELOG.txt
```
# Drupal scan
```
droopescan scan drupal -u http://drupal.inlanefreight.local
```