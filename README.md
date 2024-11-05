-- Script: Teleporte entre Mapas no Blox Fruits
-- Coloque este script no StarterPlayer -> StarterPlayerScripts -> LocalScript

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local teleportService = game:GetService("TeleportService")

-- Definindo as localizações dos mapas. 
-- Substitua os valores de "CFrame" com as localizações reais de cada mapa no seu jogo.

local mapLocations = {
    ["Starter Island"] = CFrame.new(100, 10, 100),  -- Localização do Starter Island
    ["Pirate Island"] = CFrame.new(500, 10, 200),   -- Localização do Pirate Island
    ["Desert Island"] = CFrame.new(2000, 10, 500),  -- Localização do Desert Island
    ["Sky Island"] = CFrame.new(1500, 100, 1500),   -- Localização do Sky Island
    ["Ice Island"] = CFrame.new(3000, 10, 1000),    -- Localização do Ice Island
    ["Marineford"] = CFrame.new(3500, 50, 2000),    -- Localização do Marineford
    ["Cake Island"] = CFrame.new(2500, 50, 3000),   -- Localização do Cake Island
    ["Third Sea"] = CFrame.new(4500, 200, 4000),   -- Localização do Third Sea
}

-- Função para teleportar para um mapa
local function teleportToMap(mapName)
    local targetLocation = mapLocations[mapName]
    if targetLocation then
        humanoidRootPart.CFrame = targetLocation
        print("Teleportado para " .. mapName)
    else
        warn("Mapa não encontrado: " .. mapName)
    end
end

-- Exemplo de Teleporte via Teclado: Usando a tecla "T" para mudar para o próximo mapa na lista
local mapList = {"Starter Island", "Pirate Island", "Desert Island", "Sky Island", "Ice Island", "Marineford", "Cake Island", "Third Sea"}
local currentMapIndex = 1

-- Teleportar para o próximo mapa ao pressionar "T"
local function onKeyPress(input)
    if input.KeyCode == Enum.KeyCode.T then
        currentMapIndex = currentMapIndex + 1
        if currentMapIndex > #mapList then
            currentMapIndex = 1 -- Volta para o primeiro mapa
        end
        local nextMap = mapList[currentMapIndex]
        teleportToMap(nextMap)
    end
end

-- Conectar o evento de pressionamento de tecla
game:GetService("UserInputService").InputBegan:Connect(onKeyPress)

