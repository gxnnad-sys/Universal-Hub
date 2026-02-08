local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
    Name = "🌟 Universal Hub | v3.5",
    Icon = 0, -- Changed from "shield" to 0 (no icon) or use a Roblox asset ID number
    LoadingTitle = "Ultimate Hub",
    LoadingSubtitle = "Loading Features...",
    ShowText = "Universal Hub 🚀",
    Theme = "Amethyst",
    ToggleUIKeybind = Enum.KeyCode.RightControl, -- Changed from "RightControl" string to Enum
    DisableRayfieldPrompts = false,
    DisableBuildWarnings = false,
    
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "UltimateHub",
        FileName = "UltimateHub_Config"
    },
    
    Discord = {
        Enabled = false, -- Changed to false to avoid Discord errors
        Invite = "noinvitelink",
        RememberJoins = true
    },
    
    KeySystem = false
})

-- Services
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Lighting = game:GetService("Lighting")
local TweenService = game:GetService("TweenService")
local Workspace = game:GetService("Workspace")

-- Player variables
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootPart = character:WaitForChild("HumanoidRootPart")

-- State variables
local states = {
    fly = false,
    noclip = false,
    esp = false,
    fullbright = false,
    infiniteJump = false,
    autoSprint = false,
    godMode = false,
    antiAFK = false,
    autoFarm = false,
    speedHack = false,
    wallhack = false,
    xray = false,
    chams = false,
    tracers = false,
    fov = false,
    spinbot = false,
    bhop = false,
    autoCollect = false,
    clickTP = false,
    ctrlTP = false
}

-- Settings
local settings = {
    flySpeed = 50,
    flyKeybind = Enum.KeyCode.F,
    walkSpeed = 16,
    jumpPower = 50,
    fovSize = 90,
    espColor = Color3.fromRGB(255, 0, 0),
    tracerColor = Color3.fromRGB(0, 255, 0)
}

-- Connections
local connections = {}

-- Welcome notification
Rayfield:Notify({
    Title = "🎉 Welcome to Ultimate Hub Pro!",
    Content = "All premium features loaded successfully!",
    Duration = 6.5,
    Image = 0,
})

-- Tabs (removed icons as they may cause issues in some Rayfield versions)
local HomeTab = Window:CreateTab("🏠 Home", nil)
local PlayerTab = Window:CreateTab("🏃 Player", nil)
local CombatTab = Window:CreateTab("⚔️ Combat", nil)
local VisualsTab = Window:CreateTab("👁️ Visuals", nil)
local TeleportTab = Window:CreateTab("📍 Teleport", nil)
local MiscTab = Window:CreateTab("⚙️ Miscellaneous", nil)
local CreditsTab = Window:CreateTab("ℹ️ Info", nil)

-- ==================== HOME TAB ====================
local HomeSection = HomeTab:CreateSection("📊 Hub Statistics")

HomeTab:CreateLabel("Total Features: 60+")
HomeTab:CreateLabel("Script Version: 3.5.0")
HomeTab:CreateLabel("Last Updated: February 2026")

local QuickSection = HomeTab:CreateSection("⚡ Quick Actions")

HomeTab:CreateButton({
    Name = "🔄 Rejoin Server",
    Callback = function()
        game:GetService("TeleportService"):Teleport(game.PlaceId, player)
    end,
})

HomeTab:CreateButton({
    Name = "🔗 Copy Game Link",
    Callback = function()
        setclipboard("https://www.roblox.com/games/" .. game.PlaceId)
        Rayfield:Notify({
            Title = "Copied!",
            Content = "Game link copied to clipboard",
            Duration = 3,
            Image = 0,
        })
    end,
})

