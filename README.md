-- Script para Menu de Interação no Blox Fruits
-- Coloque este script dentro de StarterPlayer -> StarterPlayerScripts -> LocalScript

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local userInputService = game:GetService("UserInputService")
local tweenService = game:GetService("TweenService")

-- Criando o menu GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player.PlayerGui
screenGui.Name = "InteractionMenu"

local menuFrame = Instance.new("Frame")
menuFrame.Size = UDim2.new(0, 300, 0, 400)
menuFrame.Position = UDim2.new(0, 50, 0, 50)
menuFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
menuFrame.BackgroundTransparency = 0.3
menuFrame.Parent = screenGui

local menuTitle = Instance.new("TextLabel")
menuTitle.Size = UDim2.new(1, 0, 0, 40)
menuTitle.BackgroundTransparency = 1
menuTitle.Text = "Menu de Interação"
menuTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
menuTitle.TextSize = 24
menuTitle.Parent = menuFrame

-- Funções de Ativar/Desativar
local function toggleTeleport()
    print("Teleporte Ativado/Desativado") 
    -- Coloque a lógica para ativar/desativar o teleporte aqui
end

local function toggleHabilidade()
    print("Habilidade Ativada/Desativada")
    -- Coloque a lógica para ativar/desativar as habilidades aqui
end

local function toggleBuff()
    print("Buff Ativado/Desativado")
    -- Coloque a lógica para ativar/desativar o buff aqui
end

-- Botões de Interação
local teleportButton = Instance.new("TextButton")
teleportButton.Size = UDim2.new(1, 0, 0, 50)
teleportButton.Position = UDim2.new(0, 0, 0, 50)
teleportButton.Text = "Ativar/Desativar Teleporte"
teleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
teleportButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
teleportButton.Parent = menuFrame
teleportButton.MouseButton1Click:Connect(toggleTeleport)

local habilidadeButton = Instance.new("TextButton")
habilidadeButton.Size = UDim2.new(1, 0, 0, 50)
habilidadeButton.Position = UDim2.new(0, 0, 0, 100)
habilidadeButton.Text = "Ativar/Desativar Habilidade"
habilidadeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
habilidadeButton.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
habilidadeButton.Parent = menuFrame
habilidadeButton.MouseButton1Click:Connect(toggleHabilidade)

local buffButton = Instance.new("TextButton")
buffButton.Size = UDim2.new(1, 0, 0, 50)
buffButton.Position = UDim2.new(0, 0, 0, 150)
buffButton.Text = "Ativar/Desativar Buff"
buffButton.TextColor3 = Color3.fromRGB(255, 255, 255)
buffButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
buffButton.Parent = menuFrame
buffButton.MouseButton1Click:Connect(toggleBuff)

-- Função para ativar/desativar o Menu
local menuVisible = true

local function toggleMenu()
    if menuVisible then
        -- Esconde o menu
        local hideTween = tweenService:Create(menuFrame, TweenInfo.new(0.5), {Position = UDim2.new(0, -menuFrame.Size.X.Offset, 0, 50)})
        hideTween:Play()
    else
        -- Exibe o menu
        local showTween = tweenService:Create(menuFrame, TweenInfo.new(0.5), {Position = UDim2.new(0, 50, 0, 50)})
        showTween:Play()
    end
    menuVisible = not menuVisible
end

-- Ativar o Menu com a tecla "M"
userInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.M then
        toggleMenu()
    end
end)

