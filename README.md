if game:GetService("CoreGui"):FindFirstChild("Owernetwork") then
    game:GetService("CoreGui").Owernetwork:Destroy()
end
if game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui"):FindFirstChild("Owernetwork") then
    game:GetService("Players").LocalPlayer.PlayerGui.Owernetwork:Destroy()
end

_G.Running = false
_G.PauseRequested = false
_G.CurrentIndex = 1
_G.PlateRunning = false
_G.PlatePauseRequested = false
_G.CurrentPlateIndex = 1
_G.Bringing = false
_G.SelectedItemName = "Tất Cả Vật Phẩm"
_G.SearchText = ""
_G.HoldingGrab = false
_G.HeldObjects = {}
_G.BringConnection = nil
_G.HoldConnection = nil
_G.TargetCFrame = CFrame.new(-99.4940567, 9.73970222, 63.4564552, 0.866007268, -0, -0.500031412, 0, 1, -0, 0.500031412, 0, 0.866007268)

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local MinBtn = Instance.new("TextButton")
local CloseBtn = Instance.new("TextButton")
local ContentFrame = Instance.new("Frame")
local StartBtn = Instance.new("TextButton")
local BringBtn = Instance.new("TextButton")
local SearchBar = Instance.new("TextBox")
local SelectBtn = Instance.new("TextButton")
local RefreshBtn = Instance.new("TextButton")
local PlateBtn = Instance.new("TextButton")
local HoldBtn = Instance.new("TextButton")
local FuelBtn = Instance.new("TextButton")
local Status = Instance.new("TextLabel")

local ConfirmFrame = Instance.new("Frame")
local ConfirmTitle = Instance.new("TextLabel")
local YesBtn = Instance.new("TextButton")
local NoBtn = Instance.new("TextButton")

ScreenGui.Name = "Owernetwork"
ScreenGui.Parent = game:GetService("CoreGui") or game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.5, -110, 0.5, -180)
MainFrame.Size = UDim2.new(0, 220, 0, 360)
MainFrame.Active = true
MainFrame.Draggable = true

Title.Name = "Title"
Title.Parent = MainFrame
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 10, 0, 0)
Title.Size = UDim2.new(0, 140, 0, 30)
Title.Font = Enum.Font.SourceSansBold
Title.Text = "Cook pizzas Panel"
Title.TextSize = 14
Title.TextXAlignment = Enum.TextXAlignment.Left

local TitleGradient = Instance.new("UIGradient")
TitleGradient.Parent = Title
TitleGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)),
    ColorSequenceKeypoint.new(0.166, Color3.fromRGB(255, 165, 0)),
    ColorSequenceKeypoint.new(0.333, Color3.fromRGB(255, 255, 0)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(0, 128, 0)),
    ColorSequenceKeypoint.new(0.666, Color3.fromRGB(0, 0, 255)),
    ColorSequenceKeypoint.new(0.833, Color3.fromRGB(75, 0, 130)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(238, 130, 238))
})

task.spawn(function()
    local RunService = game:GetService("RunService")
    while true do
        for degree = 0, 360, 2 do
            if not Title or not Title.Parent then break end
            TitleGradient.Rotation = degree
            RunService.Heartbeat:Wait()
        end
    end
end)

MinBtn.Name = "MinBtn"
MinBtn.Parent = MainFrame
MinBtn.BackgroundTransparency = 1
MinBtn.Position = UDim2.new(0, 160, 0, 0)
MinBtn.Size = UDim2.new(0, 25, 0, 30)
MinBtn.Font = Enum.Font.SourceSansBold
MinBtn.Text = "-"
MinBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinBtn.TextSize = 20

CloseBtn.Name = "CloseBtn"
CloseBtn.Parent = MainFrame
CloseBtn.BackgroundTransparency = 1
CloseBtn.Position = UDim2.new(0, 185, 0, 0)
CloseBtn.Size = UDim2.new(0, 25, 0, 30)
CloseBtn.Font = Enum.Font.SourceSansBold
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(220, 50, 50)
CloseBtn.TextSize = 16

