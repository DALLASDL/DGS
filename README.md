# DGS-- Arquivo: vehicle_speed.lua

local screenW, screenH = guiGetScreenSize()
local showingSpeed = true

-- Função que converte m/s para km/h
local function getVehicleSpeed(vehicle)
    if not isElement(vehicle) or not getElementType(vehicle) == "vehicle" then return 0 end
    local vx, vy, vz = getElementVelocity(vehicle)
    local speed = math.sqrt(vx^2 + vy^2 + vz^2) * 180 -- Conversão para km/h aproximada
    return math.floor(speed)
end

-- Renderização do velocímetro simples
addEventHandler("onClientRender", root, function()
    if showingSpeed then
        local vehicle = getPedOccupiedVehicle(localPlayer)
        if vehicle and getVehicleController(vehicle) == localPlayer then
            local speed = getVehicleSpeed(vehicle)
            dxDrawText("Velocidade: " .. speed .. " km/h", screenW - 250, screenH - 100, screenW, screenH, tocolor(255, 255, 255, 200), 1.2, "default-bold", "left", "top")
        end
    end
end)

-- Comando para ativar/desativar HUD de velocidade
addCommandHandler("velocimetro", function()
    showingSpeed = not showingSpeed
    outputChatBox("Velocímetro " .. (showingSpeed and "ativado" or "desativado") .. ".", 255, 255, 0)
end)
