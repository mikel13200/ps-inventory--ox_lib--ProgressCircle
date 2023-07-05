# ps-inventory--ox_lib--ProgressCircle

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
