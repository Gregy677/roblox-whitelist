--// CheeseUILib.lua
-- Simple UI Library (Blue + Yellow theme, Cheese Hub style)

local Library = {}
Library.__index = Library

--// Create a window
function Library:CreateWindow(title)
    local Window = {}
    Window.Tabs = {}

    -- ScreenGui
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "CheeseHubUI"
    ScreenGui.Parent = game:GetService("CoreGui")

    -- Main Frame
    local MainFrame = Instance.new("Frame")
    MainFrame.Size = UDim2.new(0, 460, 0, 330)
    MainFrame.Position = UDim2.new(0.25, 0, 0.25, 0)
    MainFrame.BackgroundColor3 = Color3.fromRGB(10, 30, 60)
    MainFrame.BorderSizePixel = 0
    MainFrame.Active = true
    MainFrame.Draggable = true
    MainFrame.Visible = true
    MainFrame.Parent = ScreenGui
    Window.MainFrame = MainFrame

    -- Round corners + outline
    local UICorner = Instance.new("UICorner")
    UICorner.CornerRadius = UDim.new(0, 14)
    UICorner.Parent = MainFrame

    local UIStroke = Instance.new("UIStroke")
    UIStroke.Thickness = 3
    UIStroke.Color = Color3.fromRGB(255, 215, 0)
    UIStroke.Parent = MainFrame

    -- Title
    local TitleBar = Instance.new("Frame")
    TitleBar.Size = UDim2.new(1, 0, 0, 40)
    TitleBar.BackgroundColor3 = Color3.fromRGB(20, 50, 100)
    TitleBar.BorderSizePixel = 0
    TitleBar.Parent = MainFrame

    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1, 0, 1, 0)
    Title.BackgroundTransparency = 1
    Title.Text = title
    Title.TextColor3 = Color3.fromRGB(255, 215, 0)
    Title.Font = Enum.Font.GothamBold
    Title.TextSize = 18
    Title.Parent = TitleBar

    -- Tab bar
    local TabBar = Instance.new("Frame")
    TabBar.Size = UDim2.new(1, 0, 0, 40)
    TabBar.Position = UDim2.new(0, 0, 0, 40)
    TabBar.BackgroundColor3 = Color3.fromRGB(25, 70, 130)
    TabBar.BorderSizePixel = 0
    TabBar.Parent = MainFrame
    Window.TabBar = TabBar

    local TabLayout = Instance.new("UIListLayout")
    TabLayout.FillDirection = Enum.FillDirection.Horizontal
    TabLayout.SortOrder = Enum.SortOrder.LayoutOrder
    TabLayout.Padding = UDim.new(0, 5)
    TabLayout.Parent = TabBar

    --// Create a tab
    function Window:CreateTab(tabName)
        local Tab = {}
        Tab.Elements = {}

        local Button = Instance.new("TextButton")
        Button.Size = UDim2.new(0, 150, 1, 0)
        Button.Text = tabName
        Button.TextColor3 = Color3.fromRGB(255, 255, 255)
        Button.BackgroundColor3 = Color3.fromRGB(40, 90, 160)
        Button.BorderSizePixel = 0
        Button.Font = Enum.Font.GothamBold
        Button.TextSize = 14
        Button.Parent = TabBar

        local BC = Instance.new("UICorner")
        BC.CornerRadius = UDim.new(0, 10)
        BC.Parent = Button

        local TabFrame = Instance.new("Frame")
        TabFrame.Size = UDim2.new(1, -10, 1, -90)
        TabFrame.Position = UDim2.new(0, 5, 0, 85)
        TabFrame.BackgroundTransparency = 1
        TabFrame.Visible = false
        TabFrame.Parent = MainFrame

        local UIList = Instance.new("UIListLayout")
        UIList.Padding = UDim.new(0, 10)
        UIList.Parent = TabFrame

        Tab.Button = Button
        Tab.Frame = TabFrame

        -- button to show/hide tabs
        Button.MouseButton1Click:Connect(function()
            for _, t in pairs(Window.Tabs) do
                t.Frame.Visible = false
            end
            TabFrame.Visible = true
        end)

        --// Add a button
        function Tab:AddButton(text, callback)
            local Btn = Instance.new("TextButton")
            Btn.Size = UDim2.new(0, 230, 0, 40)
            Btn.Text = text
            Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
            Btn.Font = Enum.Font.GothamBold
            Btn.TextSize = 14
            Btn.BackgroundColor3 = Color3.fromRGB(50, 110, 190)
            Btn.BorderSizePixel = 0
            Btn.Parent = TabFrame

            local BC = Instance.new("UICorner")
            BC.CornerRadius = UDim.new(0, 10)
            BC.Parent = Btn

            Btn.MouseButton1Click:Connect(function()
                if callback then callback() end
            end)
        end

        --// Add a toggle
        function Tab:AddToggle(text, callback)
            local Holder = Instance.new("Frame")
            Holder.Size = UDim2.new(0, 230, 0, 40)
            Holder.BackgroundTransparency = 1
            Holder.Parent = TabFrame

            local Label = Instance.new("TextLabel")
            Label.Size = UDim2.new(0.65, 0, 1, 0)
            Label.BackgroundTransparency = 1
            Label.Text = text
            Label.TextColor3 = Color3.fromRGB(255, 255, 255)
            Label.Font = Enum.Font.Gotham
            Label.TextSize = 14
            Label.Parent = Holder

            local Switch = Instance.new("TextButton")
            Switch.Size = UDim2.new(0.3, 0, 0.8, 0)
            Switch.Position = UDim2.new(0.68, 0, 0.1, 0)
            Switch.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
            Switch.Text = "OFF"
            Switch.TextColor3 = Color3.fromRGB(255, 255, 255)
            Switch.Font = Enum.Font.GothamBold
            Switch.TextSize = 12
            Switch.BorderSizePixel = 0
            Switch.Parent = Holder

            local SC = Instance.new("UICorner")
            SC.CornerRadius = UDim.new(1, 0)
            SC.Parent = Switch

            local On = false
            Switch.MouseButton1Click:Connect(function()
                On = not On
                if On then
                    Switch.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
                    Switch.Text = "ON"
                else
                    Switch.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
                    Switch.Text = "OFF"
                end
                if callback then callback(On) end
            end)
        end

        Window.Tabs[tabName] = Tab
        return Tab
    end

    -- Show first tab by default
    return Window
end

return Library