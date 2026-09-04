-- MGS ULTRA PAINEL - COMPLETO COM GIRAR RAPIDO NO MENU
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RS = game:GetService("RunService")

repeat wait() until player:FindFirstChild("PlayerGui") and player.Character

local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "MGSGui"
gui.ResetOnSpawn = false

local menu = Instance.new("ScrollingFrame", gui)
menu.Size = UDim2.new(0,320,0,600)
menu.Position = UDim2.new(0,15,0.5,-300)
menu.BackgroundColor3 = Color3.fromRGB(15,15,15)
menu.CanvasSize = UDim2.new(0,0,0,1250)
menu.ScrollBarThickness = 6
Instance.new("UICorner", menu)

local function criarBotao(txt, y, cor)
	local b = Instance.new("TextButton", menu)
	b.Size = UDim2.new(0.9,0,0,38)
	b.Position = UDim2.new(0.05,0,0,y)
	b.Text = txt
	b.TextScaled = true
	b.BackgroundColor3 = cor or Color3.fromRGB(35,35,35)
	b.TextColor3 = Color3.new(1,1,1)
	b.Font = Enum.Font.GothamBold
	Instance.new("UICorner", b)
	return b
end

local t = Instance.new("TextLabel", menu)
t.Size = UDim2.new(1,0,0,40)
t.Text = "🤡 MGS PALHAÇO ULTRA"
t.TextScaled = true
t.BackgroundTransparency = 1
t.TextColor3 = Color3.fromRGB(255,0,0)
t.Font = Enum.Font.GothamBlack

-- BOTOES NO MENU
local b1 = criarBotao("VELOCIDADE 150: OFF", 45)
local b2 = criarBotao("NOCLIP: OFF", 85)
local b3 = criarBotao("VOAR 200 WASD: OFF", 125)
local b4 = criarBotao("AUTO VOAR: OFF", 165)
local b5 = criarBotao("AUTO BOIAR: OFF", 205)
local b6 = criarBotao("PULO INFINITO: OFF", 245)
local b7 = criarBotao("AUTO ROUBAR: OFF", 285)
local b8 = criarBotao("INVISIVEL REAL: OFF", 325)
local b9 = criarBotao("ESP PALHAÇOS: OFF", 365)
local b10 = criarBotao("ANTI VOID: OFF", 405)
local b11 = criarBotao("SUPER PULO 200", 445)
local b12 = criarBotao("GIRAR RAPIDO: OFF", 485)
local b13 = criarBotao("TELEPORTE MINHA BASE", 525)
local b14 = criarBotao("DAR PENNYWISE SECRET", 565, Color3.fromRGB(150,0,0))
local b15 = criarBotao("DAR 10M", 605, Color3.fromRGB(0,120,0))
local b16 = criarBotao("FECHAR (M)", 645, Color3.fromRGB(80,80,80))

local noclipOn, flyOn, autoFlyOn, autoBoiarOn, infOn, autoOn, invisOn, espOn, antiVoidOn, girandoOn = false,false,false,false,false,false,false,false,false,false
local invisParts = {}
local velocidadeGiro = 50

-- VELOCIDADE
b1.MouseButton1Click:Connect(function()
	if player.Character.Humanoid.WalkSpeed == 16 then
		player.Character.Humanoid.WalkSpeed = 150
		b1.Text = "VELOCIDADE 150: ON" b1.BackgroundColor3 = Color3.fromRGB(0,150,0)
	else player.Character.Humanoid.WalkSpeed = 16 b1.Text = "VELOCIDADE 150: OFF" b1.BackgroundColor3 = Color3.fromRGB(35,35,35) end
end)