ContentFrame.Name = "ContentFrame"
ContentFrame.Parent = MainFrame
ContentFrame.BackgroundTransparency = 1
ContentFrame.Position = UDim2.new(0, 0, 0, 30)
ContentFrame.Size = UDim2.new(1, 0, 1, -30)

StartBtn.Name = "StartBtn"
StartBtn.Parent = ContentFrame
StartBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 100)
StartBtn.BorderSizePixel = 0
StartBtn.Position = UDim2.new(0.05, 0, 0.02, 0)
StartBtn.Size = UDim2.new(0.9, 0, 0, 28)
StartBtn.Font = Enum.Font.SourceSansBold
StartBtn.Text = "Ép Sở Hữu: BẮT ĐẦU"
StartBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
StartBtn.TextSize = 13

BringBtn.Name = "BringBtn"
BringBtn.Parent = ContentFrame
BringBtn.BackgroundColor3 = Color3.fromRGB(0, 120, 200)
BringBtn.BorderSizePixel = 0
BringBtn.Position = UDim2.new(0.05, 0, 0.12, 0)
BringBtn.Size = UDim2.new(0.9, 0, 0, 28)
BringBtn.Font = Enum.Font.SourceSansBold
BringBtn.Text = "Bring Item: TẮT"
BringBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
BringBtn.TextSize = 13

SearchBar.Name = "SearchBar"
SearchBar.Parent = ContentFrame
SearchBar.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
SearchBar.BorderSizePixel = 0
SearchBar.Position = UDim2.new(0.05, 0, 0.22, 0)
SearchBar.Size = UDim2.new(0.9, 0, 0, 25)
SearchBar.Font = Enum.Font.SourceSans
SearchBar.PlaceholderText = "🔍 Tìm kiếm vật phẩm để bring..."
SearchBar.Text = ""
SearchBar.TextColor3 = Color3.fromRGB(255, 255, 255)
SearchBar.TextSize = 12

SelectBtn.Name = "SelectBtn"
SelectBtn.Parent = ContentFrame
SelectBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
SelectBtn.BorderSizePixel = 0
SelectBtn.Position = UDim2.new(0.05, 0, 0.31, 0)
SelectBtn.Size = UDim2.new(0.55, 0, 0, 25)
SelectBtn.Font = Enum.Font.SourceSansItalic
SelectBtn.Text = "Chọn: Tất Cả ▼"
SelectBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
SelectBtn.TextSize = 12

RefreshBtn.Name = "RefreshBtn"
RefreshBtn.Parent = ContentFrame
RefreshBtn.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
RefreshBtn.BorderSizePixel = 0
RefreshBtn.Position = UDim2.new(0.65, 0, 0.31, 0)
RefreshBtn.Size = UDim2.new(0.3, 0, 0, 25)
RefreshBtn.Font = Enum.Font.SourceSans
RefreshBtn.Text = "Làm Mới"
RefreshBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
RefreshBtn.TextSize = 12

PlateBtn.Name = "PlateBtn"
PlateBtn.Parent = ContentFrame
PlateBtn.BackgroundColor3 = Color3.fromRGB(130, 50, 180)
PlateBtn.BorderSizePixel = 0
PlateBtn.Position = UDim2.new(0.05, 0, 0.40, 0)
PlateBtn.Size = UDim2.new(0.9, 0, 0, 28)
PlateBtn.Font = Enum.Font.SourceSansBold
PlateBtn.Text = "Bring bằng Plate: BẮT ĐẦU"
PlateBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
PlateBtn.TextSize = 13

HoldBtn.Name = "HoldBtn"
HoldBtn.Parent = ContentFrame
HoldBtn.BackgroundColor3 = Color3.fromRGB(180, 130, 0)
HoldBtn.BorderSizePixel = 0
HoldBtn.Position = UDim2.new(0.05, 0, 0.50, 0)
HoldBtn.Size = UDim2.new(0.9, 0, 0, 28)
HoldBtn.Font = Enum.Font.SourceSansBold
HoldBtn.Text = "Hold Grab: TẮT"
HoldBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
HoldBtn.TextSize = 13

