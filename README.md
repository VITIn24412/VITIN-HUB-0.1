if game.PlaceId == 16732694052 then

    -- Load
    local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

    -- Main
    local Window = OrionLib:MakeWindow({Name = "VITIN HUB 1.01", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

    -- Global settings
    _G.AutoCast = false
    _G.AutoLancar = false
    _G.InstatanicReel = false
    _G.FixMapBeta = false
    _G.RepairMapBeta = false

    -- Function for AutoCast
    local function AutoCast()
        while _G.AutoCast do
            local args = {
                [1] = game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flimsy Rod")
            }
            game:GetService("Players").LocalPlayer.PlayerGui.hud.safezone.backpack.events.equip:FireServer(unpack(args))
            print("Auto-equipping Flimsy Rod.")
            wait(5)  -- Adjust the wait time as needed
        end
    end

    -- Function for AutoLancar
    local function AutoLancar()
        while _G.AutoLancar do
            local args = {
                [1] = 94.60000000000014,
                [2] = 1
            }
            local rod = game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flimsy Rod")
            if rod then
                rod.events.cast:FireServer(unpack(args))
                print("Auto-casting...")
            else
                print("Flimsy Rod not found!")
            end
            wait(10)  -- Adjust the wait time as needed
        end
    end

    -- Function for Instatanic Reel
    local function InstatanicReel()
        while _G.InstatanicReel do
            local args = {
                [1] = 100,
                [2] = true
            }
            game:GetService("ReplicatedStorage").events.reelfinished:FireServer(unpack(args))
            print("Instatanic Reel activated.")
            wait(1)  -- Adjust the frequency as needed
        end
    end

    -- Function for Fix Map Beta
    local function FixMapBeta()
        while _G.FixMapBeta do
            local args = {
                [1] = game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Treasure Map")
            }
            game:GetService("Players").LocalPlayer.PlayerGui.hud.safezone.backpack.events.equip:FireServer(unpack(args))
            print("Equipping Treasure Map.")
            wait(5)  -- Adjust the wait time as needed
        end
    end

    -- Function for Repair Map Beta
    local function RepairMapBeta()
        while _G.RepairMapBeta do
            workspace.world.npcs:FindFirstChild("Jack Marrow").treasure.repairmap:InvokeServer()
            print("Repairing Treasure Map.")
            wait(5)  -- Adjust the wait time as needed
        end
    end

    -- Function to teleport to specific islands
    local function TeleportToIsland(islandPosition)
        local player = game.Players.LocalPlayer
        if player and player.Character then
            local humanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")
            if humanoidRootPart then
                humanoidRootPart.CFrame = CFrame.new(islandPosition + Vector3.new(0, 100, 0))  -- Teleport to 100 units above the island
                print("Teleporting to island.")
            end
        end
    end

    -- Create Tabs and Toggles
    local EquiprodTab = Window:MakeTab({
        Name = "Equip rod",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    })

    local AutoCastSection = EquiprodTab:AddSection({
        Name = "Auto-Cast"
    })
    
    EquiprodTab:AddToggle({
        Name = "Auto-Cast",
        Default = false,
        Callback = function(Value)
            _G.AutoCast = Value
            if _G.AutoCast then
                AutoCast()
            end
        end   
    })

    local AutoLancarSection = EquiprodTab:AddSection({
        Name = "Auto-Lancar"
    })
    
    EquiprodTab:AddToggle({
        Name = "Auto-Lancar",
        Default = false,
        Callback = function(Value)
            _G.AutoLancar = Value
            if _G.AutoLancar then
                AutoLancar()
            end
        end    
    })

    local InstatanicReelSection = EquiprodTab:AddSection({
        Name = "Instatanic Reel"
    })
    
    EquiprodTab:AddToggle({
        Name = "Instatanic Reel",
        Default = false,
        Callback = function(Value)
            _G.InstatanicReel = Value
            if _G.InstatanicReel then
                InstatanicReel()
            end
        end
    })

    -- Create Fix Map Tab
    local FixMapTab = Window:MakeTab({
        Name = "Fix Map Beta",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    })

    local FixMapSection = FixMapTab:AddSection({
        Name = "Fix Map Beta"
    })
    
    FixMapSection:AddToggle({
        Name = "Enable Fix Map Beta",
        Default = false,
        Callback = function(Value)
            _G.FixMapBeta = Value
            if _G.FixMapBeta then
                FixMapBeta()
            end
        end
    })

    local RepairMapSection = FixMapTab:AddSection({
        Name = "Repair Map Beta"
    })
    
    RepairMapSection:AddToggle({
        Name = "Enable Repair Map Beta",
        Default = false,
        Callback = function(Value)
            _G.RepairMapBeta = Value
            if _G.RepairMapBeta then
                RepairMapBeta()
            end
        end
    })

    -- Create Teleport Tab and Buttons for Islands
    local TeleportTab = Window:MakeTab({
        Name = "Teleport",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    })

    local IslandSection = TeleportTab:AddSection({
        Name = "Islands"
    })
    
    IslandSection:AddButton({
        Name = "Sunstone",
        Callback = function()
            local islandPosition = Vector3.new(-932, 131, -1109)
            TeleportToIsland(islandPosition)
        end   
    })
    
    IslandSection:AddButton({
        Name = "Merlin",
        Callback = function()
            local islandPosition = Vector3.new(-1223, 195, -1044)
            TeleportToIsland(islandPosition)
        end   
    })
    
    IslandSection:AddButton({
        Name = "Rod Of The Depths",
        Callback = function()
            local islandPosition = Vector3.new(1689.9, -902.4, 1437.7)
            TeleportToIsland(islandPosition)
        end   
    })

    IslandSection:AddButton({
        Name = "Moosewood Dock",
        Callback = function()
            local islandPosition = Vector3.new(360, 133, 264)
            TeleportToIsland(islandPosition)
        end   
    })

    IslandSection:AddButton({
        Name = "Terrapin Island Dock",
        Callback = function()
            local islandPosition = Vector3.new(-196, 133, 1945)
            TeleportToIsland(islandPosition)
        end   
    })

    IslandSection:AddButton({
        Name = "Forsaken Shores Dock",
        Callback = function()
            local islandPosition = Vector3.new(-2485, 133, 1562)
            TeleportToIsland(islandPosition)
        end   
    })

    IslandSection:AddButton({
        Name = "Jack Marrow and Sunken Rod",
        Callback = function()
            local islandPosition = Vector3.new(-2828, 214, 1519)
            TeleportToIsland(islandPosition)
        end   
    })

    IslandSection:AddButton({
        Name = "Roslit Bay Dock",
        Callback = function()
            local islandPosition = Vector3.new(-1462, 132, 717)
            TeleportToIsland(islandPosition)
        end   
    })

    IslandSection:AddButton({
        Name = "Kings Rod",
        Callback = function()
            local islandPosition = Vector3.new(1377, -811, -297)
            TeleportToIsland(islandPosition)
        end   
    })

end
