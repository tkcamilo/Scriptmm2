-- Sistema de autenticação
local KeySystem = {}

-- CONFIGURAÇÃO COM SEU LINK
KeySystem.KeySite = "https://mineurl.com/2844e0"
KeySystem.ValidKeys = {
    "Ana",
    "ana",
    "ANA",
}

-- Interface gráfica
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "KeyAuthGUI"
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 420, 0, 320) -- Aumentado para caber o botão de copiar
Frame.Position = UDim2.new(0.5, -210, 0.5, -160)
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 12)
UICorner.Parent = Frame

-- Gradiente de fundo
local UIGradient = Instance.new("UIGradient")
UIGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(40, 40, 40)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(25, 25, 25))
})
UIGradient.Rotation = 45
UIGradient.Parent = Frame

-- Título
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 60)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "🔐 ACESSO RESTRITO"
Title.TextColor3 = Color3.fromRGB(255, 105, 180)
Title.Font = Enum.Font.GothamBlack
Title.TextSize = 26
Title.Parent = Frame

-- Linha decorativa
local Line = Instance.new("Frame")
Line.Size = UDim2.new(0.8, 0, 0, 2)
Line.Position = UDim2.new(0.1, 0, 0.15, 0)
Line.BackgroundColor3 = Color3.fromRGB(255, 105, 180)
Line.BorderSizePixel = 0
Line.Parent = Frame

-- Instruções principais
local MainInstruction = Instance.new("TextLabel")
MainInstruction.Size = UDim2.new(0.9, 0, 0, 30)
MainInstruction.Position = UDim2.new(0.05, 0, 0.22, 0)
MainInstruction.BackgroundTransparency = 1
MainInstruction.Text = "Para obter a senha, visite:"
MainInstruction.TextColor3 = Color3.fromRGB(200, 200, 200)
MainInstruction.Font = Enum.Font.GothamMedium
MainInstruction.TextSize = 16
MainInstruction.TextXAlignment = Enum.TextXAlignment.Left
MainInstruction.Parent = Frame

-- MOSTRAR O LINK DIRETAMENTE
local LinkDisplay = Instance.new("TextLabel")
LinkDisplay.Size = UDim2.new(0.9, 0, 0, 40)
LinkDisplay.Position = UDim2.new(0.05, 0, 0.3, 0)
LinkDisplay.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
LinkDisplay.Text = KeySystem.KeySite
LinkDisplay.TextColor3 = Color3.fromRGB(100, 200, 255)
LinkDisplay.Font = Enum.Font.GothamBold
LinkDisplay.TextSize = 16
LinkDisplay.TextXAlignment = Enum.TextXAlignment.Center
LinkDisplay.Parent = Frame

local LinkCorner = Instance.new("UICorner")
LinkCorner.CornerRadius = UDim.new(0, 6)
LinkCorner.Parent = LinkDisplay

-- Botão para copiar link
local CopyButton = Instance.new("TextButton")
CopyButton.Size = UDim2.new(0.4, 0, 0, 35)
CopyButton.Position = UDim2.new(0.3, 0, 0.42, 0)
CopyButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
CopyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CopyButton.Font = Enum.Font.GothamBold
CopyButton.TextSize = 16
CopyButton.Text = "📋 COPIAR LINK"
CopyButton.Parent = Frame

local CopyButtonCorner = Instance.new("UICorner")
CopyButtonCorner.CornerRadius = UDim.new(0, 6)
CopyButtonCorner.Parent = CopyButton

-- Campo de senha
local PasswordLabel = Instance.new("TextLabel")
PasswordLabel.Size = UDim2.new(0.9, 0, 0, 25)
PasswordLabel.Position = UDim2.new(0.05, 0, 0.55, 0)
PasswordLabel.BackgroundTransparency = 1
PasswordLabel.Text = "Digite a senha que você encontrou:"
PasswordLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
PasswordLabel.Font = Enum.Font.Gotham
PasswordLabel.TextSize = 14
PasswordLabel.TextXAlignment = Enum.TextXAlignment.Left
PasswordLabel.Parent = Frame

local KeyBox = Instance.new("TextBox")
KeyBox.Size = UDim2.new(0.9, 0, 0, 45)
KeyBox.Position = UDim2.new(0.05, 0, 0.62, 0)
KeyBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
KeyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyBox.Font = Enum.Font.Gotham
KeyBox.TextSize = 18
KeyBox.PlaceholderText = "Cole a senha aqui..."
KeyBox.ClearTextOnFocus = false
KeyBox.Parent = Frame

