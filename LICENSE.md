-- Interface básica para teleportes com JJSploit

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", game.CoreGui)

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 250, 0, 400)
frame.Position = UDim2.new(0, 50, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 40)
title.Text = "📍 Teleporte Rápido"
title.TextColor3 = Color3.new(1,1,1)
title.BackgroundColor3 = Color3.fromRGB(35,35,35)
title.Font = Enum.Font.SourceSansBold
title.TextSize = 20

local function addButton(name, position)
    local btn = Instance.new("TextButton", frame)
    btn.Size = UDim2.new(1, -20, 0, 30)
    btn.Position = UDim2.new(0, 10, 0, #frame:GetChildren() * 35)
    btn.Text = name
    btn.Font = Enum.Font.SourceSans
    btn.TextColor3 = Color3.new(1,1,1)
    btn.BackgroundColor3 = Color3.fromRGB(40,40,40)
    btn.TextSize = 16
    btn.BorderSizePixel = 0

    btn.MouseButton1Click:Connect(function()
        local char = player.Character or player.CharacterAdded:Wait()
        char:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(unpack(position))
    end)
end

-- Exemplo de posições
addButton("Caixa", {-25545.998, 154.992065, -2160.31055})
addButton("Valley Drag Race", {-4037.16089, 154.239578, -1003.14001})
addButton("Posto Mectropoly", {-3416.36597, 155.478592, 18.065})
addButton("Mercadão", {-3811.00903, 183.00058, 2048.18408})
addButton("Fábrica 1", {-25659.7578, 154.813675, -590.995972})
addButton("Borracharia", {-3285.76, 167.737549, 1614.28894})
