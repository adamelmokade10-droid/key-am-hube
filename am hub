-- [[ AM HUB | +1 Double Jump Bike Edition ]]
-- COLOR: RED

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer

-- [ 1. CONFIGURATION ]
local Config = {
    HubName = "AM HUB",
    AccentColor = Color3.fromRGB(255, 0, 0), -- Red
    BgColor = Color3.fromRGB(15, 15, 15),
    MinSize = Vector2.new(300, 380),
    MaxSize = Vector2.new(600, 600)
}

-- Destroy Previous Instance if exists
if CoreGui:FindFirstChild("AM_HUB") then
    CoreGui.AM_HUB:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "AM_HUB"
ScreenGui.Parent = CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- [ 2. DRAGGING FUNCTION ]
local function EnableDraggable(frame)
    local dragging, dragInput, dragStart, startPos

    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
            or input.UserInputType == Enum.UserInputType.Touch then

            if not _G.IsResizing then
                dragging = true
                dragStart = input.Position
                startPos = frame.Position

                input.Changed:Connect(function()
                    if input.UserInputState == Enum.UserInputState.End then
                        dragging = false
                    end
                end)
            end
        end
    end)

    frame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement
            or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(
                startPos.X.Scale,
                startPos.X.Offset + delta.X,
                startPos.Y.Scale,
                startPos.Y.Offset + delta.Y
            )
        end
    end)
end

-- [ 3. FLOATING TOGGLE BUTTON ]
local ToggleBtn = Instance.new("TextButton")
ToggleBtn.Name = "AM_Toggle"
ToggleBtn.Parent = ScreenGui
ToggleBtn.BackgroundColor3 = Config.BgColor
ToggleBtn.Position = UDim2.new(0.05, 0, 0.2, 0)
ToggleBtn.Size = UDim2.new(0, 50, 0, 50)
ToggleBtn.AutoButtonColor = false
ToggleBtn.Text = ""

Instance.new("UICorner", ToggleBtn).CornerRadius = UDim.new(0, 12)

local ToggleStroke = Instance.new("UIStroke", ToggleBtn)
ToggleStroke.Color = Config.AccentColor
ToggleStroke.Thickness = 2

local AM_Label = Instance.new("TextLabel", ToggleBtn)
AM_Label.Size = UDim2.new(1, 0, 1, 0)
AM_Label.BackgroundTransparency = 1
AM_Label.Text = "AM"
AM_Label.Font = Enum.Font.FredokaOne
AM_Label.TextColor3 = Color3.fromRGB(255, 255, 255)
AM_Label.TextSize = 20

local UIGradient = Instance.new("UIGradient", AM_Label)
UIGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(150, 0, 0))
})

-- [ 4. MAIN FRAME & CONTAINER ]
local Main = Instance.new("Frame")
Main.Name = "MainFrame"
Main.Parent = ScreenGui
Main.BackgroundColor3 = Config.BgColor
Main.Position = UDim2.new(0.5, -150, 0.5, -200)
Main.Size = UDim2.new(0, 300, 0, 400)
Main.Visible = false
Main.Active = true
Main.ClipsDescendants = true

Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 12)

local MainStroke = Instance.new("UIStroke", Main)
MainStroke.Color = Config.AccentColor
MainStroke.Thickness = 2

local Header = Instance.new("TextLabel", Main)
Header.Size = UDim2.new(1, 0, 0, 40)
Header.BackgroundTransparency = 1
Header.Font = Enum.Font.GothamBold
Header.Text = "🔴 " .. Config.HubName .. " | Bike"
Header.TextColor3 = Config.AccentColor
Header.TextSize = 16

local Container = Instance.new("ScrollingFrame", Main)
Container.Size = UDim2.new(1, -20, 1, -80)
Container.Position = UDim2.new(0, 10, 0, 45)
Container.BackgroundTransparency = 1
Container.ScrollBarThickness = 4
Container.ScrollBarImageColor3 = Config.AccentColor
Container.CanvasSize = UDim2.new(0, 0, 0, 0)

local UIListLayout = Instance.new("UIListLayout", Container)
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 8)

UIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    Container.CanvasSize = UDim2.new(
        0, 0,
        0,
        UIListLayout.AbsoluteContentSize.Y + 10
    )