FuelBtn.Name = "FuelBtn"
FuelBtn.Parent = ContentFrame
FuelBtn.BackgroundColor3 = Color3.fromRGB(200, 100, 0)
FuelBtn.BorderSizePixel = 0
FuelBtn.Position = UDim2.new(0.05, 0, 0.60, 0)
FuelBtn.Size = UDim2.new(0.9, 0, 0, 28)
FuelBtn.Font = Enum.Font.SourceSansBold
FuelBtn.Text = "Easy Fuel"
FuelBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
FuelBtn.TextSize = 13

Status.Name = "Status"
Status.Parent = ContentFrame
Status.BackgroundTransparency = 1
Status.Position = UDim2.new(0, 0, 0.88, 0)
Status.Size = UDim2.new(1, 0, 0, 25)
Status.Font = Enum.Font.SourceSansItalic
Status.Text = "Sẵn sàng..."
Status.TextColor3 = Color3.fromRGB(200, 200, 200)
Status.TextSize = 13

local DropdownScroller = Instance.new("ScrollingFrame")
DropdownScroller.Name = "DropdownScroller"
DropdownScroller.Parent = ContentFrame
DropdownScroller.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
DropdownScroller.BorderSizePixel = 1
DropdownScroller.Position = UDim2.new(0.05, 0, 0.39, 0)
DropdownScroller.Size = UDim2.new(0.9, 0, 0, 120)
DropdownScroller.Visible = false
DropdownScroller.ZIndex = 5
DropdownScroller.CanvasSize = UDim2.new(0, 0, 0, 0)

local UIListLayout = Instance.new("UIListLayout")
UIListLayout.Parent = DropdownScroller
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder

ConfirmFrame.Name = "ConfirmFrame"
ConfirmFrame.Parent = ScreenGui
ConfirmFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
ConfirmFrame.BorderSizePixel = 0
ConfirmFrame.Position = UDim2.new(0.5, -90, 0.5, -45)
ConfirmFrame.Size = UDim2.new(0, 180, 0, 90)
ConfirmFrame.Visible = false
ConfirmFrame.Active = true

ConfirmTitle.Name = "ConfirmTitle"
ConfirmTitle.Parent = ConfirmFrame
ConfirmTitle.BackgroundTransparency = 1
ConfirmTitle.Size = UDim2.new(1, 0, 0, 40)
ConfirmTitle.Font = Enum.Font.SourceSansBold
ConfirmTitle.Text = "Chắc chắn xóa GUI?"
ConfirmTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
ConfirmTitle.TextSize = 14

YesBtn.Name = "YesBtn"
YesBtn.Parent = ConfirmFrame
YesBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
YesBtn.BorderSizePixel = 0
YesBtn.Position = UDim2.new(0.1, 0, 0.55, 0)
YesBtn.Size = UDim2.new(0.35, 0, 0, 25)
YesBtn.Font = Enum.Font.SourceSansBold
YesBtn.Text = "Xóa"
YesBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
YesBtn.TextSize = 13

NoBtn.Name = "NoBtn"
NoBtn.Parent = ConfirmFrame
NoBtn.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
NoBtn.BorderSizePixel = 0
NoBtn.Position = UDim2.new(0.55, 0, 0.55, 0)
NoBtn.Size = UDim2.new(0.35, 0, 0, 25)
NoBtn.Font = Enum.Font.SourceSansBold
NoBtn.Text = "Hủy"
NoBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
NoBtn.TextSize = 13

local OwnershipEvent = game:GetService("ReplicatedStorage").Systems.GrabSystem.Network.RequestNetworkOwnership
local isMinimized = false

SearchBar:GetPropertyChangedSignal("Text"):Connect(function()
    _G.SearchText = string.lower(SearchBar.Text)
end)

MinBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    if isMinimized then
        ContentFrame.Visible = false
        MainFrame.Size = UDim2.new(0, 220, 0, 30)
        MinBtn.Text = "+"
    else
        ContentFrame.Visible = true
        MainFrame.Size = UDim2.new(0, 220, 0, 360)
        MinBtn.Text = "-"
    end
end)

CloseBtn.MouseButton1Click:Connect(function()
    ConfirmFrame.Visible = true
end)