-- NOCLIP
b2.MouseButton1Click:Connect(function() noclipOn = not noclipOn b2.Text = noclipOn and "NOCLIP: ON" or "NOCLIP: OFF" b2.BackgroundColor3 = noclipOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Stepped:Connect(function() if noclipOn or autoFlyOn or autoBoiarOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide = false end end end end)

-- VOAR WASD
b3.MouseButton1Click:Connect(function()
	flyOn = not flyOn b3.Text = flyOn and "VOAR 200 WASD: ON" or "VOAR 200 WASD: OFF" b3.BackgroundColor3 = flyOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if flyOn then spawn(function() while flyOn do RS.Heartbeat:Wait() local root=player.Character.HumanoidRootPart local cam=workspace.CurrentCamera local bv=root:FindFirstChild("MGSFly") or Instance.new("BodyVelocity",root) bv.Name="MGSFly" bv.MaxForce=Vector3.new(9e9,9e9,9e9) local vel=Vector3.new(0,0,0) local speed=200 if UIS:IsKeyDown(Enum.KeyCode.W) then vel=vel+(cam.CFrame.LookVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.S) then vel=vel-(cam.CFrame.LookVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.D) then vel=vel+(cam.CFrame.RightVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.A) then vel=vel-(cam.CFrame.RightVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.Space) then vel=vel+Vector3.new(0,speed,0) end if UIS:IsKeyDown(Enum.KeyCode.LeftShift) then vel=vel-Vector3.new(0,speed,0) end bv.Velocity=vel end if player.Character.HumanoidRootPart:FindFirstChild("MGSFly") then player.Character.HumanoidRootPart.MGSFly:Destroy() end end) end
end)

-- AUTO VOAR
b4.MouseButton1Click:Connect(function()
	autoFlyOn = not autoFlyOn b4.Text = autoFlyOn and "AUTO VOAR: ON" or "AUTO VOAR: OFF" b4.BackgroundColor3 = autoFlyOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if autoFlyOn then spawn(function() while autoFlyOn do wait(1) local minhaBase=nil for _,p in pairs(workspace.Plots:GetChildren()) do if p:GetAttribute("Owner")==player.Name then minhaBase=p end end if not minhaBase then continue end local alvo=nil for _,p in pairs(workspace.Plots:GetChildren()) do if p:GetAttribute("Owner")~=player.Name then alvo=p break end end if alvo and alvo:FindFirstChild("Chao") then player.Character.HumanoidRootPart.CFrame=CFrame.new(alvo.Chao.Position+Vector3.new(0,20,0)) wait(1) player.Character.HumanoidRootPart.CFrame=CFrame.new(alvo.Chao.Position+Vector3.new(0,3,0)) wait(1) for _,obj in pairs(alvo:GetDescendants()) do if obj:IsA("ProximityPrompt") then fireproximityprompt(obj) wait(0.2) end end wait(1) player.Character.HumanoidRootPart.CFrame=CFrame.new(minhaBase.Chao.Position+Vector3.new(0,5,0)) end end end) end
end)

-- AUTO BOIAR
b5.MouseButton1Click:Connect(function()
	autoBoiarOn = not autoBoiarOn b5.Text = autoBoiarOn and "AUTO BOIAR: ON" or "AUTO BOIAR: OFF" b5.BackgroundColor3 = autoBoiarOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if autoBoiarOn then spawn(function() local altura=player.Character.HumanoidRootPart.Position.Y+10 while autoBoiarOn do RS.Heartbeat:Wait() local root=player.Character.HumanoidRootPart local bv=root:FindFirstChild("Boiar") or Instance.new("BodyVelocity",root) bv.Name="Boiar" bv.MaxForce=Vector3.new(9e9,9e9,9e9) bv.Velocity=Vector3.new(0,math.sin(tick()*2)*5,0) root.CFrame=CFrame.new(root.Position.X, altura + math.sin(tick())*2, root.Position.Z) end if player.Character.HumanoidRootPart:FindFirstChild("Boiar") then player.Character.HumanoidRootPart.Boiar:Destroy() end end) end
end)

-- PULO INFINITO
UIS.JumpRequest:Connect(function() if infOn then player.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping) end end)
b6.MouseButton1Click:Connect(function() infOn=not infOn b6.Text=infOn and "PULO INFINITO: ON" or "PULO INFINITO: OFF" b6.BackgroundColor3=infOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)

-- AUTO ROUBAR
b7.MouseButton1Click:Connect(function() autoOn=not autoOn b7.Text=autoOn and "AUTO ROUBAR: ON" or "AUTO ROUBAR: OFF" b7.BackgroundColor3=autoOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if autoOn then spawn(function() while autoOn do wait(0.3) for _,plot in pairs(workspace.Plots:GetChildren()) do if plot:GetAttribute("Owner")~=player.Name then for _,obj in pairs(plot:GetDescendants()) do if obj:IsA("ProximityPrompt") then fireproximityprompt(obj) end end end end end end) end end)

