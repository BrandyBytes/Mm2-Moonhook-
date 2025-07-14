-- MM2 Shadow GUI - by Moonhook
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local CoreGui = game:GetService("CoreGui")

-- GUI Setup
local ScreenGui = Instance.new("ScreenGui", CoreGui)
ScreenGui.Name = "MM2ShadowGUI"

local main = Instance.new("Frame", ScreenGui)
main.Size = UDim2.new(0, 250, 0, 300)
main.Position = UDim2.new(0.05, 0, 0.3, 0)
main.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
main.BorderSizePixel = 0

local uicorner = Instance.new("UICorner", main)
uicorner.CornerRadius = UDim.new(0, 8)

local title = Instance.new("TextLabel", main)
title.Size = UDim2.new(1, 0, 0, 30)
title.Text = "MM2 Shadow GUI - by Moonhook"
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 16

-- Button Utility
local buttonsCount = 0
function addButton(text, callback)
    local btn = Instance.new("TextButton", main)
    btn.Size = UDim2.new(1, -20, 0, 30)
    btn.Position = UDim2.new(0, 10, 0, 40 + buttonsCount * 35)
    btn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Text = text
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 14
    btn.MouseButton1Click:Connect(callback)
    local uic = Instance.new("UICorner", btn)
    uic.CornerRadius = UDim.new(0, 6)
    buttonsCount = buttonsCount + 1
end

-- ESP Button
addButton("Enable ESP", function()
    for _, plr in pairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character then
            if not plr.Character:FindFirstChild("Highlight") then
                local highlight = Instance.new("Highlight", plr.Character)
                highlight.FillColor = Color3.fromRGB(255, 0, 0)
                highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
            end
        end
    end
end)

-- Charm Visual Button (Aura)
addButton("Enable Charm", function()
    local char = LocalPlayer.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        if not char.HumanoidRootPart:FindFirstChildOfClass("ParticleEmitter") then
            local aura = Instance.new("ParticleEmitter", char.HumanoidRootPart)
            aura.Texture = "rbxassetid://4841070226"
            aura.Rate = 15
            aura.Size = NumberSequence.new(1)
            aura.LightEmission = 1
            aura.Color = ColorSequence.new(Color3.fromRGB(255, 0, 255))
        end
    end
end)