YesBtn.MouseButton1Click:Connect(function()
    _G.Running = false
    _G.PlateRunning = false
    _G.Bringing = false
    _G.HoldingGrab = false
    if _G.BringConnection then _G.BringConnection:Disconnect() _G.BringConnection = nil end
    if _G.HoldConnection then _G.HoldConnection:Disconnect() _G.HoldConnection = nil end
    ScreenGui:Destroy()
end)

NoBtn.MouseButton1Click:Connect(function()
    ConfirmFrame.Visible = false
end)

StartBtn.MouseButton1Click:Connect(function()
    if _G.Running then
        _G.PauseRequested = true
        _G.Running = false
        StartBtn.Text = "Ép Sở Hữu: TIẾP TỤC"
        StartBtn.BackgroundColor3 = Color3.fromRGB(200, 150, 0)
        Status.Text = "Đã tạm dừng tại: " .. tostring(_G.CurrentIndex)
        return
    end
    _G.Running = true
    _G.PauseRequested = false
    StartBtn.Text = "Ép Sở Hữu: TẠM DỪNG"
    StartBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
    task.spawn(function()
        local objects = workspace.Objects:GetChildren()
        if _G.CurrentIndex > 500 or _G.CurrentIndex > #objects then _G.CurrentIndex = 1 end
        for i = _G.CurrentIndex, math.min(#objects, 500) do
            if _G.PauseRequested or not _G.Running then break end
            _G.CurrentIndex = i
            local targetObject = objects[i]
            if targetObject then
                pcall(function() OwnershipEvent:InvokeServer(targetObject) end)
            end
            if i % 8 == 0 then
                Status.Text = "Ép sở hữu: " .. tostring(i) .. "/500"
                task.wait(0.03)
            end
        end
        if not _G.PauseRequested and _G.Running then
            Status.Text = "Đã ép xong 500 vật phẩm!"
            StartBtn.Text = "Ép Sở Hữu: BẮT ĐẦU"
            StartBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 100)
            _G.Running = false
            _G.CurrentIndex = 1
        end
    end)
end)
local ScreenGui = game:GetService("CoreGui"):WaitForChild("Owernetwork")
local MainFrame = ScreenGui:WaitForChild("MainFrame")
local ContentFrame = MainFrame:WaitForChild("ContentFrame")
local BringBtn = ContentFrame:WaitForChild("BringBtn")
local SelectBtn = ContentFrame:WaitForChild("SelectBtn")
local RefreshBtn = ContentFrame:WaitForChild("RefreshBtn")
local PlateBtn = ContentFrame:WaitForChild("PlateBtn")
local HoldBtn = ContentFrame:WaitForChild("HoldBtn")
local FuelBtn = ContentFrame:WaitForChild("FuelBtn")
local Status = ContentFrame:WaitForChild("Status")
local DropdownScroller = ContentFrame:WaitForChild("DropdownScroller")

local GrabEvent = game:GetService("ReplicatedStorage").Systems.GrabSystem.Network.RequestNetworkOwnership
local DropEvent = game:GetService("ReplicatedStorage").Systems.GrabSystem.Network.DropNetworkOwnership
local InteractionEvent = game:GetService("ReplicatedStorage").Systems.BehaviorSystem.Network.Interaction
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer

local function getPrimaryOrFirstPart(model)
    if not model:IsA("Model") then return model:IsA("BasePart") and model or nil end
    if model.PrimaryPart then return model.PrimaryPart end
    for _, part in ipairs(model:GetDescendants()) do
        if part:IsA("BasePart") then return part end
    end
    return nil
end

