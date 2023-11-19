# Kominfo RPZ Blocklist
They're also leaking their RPZ lol  
This is a trimmed down version removing
```
$TTL 900

@       SOA     localhost.      aduankonten.mail.kominfo.go.id. (

        23111901        ;Serial
        1000            ;Refresh
        1000            ;Retry
        2592000         ;Expiry
        900)            ;TTL

@       IN      NS      localhost.
```
and
```
3600 IN CNAME trustpositif.kominfo.go.id.
```
## Steps to Update this
1. Get repo perms
2. Use Linux
3. Make a .sh file and paste this in
```
#!/bin/bash
# 4. git clone https://YOUR_USERNAME:YOUR_TOKEN@github.com/lepasid/blocklist_rpz.git in your Documents folder
# (If you just git clone normally, do git remote add origin https://YOUR_USERNAME:YOUR_TOKEN@github.com/lepasid/blocklist_rpz.git in the $TARGET_DIR folder)

TARGET_DIR=~/Documents/blocklist_rpz
FILE_NAME="$(date +"%Y-%m-%d")"
SOURCE_URL=KOMINFO'S SITE, IF YOU WANT TO KNOW WHAT IT IS JOIN OUR DISCORD
GIT_USERNAME=YOUR_USERNAME
GIT_EMAIL=YOUR_EMAIL

cd "$TARGET_DIR"
rm domains
if [ -e "$FILE_NAME" ]; then
    rm "$FILE_NAME"
fi

aria2c --check-certificate=false -x4 -o "$TARGET_DIR/domains" "$SOURCE_URL"
tail -n +12 "$TARGET_DIR/domains" | sed "s/3600 IN CNAME trustpositif.kominfo.go.id.//g" > "$TARGET_DIR/domains"
cp domains $FILE_NAME

git add domains
git add "$FILE_NAME"
git commit -m "Add $FILE_NAME"
git config user.name "$GIT_USERNAME"
git config user.email "$GIT_EMAIL"
git rebase
git push -u origin main

cd ..
echo "Script completed successfully."
```
5. chmod +x YOUR_FILE.sh
7. ./YOUR_FILE.sh
7. Enjoy
