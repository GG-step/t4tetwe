local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local targetMobName = "Bandit"  -- Nome do mob que você quer atacar

while true do
    local closestTarget = nil
    local shortestDistance = math.huge

    -- Procurar o mob mais próximo
    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Model") and obj:FindFirstChild("Humanoid") and obj.Name == targetMobName then
            local distance = (obj.HumanoidRootPart.Position - character.HumanoidRootPart.Position).Magnitude
            if distance < shortestDistance then
                closestTarget = obj
                shortestDistance = distance
            end
        end
    end

    -- Atacar o mob se encontrado
    if closestTarget then
        character:MoveTo(closestTarget.HumanoidRootPart.Position)
        wait(1)  -- Aguardar para garantir que o movimento foi completado
        closestTarget.Humanoid:TakeDamage(10)  -- Aplicar dano
    end
    wait(0.5)  -- Espera para recomeçar a busca
end
