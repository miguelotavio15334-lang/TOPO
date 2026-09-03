-- MGS AUTO PALHAÇO V11 - AUTO ROUBAR / PEGAR / SALVAR / TP
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RS = game:GetService("RunService")

repeat wait() until player:FindFirstChild("PlayerGui")

local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "MGSGui"
gui.ResetOnSpawn = false

local menu = Instance.new("ScrollingFrame", gui)
menu.Size = UDim2.new(0,300,0,500)
menu.Position = UDim2.new(0,15,0.5,-250)
menu.BackgroundColor3 = Color3.fromRGB(10,10,10)
menu.CanvasSize = UDim2.new(0,0,0,650)
menu.ScrollBarThickness = 6
Instance.new("UICorner", menu)

local function criarBotao(txt, y, cor)
	local b = Instance.new("TextButton", menu)
	b.Size = UDim2.new(0.92,0,0,32)
	b.Position = UDim2.new(0.04,0,0,y)
	b.Text = txt
	b.TextScaled = true
	b.BackgroundColor3 = cor or Color3.fromRGB(35,35,35)
	b.TextColor3 = Color3.new(1,1,1)
	b.Font = Enum.Font.GothamBold
	Instance.new("UICorner", b)
	return b
end

local t = Instance.new("TextLabel", menu)
t.Size = UDim2.new(1,0,0,28)
t.Text = "MGS AUTO PALHAÇO V11"
t.TextScaled = true
t.BackgroundTransparency = 1
t.TextColor3 = Color3.fromRGB(255,0,100)
t.Font = Enum.Font.GothamBlack

-- TOPO
local topGui = Instance.new("ScreenGui", player.PlayerGui)
topGui.Name = "TopAnuncio"
topGui.ResetOnSpawn = false
local topFrame = Instance.new("Frame", topGui)
topFrame.Size = UDim2.new(0,600,0,45)
topFrame.Position = UDim2.new(0.5,-300,0,10)
topFrame.BackgroundColor3 = Color3.fromRGB(0,0,0)
topFrame.Visible = false
Instance.new("UICorner", topFrame)
local stroke = Instance.new("UIStroke", topFrame)
stroke.Color = Color3.fromRGB(255,0,100)
stroke.Thickness = 2
local topText = Instance.new("TextLabel", topFrame)
topText.Size = UDim2.new(1,0,1,0)
topText.BackgroundTransparency = 1
topText.TextScaled = true
topText.TextColor3 = Color3.fromRGB(255,0,100)
topText.Font = Enum.Font.GothamBlack
local function anunciarTopo(msg) topText.Text="🤡 "..msg.." 🤡" topFrame.Visible=true wait(4) topFrame.Visible=false end

-- BOTOES AUTO
local b1 = criarBotao("🤡 AUTO ROUBAR PALHAÇO: OFF", 30, Color3.fromRGB(80,0,40))
local b2 = criarBotao("🤡 AUTO PEGAR PALHAÇO: OFF", 66, Color3.fromRGB(80,0,40))
local b3 = criarBotao("💾 AUTO SALVAR PALHAÇO: OFF", 102, Color3.fromRGB(0,60,80))
local b4 = criarBotao("⚡ AUTO TP QUANDO PEGAR: OFF", 138, Color3.fromRGB(0,80,0))
local b5 = criarBotao("VELOCIDADE 150: OFF", 180)
local b6 = criarBotao("NOCLIP: OFF", 216)
local b7 = criarBotao("VOAR 200: OFF", 252)
local b8 = criarBotao("ESP PALHAÇO: OFF", 288)
local b9 = criarBotao("ESP PLAYER: OFF", 324)

local caixaFala = Instance.new("TextBox", menu)
caixaFala.Size = UDim2.new(0.92,0,0,30)
caixaFala.Position = UDim2.new(0.04,0,0,362)
caixaFala.PlaceholderText = "Anunciar no topo..."
caixaFala.TextScaled = true
caixaFala.BackgroundColor3 = Color3.fromRGB(50,50,50)
caixaFala.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", caixaFala)
local bAnuncio = criarBotao("🔊 ANUNCIAR TOPO", 398, Color3.fromRGB(200,0,100))
local b14 = criarBotao("TELEPORTE MINHA BASE", 434)
local b15 = criarBotao("FECHAR (M)", 470, Color3.fromRGB(150,0,0))

-- VARS
local autoRoubar, autoPegar, autoSalvar, autoTpPegar = false,false,false,false
local noclipOn, flyOn = false,false
local flySpeed = 200
local minhaBasePos = nil

