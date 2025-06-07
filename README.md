--[[
    Script: Brainrot GUI - Delta Executor
    Key: brasil
    Mapa: Steal a Brainrot
--]]

local requiredKey = "brasil"
local player = game.Players.LocalPlayer

-- GUI
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "BrainrotDeltaUI"

-- Tela de carregamento
local loading = Instance.new("TextLabel", gui)
loading.Size = UDim2.new(1, 0, 1, 0)
loading.BackgroundColor3 = Color3.new(0, 0, 0)
loading.Text = "Carregando Steal a Brainrot..."
loading.TextColor3 = Color3.new(1, 1, 1)
loading.TextScaled = true
loading.Font = Enum.Font.SourceSansBold

task.wait(2)
loading:Destroy()

-- Tela de Key
local keyFrame = Instance.new("Frame", gui)
keyFrame.Size = UDim2.new(0, 300, 0, 150)
keyFrame.Position = UDim2.new(0.5, -150, 0.5, -75)
keyFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)

local keyBox = Instance.new("TextBox", keyFrame)
keyBox.PlaceholderText = "Digite a chave"
keyBox.Size = UDim2.new(0.8, 0, 0, 40)
keyBox.Position = UDim2.new(0.1, 0, 0.2, 0)
keyBox.Text = ""
keyBox.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
keyBox.TextColor3 = Color3.new(1, 1, 1)

local confirmBtn = Instance.new("TextButton", keyFrame)
confirmBtn.Text = "Confirmar"
confirmBtn.Size = UDim2.new(0.8, 0, 0, 40)
confirmBtn.Position = UDim2.new(0.1, 0, 0.6, 0)
confirmBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
confirmBtn.TextColor3 = Color3.new(1, 1, 1)

-- Menu principal
local menu = Instance.new("Frame", gui)
menu.Size = UDim2.new(0, 400, 0, 350)
menu.Position = UDim2.new(0.5, -200, 0.5, -175)
menu.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
menu.Visible = false

-- Verificar chave
confirmBtn.MouseButton1Click:Connect(function()
    if keyBox.Text:lower() == requiredKey then
        keyFrame.Visible = false
        menu.Visible = true
    else
        keyBox.Text = "Chave incorreta!"
    end
end)

-- Criar botões
local function criarBotao(nome, ordem, func)
    local botao = Instance.new("TextButton", menu)
    botao.Size = UDim2.new(0.8, 0, 0, 30)
    botao.Position = UDim2.new(0.1, 0, 0, 10 + ordem * 40)
    botao.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    botao.Text = nome
    botao.TextColor3 = Color3.new(1, 1, 1)
    botao.MouseButton1Click:Connect(func)
end

-- Funções
criarBotao("Auto Buy Brainrot", 0, function()
    print("🧠 Comprando Brainrot automaticamente")
end)

criarBotao("Auto Sell Brainrot", 1, function()
    print("💰 Vendendo Brainrot automaticamente")
end)

criarBotao("TP Base", 2, function()
    player.Character:MoveTo(Vector3.new(0, 5, 0)) -- Substitua pelo local real
end)

criarBotao("Auto Lock Base", 3, function()
    print("🔒 Base trancada automaticamente")
end)

criarBotao("Remover Laser", 4, function()
    for _, obj in ipairs(workspace:GetDescendants()) do
        if obj:IsA("Part") and obj.Name:lower():find("laser") then
            obj:Destroy()
        end
    end
end)

criarBotao("Speed Boost", 5, function()
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.WalkSpeed = 100 end