-- INVISIVEL REAL
b8.MouseButton1Click:Connect(function() invisOn=not invisOn b8.Text=invisOn and "INVISIVEL REAL: ON" or "INVISIVEL REAL: OFF" b8.BackgroundColor3=invisOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if invisOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") and v.Name~="HumanoidRootPart" then invisParts[v]=v.Transparency v.Transparency=1 end if v:IsA("Decal") then invisParts[v]=v.Transparency v.Transparency=1 end end else for part, trans in pairs(invisParts) do if part and part.Parent then part.Transparency=trans end end invisParts={} end end)

-- ESP
b9.MouseButton1Click:Connect(function() espOn=not espOn b9.Text=espOn and "ESP PALHAÇOS: ON" or "ESP PALHAÇOS: OFF" b9.BackgroundColor3=espOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if espOn then for _,plot in pairs(workspace.Plots:GetChildren()) do for _,obj in pairs(plot:GetDescendants()) do if obj:IsA("Part") and obj:FindFirstChild("Valor") then local h=Instance.new("Highlight",obj) h.FillColor=Color3.fromRGB(255,0,0) end end end end end)

-- ANTI VOID
b10.MouseButton1Click:Connect(function() antiVoidOn=not antiVoidOn b10.Text=antiVoidOn and "ANTI VOID: ON" or "ANTI VOID: OFF" b10.BackgroundColor3=antiVoidOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Heartbeat:Connect(function() if antiVoidOn and player.Character.HumanoidRootPart.Position.Y < -50 then player.Character.HumanoidRootPart.CFrame=CFrame.new(0,20,0) end end)

b11.MouseButton1Click:Connect(function() player.Character.Humanoid.JumpPower=200 b11.Text="SUPER PULO 200: ON" b11.BackgroundColor3=Color3.fromRGB(0,150,0) end)

-- ★ GIRAR RAPIDO - NO MENU ★
b12.MouseButton1Click:Connect(function()
	girandoOn = not girandoOn
	b12.Text = girandoOn and "GIRAR RAPIDO: ON" or "GIRAR RAPIDO: OFF"
	b12.BackgroundColor3 = girandoOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if girandoOn then
		spawn(function()
			while girandoOn and player.Character and player.Character:FindFirstChild("HumanoidRootPart") do
				RS.Heartbeat:Wait()
				local root = player.Character.HumanoidRootPart
				root.CFrame = root.CFrame * CFrame.Angles(0, math.rad(velocidadeGiro), 0)
			end
		end)
	end
end)

b13.MouseButton1Click:Connect(function() for _,p in pairs(workspace.Plots:GetChildren()) do if p:GetAttribute("Owner")==player.Name then player.Character.HumanoidRootPart.CFrame=CFrame.new(p.Chao.Position+Vector3.new(0,5,0)) end end end)
b14.MouseButton1Click:Connect(function() if game.ReplicatedStorage:FindFirstChild("DarPalhaco") then game.ReplicatedStorage.DarPalhaco:FireServer() end end)
b15.MouseButton1Click:Connect(function() if game.ReplicatedStorage:FindFirstChild("DarDinheiro") then game.ReplicatedStorage.DarDinheiro:FireServer(10000000) end end)
b16.MouseButton1Click:Connect(function() menu.Visible=not menu.Visible end)

UIS.InputBegan:Connect(function(input)
	if input.KeyCode==Enum.KeyCode.M then menu.Visible=not menu.Visible end
	if girandoOn then
		if input.KeyCode==Enum.KeyCode.Equals then velocidadeGiro+=10 b12.Text="GIRAR RAPIDO: ON ("..velocidadeGiro..")" end
		if input.KeyCode==Enum.KeyCode.Minus then velocidadeGiro=math.max(5,velocidadeGiro-10) b12.Text="GIRAR RAPIDO: ON ("..velocidadeGiro..")" end
	end
end)
