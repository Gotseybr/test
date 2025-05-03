local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", game.CoreGui)
gui.Name = "TeleportGUI"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 250, 0, 600)
frame.Position = UDim2.new(0, 20, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
frame.BorderSizePixel = 0

local layout = Instance.new("UIListLayout", frame)
layout.Padding = UDim.new(0, 5)
layout.SortOrder = Enum.SortOrder.LayoutOrder

-- Arrastar a janela
local dragging, dragInput, dragStart, startPos
frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position
    end
end)
frame.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
frame.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

-- Funções de Interface
local function addCategory(title)
    local label = Instance.new("TextLabel", frame)
    label.Size = UDim2.new(1, -10, 0, 25)
    label.Text = "📂 " .. title
    label.Font = Enum.Font.SourceSansBold
    label.TextSize = 14
    label.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    label.TextColor3 = Color3.new(1, 1, 1)
    label.BorderSizePixel = 0
end

local function addTeleportButton(name, cframe)
    local btn = Instance.new("TextButton", frame)
    btn.Size = UDim2.new(1, -10, 0, 35)
    btn.Text = "📍 " .. name
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 14
    btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.BorderSizePixel = 0

    btn.MouseButton1Click:Connect(function()
        local char = player.Character or player.CharacterAdded:Wait()
        local humanoid = char:WaitForChild("Humanoid")
        local hrp = char:WaitForChild("HumanoidRootPart")

        local seat
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("VehicleSeat") and v.Occupant == humanoid then
                seat = v
                break
            end
        end

        if seat then
            local vehicle = seat:FindFirstAncestorOfClass("Model")
            if vehicle and vehicle.PrimaryPart then
                vehicle:SetPrimaryPartCFrame(cframe)
            end
        else
            hrp.CFrame = cframe
        end
    end)
end

-- Categorias e Botões

-- Outros
addCategory("Outros")
addTeleportButton("Caixa", CFrame.new(-25545.998, 154.992065, -2160.31055))
addTeleportButton("Valley Drag Race", CFrame.new(-4037.16089, 154.239578, -1003.14001))
addTeleportButton("Ferro Velho", CFrame.new(-3317.01904, 155.092575, -522.754028))

-- Postos
addCategory("Postos")
addTeleportButton("Posto Mectropoly", CFrame.new(-3416.36597, 155.478592, 18.065))
addTeleportButton("Posto Mecdustrial", CFrame.new(-25595.5, 154.609573, -1044.80798))

-- Fábricas
addCategory("Fábricas")
addTeleportButton("Fábrica 1", CFrame.new(-25659.7578, 154.813675, -590.995972))
addTeleportButton("Fábrica 2", CFrame.new(-25659.7578, 154.813583, -1393.021))

-- Construções
addCategory("Construções")
addTeleportButton("Construção Mectropoly", CFrame.new(-3835.5061, 154.748581, 1224.54297))
addTeleportButton("Construção Mecdustrial", CFrame.new(-26116.0547, 154.58461, -802.932007))
addTeleportButton("Construção Arcozaco", CFrame.new(-9936.9082, 157.790573, 913.122986))

-- Comércios
addCategory("Comércios")
addTeleportButton("Mercadão", CFrame.new(-3811.00903, 183.00058, 2048.18408))
addTeleportButton("Concessionária", CFrame.new(-3184.74902, 155.128616, 80.0240326))
addTeleportButton("Comet Auto Peças", CFrame.new(-3522.64209, 155.053329, 323.652039))
addTeleportButton("Borracharia", CFrame.new(-3285.76001, 167.737549, 1614.28894))

-- Botão de minimizar
local minimizeButton = Instance.new("TextButton", frame)
minimizeButton.Size = UDim2.new(0, 30, 0, 30)
minimizeButton.Position = UDim2.new(1, -35, 0, 0)
minimizeButton.Text = "🔽"
minimizeButton.Font = Enum.Font.SourceSans
minimizeButton.TextSize = 20
minimizeButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
minimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeButton.BorderSizePixel = 0

local isMinimized = false
minimizeButton.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    frame.Size = isMinimized and UDim2.new(0, 250, 0, 40) or UDim2.new(0, 250, 0, 600)
end)

-- Tecla H para esconder/mostrar
game:GetService("UserInputService").InputBegan:Connect(function(input, gpe)
    if not gpe and input.KeyCode == Enum.KeyCode.H then
        frame.Visible = not frame.Visible
    end
end)