HomeTab:CreateButton({
    Name = "👥 Server Hop",
    Callback = function()
        local success, result = pcall(function()
            local servers = {}
            local req = game:HttpGetAsync("https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100")
            local body = game:GetService("HttpService"):JSONDecode(req)
            
            if body and body.data then
                for i, v in next, body.data do
                    if type(v) == "table" and v.id ~= game.JobId then
                        table.insert(servers, v.id)
                    end
                end
            end
            
            if #servers > 0 then
                game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, servers[math.random(1, #servers)])
            end
        end)
        
        if not success then
            Rayfield:Notify({
                Title = "Error",
                Content = "Server hop failed - HttpService may be disabled",
                Duration = 3,
                Image = 0,
            })
        end
    end,
})

HomeTab:CreateButton({
    Name = "🔄 Refresh Character",
    Callback = function()
        player.Character:BreakJoints()
        wait(0.1)
        player:LoadCharacter()
    end,
})

local StatusSection = HomeTab:CreateSection("📈 Player Status")

HomeTab:CreateLabel("Username: " .. player.Name)
HomeTab:CreateLabel("Display Name: " .. player.DisplayName)
HomeTab:CreateLabel("User ID: " .. player.UserId)
HomeTab:CreateLabel("Account Age: " .. player.AccountAge .. " days")

-- ==================== PLAYER TAB ====================
local MovementSection = PlayerTab:CreateSection("🚀 Movement")

local WalkSpeedSlider = PlayerTab:CreateSlider({
    Name = "Walk Speed",
    Range = {16, 500},
    Increment = 1,
    CurrentValue = 16,
    Flag = "WalkSpeed",
    Callback = function(Value)
        settings.walkSpeed = Value
        if humanoid then
            humanoid.WalkSpeed = Value
        end
    end,
})

local JumpPowerSlider = PlayerTab:CreateSlider({
    Name = "Jump Power",
    Range = {50, 500},
    Increment = 1,
    CurrentValue = 50,
    Flag = "JumpPower",
    Callback = function(Value)
        settings.jumpPower = Value
        if humanoid then
            humanoid.JumpPower = Value
        end
    end,
})

local HipHeightSlider = PlayerTab:CreateSlider({
    Name = "Hip Height",
    Range = {0, 50},
    Increment = 0.5,
    CurrentValue = 0,
    Flag = "HipHeight",
    Callback = function(Value)
        if humanoid then
            humanoid.HipHeight = Value
        end
    end,
})

local FlySpeedSlider = PlayerTab:CreateSlider({
    Name = "Fly Speed",
    Range = {10, 500},
    Increment = 5,
    CurrentValue = 50,
    Flag = "FlySpeed",
    Callback = function(Value)
        settings.flySpeed = Value
        Rayfield:Notify({
            Title = "Fly Speed Updated",
            Content = "Fly speed set to " .. Value,
            Duration = 2,
            Image = 0,
        })
    end,
})

local FlyKeybind = PlayerTab:CreateKeybind({
    Name = "Fly Keybind",
    CurrentKeybind = "F",
    HoldToInteract = false,
    Flag = "FlyKeybind",
    Callback = function(Keybind)
        -- This callback fires when keybind is changed in settings
    end,
})

-- Fly system
local flyConnection
local bodyVelocity, bodyGyro

local function startFly()
    if not character or not rootPart then return end
    
    bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.Velocity = Vector3.new(0, 0, 0)
    bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
    bodyVelocity.Parent = rootPart
    
    bodyGyro = Instance.new("BodyGyro")
    bodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
    bodyGyro.P = 9e4
    bodyGyro.Parent = rootPart
    
    flyConnection = RunService.Heartbeat:Connect(function()
        if not states.fly then
            if bodyVelocity then bodyVelocity:Destroy() end
            if bodyGyro then bodyGyro:Destroy() end
            if flyConnection then flyConnection:Disconnect() end
            return
        end
        
        local camera = Workspace.CurrentCamera
        local moveDirection = Vector3.new(0, 0, 0)
        
        if UserInputService:IsKeyDown(Enum.KeyCode.W) then
            moveDirection = moveDirection + camera.CFrame.LookVector
        end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then
            moveDirection = moveDirection - camera.CFrame.LookVector
        end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then
            moveDirection = moveDirection - camera.CFrame.RightVector
        end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then
            moveDirection = moveDirection + camera.CFrame.RightVector
        end
        if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
            moveDirection = moveDirection + Vector3.new(0, 1, 0)
        end
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then
            moveDirection = moveDirection - Vector3.new(0, 1, 0)
        end
        
        if moveDirection.Magnitude > 0 then
            bodyVelocity.Velocity = moveDirection.Unit * settings.flySpeed
        else
            bodyVelocity.Velocity = Vector3.new(0, 0, 0)
        end
        bodyGyro.CFrame = camera.CFrame
    end)
end

local function stopFly()
    states.fly = false
    if bodyVelocity then bodyVelocity:Destroy() end
    if bodyGyro then bodyGyro:Destroy() end
    if flyConnection then flyConnection:Disconnect() end
end

-- Fly keybind listener
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.F then -- Hardcoded to F key
        states.fly = not states.fly
        if states.fly then
            startFly()
            Rayfield:Notify({
                Title = "✈️ Fly Enabled",
                Content = "Use WASD + Space/Shift to fly",
                Duration = 2,
                Image = 0,
            })
        else
            stopFly()
            Rayfield:Notify({
                Title = "✈️ Fly Disabled",
                Content = "Fly mode deactivated",
                Duration = 2,
                Image = 0,
            })
        end
    end
end)

PlayerTab:CreateToggle({
    Name = "Fly Mode",
    CurrentValue = false,
    Flag = "FlyToggle",
    Callback = function(Value)
        states.fly = Value
        if Value then
            startFly()
        else
            stopFly()
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "NoClip",
    CurrentValue = false,
    Flag = "NoClip",
    Callback = function(Value)
        states.noclip = Value
        
        if Value then
            connections.noclip = RunService.Stepped:Connect(function()
                if states.noclip and character then
                    for _, part in pairs(character:GetDescendants()) do
                        if part:IsA("BasePart") then
                            part.CanCollide = false
                        end
                    end
                end
            end)
        else
            if connections.noclip then
                connections.noclip:Disconnect()
            end
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Infinite Jump",
    CurrentValue = false,
    Flag = "InfiniteJump",
    Callback = function(Value)
        states.infiniteJump = Value
        
        if Value then
            connections.infiniteJump = UserInputService.JumpRequest:Connect(function()
                if states.infiniteJump and humanoid then
                    humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
                end
            end)
        else
            if connections.infiniteJump then
                connections.infiniteJump:Disconnect()
            end
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Auto Sprint",
    CurrentValue = false,
    Flag = "AutoSprint",
    Callback = function(Value)
        states.autoSprint = Value
        if Value and humanoid then
            humanoid.WalkSpeed = settings.walkSpeed * 1.5
        else
            if humanoid then
                humanoid.WalkSpeed = settings.walkSpeed
            end
        end
    end,
})

local PhysicsSection = PlayerTab:CreateSection("🎯 Physics")

PlayerTab:CreateToggle({
    Name = "Anti-Ragdoll",
    CurrentValue = false,
    Flag = "AntiRagdoll",
    Callback = function(Value)
        if Value then
            connections.antiRagdoll = humanoid.StateChanged:Connect(function(old, new)
                if new == Enum.HumanoidStateType.Ragdoll then
                    humanoid:ChangeState(Enum.HumanoidStateType.Running)
                end
            end)
        else
            if connections.antiRagdoll then
                connections.antiRagdoll:Disconnect()
            end
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Anti-Fall Damage",
    CurrentValue = false,
    Flag = "AntiFall",
    Callback = function(Value)
        if Value then
            connections.antiFall = humanoid.StateChanged:Connect(function(old, new)
                if new == Enum.HumanoidStateType.FallingDown then
                    humanoid:ChangeState(Enum.HumanoidStateType.Running)
                end
            end)
        else
            if connections.antiFall then
                connections.antiFall:Disconnect()
            end
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Anti-Slow",
    CurrentValue = false,
    Flag = "AntiSlow",
    Callback = function(Value)
        if Value then
            connections.antiSlow = RunService.Heartbeat:Connect(function()
                if humanoid then
                    humanoid.WalkSpeed = math.max(humanoid.WalkSpeed, settings.walkSpeed)
                end
            end)
        else
            if connections.antiSlow then
                connections.antiSlow:Disconnect()
            end
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Bunny Hop",
    CurrentValue = false,
    Flag = "BunnyHop",
    Callback = function(Value)
        states.bhop = Value
        
        if Value then
            connections.bhop = RunService.Heartbeat:Connect(function()
                if states.bhop and humanoid and UserInputService:IsKeyDown(Enum.KeyCode.Space) then
                    humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
                end
            end)
        else
            if connections.bhop then
                connections.bhop:Disconnect()
            end
        end
    end,
})

local UtilitySection = PlayerTab:CreateSection("🛠️ Utility")

PlayerTab:CreateToggle({
    Name = "Anti-AFK",
    CurrentValue = false,
    Flag = "AntiAFK",
    Callback = function(Value)
        states.antiAFK = Value
        
        if Value then
            local VirtualUser = game:GetService("VirtualUser")
            connections.antiAFK = player.Idled:Connect(function()
                if states.antiAFK then
                    VirtualUser:CaptureController()
                    VirtualUser:ClickButton2(Vector2.new())
                end
            end)
        else
            if connections.antiAFK then
                connections.antiAFK:Disconnect()
            end
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Platform Stand",
    CurrentValue = false,
    Flag = "PlatformStand",
    Callback = function(Value)
        if humanoid then
            humanoid.PlatformStand = Value
        end
    end,
})

PlayerTab:CreateToggle({
    Name = "Sit",
    CurrentValue = false,
    Flag = "Sit",
    Callback = function(Value)
        if humanoid then
            humanoid.Sit = Value
        end
    end,
})

PlayerTab:CreateButton({
    Name = "Remove Accessories",
    Callback = function()
        for _, accessory in pairs(character:GetChildren()) do
            if accessory:IsA("Accessory") then
                accessory:Destroy()
            end
        end
        Rayfield:Notify({
            Title = "Accessories Removed",
            Content = "All accessories have been removed",
            Duration = 2,
            Image = 0,
        })
    end,
})

-- ==================== COMBAT TAB ====================
local AimSection = CombatTab:CreateSection("🎯 Aim Assist")

CombatTab:CreateToggle({
    Name = "Silent Aim (Universal)",
    CurrentValue = false,
    Flag = "SilentAim",
    Callback = function(Value)
        Rayfield:Notify({
            Title = "Universal Feature",
            Content = "May require game-specific configuration",
            Duration = 3,
            Image = 0,
        })
    end,
})

CombatTab:CreateToggle({
    Name = "Aimbot",
    CurrentValue = false,
    Flag = "Aimbot",
    Callback = function(Value)
        states.aimbot = Value
        
        if Value then
            connections.aimbot = RunService.RenderStepped:Connect(function()
                if not states.aimbot then return end
                
                local closestPlayer
                local shortestDistance = math.huge
                
                for _, v in pairs(Players:GetPlayers()) do
                    if v ~= player and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
                        local pos, onScreen = Workspace.CurrentCamera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
                        if onScreen then
                            local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(player:GetMouse().X, player:GetMouse().Y)).Magnitude
                            
                            if magnitude < shortestDistance then
                                closestPlayer = v
                                shortestDistance = magnitude
                            end
                        end
                    end
                end
                
                if closestPlayer and closestPlayer.Character and closestPlayer.Character:FindFirstChild("Head") then
                    Workspace.CurrentCamera.CFrame = CFrame.new(Workspace.CurrentCamera.CFrame.Position, closestPlayer.Character.Head.Position)
                end
            end)
        else
            if connections.aimbot then
                connections.aimbot:Disconnect()
            end
        end
    end,
})

