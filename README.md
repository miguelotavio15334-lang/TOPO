--// AUTO PALHAÇO
--// Coloque como Script em ServerScriptService

local Players = game:GetService("Players")

local BRAINROT_FOLDER = workspace:WaitForChild("Palhacos")
local BASES_FOLDER = workspace:WaitForChild("Bases")

local function getBase(player)
	return BASES_FOLDER:FindFirstChild(player.Name)
end

local function getCharacterRoot(player)
	local character = player.Character
	if not character then return nil end

	return character:FindFirstChild("HumanoidRootPart")
end

local function pegarPalhaco(player, palhaco)
	local root = getCharacterRoot(player)
	if not root or not palhaco then return end

	-- Aproxima o jogador do Palhaço
	root.CFrame = palhaco:GetPivot() + Vector3.new(0, 3, 0)

	task.wait(0.3)

	-- Guarda o Palhaço com o jogador
	palhaco:SetAttribute("Dono", player.UserId)
	palhaco:SetAttribute("Carregado", true)

	-- Teleporta automaticamente para a base
	local base = getBase(player)

	if base then
		local destino = base:FindFirstChild("Deposito")
			or base:FindFirstChild("Spawn")
			or base:FindFirstChild("BaseSpawn")

		if destino and destino:IsA("BasePart") then
			root.CFrame = destino.CFrame + Vector3.new(0, 3, 0)
		end
	end

	-- Salva/deposita
	task.wait(0.5)

	palhaco:SetAttribute("Carregado", false)
	palhaco:SetAttribute("Salvo", true)

	print(player.Name .. " salvou o Palhaço!")
end

local function iniciar(player)
	task.spawn(function()
		while player.Parent do
			task.wait(1)

			-- Não pega outro enquanto estiver carregando
			local encontrou = false

			for _, palhaco in ipairs(BRAINROT_FOLDER:GetChildren()) do
				if not palhaco:GetAttribute("Salvo") then
					encontrou = true

					pegarPalhaco(player, palhaco)

					break
				end
			end

			if not encontrou then
				task.wait(2)
			end
		end
	end)
end

Players.PlayerAdded:Connect(iniciar)

for _, player in ipairs(Players:GetPlayers()) do
	iniciar(player)
end
