-- MGS ULTRA PAINEL - TODAS AS FUNÇÕES
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RS = game:GetService("RunService")

repeat wait() until player:FindFirstChild("PlayerGui")

local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "MGSGui"
gui.ResetOnSpawn = false

local menu = Instance.new("ScrollingFrame", gui)
menu.Size = UDim2.new(0,280,0,550)
menu.Position = UDim2.new(0,15,0.5,-275)
menu.BackgroundColor3 = Color3.fromRGB(15,15,15)
menu.CanvasSize = UDim2.new(0,0,0,800)
menu.ScrollBarThickness = 6
Instance.new("UICorner", menu)

local function criarBotao(txt, y)
	local b = Instance.new("TextButton", menu)
	b.Size = UDim2.new(0.9,0,0,36)
	b.Position = UDim2.new(0.05,0,0,y)
	b.Text = txt
	b.TextScaled = true
	b.BackgroundColor3 = Color3.fromRGB(35,35,35)
	b.TextColor3 = Color3.new(1,1,1)
	b.Font = Enum.Font.GothamBold
	Instance.new("UICorner", b)
	return b
end

local t = Instance.new("TextLabel", menu)
t.Size = UDim2.new(1,0,0,30)
t.Text = "MGS ULTRA PRO"
t.TextScaled = true
t.BackgroundTransparency = 1
t.TextColor3 = Color3.fromRGB(0,255,0)
t.Font = Enum.Font.GothamBlack

local b1 = criarBotao("VELOCIDADE 150: OFF", 35)
local b2 = criarBotao("NOCLIP: OFF", 75)
local b3 = criarBotao("ANTI RAGDOLL: OFF", 115)
local b4 = criarBotao("VOAR 200 WASD: OFF", 155)
local b5 = criarBotao("PULO INFINITO: OFF", 195)
local b6 = criarBotao("FICAR EM BAIXO: OFF", 235)
local b7 = criarBotao("AUTO ROUBAR: OFF", 275)
local b8 = criarBotao("HITBOX GRANDE: OFF", 315)
local b9 = criarBotao("ANTI HIT: OFF", 355)
local b10 = criarBotao("ROUBAR PAREDE: OFF", 395)
local b11 = criarBotao("ESP BICHOS: OFF", 435)
local b12 = criarBotao("INVISIVEL: OFF", 475)
local b13 = criarBotao("ANTI VOID: OFF", 515)
local b14 = criarBotao("SUPER PULO 200: OFF", 555)
local b15 = criarBotao("TELEPORTE MINHA BASE", 595)
local b16 = criarBotao("FECHAR (M)", 635)
b16.BackgroundColor3 = Color3.fromRGB(150,0,0)

local noclipOn, flyOn, infOn, baixoOn, autoOn, hitboxOn, antiHitOn, paredeOn, espOn, invisOn, antiVoidOn = false,false,false,false,false,false,false,false,false,false,false

-- FUNÇÕES BÁSICAS (1-6)
b1.MouseButton1Click:Connect(function()
	if player.Character.Humanoid.WalkSpeed == 16 then
		player.Character.Humanoid.WalkSpeed = 150
		b1.Text = "VELOCIDADE 150: ON" b1.BackgroundColor3 = Color3.fromRGB(0,150,0)
	else player.Character.Humanoid.WalkSpeed = 16 b1.Text = "VELOCIDADE 150: OFF" b1.BackgroundColor3 = Color3.fromRGB(35,35,35) end
end)

b2.MouseButton1Click:Connect(function() noclipOn = not noclipOn b2.Text = noclipOn and "NOCLIP: ON" or "NOCLIP: OFF" b2.BackgroundColor3 = noclipOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Stepped:Connect(function() if noclipOn or baixoOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide = false end end end end)

b3.MouseButton1Click:Connect(function() player.Character.Humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown,false) player.Character.Humanoid:SetStateEnabled(Enum.HumanoidStateType.Ragdoll,false) b3.Text="ANTI RAGDOLL: ON" b3.BackgroundColor3=Color3.fromRGB(0,150,0) end)

b4.MouseButton1Click:Connect(function()
	flyOn = not flyOn b4.Text = flyOn and "VOAR 200 WASD: ON" or "VOAR 200 WASD: OFF" b4.BackgroundColor3 = flyOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if flyOn then spawn(function() while flyOn do RS.Heartbeat:Wait() local root=player.Character.HumanoidRootPart local cam=workspace.CurrentCamera local bv=root:FindFirstChild("MGSFly") or Instance.new("BodyVelocity",root) bv.Name="MGSFly" bv.MaxForce=Vector3.new(9e9,9e9,9e9) local vel=Vector3.new(0,0,0) local speed=200 if UIS:IsKeyDown(Enum.KeyCode.W) then vel=vel+(cam.CFrame.LookVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.S) then vel=vel-(cam.CFrame.LookVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.D) then vel=vel+(cam.CFrame.RightVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.A) then vel=vel-(cam.CFrame.RightVector*speed) end if UIS:IsKeyDown(Enum.KeyCode.Space) then vel=vel+Vector3.new(0,speed,0) end if UIS:IsKeyDown(Enum.KeyCode.LeftShift) then vel=vel-Vector3.new(0,speed,0) end bv.Velocity=vel end if player.Character.HumanoidRootPart:FindFirstChild("MGSFly") then player.Character.HumanoidRootPart.MGSFly:Destroy() end end) end
end)

