-- Vanxell Hub for Blox Fruits Auto-Farming
-- Created by [Your Name or Team]
-- WARNING: Use this script at your own risk.

local VanxellHub = Instance.new("ScreenGui")
VanxellHub.Name = "VanxellHub"
VanxellHub.Parent = game.CoreGui

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 400, 0, 300)
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
MainFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
MainFrame.Parent = VanxellHub

local Title = Instance.new("TextLabel")
Title.Text = "Vanxell Hub - Blox Fruits Auto Farm"
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.TextScaled = true
Title.Parent = MainFrame

-- Function to create toggle buttons for each feature
local function CreateToggleButton(name, callback)
    local Button = Instance.new("TextButton")
    Button.Text = name
    Button.Size = UDim2.new(0.9, 0, 0, 40)
    Button.Position = UDim2.new(0.05, 0, #MainFrame:GetChildren() * 0.12, 0)
    Button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Parent = MainFrame
    Button.MouseButton1Click:Connect(callback)
end

-- Auto-Farm Feature
local autofarm = false
CreateToggleButton("Toggle Auto-Farm", function()
    autofarm = not autofarm
    if autofarm then
        Button.Text = "Auto-Farm: ON"
        while autofarm do
            -- Code for Auto-Farming (attack enemies in range)
            local player = game.Players.LocalPlayer
            local character = player.Character
            -- Add Auto-Farm code to attack enemies
            wait(0.5) -- Adjust as needed
        end
    else
        Button.Text = "Auto-Farm: OFF"
    end
end)

-- Auto-Quest Feature
local autoquest = false
CreateToggleButton("Toggle Auto-Quest", function()
    autoquest = not autoquest
    if autoquest then
        Button.Text = "Auto-Quest: ON"
        while autoquest do
            -- Code for Auto-Quest (collect quests from NPCs)
            -- Replace with actual quest-collection logic
            wait(1)
        end
    else
        Button.Text = "Auto-Quest: OFF"
    end
end)

-- Auto-Stat Feature
local autostat = false
CreateToggleButton("Toggle Auto-Stat", function()
    autostat = not autostat
    if autostat then
        Button.Text = "Auto-Stat: ON"
        while autostat do
            -- Code for Auto-Stat (allocate stats automatically)
            wait(1)
        end
    else
        Button.Text = "Auto-Stat: OFF"
    end
end)

-- Exit Button
local ExitButton = Instance.new("TextButton")
ExitButton.Text = "Exit"
ExitButton.Size = UDim2.new(0.9, 0, 0, 40)
ExitButton.Position = UDim2.new(0.05, 0, 0.8, 0)
ExitButton.BackgroundColor3 = Color3.fromRGB(255, 60, 60)
ExitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ExitButton.Parent = MainFrame
ExitButton.MouseButton1Click:Connect(function()
    VanxellHub:Destroy()
end)

-- Draggable UI Function
local UIS = game:GetService("UserInputService")
local dragging, dragInput, dragStart, startPos

MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UIS.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