-- ACHA MINHA BASE
for _,p in pairs(workspace:FindFirstChild("Plots") and workspace.Plots:GetChildren() or {}) do
	if string.find(p.Name, player.Name) then
		minhaBasePos = p:GetPivot().Position + Vector3.new(0,10,0)
	end
end

-- FUNÇÕES AUTO
local function getPalhacoMaisRaro()
	local melhor = nil
	local melhorNome = ""
	for _,plot in pairs(workspace.Plots:GetChildren()) do
		if not string.find(plot.Name, player.Name) then
			for _,obj in pairs(plot:GetDescendants()) do
				if obj:IsA("Model") and obj.Name:lower():find("palha") or obj.Name:lower():find("clown") or obj.Name:lower():find("brainrot") then
					melhor = obj
					melhorNome = obj.Name
				end
				-- procura ProximityPrompt de roubar
				if obj:IsA("ProximityPrompt") and obj.ObjectText:lower():find("steal") or obj.ObjectText:lower():find("roubar") then
					melhor = obj.Parent
				end
			end
		end
	end
	return melhor
end

-- AUTO ROUBAR PALHAÇO
b1.MouseButton1Click:Connect(function()
	autoRoubar=not autoRoubar
	b1.Text=autoRoubar and "🤡 AUTO ROUBAR: ON" or "🤡 AUTO ROUBAR PALHAÇO: OFF"
	b1.BackgroundColor3=autoRoubar and Color3.fromRGB(0,150,0) or Color3.fromRGB(80,0,40)
	if autoRoubar then
		spawn(function()
			while autoRoubar do
				for _,plot in pairs(workspace.Plots:GetChildren()) do
					if not string.find(plot.Name, player.Name) then
						for _,prompt in pairs(plot:GetDescendants()) do
							if prompt:IsA("ProximityPrompt") then
								prompt.MaxActivationDistance=40
								prompt.HoldDuration=0
								if autoRoubar then
									pcall(function() fireproximityprompt(prompt) end)
								end
							end
						end
					end
				end
				wait(0.3)
			end
		end)
		anunciarTopo("AUTO ROUBAR PALHAÇO LIGADO!")
	end
end)

-- AUTO PEGAR PALHAÇO (NO CHÃO)
b2.MouseButton1Click:Connect(function()
	autoPegar=not autoPegar
	b2.Text=autoPegar and "🤡 AUTO PEGAR: ON" or "🤡 AUTO PEGAR PALHAÇO: OFF"
	b2.BackgroundColor3=autoPegar and Color3.fromRGB(0,150,0) or Color3.fromRGB(80,0,40)
	if autoPegar then
		spawn(function()
			while autoPegar do
				for _,v in pairs(workspace:GetDescendants()) do
					if v:IsA("Tool") or v:IsA("Model") and v.Name:lower():find("palha") then
						if v:FindFirstChild("Handle") or v:IsA("Tool") then
							local handle = v:FindFirstChild("Handle") or v
							if (handle.Position - player.Character.HumanoidRootPart.Position).Magnitude < 30 then
								pcall(function() fireproximityprompt(v:FindFirstChildOfClass("ProximityPrompt"),1) end)
								if v:IsA("Tool") then
									player.Character.Humanoid:EquipTool(v)
								end
							end
						end
					end
				end
				wait(0.2)
			end
		end)
	end
end)

-- AUTO SALVAR (TELEPORTA PRA BASE E SALVA)
b3.MouseButton1Click:Connect(function()
	autoSalvar=not autoSalvar
	b3.Text=autoSalvar and "💾 AUTO SALVAR: ON" or "💾 AUTO SALVAR PALHAÇO: OFF"
	b3.BackgroundColor3=autoSalvar and Color3.fromRGB(0,150,0) or Color3.fromRGB(0,60,80)
	if autoSalvar then
		spawn(function()
			while autoSalvar do
				wait(1)
				if player.Character:FindFirstChildOfClass("Tool") and minhaBasePos then
					-- Se tiver com palhaço na mão, volta pra base
					local tool = player.Character:FindFirstChildOfClass("Tool")
					if tool.Name:lower():find("palha") or tool.Name:lower():find("clown") or tool.Name:lower():find("brain") then
						player.Character.HumanoidRootPart.CFrame = CFrame.new(minhaBasePos)
						anunciarTopo("PALHAÇO SALVO NA BASE!")
					end
				end
			end
		end)
	end
end)