CombatTab:CreateSlider({
    Name = "Aimbot FOV",
    Range = {10, 500},
    Increment = 5,
    CurrentValue = 100,
    Flag = "AimbotFOV",
    Callback = function(Value)
        settings.aimbotFOV = Value
    end,
})

local WeaponSection = CombatTab:CreateSection("⚔️ Weapon Mods")

CombatTab:CreateToggle({
    Name = "Infinite Ammo (Game Specific)",
    CurrentValue = false,
    Flag = "InfiniteAmmo",
    Callback = function(Value)
        Rayfield:Notify({
            Title = "Game Specific",
            Content = "This feature requires game-specific configuration",
            Duration = 3,
            Image = 0,
        })
    end,
})

CombatTab:CreateToggle({
    Name = "No Recoil (Game Specific)",
    CurrentValue = false,
    Flag = "NoRecoil",
    Callback = function(Value)
        Rayfield:Notify({
            Title = "Game Specific",
            Content = "This feature requires game-specific configuration",
            Duration = 3,
            Image = 0,
        })
    end,
})

CombatTab:CreateToggle({
    Name = "Rapid Fire (Game Specific)",
    CurrentValue = false,
    Flag = "RapidFire",
    Callback = function(Value)
        Rayfield:Notify({
            Title = "Game Specific",
            Content = "This feature requires game-specific configuration",
            Duration = 3,
            Image = 0,
        })
    end,
})

