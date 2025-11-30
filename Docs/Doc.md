# 📜 Syde Documentation

## Loading

```lua
local SydeUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/SupermanMario/UI/refs/heads/main/Syde/Source", true))()
```
*Note: This is a loader. It fetches and executes the actual Syde UI source from the Github repo.*

## Loader configuration
```lua
SydeUI:Load({
  Logo = '7488932274',                -- numeric asset id (no rbxassetid:// prefix)
  Name = 'Lavender',
  Status = 'Stable',                  -- Stable | Unstable | Detected | Patched
  Accent = Color3.fromRGB(251, 144, 255),
  HitBox = Color3.fromRGB(251, 144, 255),
  AutoLoad = false,                   -- not recommended
  Socials = {                         -- allows 1 Large and up to 2 Small blocks
    { Name = 'Syde', Style = 'Discord', Size = "Large", CopyToClip = true },
    { Name = 'GitHub', Style = 'GitHub', Size = "Small", CopyToClip = true },
  },
  ConfigurationSaving = {             -- requires executor FS support
    Enabled = true,
    FolderName = 'since',
    FileName = "hot"                  -- saved as JSON by the library
  },
  AutoJoinDiscord = {
    Enabled = true,                   -- wrap RPC with fallbacks
    Invite = "ABCD",              -- invite code only (no discord.gg/)
    RememberJoins = false,
  },
})
```

## Window
```lua
local Window = SydeUI:Init({
  Title = 'Lavender',
  SubText = 'Modified With 💓 By @Javen'
})
```
## Creating tabs
```lua
local a = Window:InitTab('Main')
local b = Window:InitTab('AutoFarms')
local c = Window:InitTab('Fun')
local d = Window:InitTab('Esp')
local e = Window:InitTab('FE')
```
## Notify
```lua
SydeUI:Notify({
  Title = 'This is a Notification',
  Content = 'This is a Notification',
  Duration = 5
})
```
## Popup
```lua
SydeUI:Popup({
  Title = 'Popup Title',
  Content = 'Popup content here.',
})
```
## Modal
```lua
SydeUI:Modal({
  Title = 'Confirm Action',
  Content = 'Are you sure you want to proceed?',
  ConfirmCallBack = function()
    print('Confirmed')
  end,
  CancelCallBack = function()
    print('Cancelled')
  end,
  -- Backwards compatibility for older builds (typo):
  ConfimCallBack = function()
    print('Confirmed (compat)')
  end,
})
```

## Button
```lua
a:Button({
  Title = 'Button',
  Description = '',
  Type = 'Default', -- Default | Hold
  HoldTime = 2,
  CallBack = function() print('Clicked') end,
})
```

## Toggle
```lua
a:Toggle({
  Title = 'Toggle',
  Value = true,
  Config = true, -- shows a keybind config UI if supported
  CallBack = function(v) print(v) end,
})
```

## Slider group
```lua
a:CreateSlider({
  Title = 'Slider Group',
  Sliders = {
    { Title = 'Slider 1', Range = {0,100}, Increment = 1, StarterValue = 50, CallBack = function(v) print(v) end, Flag = 'slider1' },
    { Title = 'Slider 2', Range = {0,10}, Increment = 0.1, StarterValue = 5, CallBack = function(v) print(v) end, Flag = 'slider2' }
  }
})
```

## Dropdown
```lua
a:Dropdown({
  Title = 'Dropdown',
  Options = {'Option 1', 'Option 2'},
  StarterOption = 'Option 1',
  PlaceHolder = 'Select Option...',
  Multi = false,
  CallBack = function(selected) print(selected) end,
})
```

## Text input
```lua
a:TextInput({
  Title = 'Text Input',
  PlaceHolder = 'Enter text...',
  NumbersOnly = false,
  ClearOnLost = true,
  MaxSize = 100,
  CallBack = function(text) print(text) end,
})
```
## Color picker
```lua
a:ColorPicker({
  Title = 'Color Picker',
  Linkable = true,
  Color = Color3.fromRGB(255, 0, 0),
  CallBack = function(color) print(color) end,
  Flag = 'color1'
})
```
## Keybind
```lua
a:Keybind({
  Title = 'Keybind',
  Key = Enum.KeyCode.F,
  Description = 'Optional Description',
  CallBack = function() print('Key pressed') end,
})
```

## Section
```lua
a:Section('Section Title', 'icon_id')
```

## Paragraph
```lua
a:Paragraph({
  Title = 'Paragraph Title',
  Content = 'Paragraph content here. This can be multi-line text.',
})
```

## Label
```lua
a:Label('Label Text', 'Left') -- Left | Center | Right
```

## Image
```lua
a:Img({ Image = 'image_id' })
```
## Enhanced view
```lua
a:EnhancedView({
  Title = '3D View',
  Object = workspace.Part,
  UserRotate = true,
  AutoRotate = true
})
```

## Rate
```lua
a:Rate({
  Title = 'Rate Us',
  WebHook = 'webhook_url' -- optional
})
```

```lua
SydeUI:SaveSettingsConfig()
SydeUI:LoadSettingsConfig()
```
*Files: Saved as JSON. Requires executor FS APIs (writefile, readfile).*

## Executor safety and guards
```lua
local hasClipboard = typeof(setclipboard) == "function"
local hasFS = typeof(writefile) == "function" and typeof(readfile) == "function"
local hasRequest = typeof(request) == "function" or typeof(http_request) == "function"
```



## Examples
*Include examples/demo.lua that shows Load, Init, basic elements, and a modal:*

```lua
local SydeUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/SupermanMario/UI/refs/heads/main/Syde/Source", true))()
local Window = SydeUI:Init({ Title = 'Lavender', SubText = 'Made With 💓 By @SellEssence' })
local Main = Window:InitTab('Main')

SydeUI:Notify({ Title = 'Syde', Content = 'Loaded successfully', Duration = 3 })

Main:Button({
  Title = 'Show Modal',
  CallBack = function()
    SydeUI:Modal({
      Title = 'Delete Save',
      Content = 'Are you sure you want to delete your saved config?',
      ConfirmCallBack = function()
        SydeUI:Notify({ Title = 'Deleted', Content = 'Config removed', Duration = 3 })
        -- guard FS before deletion
      end,
      CancelCallBack = function()
        SydeUI:Notify({ Title = 'Cancelled', Content = 'No changes made', Duration = 2 })
      end,
      ConfimCallBack = function() end, -- compatibility
    })
  end
})
```
