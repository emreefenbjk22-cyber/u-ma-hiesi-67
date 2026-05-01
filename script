--[[ 
    MADE BY EMRE - FULL MENÜ (HER ŞEY DAHİL)
--]]

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TeleportService = game:GetService("TeleportService")

local player = Players.LocalPlayer
local noclip = false
local flying = false
local infJump = false
local flySpeed = 50
local walkSpeed = 16
local jumpPower = 50
local bv, bg

-- --- ARAYÜZ ---
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "EmreMasterMenu"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame", screenGui)
mainFrame.Size = UDim2.new(0, 220, 0, 400)
mainFrame.Position = UDim2.new(0.05, 0, 0.2, 0)
mainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
mainFrame.Active = true
Instance.new("UICorner", mainFrame)

local title = Instance.new("TextLabel", mainFrame)
title.Text = "MADE BY EMRE"
title.Size = UDim2.new(1, 0, 0, 35)
title.TextColor3 = Color3.fromRGB(0, 255, 150)
title.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
title.Font = Enum.Font.GothamBold
Instance.new("UICorner", title)

local container = Instance.new("ScrollingFrame", mainFrame)
container.Size = UDim2.new(1, 0, 1, -40)
container.Position = UDim2.new(0, 0, 0, 40)
container.BackgroundTransparency = 1
container.CanvasSize = UDim2.new(0, 0, 1.8, 0)
container.ScrollBarThickness = 2
local layout = Instance.new("UIListLayout", container)
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
layout.Padding = UDim.new(0, 8)

-- Sürükleme Sistemi
local dragging, dragStart, startPos
title.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true; dragStart = input.Position; startPos = mainFrame.Position
    end