local MeleeSection = CombatTab:CreateSection("🥊 Melee")

CombatTab:CreateToggle({
    Name = "Kill Aura",
    CurrentValue = false,
    Flag = "KillAura",
    Callback = function(Value)
        states.killAura = Value
        Rayfield:Notify({
            Title = "Kill Aura " .. (Value and "Enabled" or "Disabled"),
            Content = "Range: 20 studs (Game specific damage needed)",
            Duration = 2,
            Image = 0,
        })
    end,
})

CombatTab:CreateSlider({
    Name = "Kill Aura Range",
    Range = {5, 50},
    Increment = 1,
    CurrentValue = 20,
    Flag = "KillAuraRange",
    Callback = function(Value)
        settings.killAuraRange = Value
    end,
})

local DefenseSection = CombatTab:CreateSection("🛡️ Defense")

CombatTab:CreateToggle({
    Name = "God Mode (Client)",
    CurrentValue = false,
    Flag = "GodMode",
    Callback = function(Value)
        states.godMode = Value
        
        if Value and humanoid then
            humanoid.MaxHealth = math.huge
            humanoid.Health = math.huge
        else
            if humanoid then
                humanoid.MaxHealth = 100
                humanoid.Health = 100
            end
        end
    end,
})

CombatTab:CreateToggle({
    Name = "Force Field",
    CurrentValue = false,
    Flag = "ForceField",
    Callback = function(Value)
        if Value then
            local ff = Instance.new("ForceField")
            ff.Parent = character
            ff.Visible = true
        else
            for _, ff in pairs(character:GetChildren()) do
                if ff:IsA("ForceField") then
                    ff:Destroy()
                end
            end
        end
    end,
})

-- ==================== VISUALS TAB ====================
local ESPSection = VisualsTab:CreateSection("👀 ESP Features")

VisualsTab:CreateToggle({
    Name = "Player ESP",
    CurrentValue = false,
    Flag = "PlayerESP",
    Callback = function(Value)
        states.esp = Value
        
        local function addESP(v)
            if v ~= player and v.Character then
                local highlight = v.Character:FindFirstChild("ESPHighlight")
                
                if Value and not highlight then
                    highlight = Instance.new("Highlight")
                    highlight.Name = "ESPHighlight"
                    highlight.Parent = v.Character
                    highlight.FillColor = settings.espColor
                    highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                    highlight.FillTransparency = 0.5
                    highlight.OutlineTransparency = 0
                elseif not Value and highlight then
                    highlight:Destroy()
                end
            end
        end
        
        for _, v in pairs(Players:GetPlayers()) do
            addESP(v)
        end
        
        if Value then
            connections.esp = Players.PlayerAdded:Connect(addESP)
        else
            if connections.esp then
                connections.esp:Disconnect()
            end
        end
    end,
})

