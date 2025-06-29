# DGS-- Arquivo: vehicle_speed.lua

-- Interface Roblox 100% compatível com celular (Touch) -- Substitui a UILibrary por uma UI simples com suporte a clique e toque

local Players = game:GetService("Players") local LocalPlayer = Players.LocalPlayer local PlayerGui = LocalPlayer:WaitForChild("PlayerGui") local Workspace = game:GetService("Workspace") local SessionVehicles = Workspace:WaitForChild("SessionVehicles")

-- UI Setup local screenGui = Instance.new("ScreenGui") screenGui.Name = "MobileTuningUI" screenGui.ResetOnSpawn = false screenGui.Parent = PlayerGui

local function createButton(text, pos, callback) local button = Instance.new("TextButton") button.Size = UDim2.new(0, 200, 0, 50) button.Position = pos button.BackgroundColor3 = Color3.fromRGB(0, 0, 0) button.TextColor3 = Color3.fromRGB(255, 255, 255) button.Font = Enum.Font.SourceSansBold button.TextSize = 20 button.Text = text button.Parent = screenGui

button.MouseButton1Click:Connect(callback)
return button

end

-- Ações de Tuning local function applyTuning() local car = SessionVehicles:FindFirstChild(LocalPlayer.Name.."-Car") if car then local tune = require(car:FindFirstChild("A-Chassis Tune")) tune.Horsepower = 1200 tune.E_Horsepower = 1200 tune.FinalDrive = 2.5 tune.Ratios = {3.7, 0, 2.84, 1.55, 1, 0.65} tune.ClutchTol = 10000 tune.Redline = 10000 tune.TurboEnabled = true tune.Turbochargers = 4 tune.Superchargers = 2 tune.Weight = 3 print("Tuning aplicado") else warn("Carro não encontrado") end end

local function applyBrakes() local car = SessionVehicles:FindFirstChild(LocalPlayer.Name.."-Car") if car then local tune = require(car:FindFirstChild("A-Chassis Tune")) tune.BrakeForce = 1e12 tune.PBrakeForce = 1e12 print("Freios aplicados") else warn("Carro não encontrado") end end

-- Botões createButton("Aplicar Tuning", UDim2.new(0, 20, 0, 100), applyTuning) createButton("Freios Fortes", UDim2.new(0, 20, 0, 160), applyBrakes)