-- AUTO TP NA HORA QUE PEGAR PALHAÇO NA MÃO
b4.MouseButton1Click:Connect(function()
	autoTpPegar=not autoTpPegar
	b4.Text=autoTpPegar and "⚡ AUTO TP: ON" or "⚡ AUTO TP QUANDO PEGAR: OFF"
	b4.BackgroundColor3=autoTpPegar and Color3.fromRGB(0,150,0) or Color3.fromRGB(0,80,0)
	if autoTpPegar then
		player.Character.ChildAdded:Connect(function(child)
			if autoTpPegar and child:IsA("Tool") then
				if child.Name:lower():find("palha") or child.Name:lower():find("clown") or child.Name:lower():find("brain") or true then -- pega qualquer um
					wait(0.2)
					if minhaBasePos then
						player.Character.HumanoidRootPart.CFrame = CFrame.new(minhaBasePos)
						anunciarTopo("PEGUEI "..child.Name.." FUGINDO!")
					end
				end
			end
		end)
	end
end)

-- BASICOS
b5.MouseButton1Click:Connect(function() if player.Character.Humanoid.WalkSpeed==16 then player.Character.Humanoid.WalkSpeed=150 b5.Text="VELOCIDADE 150: ON" b5.BackgroundColor3=Color3.fromRGB(0,150,0) else player.Character.Humanoid.WalkSpeed=16 b5.Text="VELOCIDADE 150: OFF" b5.BackgroundColor3=Color3.fromRGB(35,35,35) end end)
b6.MouseButton1Click:Connect(function() noclipOn=not noclipOn b6.Text=noclipOn and "NOCLIP: ON" or "NOCLIP: OFF" b6.BackgroundColor3=noclipOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Stepped:Connect(function() if noclipOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide=false end end end end)
b7.MouseButton1Click:Connect(function() flyOn=not flyOn b7.Text=flyOn and "VOAR 200: ON" or "VOAR 200: OFF" b7.BackgroundColor3=flyOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if flyOn then spawn(function() while flyOn do RS.Heartbeat:Wait() local root=player.Character.HumanoidRootPart local cam=workspace.CurrentCamera local bv=root:FindFirstChild("MGSFly") or Instance.new("BodyVelocity",root) bv.Name="MGSFly" bv.MaxForce=Vector3.new(9e9,9e9,9e9) local vel=Vector3.new(0,0,0) if UIS:IsKeyDown(Enum.KeyCode.W) then vel=vel+(cam.CFrame.LookVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.S) then vel=vel-(cam.CFrame.LookVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.D) then vel=vel+(cam.CFrame.RightVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.A) then vel=vel-(cam.CFrame.RightVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.Space) then vel=vel+Vector3.new(0,flySpeed,0) end if UIS:IsKeyDown(Enum.KeyCode.LeftShift) then vel=vel-Vector3.new(0,flySpeed,0) end bv.Velocity=vel end if player.Character.HumanoidRootPart:FindFirstChild("MGSFly") then player.Character.HumanoidRootPart.MGSFly:Destroy() end end) end end)
b8.MouseButton1Click:Connect(function() for _,plot in pairs(workspace.Plots:GetChildren()) do for _,obj in pairs(plot:GetDescendants()) do if obj:IsA("Model") and not obj:FindFirstChild("Highlight") then local h=Instance.new("Highlight",obj) h.FillColor=Color3.fromRGB(255,0,100) end end end b8.Text="ESP PALHAÇO: ON" b8.BackgroundColor3=Color3.fromRGB(0,150,0) end)
b9.MouseButton1Click:Connect(function() for _,p in pairs(game.Players:GetPlayers()) do if p~=player and p.Character then local hl=Instance.new("Highlight",p.Character) hl.FillColor=Color3.fromRGB(255,0,0) end end b9.Text="ESP PLAYER: ON" b9.BackgroundColor3=Color3.fromRGB(0,150,0) end)

bAnuncio.MouseButton1Click:Connect(function() if caixaFala.Text~="" then anunciarTopo(caixaFala.Text) end end)
b14.MouseButton1Click:Connect(function() if minhaBasePos then player.Character.HumanoidRootPart.CFrame=CFrame.new(minhaBasePos) end end)
b15.MouseButton1Click:Connect(function() menu.Visible=not menu.Visible end)
UIS.InputBegan:Connect(function(i) if i.KeyCode==Enum.KeyCode.M then menu.Visible=not menu.Visible end end)

anunciarTopo("MGS AUTO PALHAÇO V11 CARREGADO!")