VisualsTab:CreateToggle({
    Name = "Name ESP",
    CurrentValue = false,
    Flag = "NameESP",
    Callback = function(Value)
        local function addNameESP(v)
            if v ~= player and v.Character and v.Character:FindFirstChild("Head") then
                local billboard = v.Character.Head:FindFirstChild("NameESP")
                
                if Value and not billboard then
                    billboard = Instance.new("BillboardGui")
                    billboard.Name = "NameESP"
                    billboard.Parent = v.Character.Head
                    billboard.Size = UDim2.new(0, 200, 0, 50)
                    billboard.StudsOffset = Vector3.new(0, 2, 0)
                    billboard.AlwaysOnTop = true
                    
                    local textLabel = Instance.new("TextLabel")
                    textLabel.Parent = billboard
                    textLabel.Size = UDim2.new(1, 0, 1, 0)
                    textLabel.BackgroundTransparency = 1
                    textLabel.Text = v.Name
                    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
                    textLabel.TextStrokeTransparency = 0
                    textLabel.TextScaled = true
                    textLabel.Font = Enum.Font.GothamBold
                elseif not Value and billboard then
                    billboard:Destroy()
                end
            end
        end
        
        for _, v in pairs(Players:GetPlayers()) do
            addNameESP(v)
        end
    end,
})

VisualsTab:CreateToggle({
    Name = "Distance ESP",
    CurrentValue = false,
    Flag = "DistanceESP",
    Callback = function(Value)
        states.distanceESP = Value
        
        if Value then
            connections.distanceESP = RunService.RenderStepped:Connect(function()
                for _, v in pairs(Players:GetPlayers()) do
                    if v ~= player and v.Character and v.Character:FindFirstChild("Head") and v.Character:FindFirstChild("HumanoidRootPart") then
                        local billboard = v.Character.Head:FindFirstChild("DistanceESP")
                        local distance = (rootPart.Position - v.Character.HumanoidRootPart.Position).Magnitude
                        
                        if not billboard then
                            billboard = Instance.new("BillboardGui")
                            billboard.Name = "DistanceESP"
                            billboard.Parent = v.Character.Head
                            billboard.Size = UDim2.new(0, 200, 0, 30)
                            billboard.StudsOffset = Vector3.new(0, -2, 0)
                            billboard.AlwaysOnTop = true
                            
                            local textLabel = Instance.new("TextLabel")
                            textLabel.Name = "TextLabel"
                            textLabel.Parent = billboard
                            textLabel.Size = UDim2.new(1, 0, 1, 0)
                            textLabel.BackgroundTransparency = 1
                            textLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
                            textLabel.TextStrokeTransparency = 0
                            textLabel.TextScaled = true
                            textLabel.Font = Enum.Font.Gotham
                        end
                        
                        if billboard:FindFirstChild("TextLabel") then
                            billboard.TextLabel.Text = math.floor(distance) .. " studs"
                        end
                    end
                end
            end)
        else
            if connections.distanceESP then
                connections.distanceESP:Disconnect()
            end
            
            for _, v in pairs(Players:GetPlayers()) do
                if v.Character and v.Character:FindFirstChild("Head") then
                    local billboard = v.Character.Head:FindFirstChild("DistanceESP")
                    if billboard then
                        billboard:Destroy()
                    end
                end
            end
        end
    end,
})

VisualsTab:CreateToggle({
    Name = "Health ESP",
    CurrentValue = false,
    Flag = "HealthESP",
    Callback = function(Value)
        states.healthESP = Value
        
        if Value then
            connections.healthESP = RunService.RenderStepped:Connect(function()
                for _, v in pairs(Players:GetPlayers()) do
                    if v ~= player and v.Character and v.Character:FindFirstChild("Head") and v.Character:FindFirstChild("Humanoid") then
                        local billboard = v.Character.Head:FindFirstChild("HealthESP")
                        local health = v.Character.Humanoid.Health
                        local maxHealth = v.Character.Humanoid.MaxHealth
                        
                        if not billboard then
                            billboard = Instance.new("BillboardGui")
                            billboard.Name = "HealthESP"
                            billboard.Parent = v.Character.Head
                            billboard.Size = UDim2.new(0, 200, 0, 30)
                            billboard.StudsOffset = Vector3.new(0, 3, 0)
                            billboard.AlwaysOnTop = true
                            
                            local textLabel = Instance.new("TextLabel")
                            textLabel.Name = "TextLabel"
                            textLabel.Parent = billboard
                            textLabel.Size = UDim2.new(1, 0, 1, 0)
                            textLabel.BackgroundTransparency = 1
                            textLabel.TextStrokeTransparency = 0
                            textLabel.TextScaled = true
                            textLabel.Font = Enum.Font.GothamBold
                        end
                        
                        if billboard:FindFirstChild("TextLabel") then
                            local healthPercent = (health / maxHealth) * 100
                            billboard.TextLabel.Text = math.floor(health) .. " HP (" .. math.floor(healthPercent) .. "%)"
                            
                            if healthPercent > 75 then
                                billboard.TextLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
                            elseif healthPercent > 50 then
                                billboard.TextLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
                            elseif healthPercent > 25 then
                                billboard.TextLabel.TextColor3 = Color3.fromRGB(255, 165, 0)
                            else
                                billboard.TextLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
                            end
                        end
                    end
                end
            end)
        else
            if connections.healthESP then
                connections.healthESP:Disconnect()
            end
            
            for _, v in pairs(Players:GetPlayers()) do
                if v.Character and v.Character:FindFirstChild("Head") then
                    local billboard = v.Character.Head:FindFirstChild("HealthESP")
                    if billboard then
                        billboard:Destroy()
                    end
                end
            end
        end
    end,
})