local KeyBoxCorner = Instance.new("UICorner")
KeyBoxCorner.CornerRadius = UDim.new(0, 8)
KeyBoxCorner.Parent = KeyBox

-- Botão de verificação
local VerifyButton = Instance.new("TextButton")
VerifyButton.Size = UDim2.new(0.9, 0, 0, 45)
VerifyButton.Position = UDim2.new(0.05, 0, 0.78, 0)
VerifyButton.BackgroundColor3 = Color3.fromRGB(255, 105, 180)
VerifyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
VerifyButton.Font = Enum.Font.GothamBlack
VerifyButton.TextSize = 18
VerifyButton.Text = "🔓 VERIFICAR SENHA"
VerifyButton.Parent = Frame

local VerifyButtonCorner = Instance.new("UICorner")
VerifyButtonCorner.CornerRadius = UDim.new(0, 8)
VerifyButtonCorner.Parent = VerifyButton

-- Status
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Size = UDim2.new(0.9, 0, 0, 25)
StatusLabel.Position = UDim2.new(0.05, 0, 0.7, 0)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = ""
StatusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
StatusLabel.Font = Enum.Font.Gotham
StatusLabel.TextSize = 14
StatusLabel.TextXAlignment = Enum.TextXAlignment.Center
StatusLabel.Parent = Frame

-- Função para verificar senha
local function CheckKey(key)
    key = string.gsub(key, "%s+", "")
    local keyLower = string.lower(key)
    
    for _, validKey in pairs(KeySystem.ValidKeys) do
        if keyLower == string.lower(validKey) then
            return true
        end
    end
    
    return false
end

-- Função para carregar o script principal
local function LoadMainScript()
    StatusLabel.Text = "✅ Senha correta! Carregando..."
    StatusLabel.TextColor3 = Color3.fromRGB(0, 255, 150)
    
    wait(1.5)
    
    ScreenGui:Destroy()
    
    -- Carregar o script do Murder Mystery 2
    loadstring(game:HttpGet("https://raw.githubusercontent.com/spawnerscript/MurderMystery2/refs/heads/main/autofarm.lua"))()
end

-- Botão para copiar link
CopyButton.MouseButton1Click:Connect(function()
    if setclipboard then
        setclipboard(KeySystem.KeySite)
        
        -- Efeito visual
        local originalText = CopyButton.Text
        local originalColor = CopyButton.BackgroundColor3
        
        CopyButton.Text = "✅ LINK COPIADO!"
        CopyButton.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
        
        wait(1.5)
        
        CopyButton.Text = originalText
        CopyButton.BackgroundColor3 = originalColor
        
        StatusLabel.Text = "Link copiado para área de transferência!"
        StatusLabel.TextColor3 = Color3.fromRGB(0, 200, 100)
    else
        StatusLabel.Text = "Erro: função setclipboard não disponível"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
    end
end)

-- Botão de verificação
VerifyButton.MouseButton1Click:Connect(function()
    local key = KeyBox.Text
    
    if key == "" then
        StatusLabel.Text = "⚠️ Digite a senha primeiro"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 200, 0)
        return
    end
    
    StatusLabel.Text = "⏳ Verificando senha..."
    StatusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    
    wait(0.5)
    
    if CheckKey(key) then
        LoadMainScript()
    else
        StatusLabel.Text = "❌ Senha incorreta!"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
        
        -- Efeito de erro
        for i = 1, 2 do
            KeyBox.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
            wait(0.15)
            KeyBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            wait(0.15)
        end
    end
end)

-- Permitir Enter para enviar
KeyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        VerifyButton:MouseButton1Click()
    end
end)

-- Clique no link para copiar também
LinkDisplay.MouseButton1Click:Connect(function()
    CopyButton:MouseButton1Click()
end)

-- Mensagem no console
print("=========================================")
print("🔐 SISTEMA DE ACESSO ATIVADO")
print("🌐 Link para senha: " .. KeySystem.KeySite)
print("📋 Clique no botão para copiar o link")
print("🔑 Senha correta: Ana")
print("=========================================")

-- Focar no campo de senha após 1 segundo
wait(1)
KeyBox:CaptureFocus()