end)
UserInputService.InputChanged:Connect(function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
UserInputService.InputEnded:Connect(function() dragging = false end)

-- --- YARDIMCI FONKSİYONLAR ---
local function makeToggleBtn(text)
    local btn = Instance.new("TextButton", container)
    btn.Text = text .. ": KAPALI"
    btn.Size = UDim2.new(0.9, 0, 0, 35)
    btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    btn.TextColor3 = Color3.new(1, 1, 1)
    Instance.new("UICorner", btn)
    return btn
end

local function createStepper(name, defaultValue, callback)
    local frame = Instance.new("Frame", container)
    frame.Size = UDim2.new(0.9, 0, 0, 55)
    frame.BackgroundTransparency = 1
    
    local label = Instance.new("TextLabel", frame)
    label.Text = name .. ": " .. defaultValue
    label.Size = UDim2.new(1, 0, 0, 20); label.TextColor3 = Color3.new(1, 1, 1); label.BackgroundTransparency = 1
    
    local minus = Instance.new("TextButton", frame)
    minus.Text = "-"; minus.Size = UDim2.new(0.35, 0, 0, 25); minus.Position = UDim2.new(0.05, 0, 0.45, 0); minus.BackgroundColor3 = Color3.fromRGB(180, 50, 50); minus.TextColor3 = Color3.new(1, 1, 1)
    Instance.new("UICorner", minus)
    
    local plus = Instance.new("TextButton", frame)
    plus.Text = "+"; plus.Size = UDim2.new(0.35, 0, 0, 25); plus.Position = UDim2.new(0.6, 0, 0.45, 0); plus.BackgroundColor3 = Color3.fromRGB(50, 180, 50); plus.TextColor3 = Color3.new(1, 1, 1)
    Instance.new("UICorner", plus)
    
    local val = defaultValue
    minus.MouseButton1Click:Connect(function() val = math.max(0, val - 10); label.Text = name .. ": " .. val; callback(val) end)
    plus.MouseButton1Click:Connect(function() val = val + 10; label.Text = name .. ": " .. val; callback(val) end)
end

-- --- ÖZELLİKLER ---
local noclipBtn = makeToggleBtn("NOCLIP")
local flyBtn = makeToggleBtn("UÇUŞ (E)")
local infJumpBtn = makeToggleBtn("INF JUMP")

createStepper("Uçuş Hızı", flySpeed, function(v) flySpeed = v end)
createStepper("Yürüme Hızı", walkSpeed, function(v) if player.Character and player.Character:FindFirstChild("Humanoid") then player.Character.Humanoid.WalkSpeed = v end end)
createStepper("Zıplama Gücü", jumpPower, function(v) if player.Character and player.Character:FindFirstChild("Humanoid") then player.Character.Humanoid.UseJumpPower = true; player.Character.Humanoid.JumpPower = v end end)

local rjBtn = Instance.new("TextButton", container)
rjBtn.Text = "REJOIN"; rjBtn.Size = UDim2.new(0.9, 0, 0, 35); rjBtn.BackgroundColor3 = Color3.fromRGB(150, 50, 50); rjBtn.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", rjBtn); rjBtn.MouseButton1Click:Connect(function() TeleportService:Teleport(game.PlaceId, player) end)

-- --- MANTIKLAR ---

-- NOCLIP
noclipBtn.MouseButton1Click:Connect(function()
    noclip = not noclip
    noclipBtn.Text = "NOCLIP: " .. (noclip and "AÇIK" or "KAPALI")
    noclipBtn.BackgroundColor3 = noclip and Color3.fromRGB(0, 150, 0) or Color3.fromRGB(50, 50, 50)
end)

RunService.Stepped:Connect(function()
    if noclip and player.Character then
        for _, v in pairs(player.Character:GetDescendants()) do
            if v:IsA("BasePart") then v.CanCollide = false end
        end
    end
end)

-- INF JUMP
infJumpBtn.MouseButton1Click:Connect(function()
    infJump = not infJump
    infJumpBtn.Text = "INF JUMP: " .. (infJump and "AÇIK" or "KAPALI")
    infJumpBtn.BackgroundColor3 = infJump and Color3.fromRGB(0, 150, 0) or Color3.fromRGB(50, 50, 50)
end)
UserInputService.JumpRequest:Connect(function() if infJump and player.Character:FindFirstChildOfClass("Humanoid") then player.Character:FindFirstChildOfClass("Humanoid"):ChangeState(Enum.HumanoidStateType.Jumping) end end)

-- FLY
local function toggleFly()
    local char = player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local hum = char and char:FindFirstChildOfClass("Humanoid")
    if not root or not hum then return end
    flying = not flying
    flyBtn.Text = "UÇUŞ (E): " .. (flying and "AÇIK" or "KAPALI")
    flyBtn.BackgroundColor3 = flying and Color3.fromRGB(0, 150, 0) or Color3.fromRGB(50, 50, 50)
    if flying then
        hum.PlatformStand = true
        bg = Instance.new("BodyGyro", root); bg.maxTorque = Vector3.new(9e9, 9e9, 9e9)
        bv = Instance.new("BodyVelocity", root); bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
        task.spawn(function()
            while flying and root.Parent do
                RunService.RenderStepped:Wait()
                local cam = workspace.CurrentCamera
                local dir = hum.MoveDirection
                if UserInputService:IsKeyDown(Enum.KeyCode.W) then dir = dir + cam.CFrame.LookVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.S) then dir = dir - cam.CFrame.LookVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.A) then dir = dir - cam.CFrame.RightVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.D) then dir = dir + cam.CFrame.RightVector end
                bv.velocity = (dir.Magnitude > 0 and dir.Unit * flySpeed) or Vector3.new(0, 0.1, 0)
                bg.cframe = cam.CFrame
            end
            if bv then bv:Destroy() end; if bg then bg:Destroy() end; hum.PlatformStand = false
        end)
    end
end
flyBtn.MouseButton1Click:Connect(toggleFly)
UserInputService.InputBegan:Connect(function(i, p) if not p and i.KeyCode == Enum.KeyCode.E then toggleFly() end end)

-- PANEL KONTROL
local closeBtn = Instance.new("TextButton", mainFrame)
closeBtn.Text = "X"; closeBtn.Size = UDim2.new(0, 25, 0, 25); closeBtn.Position = UDim2.new(1, -30, 0, 5); closeBtn.BackgroundColor3 = Color3.new(0.8, 0, 0); closeBtn.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", closeBtn); closeBtn.MouseButton1Click:Connect(function() noclip = false; flying = false; screenGui:Destroy() end)

local minBtn = Instance.new("TextButton", mainFrame)
minBtn.Text = "-"; minBtn.Size = UDim2.new(0, 25, 0, 25); minBtn.Position = UDim2.new(1, -60, 0, 5); minBtn.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3); minBtn.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", minBtn)
local minimized = false
minBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    container.Visible = not minimized
    mainFrame.Size = minimized and UDim2.new(0, 220, 0, 35) or UDim2.new(0, 220, 0, 400)
end)