end)

-- [ 5. UI ELEMENTS GENERATOR ]
local function CreateToggle(text, callback)
    local Frame = Instance.new("Frame", Container)
    Frame.Size = UDim2.new(1, -5, 0, 40)
    Frame.BackgroundColor3 = Color3.fromRGB(22, 22, 22)

    Instance.new("UICorner", Frame).CornerRadius = UDim.new(0, 8)

    local Label = Instance.new("TextLabel", Frame)
    Label.Size = UDim2.new(0.7, 0, 1, 0)
    Label.Position = UDim2.new(0, 10, 0, 0)
    Label.BackgroundTransparency = 1
    Label.Font = Enum.Font.GothamSemibold
    Label.Text = text
    Label.TextColor3 = Color3.fromRGB(255, 255, 255)
    Label.TextSize = 13
    Label.TextXAlignment = Enum.TextXAlignment.Left

    local Btn = Instance.new("TextButton", Frame)
    Btn.Size = UDim2.new(0, 45, 0, 22)
    Btn.Position = UDim2.new(1, -55, 0.5, -11)
    Btn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    Btn.Text = ""

    Instance.new("UICorner", Btn).CornerRadius = UDim.new(1, 0)

    local Circle = Instance.new("Frame", Btn)
    Circle.Size = UDim2.new(0, 16, 0, 16)
    Circle.Position = UDim2.new(0, 3, 0.5, -8)
    Circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)

    Instance.new("UICorner", Circle).CornerRadius = UDim.new(1, 0)

    local toggled = false

    Btn.MouseButton1Click:Connect(function()
        toggled = not toggled

        if toggled then
            Btn.BackgroundColor3 = Config.AccentColor
            Circle:TweenPosition(
                UDim2.new(1, -19, 0.5, -8),
                "Out",
                "Sine",
                0.15,
                true
            )
        else
            Btn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
            Circle:TweenPosition(
                UDim2.new(0, 3, 0.5, -8),
                "Out",
                "Sine",
                0.15,
                true
            )
        end

        pcall(callback, toggled)
    end)
end

-- [ 6. SCRIPT LOGIC ]

_G.Wins = false
local function ToggleWins(state)
    _G.Wins = state

    if state then
        task.spawn(function()
            while _G.Wins do
                pcall(function()
                    if LocalPlayer.Character
                        and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then

                        local hrp = LocalPlayer.Character.HumanoidRootPart
                        hrp.CFrame = CFrame.new(-71469, 1902, 5)

                        task.wait(1)

                        local currentPos = hrp.CFrame
                        hrp.CFrame = currentPos
                    end
                end)

                task.wait(2)
            end
        end)
    end
end

_G.Train = false
local function ToggleTrain(state)
    _G.Train = state

    if state then
        task.spawn(function()
            while _G.Train do
                pcall(function()
                    if LocalPlayer.Character
                        and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then

                        local hrp = LocalPlayer.Character.HumanoidRootPart
                        local treadmills =
                            workspace:FindFirstChild("LobbyThings")
                            and workspace.LobbyThings:FindFirstChild("treadmills")

                        if treadmills then
                            local bestTreadmill = nil
                            local playerRebirths =
                                LocalPlayer.Progression.Rebirths.Value

                            for _, v in pairs(treadmills:GetDescendants()) do
                                if v.Name == "UIPart"
                                    and v:FindFirstChild("GUI")
                                    and v.GUI:FindFirstChild("WinCost") then

                                    local text = v.GUI.WinCost.Text
                                    local reqRebirths =
                                        tonumber(text:match("Rebirth%s+(%d+)%+"))

                                    if reqRebirths
                                        and playerRebirths >= reqRebirths then
                                        bestTreadmill = v
                                    end
                                end
                            end

                            if bestTreadmill then
                                hrp.CFrame = bestTreadmill.CFrame
                            end
                        end
                    end
                end)

                task.wait(1)
            end
        end)
    end
end

