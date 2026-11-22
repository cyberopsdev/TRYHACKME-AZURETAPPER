Login to [AZUREPORTAL]https://portal.azure.com

![GOOLOGIN]<img width="184" height="31" alt="image" src="https://github.com/user-attachments/assets/14597858-a4b3-42af-8582-ec35a04d2fd3" />

Assign a public IP address to this private network:

![PUBLICIP]<img width="1913" height="577" alt="image" src="https://github.com/user-attachments/assets/a0a36c93-5c55-4b2d-a3c2-bd3ceb61cda2" />

After got the Public Ip, we still can not access to VM due to affect of SKU so we need to check it
# is the public IP Standard SKU? (this is why no-NSG = blocked)

`az network public-ip list --resource-group <your rg-*******> --query "[].{Name:name, SKU:sku.name, IP:ipAddress}" -o table`

[SKU]<img width="922" height="75" alt="image" src="https://github.com/user-attachments/assets/b0e60be9-73d8-416a-9115-29cf9a500b76" />

This is SKU standard as Microsoft doccument, it will block all inbound connections by default. It will result time-out for your ssh connection withoput Network Security Group (NSG) in place so we need to set up the NSG to allow our SSH connection inbound and associate it to our private network.

![NSGALLOWSSH]
<img width="1415" height="130" alt="image" src="https://github.com/user-attachments/assets/2350fd0c-0205-40ac-ad5e-23294845190c" />

![NSGRULESETUP]
<img width="1446" height="519" alt="image" src="https://github.com/user-attachments/assets/6b5fc1b9-44b2-4f58-b5dc-8727607274ed" />

![ASSOCIATETONIC]
<img width="838" height="176" alt="image" src="https://github.com/user-attachments/assets/72ceceaa-baa0-4930-82e3-4bb2faed947c" />



