-- MGS GHOST DUPE V9 - ANUNCIO NO TOPO IGUAL BRAINROT
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RS = game:GetService("RunService")

repeat wait() until player:FindFirstChild("PlayerGui")

-- MENU LATERAL
local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "MGSGui"
gui.ResetOnSpawn = false

local menu = Instance.new("ScrollingFrame", gui)
menu.Size = UDim2.new(0,285,0,580)
menu.Position = UDim2.new(0,15,0.5,-290)
menu.BackgroundColor3 = Color3.fromRGB(10,10,10)
menu.CanvasSize = UDim2.new(0,0,0,750)
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
t.Text = "MGS GHOST DUPE V9"
t.TextScaled = true
t.BackgroundTransparency = 1
t.TextColor3 = Color3.fromRGB(0,255,0)
t.Font = Enum.Font.GothamBlack

-- ANUNCIO NO TOPO (ESTILO BRAINROT)
local topGui = Instance.new("ScreenGui", player.PlayerGui)
topGui.Name = "TopAnuncio"

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

-- FUNÇÃO ANUNCIO
local function anunciarTopo(msg)
	topText.Text = "📢 "..msg.." 📢"
	topFrame.Visible = true
	-- Tenta mandar pro chat também
	pcall(function()
		game:GetService("TextChatService").TextChannels.RBXGeneral:SendAsync(msg)
	end)
	wait(5)
	topFrame.Visible = false
end

local b1 = criarBotao("VELOCIDADE 150: OFF", 30)
local b2 = criarBotao("NOCLIP: OFF", 68)
local b3 = criarBotao("VOAR 200: OFF", 106)
local b4 = criarBotao("FICAR EM BAIXO: OFF", 144)
local b5 = criarBotao("HITBOX 35: OFF", 182)
local b6 = criarBotao("ESP: OFF", 220)
local b7 = criarBotao("INVISIVEL: OFF", 258)
local b8 = criarBotao("[4] AUTO TRANCAR: OFF", 296)
local b9 = criarBotao("[10] ANTI AFK: ON", 334)
local b10 = criarBotao("[9] VOAR BICHO 400: OFF", 372)

-- CAIXINHA DO ANUNCIO TOPO
local caixaFala = Instance.new("TextBox", menu)
caixaFala.Size = UDim2.new(0.92,0,0,32)
caixaFala.Position = UDim2.new(0.04,0,0,414)
caixaFala.PlaceholderText = "O que anunciar no topo?"
caixaFala.Text = ""
caixaFala.TextScaled = true
caixaFala.BackgroundColor3 = Color3.fromRGB(50,50,50)
caixaFala.TextColor3 = Color3.new(1,1,1)
caixaFala.Font = Enum.Font.GothamBold
Instance.new("UICorner", caixaFala)

local bAnuncio = criarBotao("🔊 ANUNCIAR NO TOPO", 452, Color3.fromRGB(200,150,0))
local b14 = criarBotao("TELEPORTE BASE", 492)
local b15 = criarBotao("FECHAR (M)", 530, Color3.fromRGB(150,0,0))

-- LOGICA
local noclipOn, flyOn, baixoOn, voarBichoOn = false,false,false,false
local flySpeed = 200
local antiAfkOn = true

