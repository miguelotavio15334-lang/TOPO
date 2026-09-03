-- ESP BRAINROT
b4.MouseButton1Click:Connect(function() 
	for _,plot in pairs(workspace:FindFirstChild("Plots") and workspace.Plots:GetChildren() or {}) do 
		for _,obj in pairs(plot:GetDescendants()) do 
			if obj:IsA("Model") and not obj:FindFirstChild("Highlight") then 
				local h=Instance.new("Highlight",obj) 
				h.FillColor=Color3.fromRGB(0,255,0) 
				h.FillTransparency=0.5
			end 
		end 
	end 
	b4.Text="ESP BRAINROT: ON" 
	b4.BackgroundColor3=Color3.fromRGB(0,150,0) 
end)

-- ESP PLAYER - NOVO
local espPlayerOn = false
b4p.MouseButton1Click:Connect(function()
	espPlayerOn = not espPlayerOn
	b4p.Text = espPlayerOn and "ESP PLAYER: ON" or "ESP PLAYER: OFF"
	b4p.BackgroundColor3 = espPlayerOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	
	if espPlayerOn then
		spawn(function()
			while espPlayerOn do
				for _, p in pairs(game.Players:GetPlayers()) do
					if p ~= player and p.Character and p.Character:FindFirstChild("Head") then
						if not p.Character.Head:FindFirstChild("ESPPlayer") then
							local bill = Instance.new("BillboardGui", p.Character.Head)
							bill.Name = "ESPPlayer"
							bill.Size = UDim2.new(0,100,0,40)
							bill.StudsOffset = Vector3.new(0,3,0)
							bill.AlwaysOnTop = true
							
							local nome = Instance.new("TextLabel", bill)
							nome.Size = UDim2.new(1,0,0.5,0)
							nome.BackgroundTransparency = 1
							nome.Text = p.Name
							nome.TextColor3 = Color3.fromRGB(255,0,0)
							nome.TextScaled = true
							nome.Font = Enum.Font.GothamBold
							
							local dist = Instance.new("TextLabel", bill)
							dist.Size = UDim2.new(1,0,0.5,0)
							dist.Position = UDim2.new(0,0,0.5,0)
							dist.BackgroundTransparency = 1
							dist.TextColor3 = Color3.fromRGB(255,255,255)
							dist.TextScaled = true
							dist.Font = Enum.Font.Gotham
							dist.Name = "Dist"
							
							local hl = Instance.new("Highlight", p.Character)
							hl.Name = "ESPHighlight"
							hl.FillColor = Color3.fromRGB(255,0,0)
							hl.OutlineColor = Color3.fromRGB(255,255,255)
							hl.FillTransparency = 0.5
						end
						-- atualiza distancia
						if p.Character.Head:FindFirstChild("ESPPlayer") then
							local d = math.floor((player.Character.HumanoidRootPart.Position - p.Character.HumanoidRootPart.Position).Magnitude)
							p.Character.Head.ESPPlayer.Dist.Text = d.."m"
						end
					end
				end
				wait(0.2)
			end
		end)
	else
		for _, p in pairs(game.Players:GetPlayers()) do
			if p.Character then
				if p.Character.Head:FindFirstChild("ESPPlayer") then p.Character.Head.ESPPlayer:Destroy() end
				if p.Character:FindFirstChild("ESPHighlight") then p.Character.ESPHighlight:Destroy() end
			end
		end
	end
end)

-- MGS GHOST V10 LIMPO - SÓ O NECESSÁRIO + ANUNCIO GLOBAL
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RS = game:GetService("RunService")

repeat wait() until player:FindFirstChild("PlayerGui")

local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "MGSGui"
gui.ResetOnSpawn = false

local menu = Instance.new("ScrollingFrame", gui)
menu.Size = UDim2.new(0,285,0,420)
menu.Position = UDim2.new(0,15,0.5,-210)
menu.BackgroundColor3 = Color3.fromRGB(10,10,10)
menu.CanvasSize = UDim2.new(0,0,0,500)
menu.ScrollBarThickness = 6
Instance.new("UICorner", menu)

local function criarBotao(txt, y, cor)
	local b = Instance.new("TextButton", menu)
	b.Size = UDim2.new(0.92,0,0,34)
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
t.Text = "MGS V10 LIMPO"
t.TextScaled = true
t.BackgroundTransparency = 1
t.TextColor3 = Color3.fromRGB(0,255,0)
t.Font = Enum.Font.GothamBlack

-- FAIXA DO TOPO IGUAL BRAINROT
local topGui = Instance.new("ScreenGui", player.PlayerGui)
topGui.Name = "TopAnuncio"
topGui.ResetOnSpawn = false

local topFrame = Instance.new("Frame", topGui)
topFrame.Size = UDim2.new(0,600,0,45)
topFrame.Position = UDim2.new(0.5,-300,0,10)
topFrame.BackgroundColor3 = Color3.fromRGB(0,0,0)
topFrame.BackgroundTransparency = 0.2
topFrame.Visible = false
Instance.new("UICorner", topFrame)
local stroke = Instance.new("UIStroke", topFrame)
stroke.Color = Color3.fromRGB(255,255,0)
stroke.Thickness = 2

local topText = Instance.new("TextLabel", topFrame)
topText.Size = UDim2.new(1,0,1,0)
topText.BackgroundTransparency = 1
topText.Text = ""
topText.TextScaled = true
topText.TextColor3 = Color3.fromRGB(255,255,0)
topText.Font = Enum.Font.GothamBlack