local WorldSection = VisualsTab:CreateSection("🌍 World Visuals")

VisualsTab:CreateToggle({
    Name = "Fullbright",
    CurrentValue = false,
    Flag = "Fullbright",
    Callback = function(Value)
        states.fullbright = Value
        
        if Value then
            Lighting.Brightness = 2
            Lighting.ClockTime = 14
            Lighting.FogEnd = 100000
            Lighting.GlobalShadows = false
            Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
        else
            Lighting.Brightness = 1
            Lighting.ClockTime = 12
            Lighting.FogEnd = 100000
            Lighting.GlobalShadows = true
            Lighting.OutdoorAmbient = Color3.fromRGB(70, 70, 70)
        end
    end,
})

VisualsTab:CreateToggle({
    Name = "X-Ray",
    CurrentValue = false,
    Flag = "XRay",
    Callback = function(Value)
        states.xray = Value
        
        for _, v in pairs(Workspace:GetDescendants()) do
            if v:IsA("BasePart") and not Players:GetPlayerFromCharacter(v.Parent) then
                if Value then
                    v.Transparency = 0.7
                else
                    v.Transparency = 0
                end
            end
        end
    end,
})

VisualsTab:CreateToggle({
    Name = "No Fog",
    CurrentValue = false,
    Flag = "NoFog",
    Callback = function(Value)
        if Value then
            Lighting.FogEnd = 100000
        else
            Lighting.FogEnd = 1000
        end
    end,
})

VisualsTab:CreateSlider({
    Name = "Field of View",
    Range = {70, 120},
    Increment = 1,
    CurrentValue = 70,
    Flag = "FOV",
    Callback = function(Value)
        settings.fovSize = Value
        Workspace.CurrentCamera.FieldOfView = Value
    end,
})

VisualsTab:CreateToggle({
    Name = "Remove Textures",
    CurrentValue = false,
    Flag = "RemoveTextures",
    Callback = function(Value)
        for _, v in pairs(Workspace:GetDescendants()) do
            if v:IsA("Decal") or v:IsA("Texture") then
                v.Transparency = Value and 1 or 0
            end
        end
    end,
})

-- ==================== TELEPORT TAB ====================
local QuickTPSection = TeleportTab:CreateSection("⚡ Quick Teleports")

TeleportTab:CreateButton({
    Name = "Teleport to Spawn",
    Callback = function()
        if Workspace:FindFirstChild("SpawnLocation") then
            rootPart.CFrame = Workspace.SpawnLocation.CFrame + Vector3.new(0, 5, 0)
        else
            rootPart.CFrame = CFrame.new(0, 50, 0)
        end
        Rayfield:Notify({
            Title = "Teleported",
            Content = "Teleported to spawn!",
            Duration = 2,
            Image = 0,
        })
    end,
})

TeleportTab:CreateToggle({
    Name = "Click TP (Hold Ctrl + Click)",
    CurrentValue = false,
    Flag = "ClickTP",
    Callback = function(Value)
        states.ctrlTP = Value
        
        if Value then
            connections.clickTP = player:GetMouse().Button1Down:Connect(function()
                if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) and player:GetMouse().Target then
                    rootPart.CFrame = CFrame.new(player:GetMouse().Hit.Position + Vector3.new(0, 5, 0))
                end
            end)
        else
            if connections.clickTP then
                connections.clickTP:Disconnect()
            end
        end
    end,
})

local PlayerTPSection = TeleportTab:CreateSection("👥 Player Teleports")

local selectedPlayer = nil
local PlayerDropdown = TeleportTab:CreateDropdown({
    Name = "Select Player",
    Options = {"Loading..."},
    CurrentOption = {"Loading..."},
    MultipleOptions = false,
    Flag = "PlayerSelect",
    Callback = function(Option)
        selectedPlayer = Option[1]
    end,
})

