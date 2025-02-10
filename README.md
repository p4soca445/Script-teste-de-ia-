-- Aguarda o jogo carregar completamente
repeat wait() until game:IsLoaded()

-- Variáveis principais
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Configuração de voo
local flying = false
local speed = 75  -- Velocidade do voo

-- Criando objetos de voo
local bodyVelocity = Instance.new("BodyVelocity")
local bodyGyro = Instance.new("BodyGyro")

-- Criar botão na tela
local ScreenGui = Instance.new("ScreenGui")
local FlyButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
FlyButton.Parent = ScreenGui
FlyButton.Size = UDim2.new(0, 200, 0, 50)
FlyButton.Position = UDim2.new(0.4, 0, 0.85, 0)  -- Ajuste a posição como quiser
FlyButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
FlyButton.TextSize = 20
FlyButton.Text = "Ativar Voo"
FlyButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Função para ativar/desativar voo
local function toggleFly()
    flying = not flying
    
    if flying then
        -- Configurar voo
        bodyVelocity.Parent = humanoidRootPart
        bodyVelocity.Velocity = Vector3.new(0, speed, 0)
        bodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)

        bodyGyro.Parent = humanoidRootPart
        bodyGyro.CFrame = humanoidRootPart.CFrame
        bodyGyro.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)

        FlyButton.Text = "Desativar Voo"
        FlyButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    else
        -- Desativar voo
        bodyVelocity:Destroy()
        bodyGyro:Destroy()

        FlyButton.Text = "Ativar Voo"
        FlyButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
    end
end

-- Quando o botão for pressionado, ativa ou desativa o voo
FlyButton.MouseButton1Click:Connect(toggleFly)

-- Mensagem para confirmar ativação do script
game.StarterGui:SetCore("SendNotification", {
    Title = "Script de Voo Ativado!";
    Text = "Use o botão na tela para voar.";
    Duration = 5;
})