local function anunciarTopo(msg)
	topText.Text = "📢 "..msg.." 📢"
	topFrame.Visible = true
	pcall(function() game:GetService("TextChatService").TextChannels.RBXGeneral:SendAsync(msg) end)
	wait(5)
	topFrame.Visible = false
end

local b1 = criarBotao("VELOCIDADE 150: OFF", 30)
local b2 = criarBotao("NOCLIP: OFF", 68)
local b3 = criarBotao("VOAR 200 WASD: OFF", 106)
local b4 = criarBotao("ESP BRAINROT: OFF", 144)
local b5 = criarBotao("ANTI AFK: ON", 182, Color3.fromRGB(0,80,0))

local caixaFala = Instance.new("TextBox", menu)
caixaFala.Size = UDim2.new(0.92,0,0,32)
caixaFala.Position = UDim2.new(0.04,0,0,224)
caixaFala.PlaceholderText = "O que anunciar no topo?"
caixaFala.Text = ""
caixaFala.TextScaled = true
caixaFala.BackgroundColor3 = Color3.fromRGB(50,50,50)
caixaFala.TextColor3 = Color3.new(1,1,1)
caixaFala.Font = Enum.Font.GothamBold
Instance.new("UICorner", caixaFala)

local bAnuncio = criarBotao("🔊 ANUNCIAR NO TOPO", 264, Color3.fromRGB(200,150,0))
local b14 = criarBotao("TELEPORTE MINHA BASE", 302)
local b15 = criarBotao("FECHAR (M)", 340, Color3.fromRGB(150,0,0))

local noclipOn, flyOn = false,false
local flySpeed = 200
local antiAfkOn = true

b1.MouseButton1Click:Connect(function() if player.Character.Humanoid.WalkSpeed==16 then player.Character.Humanoid.WalkSpeed=150 b1.Text="VELOCIDADE 150: ON" b1.BackgroundColor3=Color3.fromRGB(0,150,0) else player.Character.Humanoid.WalkSpeed=16 b1.Text="VELOCIDADE 150: OFF" b1.BackgroundColor3=Color3.fromRGB(35,35,35) end end)
b2.MouseButton1Click:Connect(function() noclipOn=not noclipOn b2.Text=noclipOn and "NOCLIP: ON" or "NOCLIP: OFF" b2.BackgroundColor3=noclipOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Stepped:Connect(function() if noclipOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide=false end end end end)

b3.MouseButton1Click:Connect(function()
	flyOn=not flyOn b3.Text=flyOn and "VOAR "..flySpeed.." WASD: ON" or "VOAR 200 WASD: OFF" b3.BackgroundColor3=flyOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
	if flyOn then spawn(function() while flyOn do RS.Heartbeat:Wait() local root=player.Character.HumanoidRootPart local cam=workspace.CurrentCamera local bv=root:FindFirstChild("MGSFly") or Instance.new("BodyVelocity",root) bv.Name="MGSFly" bv.MaxForce=Vector3.new(9e9,9e9,9e9) local vel=Vector3.new(0,0,0) if UIS:IsKeyDown(Enum.KeyCode.W) then vel=vel+(cam.CFrame.LookVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.S) then vel=vel-(cam.CFrame.LookVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.D) then vel=vel+(cam.CFrame.RightVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.A) then vel=vel-(cam.CFrame.RightVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.Space) then vel=vel+Vector3.new(0,flySpeed,0) end if UIS:IsKeyDown(Enum.KeyCode.LeftShift) then vel=vel-Vector3.new(0,flySpeed,0) end bv.Velocity=vel end if player.Character.HumanoidRootPart:FindFirstChild("MGSFly") then player.Character.HumanoidRootPart.MGSFly:Destroy() end end) end
end)

b4.MouseButton1Click:Connect(function() for _,plot in pairs(workspace:FindFirstChild("Plots") and workspace.Plots:GetChildren() or {}) do for _,obj in pairs(plot:GetDescendants()) do if obj:IsA("Model") and not obj:FindFirstChild("Highlight") then local h=Instance.new("Highlight",obj) h.FillColor=Color3.fromRGB(0,255,0) end end end b4.Text="ESP: ON" b4.BackgroundColor3=Color3.fromRGB(0,150,0) end)

b5.MouseButton1Click:Connect(function() antiAfkOn=not antiAfkOn b5.Text=antiAfkOn and "ANTI AFK: ON" or "ANTI AFK: OFF" b5.BackgroundColor3=antiAfkOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
player.Idled:Connect(function() if antiAfkOn then game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame) wait(1) game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame) end end)

bAnuncio.MouseButton1Click:Connect(function() if caixaFala.Text ~= "" then anunciarTopo(caixaFala.Text) end end)
b14.MouseButton1Click:Connect(function() if workspace:FindFirstChild("Plots") then for _,p in pairs(workspace.Plots:GetChildren()) do if string.find(p.Name,player.Name) then player.Character.HumanoidRootPart.CFrame=CFrame.new(p:GetPivot().Position+Vector3.new(0,10,0)) end end end end)
b15.MouseButton1Click:Connect(function() menu.Visible=not menu.Visible end)
UIS.InputBegan:Connect(function(i) if i.KeyCode==Enum.KeyCode.M then menu.Visible=not menu.Visible end end)