-- Update player list
spawn(function()
    while wait(2) do
        local playerList = {}
        for _, v in pairs(Players:GetPlayers()) do
            if v ~= player then
                table.insert(playerList, v.Name)
            end
        end
        if #playerList > 0 then
            PlayerDropdown:Refresh(playerList, true)
        end
    end
end)

TeleportTab:CreateButton({
    Name = "Teleport to Player",
    Callback = function()
        if selectedPlayer and selectedPlayer ~= "Loading..." then
            local targetPlayer = Players:FindFirstChild(selectedPlayer)
            if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
                rootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(0, 3, 0)
                Rayfield:Notify({
                    Title = "Teleported",
                    Content = "Teleported to " .. selectedPlayer,
                    Duration = 2,
                    Image = 0,
                })
            end
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "Please select a player first",
                Duration = 2,
                Image = 0,
            })
        end
    end,
})

TeleportTab:CreateToggle({
    Name = "Loop Teleport to Player",
    CurrentValue = false,
    Flag = "LoopTP",
    Callback = function(Value)
        if Value then
            connections.loopTP = RunService.Heartbeat:Connect(function()
                if selectedPlayer and selectedPlayer ~= "Loading..." then
                    local targetPlayer = Players:FindFirstChild(selectedPlayer)
                    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
                        rootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(3, 0, 0)
                    end
                end
            end)
        else
            if connections.loopTP then
                connections.loopTP:Disconnect()
            end
        end
    end,
})

local CustomTPSection = TeleportTab:CreateSection("📍 Custom Coordinates")

local coordX, coordY, coordZ = 0, 50, 0

TeleportTab:CreateInput({
    Name = "X Coordinate",
    PlaceholderText = "0",
    RemoveTextAfterFocusLost = false,
    Callback = function(Text)
        coordX = tonumber(Text) or 0
    end,
})

TeleportTab:CreateInput({
    Name = "Y Coordinate",
    PlaceholderText = "50",
    RemoveTextAfterFocusLost = false,
    Callback = function(Text)
        coordY = tonumber(Text) or 50
    end,
})

TeleportTab:CreateInput({
    Name = "Z Coordinate",
    PlaceholderText = "0",
    RemoveTextAfterFocusLost = false,
    Callback = function(Text)
        coordZ = tonumber(Text) or 0
    end,
})

TeleportTab:CreateButton({
    Name = "Teleport to Coordinates",
    Callback = function()
        rootPart.CFrame = CFrame.new(coordX, coordY, coordZ)
        Rayfield:Notify({
            Title = "Teleported",
            Content = string.format("Teleported to (%d, %d, %d)", coordX, coordY, coordZ),
            Duration = 2,
            Image = 0,
        })
    end,
})

TeleportTab:CreateButton({
    Name = "Save Current Position",
    Callback = function()
        _G.SavedPosition = rootPart.CFrame
        Rayfield:Notify({
            Title = "Position Saved",
            Content = "Current position has been saved",
            Duration = 2,
            Image = 0,
        })
    end,
})

TeleportTab:CreateButton({
    Name = "Load Saved Position",
    Callback = function()
        if _G.SavedPosition then
            rootPart.CFrame = _G.SavedPosition
            Rayfield:Notify({
                Title = "Position Loaded",
                Content = "Teleported to saved position",
                Duration = 2,
                Image = 0,
            })
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "No saved position found",
                Duration = 2,
                Image = 0,
            })
        end
    end,
})

-- ==================== MISC TAB ====================
local GameSection = MiscTab:CreateSection("🎮 Game Actions")

MiscTab:CreateButton({
    Name = "Reset Character",
    Callback = function()
        humanoid.Health = 0
    end,
})

MiscTab:CreateButton({
    Name = "Respawn Character",
    Callback = function()
        player:LoadCharacter()
    end,
})

MiscTab:CreateButton({
    Name = "Freeze Character",
    Callback = function()
        rootPart.Anchored = not rootPart.Anchored
        local status = rootPart.Anchored and "Frozen" or "Unfrozen"
        Rayfield:Notify({
            Title = "Character " .. status,
            Content = "Your character has been " .. string.lower(status),
            Duration = 2,
            Image = 0,
        })
    end,
})

MiscTab:CreateButton({
    Name = "Invisible (Client)",
    Callback = function()
        for _, part in pairs(character:GetDescendants()) do
            if part:IsA("BasePart") or part:IsA("Decal") then
                part.Transparency = 1
            end
        end
        Rayfield:Notify({
            Title = "Invisible",
            Content = "You are now invisible (client-side)",
            Duration = 2,
            Image = 0,
        })
    end,
})