b1.MouseButton1Click:Connect(function() if player.Character.Humanoid.WalkSpeed==16 then player.Character.Humanoid.WalkSpeed=150 b1.Text="VELOCIDADE 150: ON" b1.BackgroundColor3=Color3.fromRGB(0,150,0) else player.Character.Humanoid.WalkSpeed=16 b1.Text="VELOCIDADE 150: OFF" b1.BackgroundColor3=Color3.fromRGB(35,35,35) end end)
b2.MouseButton1Click:Connect(function() noclipOn=not noclipOn b2.Text=noclipOn and "NOCLIP: ON" or "NOCLIP: OFF" b2.BackgroundColor3=noclipOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
RS.Stepped:Connect(function() if noclipOn or baixoOn then for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide=false end end end end)
b3.MouseButton1Click:Connect(function() flyOn=not flyOn b3.Text=flyOn and "VOAR "..flySpeed..": ON" or "VOAR 200: OFF" b3.BackgroundColor3=flyOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if flyOn then spawn(function() while flyOn do RS.Heartbeat:Wait() local root=player.Character.HumanoidRootPart local cam=workspace.CurrentCamera local bv=root:FindFirstChild("MGSFly") or Instance.new("BodyVelocity",root) bv.Name="MGSFly" bv.MaxForce=Vector3.new(9e9,9e9,9e9) local vel=Vector3.new(0,0,0) if UIS:IsKeyDown(Enum.KeyCode.W) then vel=vel+(cam.CFrame.LookVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.S) then vel=vel-(cam.CFrame.LookVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.D) then vel=vel+(cam.CFrame.RightVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.A) then vel=vel-(cam.CFrame.RightVector*flySpeed) end if UIS:IsKeyDown(Enum.KeyCode.Space) then vel=vel+Vector3.new(0,flySpeed,0) end if UIS:IsKeyDown(Enum.KeyCode.LeftShift) then vel=vel-Vector3.new(0,flySpeed,0) end bv.Velocity=vel end if player.Character.HumanoidRootPart:FindFirstChild("MGSFly") then player.Character.HumanoidRootPart.MGSFly:Destroy() end end) end end)
b4.MouseButton1Click:Connect(function() baixoOn=not baixoOn b4.Text=baixoOn and "FICAR EM BAIXO: ON" or "FICAR EM BAIXO: OFF" b4.BackgroundColor3=baixoOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) if baixoOn then player.Character.ChildAdded:Connect(function(c) if c:IsA("Tool") then wait(0.2) player.Character.HumanoidRootPart.CFrame=player.Character.HumanoidRootPart.CFrame-Vector3.new(0,15,0) noclipOn=true end end) end end)
b5.MouseButton1Click:Connect(function() for _,v in pairs(workspace:GetDescendants()) do if v:IsA("ProximityPrompt") then v.MaxActivationDistance=35 v.HoldDuration=0 end end b5.Text="HITBOX 35: ON" b5.BackgroundColor3=Color3.fromRGB(0,150,0) end)
b6.MouseButton1Click:Connect(function() for _,plot in pairs(workspace:FindFirstChild("Plots") and workspace.Plots:GetChildren() or {}) do for _,obj in pairs(plot:GetDescendants()) do if obj:IsA("Model") and not obj:FindFirstChild("Highlight") then local h=Instance.new("Highlight",obj) h.FillColor=Color3.fromRGB(0,255,0) end end end b6.Text="ESP: ON" b6.BackgroundColor3=Color3.fromRGB(0,150,0) end)
b7.MouseButton1Click:Connect(function() for _,v in pairs(player.Character:GetDescendants()) do if v:IsA("BasePart") and v.Name~="HumanoidRootPart" then v.Transparency=0.8 end end b7.Text="INVISIVEL: ON" b7.BackgroundColor3=Color3.fromRGB(0,150,0) end)
b8.MouseButton1Click:Connect(function() b8.Text="AUTO TRANCAR: ON (BETA)" b8.BackgroundColor3=Color3.fromRGB(0,150,0) end)
b9.MouseButton1Click:Connect(function() antiAfkOn=not antiAfkOn b9.Text=antiAfkOn and "[10] ANTI AFK: ON" or "ANTI AFK: OFF" b9.BackgroundColor3=antiAfkOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) end)
player.Idled:Connect(function() if antiAfkOn then game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame) wait(1) game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame) end end)
b10.MouseButton1Click:Connect(function() voarBichoOn=not voarBichoOn b10.Text=voarBichoOn and "[9] VOAR BICHO 400: ON" or "[9] VOAR BICHO 400: OFF" b10.BackgroundColor3=voarBichoOn and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35) spawn(function() while voarBichoOn do wait(0.2) if player.Character:FindFirstChildOfClass("Tool") then flySpeed=400 else flySpeed=200 end end end) end)

-- BOTÃO QUE FAZ APARECER EM CIMA
bAnuncio.MouseButton1Click:Connect(function()
	if caixaFala.Text ~= "" then
		anunciarTopo(caixaFala.Text)
	end
end)

b14.MouseButton1Click:Connect(function() if workspace:FindFirstChild("Plots") then for _,p in pairs(workspace.Plots:GetChildren()) do if string.find(p.Name,player.Name) then player.Character.HumanoidRootPart.CFrame=CFrame.new(p:GetPivot().Position+Vector3.new(0,10,0)) end end end end)
b15.MouseButton1Click:Connect(function() menu.Visible=not menu.Visible end)
UIS.InputBegan:Connect(function(i) if i.KeyCode==Enum.KeyCode.M then menu.Visible=not menu.Visible end end)
