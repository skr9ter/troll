local mouse = game:GetService("Players").LocalPlayer:GetMouse()
local hold=false

local FOV = Drawing.new("Circle")
FOV.Visible = true
FOV.Color = Color3.fromRGB(255, 0, 0)
FOV.Thickness = 1
FOV.NumSides = 100
FOV.Radius = 100 --
FOV.Filled = false



--settings
local keybind=Enum.KeyCode.E
local enablepconsole=false
local teamcheck=false

--here is a visible check. this only functions in games 3rd person games or anything where your camera is not obscured.
local function inlos(p, ...) -- In line of site? p == player head, ... character
return #workspace.CurrentCamera:GetPartsObscuringTarget({p}, {workspace.CurrentCamera, game.Players.LocalPlayer.Character, ...}) == 0
end


local esp = { }

local function NewQuad(thickness, color)
local quad = Drawing.new("Quad")
quad.Visible = false
quad.PointA = Vector2.new(0,0)
quad.PointB = Vector2.new(0,0)
quad.PointC = Vector2.new(0,0)
quad.PointD = Vector2.new(0,0)
quad.Color = color
quad.Filled = false
quad.Thickness = thickness
quad.Transparency = 0.9
return quad
end


local plr = game.Players.LocalPlayer
local camera = game.Workspace.CurrentCamera
game:GetService("UserInputService").InputBegan:connect(function(input)
if input.KeyCode == keybind then
hold=true
end
end)

game:GetService("UserInputService").InputEnded:connect(function(input)
if input.KeyCode == keybind then
hold=false
for index, descendant in pairs(esp) do
descendant:Remove()
end
esp = { }
end
end)
local function round( n, to ) return math.floor(n/to + 0.5) * to end

local close = nil
local hum = plr.Character.HumanoidRootPart
game:GetService("RunService").RenderStepped:Connect(function(step)
local closest = nil
close = nil
local min = math.huge
FOV.Position = Vector2.new(camera.ViewportSize.X/2, camera.ViewportSize.Y/2)
if hold == true then
for i, v in pairs(game.Players:GetChildren()) do
if plr.Character and v.Character and v.Character ~= plr.Character then --and plr.TeamColor ~= v.TeamColor then
if v.Character:FindFirstChild("Head",0) ~= nil then
local plrpos,OnScreen = camera:WorldToViewportPoint(v.Character.Head.Position)
if OnScreen==true then
local distance = math.sqrt(math.pow(mouse.X - plrpos.X, 2), math.pow(mouse.Y - plrpos.Y, 2))
local fovdistance = math.sqrt(math.pow(FOV.Position.X - plrpos.X, 2) + math.pow(FOV.Position.Y - plrpos.Y, 2))
if fovdistance <= FOV.Radius then
if distance < min then
min = distance
closest = v
close = v
end
end end
end end

end

if closest~=nil and close~=nil and mouse.Target.Parent ~= close.Character then
local vector, onScreen = workspace.CurrentCamera:WorldToScreenPoint(close.Character.Head.Position)
if onScreen == true then
local dist = (Vector2.new(vector.X, vector.Y) - Vector2.new(mouse.X,mouse.Y)).Magnitude
local magnitudeX = round(mouse.X - vector.X, 1)
local magnitudeY = round(mouse.Y - vector.Y, 1)
local mag1 = round(-magnitudeX * 0.25, 2)
local mag2 = round(-magnitudeY * 0.25, 2)

mousemoverel(mag1, mag2)
game:GetService('RunService').RenderStepped:Wait()
end
end
end
end)
