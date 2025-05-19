--KoKaS BR
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/wall"))()

local Window = Library:CreateWindow("KoKaS BR        [ Versão Grátis")

-- Variáveis globais
getgenv().autoFarm = true
getgenv().autoMaestria = true

-- Auto Farm Tab
local FarmTab = Window:CreateFolder("Auto Farm")

FarmTab:Toggle("Ativar Auto Farm (Bandit)", function(state)
    getgenv().autoFarm = state
    if state then
        spawn(function()
            while getgenv().autoFarm do
                for _, v in pairs(workspace.Enemies:GetChildren()) do
                    if v.Name == "Bandit" and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                        local hrp = game.Players.LocalPlayer.Character.HumanoidRootPart
                        hrp.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 5, 0)
                        game:GetService("VirtualInputManager"):SendMouseButtonEvent(0, 0, 0, true, game, 1)
                        game:GetService("VirtualInputManager"):SendMouseButtonEvent(0, 0, 0, true, game, 1)
                        repeat task.wait() until v.Humanoid.Health <= 0 or not getgenv().autoFarm
                    end
                end
                task.wait()
            end
        end)
    end
end)

-- Maestria Tab
FarmTab:Toggle("Auto Maestria (simples)", function(state)
    getgenv().autoMaestria = state
end)

-- Teleporte Tab
local TeleportTab = Window:CreateFolder("Teleportes")

TeleportTab:Button("TP Ilha Prehistoric", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-12000, 300, -7000)
end)

TeleportTab:Button("TP Mirage Island", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5000, 200, 14000)
end)

TeleportTab:Button("TP Dragon Dojo", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(3800, 100, -2900)
end)

-- V4 e God Human
local V4Tab = Window:CreateFolder("V4 & God Human")

V4Tab:Button("Ativar Trial V4 (beta)", function()
    print("Trial V4 iniciado (placeholder)")
end)

V4Tab:Button("Auto God Human (futuro)", function()
    print("Auto God Human ativado (placeholder)")
end)

-- Créditos
local Creditos = Window:CreateFolder("Créditos")
Creditos:Button("Script feito por ikaro ale miguel gabriel ruan", function()
    setclipboard("https://discord.gg/bBacZyU3")
end)