local function updateDropdown()
    for _, child in ipairs(DropdownScroller:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end
    local names = {"Tất Cả Vật Phẩm"}
    local added = {["Tất Cả Vật Phẩm"] = true}
    local objects = workspace.Objects:GetChildren()
    for i = 1, math.min(#objects, 500) do
        local item = objects[i]
        if item.Name and not added[item.Name] then
            table.insert(names, item.Name)
            added[item.Name] = true
        end
    end
    DropdownScroller.CanvasSize = UDim2.new(0, 0, 0, #names * 20)
    for _, name in ipairs(names) do
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(1, 0, 0, 20)
        btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        btn.Font = Enum.Font.SourceSans
        btn.TextSize = 12
        btn.Text = name
        btn.ZIndex = 6
        btn.Parent = DropdownScroller
        btn.MouseButton1Click:Connect(function()
            _G.SelectedItemName = name
            SelectBtn.Text = "Chọn: " .. (name == "Tất Cả Vật Phẩm" and "Tất Cả" or name) .. " ▼"
            DropdownScroller.Visible = false
        end)
    end
end

SelectBtn.MouseButton1Click:Connect(function()
    DropdownScroller.Visible = not DropdownScroller.Visible
    if DropdownScroller.Visible then updateDropdown() end
end)

RefreshBtn.MouseButton1Click:Connect(function()
    updateDropdown()
    Status.Text = "Đã làm mới mục quét!"
end)

BringBtn.MouseButton1Click:Connect(function()
    _G.Bringing = not _G.Bringing
    if _G.Bringing then
        BringBtn.Text = "Bring Item: BẬT"
        BringBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
        Status.Text = "Bring bất chấp đang chạy..."
        _G.BringConnection = RunService.Heartbeat:Connect(function()
            local character = LocalPlayer.Character
            local root = character and character:FindFirstChild("HumanoidRootPart")
            if not root then return end
            local targetPos = (root.CFrame * CFrame.new(0, 0, -6)).Position
            local objects = workspace.Objects:GetChildren()
            for i = 1, math.min(#objects, 500) do
                local targetObject = objects[i]
                if targetObject then
                    local nameLower = string.lower(targetObject.Name)
                    local matchesSearch = (_G.SearchText == "") or (string.find(nameLower, _G.SearchText))
                    local matchesDropdown = (_G.SelectedItemName == "Tất Cả Vật Phẩm") or (targetObject.Name == _G.SelectedItemName)
                    
                    if matchesSearch and matchesDropdown then
                        local mainPart = getPrimaryOrFirstPart(targetObject)
                        if mainPart and not mainPart.Anchored then
                            pcall(function()
                                mainPart.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                                mainPart.AssemblyAngularVelocity = Vector3.new(0, 0, 0)
                                if targetObject:IsA("Model") then
                                    targetObject:PivotTo(CFrame.new(targetPos) * mainPart.CFrame.Rotation)
                                else
                                    mainPart.CFrame = CFrame.new(targetPos) * mainPart.CFrame.Rotation
                                end
                            end)
                        end
                    end
                end
            end
        end)
    else
        BringBtn.Text = "Bring Item: TẮT"
        BringBtn.BackgroundColor3 = Color3.fromRGB(0, 120, 200)
        Status.Text = "Đã hủy Bring."
        if _G.BringConnection then _G.BringConnection:Disconnect() _G.BringConnection = nil end
    end
end)

PlateBtn.MouseButton1Click:Connect(function()
    if _G.PlateRunning then
        _G.PlatePauseRequested = true
        _G.PlateRunning = false
        PlateBtn.Text = "Bring bằng Plate: TIẾP TỤC"
        PlateBtn.BackgroundColor3 = Color3.fromRGB(200, 150, 0)
        Status.Text = "Plate tạm dừng tại: " .. tostring(_G.CurrentPlateIndex)
        return
    end
    local char = LocalPlayer.Character
    local plate = char and char:FindFirstChild("Plate")
    if not plate then
        Status.Text = "Không tìm thấy dĩa (Plate)!"
        return
    end
    _G.PlateRunning = true
    _G.PlatePauseRequested = false
    PlateBtn.Text = "Bring bằng Plate: TẠM DỪNG"
    PlateBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
    task.spawn(function()
        local objects = workspace.Objects:GetChildren()
        if _G.CurrentPlateIndex > 500 or _G.CurrentPlateIndex > #objects then _G.CurrentPlateIndex = 1 end
        for i = _G.CurrentPlateIndex, math.min(#objects, 500) do
            if _G.PlatePauseRequested or not _G.PlateRunning then break end
            _G.CurrentPlateIndex = i
            local targetObject = objects[i]
            if targetObject then
                local nameLower = string.lower(targetObject.Name)
                local matchesSearch = (_G.SearchText == "") or (string.find(nameLower, _G.SearchText))
                local matchesDropdown = (_G.SelectedItemName == "Tất Cả Vật Phẩm") or (targetObject.Name == _G.SelectedItemName)
                
                if matchesSearch and matchesDropdown then
                    pcall(function() InteractionEvent:FireServer(plate, "placeInPlate", targetObject) end)
                end
            end
            if i % 8 == 0 then
                Status.Text = "Plate quét: " .. tostring(i) .. "/500"
                task.wait(0.03)
            end
        end
        if not _G.PlatePauseRequested and _G.PlateRunning then
            Status.Text = "Đã quét Plate xong!"
            PlateBtn.Text = "Bring bằng Plate: BẮT ĐẦU"
            PlateBtn.BackgroundColor3 = Color3.fromRGB(130, 50, 180)
            _G.PlateRunning = false
            _G.CurrentPlateIndex = 1
        end
    end)
end)

HoldBtn.MouseButton1Click:Connect(function()
    _G.HoldingGrab = not _G.HoldingGrab
    if _G.HoldingGrab then
        HoldBtn.Text = "Hold Grab: BẬT"
        HoldBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
        Status.Text = "Chu kỳ Drop & Grab siêu tốc hoạt động..."
        
        _G.HoldConnection = RunService.Heartbeat:Connect(function()
            local objects = workspace.Objects:GetChildren()
            local character = LocalPlayer.Character
            local root = character and character:FindFirstChild("HumanoidRootPart")
            if not root then return end
            
            for i = 1, math.min(#objects, 500) do
                if not _G.HoldingGrab then break end
                local item = objects[i]
                if item then
                    local mainPart = getPrimaryOrFirstPart(item)
                    if mainPart and not mainPart.Anchored then
                        pcall(function()
                            if mainPart:GetNetworkOwner() == LocalPlayer then
                                if not _G.HeldObjects[item] then
                                    if item:IsA("Model") then
                                        _G.HeldObjects[item] = root.CFrame:ToObjectSpace(item:GetPivot())
                                    else
                                        _G.HeldObjects[item] = root.CFrame:ToObjectSpace(mainPart.CFrame)
                                    end
                                end
                                
                                DropEvent:FireServer(item)
                                GrabEvent:InvokeServer(item)
                            end
                            
                            local relativeCF = _G.HeldObjects[item]
                            if relativeCF then
                                mainPart.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                                mainPart.AssemblyAngularVelocity = Vector3.new(0, 0, 0)
                                local targetCF = root.CFrame:ToWorldSpace(relativeCF)
                                if item:IsA("Model") then
                                    item:PivotTo(targetCF)
                                else
                                    mainPart.CFrame = targetCF
                                end
                            end
                        end)
                    end
                end
            end
        end)
    else
        HoldBtn.Text = "Hold Grab: TẮT"
        HoldBtn.BackgroundColor3 = Color3.fromRGB(180, 130, 0)
        Status.Text = "Đã tắt Hold Grab."
        if _G.HoldConnection then _G.HoldConnection:Disconnect() _G.HoldConnection = nil end
        _G.HeldObjects = {}
    end
end)

FuelBtn.MouseButton1Click:Connect(function()
    local objects = workspace.Objects:GetChildren()
    local count = 0
    FuelBtn.Text = "Đang nạp củi..."
    FuelBtn.BackgroundColor3 = Color3.fromRGB(150, 150, 150)
    task.spawn(function()
        for i = 1, math.min(#objects, 500) do
            local item = objects[i]
            if item and string.find(string.lower(item.Name), "log") then
                local mainPart = getPrimaryOrFirstPart(item)
                if mainPart and not mainPart.Anchored then
                    pcall(function()
                        mainPart.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                        mainPart.AssemblyAngularVelocity = Vector3.new(0, 0, 0)
                        if item:IsA("Model") then
                            item:PivotTo(_G.TargetCFrame)
                        else
                            mainPart.CFrame = _G.TargetCFrame
                        end
                        count = count + 1
                    end)
                end
            end
        end
        Status.Text = "Đã dịch chuyển " .. tostring(count) .. " thanh củi!"
        FuelBtn.Text = "Easy Fuel"
        FuelBtn.BackgroundColor3 = Color3.fromRGB(200, 100, 0)
    end)
end)
