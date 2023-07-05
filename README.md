# ps-inventory--ox_lib--ProgressCircle

#PREVIEW 

https://camo.githubusercontent.com/a22f3818de5079d6d509fb4b6011ed59d24caebd3f1ee161a8bcaf52b0b83b38/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f313132353934343838323238343939383831362f313132353934343838323633333132313834322f696d6167652e706e67

**ps-inventory/client/main.lua**

search for **RegisterNetEvent('inventory:client:OpenInventory', function(PlayerAmmo, inventory, other)**

replace it with 

```
RegisterNetEvent('inventory:client:OpenInventory', function(PlayerAmmo, inventory, other)
    if not IsEntityDead(PlayerPedId()) then
        if Config.Progressbar.Enable then
            if lib.progressActive() then
            QBCore.Functions.Notify('Not Accessible', "error", 5000) return else
            lib.progressCircle({
                duration = 600,
                label = 'Opening Inventory..',
                position = 'bottom',
                useWhileDead = false,
                allowCuffed = false,
                allowFalling = false,
                canCancel = true,
                disable = {
                    move = false,
                    combat = true,
                    car = true
                }
        })
        ToggleHotbar(false)
            if showBlur == true then
                TriggerScreenblurFadeIn(1000)
            end
            SetNuiFocus(true, true)
            if other then
                currentOtherInventory = other.name
            end
            QBCore.Functions.TriggerCallback('inventory:server:ConvertQuality', function(data)
                inventory = data.inventory
                other = data.other
                SendNUIMessage({
                    action = "open",
                    inventory = inventory,
                    slots = Config.MaxInventorySlots,
                    other = other,
                    maxweight = Config.MaxInventoryWeight,
                    Ammo = PlayerAmmo,
                    maxammo = Config.MaximumAmmoValues,
                     Name = PlayerData.charinfo.firstname .." ".. PlayerData.charinfo.lastname .." - [".. GetPlayerServerId(PlayerId()) .."]", 
                })
                inInventory = true
            end, inventory, other)
        end
    else
        Wait(500)
        ToggleHotbar(false)
        if showBlur == true then
            TriggerScreenblurFadeIn(1000)
        end
        SetNuiFocus(true, true)
        if other then
            currentOtherInventory = other.name
        end
        QBCore.Functions.TriggerCallback('inventory:server:ConvertQuality', function(data)
            inventory = data.inventory
            other = data.other
            SendNUIMessage({
                action = "open",
                inventory = inventory,
                slots = Config.MaxInventorySlots,
                other = other,
                maxweight = Config.MaxInventoryWeight,
                Ammo = PlayerAmmo,
                maxammo = Config.MaximumAmmoValues,
                Name = PlayerData.charinfo.firstname .." ".. PlayerData.charinfo.lastname .." - [".. GetPlayerServerId(PlayerId()) .."]", 
        })
            inInventory = true
        end, inventory, other)
        end
    else return end
end)
```

Go to **fxmanifest.lua** and add
```
'@ox_lib/init.lua',
```
Done .

