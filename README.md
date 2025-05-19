--KoKaS BR
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
 
 
 local Window = Fluent:CreateWindow({
    Title = "KoKaS BR       [ Versão Gratis ]" .. Fluent.Version,
    TabWidth = 160, Size = UDim2.fromOffset(580, 460), Theme = "Dark"
})

local Tabs = {
    Main = Window:AddTab({ Title = "Casa" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

local Toggle = Tabs.Main:AddToggle("MyToggle", { Title = "Auto Farm level" })
Toggle:OnChanged(function() print(Options.MyToggle.Value) end) 
 
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local Workspace = game:GetService("Workspace")

-- Fast Attack
_G.FastAttack = true

spawn(function()
    while _G.FastAttack do
        pcall(function()
            local args = {
                [1] = "Combat",
                [2] = true
            }
            ReplicatedStorage.Remotes.Combat:FireServer(unpack(args))
        end)
        wait(0.1)
    end
end)

-- Bring Mobs (puxa os NPCs para perto)
_G.BringMobs = true

spawn(function()
    while _G.BringMobs do
        for i,v in pairs(Workspace.Enemies:GetChildren()) do
            if v:FindFirstChild("HumanoidRootPart") then
                v.HumanoidRootPart.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,5)
                v.Humanoid.WalkSpeed = 0
                v.Humanoid.JumpPower = 0
            end
        end
        wait(0.5)
    end
end)

-- ESP de Frutas
_G.FruitESP = true

spawn(function()
    while _G.FruitESP do
        for i,v in pairs(Workspace:GetChildren()) do
            if string.find(v.Name, "Fruit") then
                if not v:FindFirstChild("BillboardGui") then
                    local gui = Instance.new("BillboardGui", v)
                    gui.Size = UDim2.new(0,100,0,40)
                    gui.AlwaysOnTop = true
                    local txt = Instance.new("TextLabel", gui)
                    txt.Text = v.Name
                    txt.Size = UDim2.new(1,0,1,0)
                    txt.BackgroundTransparency = 1
                    txt.TextColor3 = Color3.new(1,0,0)
                    txt.TextStrokeTransparency = 0
                end
            end
        end
        wait(2)
    end
end)

-- Auto Teleporte para Second Sea
_G.GoSecondSea = true

spawn(function()
    while _G.GoSecondSea do
        if LocalPlayer.Level.Value >= 700 then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelSecondSea")
            _G.GoSecondSea = false
        end
        wait(10)
    end
end)

-- Auto Farm básico (ataca o inimigo mais próximo)
_G.AutoFarm = true

spawn(function()
    while _G.AutoFarm do
        local closestEnemy = nil
        local shortestDistance = math.huge
        for i,v in pairs(Workspace.Enemies:GetChildren()) do
            if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                local distance = (v.HumanoidRootPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).magnitude
                if distance < shortestDistance then
                    closestEnemy = v
                    shortestDistance = distance
                end
            end
        end

        if closestEnemy then
            LocalPlayer.Character.HumanoidRootPart.CFrame = closestEnemy.HumanoidRootPart.CFrame * CFrame.new(0,10,0)
        end
        wait(0.2)
    end
end)
