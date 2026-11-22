







Check on Pokey portal, we can see:

![AFTERNETWORKALLCHANGEFROMGOO]

<img width="577" height="372" alt="image" src="https://github.com/user-attachments/assets/4507d48c-c5a3-45c8-ba6b-0e8fa7ee856b" />

Because Pokey has  Virtual Machine Data Access Administrator (preview) so it can self-assign Virtual Machine Admin Login so Pokey can login to VM with its account.

`az role assignment create \
  --assignee-object-id "$POKEY_ID" --assignee-principal-type User \
  --role "Virtual Machine Administrator Login" \
  --scope "/subscriptions/5b9a2611-6b85-49e7-89ee-a48a0bd4c1dd/resourceGroups/rg-11201416/providers/Microsoft.Compute/virtualMachines/VM1"`
  