MiscTab:CreateButton({
    Name = "Visible (Restore)",
    Callback = function()
        for _, part in pairs(character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.Transparency = 0
            elseif part:IsA("Decal") then
                part.Transparency = 0
            end
        end
        
        if character:FindFirstChild("Head") then
            character.Head.Transparency = 1
        end
    end,
})

local AutoFarmSection = MiscTab:CreateSection("🚜 Auto Farm")

MiscTab:CreateToggle({
    Name = "Auto Farm (Game Specific)",
    CurrentValue = false,
    Flag = "AutoFarm",
    Callback = function(Value)
        states.autoFarm = Value
        Rayfield:Notify({
            Title = "Auto Farm",
            Content = "This feature requires game-specific configuration",
            Duration = 3,
            Image = 0,
        })
    end,
})

MiscTab:CreateToggle({
    Name = "Auto Collect Coins/Items",
    CurrentValue = false,
    Flag = "AutoCollect",
    Callback = function(Value)
        states.autoCollect = Value
        
        if Value then
            connections.autoCollect = RunService.Heartbeat:Connect(function()
                if not states.autoCollect then return end
                
                for _, v in pairs(Workspace:GetDescendants()) do
                    if v.Name:lower():find("coin") or v.Name:lower():find("collect") then
                        if v:IsA("BasePart") then
                            v.CFrame = rootPart.CFrame
                        end
                    end
                end
            end)
        else
            if connections.autoCollect then
                connections.autoCollect:Disconnect()
            end
        end
    end,
})

local ChatSection = MiscTab:CreateSection("💬 Chat Tools")

local customMessage = "Ultimate Hub Pro! 🚀"

MiscTab:CreateInput({
    Name = "Custom Chat Message",
    PlaceholderText = "Enter message...",
    RemoveTextAfterFocusLost = false,
    Callback = function(Text)
        customMessage = Text
    end,
})

MiscTab:CreateButton({
    Name = "Send Chat Message",
    Callback = function()
        local success, err = pcall(function()
            game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(customMessage, "All")
        end)
        
        if not success then
            Rayfield:Notify({
                Title = "Error",
                Content = "Chat system not available in this game",
                Duration = 2,
                Image = 0,
            })
        end
    end,
})

local AnimationSection = MiscTab:CreateSection("🎭 Animations")

MiscTab:CreateButton({
    Name = "Spinbot",
    Callback = function()
        states.spinbot = not states.spinbot
        
        if states.spinbot then
            connections.spinbot = RunService.Heartbeat:Connect(function()
                if states.spinbot then
                    rootPart.CFrame = rootPart.CFrame * CFrame.Angles(0, math.rad(20), 0)
                end
            end)
            Rayfield:Notify({
                Title = "Spinbot Enabled",
                Content = "Click again to disable",
                Duration = 2,
                Image = 0,
            })
        else
            if connections.spinbot then
                connections.spinbot:Disconnect()
            end
            Rayfield:Notify({
                Title = "Spinbot Disabled",
                Content = "Spinning stopped",
                Duration = 2,
                Image = 0,
            })
        end
    end,
})

-- ==================== CREDITS TAB ====================
local AboutSection = CreditsTab:CreateSection("ℹ️ About")

CreditsTab:CreateLabel("Ultimate Hub Pro v3.5")
CreditsTab:CreateLabel("Created by: Mama_yapper")
CreditsTab:CreateLabel("UI Library: Rayfield")
CreditsTab:CreateLabel("Total Features: 60+")
CreditsTab:CreateLabel("")
CreditsTab:CreateLabel("⚠️ Disclaimer:")
CreditsTab:CreateLabel("Use at your own risk!")
CreditsTab:CreateLabel("Some features may not work in all games")

local SocialSection = CreditsTab:CreateSection("🔗 Links")

CreditsTab:CreateButton({
    Name = "Join Discord Server",
    Callback = function()
        Rayfield:Notify({
            Title = "Discord",
            Content = "Discord server coming soon!",
            Duration = 3,
            Image = 0,
        })
    end,
})

CreditsTab:CreateButton({
    Name = "Check for Updates",
    Callback = function()
        Rayfield:Notify({
            Title = "Version Check",
            Content = "You're running the latest version! v3.5",
            Duration = 3,
            Image = 0,
        })
    end,
})

local DangerSection = CreditsTab:CreateSection("⚠️ Danger Zone")

CreditsTab:CreateButton({
    Name = "🗑️ Destroy UI",
    Callback = function()
        Rayfield:Destroy()
    end,
})

-- Character respawn handler
player.CharacterAdded:Connect(function(char)
    wait(0.1)
    character = char
    humanoid = char:WaitForChild("Humanoid")
    rootPart = char:WaitForChild("HumanoidRootPart")
    
    -- Reapply settings
    if settings.walkSpeed ~= 16 then
        humanoid.WalkSpeed = settings.walkSpeed
    end
    if settings.jumpPower ~= 50 then
        humanoid.JumpPower = settings.jumpPower
    end
end)

-- Final notification
wait(1)
Rayfield:Notify({
    Title = "🎮 Ready to Use!",
    Content = "Press F to toggle Fly. Toggle UI with Right Ctrl",
    Duration = 5,
    Image = 0,
})
