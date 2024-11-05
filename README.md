-- Script: Localizar Frutas no Blox Fruits
-- Coloque este script no StarterPlayer -> StarterPlayerScripts -> LocalScript

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local workspace = game:GetService("Workspace")

-- Distância máxima para a busca (em studs)
local maxDistance = 500

-- Função para desenhar marcadores para frutas
local function drawFruitMarker(position)
    local marker = Instance.new("Part")
    marker.Shape = Enum.PartType.Ball
    marker.Size = Vector3.new(3, 3, 3)
    marker.Position = position
    marker.Color = Color3.fromRGB(0, 255, 0) -- Cor verde para as frutas
    marker.Anchored = true
    marker.CanCollide = false
    marker.Parent = workspace

    -- Destroi o marcador após 2 segundos
    game.Debris:AddItem(marker, 2)
end

-- Função para encontrar frutas
local function findFruits()
    -- Percorre todas as partes no workspace
    for _, item in ipairs(workspace:GetChildren()) do
        -- Verifica se a parte é uma fruta (parte com nome 'Fruit' ou características de uma fruta)
        if item:IsA("Model") and item:FindFirstChild("Handle") and item:FindFirstChild("FruitType") then
            local fruitPosition = item.Handle.Position
            local distance = (fruitPosition - character.HumanoidRootPart.Position).magnitude
            if distance <= maxDistance then
                -- Chama a função para desenhar o marcador
                drawFruitMarker(fruitPosition)
            end
        end
    end
end

-- Loop para verificar a cada 1 segundo se há frutas próximas
while true do
    wait(1)
    findFruits()
end

