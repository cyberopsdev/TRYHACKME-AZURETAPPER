LAB INFO:

Username: usr-11216086@201618.onmicrosoft.com

Password: p2zGC-8vj=EHqG@Z

TAP: p2zGC-8vj=EHqG@Z

Login via CLI `az login -u usr-11216086@201618.onmicrosoft.com -p 'p2zGC-8vj=EHqG@Z'`

![login]<img width="1094" height="448" alt="image" src="https://github.com/user-attachments/assets/d2cf767e-0203-417c-b06d-e4b1720fb633" />

Looking for users can be explored: 

`az ad user list -o table --query "[].{UPN:userPrincipalName, Name:displayName}"`

![Userslist]<img width="845" height="83" alt="image" src="https://github.com/user-attachments/assets/7728e29b-4719-4dba-b865-120a7fc0ebe4" />

Find the resource group where are in and resources related:

RG: `az group list --subscription 5b9a2611-6b85-49e7-89ee-a48a0bd4c1dd --query "[].{Name:name, Location:location, State:properties.provisioningState}" -o table`

![RG]<img width="1097" height="136" alt="image" src="https://github.com/user-attachments/assets/9d6390c8-1555-4f2a-8d31-269f3d43ac47" />

Resources: `az resource list --subscription 5b9a2611-6b85-49e7-89ee-a48a0bd4c1dd --query "[].{Name:name, Type:type, RG:resourceGroup}" -o table`

![Resources]<img width="1091" height="222" alt="image" src="https://github.com/user-attachments/assets/930e9545-8ca8-4a2b-94a1-3773e75ed51c" />

Besides, we also need to lists all app registrations in your Entra tenant with their display name, application (client) ID, and object ID:

`az ad app list --all --query "[].{Name:displayName, AppId:appId, ObjectId:id}" -o table`
![App] <img width="846" height="156" alt="image" src="https://github.com/user-attachments/assets/b6c8c437-66bb-4182-8cf7-44b3be0a8858" />

We notice there is an app named Tapper, so we can try to see if there is any user has the role to it
Find the app owner: `az ad sp show --id "b126c695-541a-4174-b75d-7df2f1607d4b" --query id -o tsv`
![Owner]<img width="1096" height="126" alt="image" src="https://github.com/user-attachments/assets/115377ad-a781-49e8-922f-32ff4af8d292" />



So we take note that, the password we have could be belong to 3 users Gumby, Goo or Pokey so we can do spray password to login to see if we can gain access to those users.

