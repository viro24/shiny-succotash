8b9af791689d8fa54d0dba26a3613fdf65f18b84

### Use this trick to bulk delete your old repos or old forks 
(Inspired by https://medium.com/@icanhazedit/clean-up-unused-github-rpositories-c2549294ee45#.3hwv4nxv5)

1. Open in a new tab all to-be-deleted github repositores (Use the mouse’s middle click or Ctrl + Click) https://github.com/username?tab=repositories

2. Use one tab https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall to shorten them to a list.

3. Save that list to some path

4. The list should be in the form of “ur_username\repo_name” per line. Use regex search (Sublime text could help). Search for ' \|.*' and replace by empty.

5. Register a new personal access token with a 'delete_repo perm' https://github.com/settings/tokens/new

6. Copy the access_token and run the following line replacing xxx with your access token.

**Linux and OS X :**
```
while read r;do curl -XDELETE -H 'Authorization: token xxx' "https://api.github.com/repos/$r ";done < repos
```
**Windows:**
```
get-content D:\repolist.txt | ForEach-Object { Invoke-WebRequest -Uri https://api.github.com/repos/$_ -Method “DELETE” -Headers @{"Authorization"="token xxx"} }

$AllProtocols = [System.Net.SecurityProtocolType]'Tls11,Tls12'
[System.Net.ServicePointManager]::SecurityProtocol = $AllProtocols
get-content D:\www\shiny-succotash\delete-repo.txt | ForEach-Object { Invoke-WebRequest -Uri https://api.github.com/repos/$_ -Method “DELETE” -Headers @{"Authorization"="token 8b9af791689d8fa54d0dba26a3613fdf65f18b84"} }
```

### Caution
I have only tested this script on Linux.

Have fun :)