UIS.JumpRequest:Connect(function() if infOn then player.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping) end end)
b5.MouseButton1Click:Connect(function() infOn=not infOn b5.Text=infOn and "PULO INFINITO: ON" or "PULO INFINITO: OFF" b5.BackgroundColor3=infOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)

b6.MouseButton1Click:Connect(function() baixoOn=not baixoOn b6.Text=baixoOn and "FICAR EM BAIXO: ON" or "FICAR EM BAIXO: OFF" b6.BackgroundColor3=baixoOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if baixoOn then player.Character.ChildAdded:Connect(function(child) if baixoOn and child:IsA("Tool") then wait(0.2) player.Character.HumanoidRootPart.CFrame=player.Character.HumanoidRootPart.CFrame-Vector3.new(0,15,0) noclipOn=true end end) end end)

-- NOVAS FUNÇÕES BRABAS
b7.MouseButton1Click:Connect(function() -- AUTO ROUBAR
	autoOn=not autoOn b7.Text=autoOn and "AUTO ROUBAR: ON" or "AUTO ROUBAR: OFF" b7.BackgroundColor3=autoOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if autoOn then spawn(function() while autoOn do wait(0.5) for _,plot in pairs(workspace:FindFirstChild("Plots") and workspace.Plots:GetChildren() or {}) do for _,bicho in pairs(plot:GetDescendants()) do if bicho:IsA("ProximityPrompt") then fireproximityprompt(bicho) end end end end end) end
end)

b8.MouseButton1Click:Connect(function() -- HITBOX GRANDE
	hitboxOn=not hitboxOn b8.Text=hitboxOn and "HITBOX GRANDE: ON" or "HITBOX GRANDE: OFF" b8.BackgroundColor3=hitboxOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if hitboxOn then for _,v in pairs(workspace:GetDescendants()) do if v:IsA("ProximityPrompt") then v.HoldDuration=0 v.MaxActivationDistance=30 end end end
end)

b9.MouseButton1Click:Connect(function() -- ANTI HIT
	antiHitOn=not antiHitOn b9.Text=antiHitOn and "ANTI HIT: ON" or "ANTI HIT: OFF" b9.BackgroundColor3=antiHitOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if antiHitOn then player.Character.Humanoid.MaxHealth=math.huge player.Character.Humanoid.Health=math.huge end
end)

b10.MouseButton1Click:Connect(function() paredeOn=not paredeOn b10.Text=paredeOn and "ROUBAR PAREDE: ON" or "ROUBAR PAREDE: OFF" b10.BackgroundColor3=paredeOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) noclipOn=paredeOn b2.Text=paredeOn and "NOCLIP: ON" or "NOCLIP: OFF" b2.BackgroundColor3=paredeOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)

b11.MouseButton1Click:Connect(function() -- ESP
	espOn=not espOn b11.Text=espOn and "ESP BICHOS: ON" or "ESP BICHOS: OFF" b11.BackgroundColor3=espOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if espOn then for _,plot in pairs(workspace:FindFirstChild("Plots") and workspace.Plots:GetChildren() or {}) do for _,obj in pairs(plot:GetDescendants()) do if obj:IsA("Model") then local h=Instance.new("Highlight",obj) h.FillColor=Color3.fromRGB(0,255,0) end end end end
end)

b12.MouseButton1Click:Connect(function() -- INVISIVEL
	invisOn=not invisOn b12.Text=invisOn and "INVISIVEL: ON" or "INVISIVEL: OFF" b12.BackgroundColor3=invisOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if invisOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") and v.Name~="HumanoidRootPart" then v.Transparency=0.7 end end else for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.Transparency=0 end end end
end)

b13.MouseButton1Click:Connect(function() antiVoidOn=not antiVoidOn b13.Text=antiVoidOn and "ANTI VOID: ON" or "ANTI VOID: OFF" b13.BackgroundColor3=antiVoidOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Heartbeat:Connect(function() if antiVoidOn and player.Character and player.Character.HumanoidRootPart.Position.Y < -50 then player.Character.HumanoidRootPart.CFrame=CFrame.new(0,20,0) end end)

b14.MouseButton1Click:Connect(function() if player.Character then player.Character.Humanoid.JumpPower=200 b14.Text="SUPER PULO 200: ON" b14.BackgroundColor3=Color3.fromRGB(0,150,0) end end)

b15.MouseButton1Click:Connect(function() if workspace:FindFirstChild("Plots") then for _,p in pairs(workspace.Plots:GetChildren()) do if p:GetAttribute("Owner")==player.Name or string.find(p.Name,player.Name) then if p:FindFirstChild("Coleta") then player.Character.HumanoidRootPart.CFrame=CFrame.new(p.Coleta.Position+Vector3.new(0,5,0)) end end end else player.Character.HumanoidRootPart.CFrame=CFrame.new(0,10,0) end end)

b16.MouseButton1Click:Connect(function() menu.Visible=not menu.Visible end)
UIS.InputBegan:Connect(function(input) if input.KeyCode==Enum.KeyCode.M then menu.Visible=not menu.Visible end end)
