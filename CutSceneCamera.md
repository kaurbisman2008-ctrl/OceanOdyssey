# OceanOdyssey

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local StarterPlayer = game:GetService("StarterPlayer")
local player = Players.LocalPlayer
local camera = workspace.CurrentCamera

local cutsceneUI = script.Parent
local playbutton = cutsceneUI:FindFirstChild("TextButton")
local titlebutton = cutsceneUI:FindFirstChild("TextButton2")
local blackFrame = cutsceneUI:FindFirstChild("blackFrame")

if blackFrame then
    blackFrame.BackgroundColor3 = Color3.new(0,0,0)
    blackFrame.Size = UDim2.new(1,0,1,0)
    blackFrame.Position = UDim2.new(0,0,0,0)
    blackFrame.BackgroundTransparency = 0
    blackFrame.Visible = true
end

if playbutton then playbutton.Visible = false end
if titlebutton then titlebutton.Visible = false end

UserInputService.MouseBehavior = Enum.MouseBehavior.Default
UserInputService.MouseIconEnabled = true
camera.CameraType = Enum.CameraType.Custom
StarterPlayer.CameraMode = Enum.CameraMode.Classic

local tweenInfo = TweenInfo.new(
    2.5,
    Enum.EasingStyle.Quad,
    Enum.EasingDirection.Out
)

task.wait(3)

if blackFrame then
    local tween = TweenService:Create(blackFrame, tweenInfo, {BackgroundTransparency = 1})
    tween:Play()
    tween.Completed:Wait()
    blackFrame.Visible = false
end

if titlebutton then titlebutton.Visible = true end
if playbutton then playbutton.Visible = true end

if playbutton then
    playbutton.MouseButton1Click:Connect(function()
        if titlebutton then titlebutton.Visible = false end
        playbutton.Visible = false

        StarterPlayer.CameraMode = Enum.CameraMode.LockFirstPerson
        camera.CameraType = Enum.CameraType.Custom
        UserInputService.MouseBehavior = Enum.MouseBehavior.LockCenter
        UserInputService.MouseIconEnabled = false
    end)
end
