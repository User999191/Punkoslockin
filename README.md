local enableSpeed = false
local enableSpeedWalk = false
local speed = 16
local speedStates = {16, 24, 32, 40, 64, 90, 115, 145, 167, 200}
local currentSpeedIndex = 1

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.IgnoreGuiInset = true
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 300, 0, 200)
Frame.Position = UDim2.new(0.5, -150, 0, 50)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2
Frame.BorderColor3 = Color3.fromRGB(255, 255, 255)
Frame.Active = true
Frame.Draggable = true
Frame.Parent = ScreenGui

local UsernameLabel = Instance.new("TextLabel")
UsernameLabel.Text = "Username"
UsernameLabel.TextSize = 20
UsernameLabel.Size = UDim2.new(1, 0, 0.1, 0)
UsernameLabel.Position = UDim2.new(0, 0, 0, 0)
UsernameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
UsernameLabel.Parent = Frame

local Highlight = Instance.new("Frame")
Highlight.Size = UDim2.new(1, 0, 0.6, 0)
Highlight.Position = UDim2.new(0, 0, 0.1, 0)
Highlight.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
Highlight.BorderSizePixel = 0
Highlight.Parent = Frame

local HealthLabel = Instance.new("TextLabel")
HealthLabel.Text = "Health: 100%"
HealthLabel.TextSize = 16
HealthLabel.Size = UDim2.new(0.2, 0, 0.6, 0)
HealthLabel.Position = UDim2.new(0, 0, 0.1, 0)
HealthLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
HealthLabel.Parent = Frame

local DistanceLabel = Instance.new("TextLabel")
DistanceLabel.Text = "Distance: 0 studs"
DistanceLabel.TextSize = 16
DistanceLabel.Size = UDim2.new(0.6, 0, 0.1, 0)
DistanceLabel.Position = UDim2.new(0, 0, 0.9, 0)
DistanceLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
DistanceLabel.Parent = Frame

local SpeedButton = Instance.new("TextButton")
SpeedButton.Text = "Speed: " .. speedStates[currentSpeedIndex]
SpeedButton.TextSize = 20
SpeedButton.Size = UDim2.new(0.3, 0, 0.1, 0)
SpeedButton.Position = UDim2.new(0.7, 0, 0, 0)
SpeedButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedButton.Parent = Frame

local SpeedWalkButton = Instance.new("TextButton")
SpeedWalkButton.Text = "Speed Walk: OFF"
SpeedWalkButton.TextSize = 20
SpeedWalkButton.Size = UDim2.new(0.3, 0, 0.1, 0)
SpeedWalkButton.Position = UDim2.new(0.7, 0, 0.1, 0)
SpeedWalkButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedWalkButton.Parent = Frame

local ESPButton = Instance.new("TextButton")
ESPButton.Text = "ESP: OFF"
ESPButton.TextSize = 20
ESPButton.Size = UDim2.new(0.3, 0, 0.1, 0)
ESPButton.Position = UDim2.new(0.7, 0, 0.2, 0)
ESPButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ESPButton.Parent = Frame

local function enableSpeedHack()
    while enableSpeedWalk do
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
        wait(0.1)
    end
end

local function toggleSpeedWalking()
    if enableSpeedWalk then
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 8
    else
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
    end
end

SpeedButton.MouseButton1Click:Connect(function()
    currentSpeedIndex = currentSpeedIndex % #speedStates + 1
    speed = speedStates[currentSpeedIndex]
    SpeedButton.Text = "Speed: " .. speedStates[currentSpeedIndex]
    if enableSpeedWalk then
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
    end
end)

SpeedWalkButton.MouseButton1Click:Connect(function()
    enableSpeedWalk = not enableSpeedWalk
    toggleSpeedWalking()
    if enableSpeedWalk then
        SpeedWalkButton.Text = "Speed Walk: ON"
    else
        SpeedWalkButton.Text = "Speed Walk: OFF"
    end
end)

local ESPEnabled = false
ESPButton.MouseButton1Click:Connect(function()
    ESPEnabled = not ESPEnabled
    if ESPEnabled then
        ESPButton.Text = "ESP: ON"
        -- Add ESP logic here
    else
        ESPButton.Text = "ESP: OFF"
        -- Disable ESP logic
    end
end)
