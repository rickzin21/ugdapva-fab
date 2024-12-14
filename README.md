--Abaixo estará nossa Lib da UI

local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

local Main = UI:Tab{
    Name = "Main"
 }
 
 local Divider = Main:Divider{
    Name = "Main shit"
 }
 
 local QuitDivider = Main:Divider{
    Name = "Quit"
 }
 
 local KillAll = Divider:Button{
    Name = "Kill all",
    Description = "Kills all the players in the game!",
    Callback = function()
        print("All players killed.")
    end
 }
 
local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")

local function createDamageCircle(radius, damage)
    local part = Instance.new("Part")
    part.Shape = Enum.PartType.Ball
    part.Size = Vector3.new(radius*2, radius*2, radius*2)
    part.Anchored = true
    part.CanCollide = false
    part.Transparency = 0.5
    part.Color = Color3.fromRGB(255, 0, 0)
    part.Parent = Workspace
    part.Position = Vector3.new(0, 10, 0) 

    local function applyDamage()
        for _, player in pairs(Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local distance = (part.Position - player.Character.HumanoidRootPart.Position).magnitude
                if distance <= radius then
                    player.Character.Humanoid:TakeDamage(damage)
                end
            end
        end
    end

    while true do
        applyDamage()
        wait(1) 
    end
end

createDamageCircle(10, 10)