_G.Rebirth = false
local function ToggleRebirth(state)
    _G.Rebirth = state

    if state then
        task.spawn(function()
            while _G.Rebirth do
                pcall(function()
                    local hud =
                        LocalPlayer.PlayerGui:FindFirstChild("UI")
                        and LocalPlayer.PlayerGui.UI:FindFirstChild("HUD")

                    if hud
                        and hud.LeftSide.RebirthHolder.Rebirth.Exclamation.Visible then

                        ReplicatedStorage.GameSystems.Remotes.RequestRebirth:FireServer()
                    end
                end)

                task.wait(1)
            end
        end)
    end
end

_G.Coin = false
local function ToggleCoin(state)
    _G.Coin = state

    if state then
        task.spawn(function()
            while _G.Coin do
                pcall(function()
                    if LocalPlayer.Character
                        and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then

                        local hrp = LocalPlayer.Character.HumanoidRootPart
                        workspace.Gravity = 0

                        local coins = {}
                        local collectibles =
                            workspace:FindFirstChild("Collectibles")

                        if collectibles then
                            for _, item in ipairs(collectibles:GetChildren()) do
                                if item:IsA("BasePart") then
                                    table.insert(coins, item)
                                end
                            end

                            table.sort(coins, function(a, b)
                                return (hrp.Position - a.Position).Magnitude
                                    < (hrp.Position - b.Position).Magnitude
                            end)

                            for _, coin in ipairs(coins) do
                                if not _G.Coin then
                                    break
                                end

                                hrp.CFrame = coin.CFrame
                                task.wait(0.3)
                            end
                        end
                    end
                end)

                task.wait(0.2)
            end

            workspace.Gravity = 196
        end)
    else
        workspace.Gravity = 196
    end
end

-- [ 7. BUILD UI ]
CreateToggle("Last Wins (Auto Win)", ToggleWins)
CreateToggle("Auto Train", ToggleTrain)
CreateToggle("Auto Rebirth", ToggleRebirth)
CreateToggle("Collect Coins", ToggleCoin)

-- [ 8. FOOTER ]
local Footer = Instance.new("TextLabel", Main)
Footer.Size = UDim2.new(1, 0, 0, 25)
Footer.Position = UDim2.new(0, 0, 1, -25)
Footer.BackgroundTransparency = 1
Footer.Font = Enum.Font.Gotham
Footer.Text = "AM HUB"
Footer.TextColor3 = Color3.fromRGB(150, 150, 150)
Footer.TextSize = 11

-- [ 9. RESIZE SYSTEM ]
local ResizeHandle = Instance.new("TextButton", Main)
ResizeHandle.Name = "ResizeHandle"
ResizeHandle.Size = UDim2.new(0, 20, 0, 20)
ResizeHandle.Position = UDim2.new(1, -20, 1, -20)
ResizeHandle.BackgroundTransparency = 1
ResizeHandle.Text = "◢"
ResizeHandle.TextColor3 = Config.AccentColor
ResizeHandle.TextSize = 15

local currentSize = Main.Size

ResizeHandle.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then

        _G.IsResizing = true

        local dragStart = input.Position
        local startSize = Main.Size

        local connection

        connection = UserInputService.InputChanged:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement
                or input.UserInputType == Enum.UserInputType.Touch then

                local delta = input.Position - dragStart

                local newX = math.clamp(
                    startSize.X.Offset + delta.X,
                    Config.MinSize.X,
                    Config.MaxSize.X
                )

                local newY = math.clamp(
                    startSize.Y.Offset + delta.Y,
                    Config.MinSize.Y,
                    Config.MaxSize.Y
                )

                Main.Size = UDim2.new(0, newX, 0, newY)
                currentSize = Main.Size
            end
        end)

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                _G.IsResizing = false
                connection:Disconnect()
            end
        end)
    end
end)

EnableDraggable(Main)
EnableDraggable(ToggleBtn)

-- [ 10. TOGGLE ]
local isOpen = false

ToggleBtn.MouseButton1Click:Connect(function()
    isOpen = not isOpen

    if isOpen then
        Main.Visible = true
        Main:TweenSize(
            currentSize,
            "Out",
            "Back",
            0.3,
            true
        )
    else
        Main:TweenSize(
            UDim2.new(0, 0, 0, 0),
            "In",
            "Back",
            0.3,
            true,
            function()
                if not isOpen then
                    Main.Visible = false
                end
            end
        )
    end
end)

print("AM HUB Loaded Successfully!")
