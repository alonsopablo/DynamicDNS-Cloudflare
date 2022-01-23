# DynamicDNS-Cloudflare

## Migrate your Domain DNS from Godaddy (or any other Domain Register) to Cloudlflare
1.- Create a free Cloudflare account: https://www.cloudflare.com/ \
2.- Browse to your Cloudflare dashboard and click on +Add site. Eter your domain name. \
3.- Replace your Name Servers with the ones provided by Cloudflare. \
4.- Registrars can take 24 hours to process nameserver updates. You will receive an email when your site is active on Cloudflare. 

## Updater Script
Update the script cloudflare-template.sh with your domain information \

```
auth_email=""       # The email used to login 'https://dash.cloudflare.com' 
auth_method="token" # Set to "global" for Global API Key or "token" for Scoped API Token 
auth_key=""         # Your API Token or Global API Key
zone_identifier=""  # Can be found in the "Overview" tab of your domain
record_name=""      # Which record you want to be synced
ttl="3600"          # Set the DNS TTL (seconds)
proxy=false         # Set the proxy to true or false
slacksitename=""    # Title of site "Example Site"
slackchannel=""     # Slack Channel #example
slackuri=""         # URI for Slack WebHook "https://hooks.slack.com/services/xxxxx"
```
Save it and execute it, confirm the IP changes on your cloudflare DNS.
```
sudo chmod +x cloudflare.sh
./cloudflare.sh
```

## Automate your Script
We will use crontab to automate our script
```
crontab -e
```
Select your favourite text editor. For every minute update use the below code.
```
*/1 * * * * /bin/bash /script/path
```
Restart cron and test changing the IP on cloudflare, it should update to your public IP in 1 minute or less.
```
systemcrl restart cron
```

