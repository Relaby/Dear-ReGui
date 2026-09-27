# ReGui Documentation

A reference guide for the ReGui Roblox UI library, covering core functions, windows, canvases, configuration, and UI elements.

---

## Table of Contents

* [ReGui Functions](#regui-functions)
* [Window](#window)
* [TabsWindow](#tabswindow)
* [PopupModal](#popupmodal)
* [Canvas Functions](#canvas-functions)
* [Configuration](#configuration)
* [Elements](#elements)

  * [Label](#label)
  * [Error](#error)
  * [Button](#button)
  * [SmallButton](#smallbutton)
  * [RadioButton](#radiobutton)
  * [Image](#image)
  * [VideoPlayer](#videoplayer)
  * [Checkbox](#checkbox)
  * [Radiobox](#radiobox)
  * [Viewport](#viewport)
  * [Console](#console)
  * [Region](#region)
  * [List](#list)
  * [CollapsingHeader](#collapsingheader)
  * [TreeNode](#treenode)
  * [Separator](#separator)
  * [Indent](#indent)
  * [BulletText](#bullettext)
  * [Bullet](#bullet)
  * [Row](#row)
  * [Table](#table)
  * [TabSelector](#tabselector)
  * [SliderInt](#sliderint)
  * [SliderFloat](#sliderfloat)
  * [SliderEnum](#sliderenum)
  * [SliderColor3](#slidercolor3)
  * [SliderCFrame](#slidercframe)
  * [SliderProgress](#sliderprogress)
  * [DragInt](#dragint)
  * [DragFloat](#dragfloat)
  * [DragColor3](#dragcolor3)
  * [DragCFrame](#dragcframe)
  * [InputText](#inputtext)
  * [InputTextMultiline](#inputtextmultiline)
  * [InputInt](#inputint)
  * [InputColor3](#inputcolor3)
  * [InputCFrame](#inputcframe)
  * [ProgressBar](#progressbar)
  * [Combo](#combo)
  * [Keybind](#keybind)
  * [PlotHistogram](#plothistogram)
* [Code Editor](#code-editor)

---

# ReGui Functions

## `ReGui:SetWindowFocusesEnabled()`

```lua
ReGui:SetWindowFocusesEnabled(Enabled: boolean)
```

Determines whether Window focuses should update.

## `ReGui:GetFocusedWindow()`

```lua
ReGui:GetFocusedWindow(): WindowClass?
```

Returns the Window with an active focus.

## `ReGui:SetFocusedWindow()`

```lua
ReGui:SetFocusedWindow(WindowClass: table?)
```

Sets the currently focused window.

## `ReGui:WindowCanFocus()`

```lua
ReGui:WindowCanFocus(WindowClass: table): boolean
```

Checks if the Window can be brought into focus.

## `ReGui:GetDictSize()`

```lua
ReGui:GetDictSize(Dict: table): number
```

Returns the number of items in a dictionary.

## `ReGui:GetAnimationData()`

```lua
ReGui:GetAnimationData(Object: GuiObject): table
```

Returns animation data connected to an object.

## `ReGui:SetAnimationsEnabled()`

```lua
ReGui:SetAnimationsEnabled(Enabled: boolean)
```

Globally enables or disables animations.

## `ReGui:SetAnimation()`

```lua
ReGui:SetAnimation(
    Object: GuiObject,
    Reference: (string|table),
    Listener: GuiObject?
)
```

Sets an animation for an object using a reference from `ReGui.Animations`.

## `ReGui:GetChildOfClass()`

```lua
ReGui:GetChildOfClass(
    Object: GuiObject,
    ClassName: string
): GuiObject
```

Returns a child matching the specified class. If one does not exist, one is created.

## `ReGui:StackWindows()`

```lua
ReGui:StackWindows()
```

Positions Windows in a cascade.

## `ReGui:MergeMetatables()`

```lua
ReGui:MergeMetatables(First, Second)
```

Merges metatables, including `__newindex` settings.

## `ReGui:GetElementFlags()`

```lua
ReGui:GetElementFlags(Object: GuiObject): table?
```

Returns flags connected with an object.

## `ReGui:IsMouseEvent()`

```lua
ReGui:IsMouseEvent(
    Input: InputObject,
    IgnoreMovement: boolean
)
```

Checks whether an `InputObject` is a mouse event.

## `ReGui:SetItemTooltip()`

```lua
ReGui:SetItemTooltip(
    Parent: GuiObject,
    Render: (Elements) -> ...any
)
```

Sets a tooltip. The `Render` function receives the tooltip Canvas.

## `ReGui:GetMouseLocation()`

```lua
ReGui:GetMouseLocation(): (number, number)
```

Returns the current mouse X/Y location.

## `ReGui:GetThemeKey()`

```lua
ReGui:GetThemeKey(
    Theme: (string|table),
    Key: string
)
```

Looks up a theme and retrieves a theme key value.

## `ReGui:CheckConfig()`

```lua
ReGui:CheckConfig(
    Source: table,
    Base: table,
    Call: boolean?,
    IgnoreKeys: table?
)
```

Compares `Source` to `Base` and adds missing or nil values from `Base`.

## `ReGui:GetScreenSize()`

```lua
ReGui:GetScreenSize(): Vector2
```

Returns the current viewport size.

## `ReGui:IsConsoleDevice()`

```lua
ReGui:IsConsoleDevice(): boolean
```

Checks whether a GamePad is connected.

## `ReGui:IsMobileDevice()`

```lua
ReGui:IsMobileDevice(): boolean
```

Checks whether the device has touchscreen input.

## `ReGui:GetVersion()`

```lua
ReGui:GetVersion(): string
```

Returns the ReGui version number.

## `ReGui:IsDoubleClick()`

```lua
ReGui:IsDoubleClick(TickRange: number): boolean
```

Checks whether the specified range should be considered a double click.

## `ReGui:Warn()`

```lua
ReGui:Warn(...)
```

Prints a concatenated warning message.

## `ReGui:Concat()`

```lua
ReGui:Concat(Table: table, Separator: " ")
```

Provides an improved `table.concat`.

## `ReGui:SetProperties()`

```lua
ReGui:SetProperties(
    Object: Instance,
    Properties: table
)
```

Applies properties from a dictionary without errors when a property cannot be applied.

## `ReGui:ApplyFlags()`

```lua
ReGui:ApplyFlags({
    Object = Instance,
    Class = table,
    WindowClass = table?
})
```

Similar to `SetProperties`, but checks `ReGui.Flags` for functions connected to property keys.

## `ReGui:InsertPrefab()`

```lua
ReGui:InsertPrefab(
    Name: string,
    Properties
): GuiObject
```

Returns a copy of a matching object from the prefabs folder.

---

# Window

Creates a standard ReGui window and returns a Canvas.

```lua
type Window = {
    AutoSize: string?,
    CloseCallback: (Window) -> boolean?,
    Collapsed: boolean?,
    IsDragging: boolean?,
    MinSize: Vector2?,
    Theme: any?,
    Title: string?,

    NoTabs: boolean?,
    NoMove: boolean?,
    NoGradients: boolean?,
    NoResize: boolean?,
    NoClose: boolean?,
    NoCollapse: boolean?,
    NoScrollBar: boolean?,
    NoSelectEffect: boolean?,
    NoFocusOnAppearing: boolean?,
    NoDefaultTitleBarButtons: boolean?,
    NoWindowRegistor: boolean?,
    OpenOnDoubleClick: boolean?,

    SetTheme: (Window, ThemeName: string) -> Window,
    SetTitle: (Window, Title: string) -> Window,
    UpdateConfig: (Window, Config: table) -> Window,
    SetCollapsed: (
        Window,
        Collapsed: boolean,
        NoAnimation: boolean?
    ) -> Window,
    SetCollapsible: (Window, Collapsible: boolean) -> Window,
    SetFocused: (Window, Focused: boolean) -> Window,
    Center: (Window) -> Window,
    SetVisible: (Window, Visible: boolean) -> Window,
    TagElements: (
        Window,
        Objects: {[GuiObject]: string}
    ) -> nil,
    Close: (Window) -> nil,
}
```

## Example

```lua
local Window = ReGui:Window({
    Title = "Hello world!",
    Size = UDim2.fromOffset(300, 200)
})

Window:Label({
    Text = "Hello world!"
})
```

The returned object can be used as a Canvas.

## Properties

| Property                   | Description                                   |
| -------------------------- | --------------------------------------------- |
| `AutoSize`                 | Controls automatic window sizing              |
| `CloseCallback`            | Called when the window is closed              |
| `Collapsed`                | Controls whether the window is collapsed      |
| `IsDragging`               | Indicates whether the window is being dragged |
| `MinSize`                  | Minimum window size                           |
| `Theme`                    | Window theme                                  |
| `Title`                    | Window title                                  |
| `NoTabs`                   | Disables tabs                                 |
| `NoMove`                   | Prevents moving                               |
| `NoGradients`              | Disables gradients                            |
| `NoResize`                 | Prevents resizing                             |
| `NoClose`                  | Removes/disables close functionality          |
| `NoCollapse`               | Prevents collapsing                           |
| `NoScrollBar`              | Hides the scrollbar                           |
| `NoSelectEffect`           | Disables selection effects                    |
| `NoFocusOnAppearing`       | Prevents focus when appearing                 |
| `NoDefaultTitleBarButtons` | Disables default title-bar buttons            |
| `NoWindowRegistor`         | Prevents window registration                  |
| `OpenOnDoubleClick`        | Opens on double-click                         |

## Methods

### `:SetTheme()`

```lua
Window:SetTheme("ThemeName")
```

Sets the window theme.

### `:SetTitle()`

```lua
Window:SetTitle("New Title")
```

Changes the window title.

### `:UpdateConfig()`

```lua
Window:UpdateConfig({
    NoResize = true
})
```

Updates the window configuration.

### `:SetCollapsed()`

```lua
Window:SetCollapsed(true)
```

Collapses or expands the window.

The second parameter can disable the animation:

```lua
Window:SetCollapsed(true, true)
```

### `:SetCollapsible()`

```lua
Window:SetCollapsible(false)
```

Controls whether the window can be collapsed.

### `:SetFocused()`

```lua
Window:SetFocused(true)
```

Sets the window's focus state.

### `:Center()`

```lua
Window:Center()
```

Centers the window.

### `:SetVisible()`

```lua
Window:SetVisible(false)
```

Shows or hides the window.

### `:TagElements()`

```lua
Window:TagElements({
    [SomeGuiObject] = "Tag"
})
```

Tags GUI objects associated with the window.

### `:Close()`

```lua
Window:Close()
```

Closes the window.

## Theme

| Tag                             | Affects                         |
| ------------------------------- | ------------------------------- |
| `WindowBg`                      | Background color                |
| `WindowBgTransparency`          | Background transparency         |
| `TitleBarBgCollapsed`           | Collapsed titlebar background   |
| `TitleBarTransparencyCollapsed` | Collapsed titlebar transparency |
| `TitleBarBgActive`              | Active titlebar background      |
| `TitleBarTransparencyActive`    | Active titlebar transparency    |
| `TitleBarBg`                    | Inactive titlebar background    |
| `TitleBarTransparency`          | Inactive titlebar transparency  |
| `Border`                        | Border color                    |
| `BorderTransparency`            | Inactive border transparency    |
| `BorderTransparencyActive`      | Active border transparency      |
| `ResizeGrab`                    | Resize grab color               |

---

# TabsWindow

`TabsWindow` combines the functionality of a Window and a TabSelector.

The returned object uses merged metatables and can therefore be used as both a Window and a TabSelector.

```lua
type TabsWindow = {
    AutoSize: string?,
    CloseCallback: (Window) -> boolean?,
    Collapsed: boolean?,
    IsDragging: boolean?,
    MinSize: Vector2?,
    Theme: any?,
    Title: string?,

    NoTabs: boolean?,
    NoMove: boolean?,
    NoGradients: boolean?,
    NoResize: boolean?,
    NoTitleBar: boolean?,
    NoClose: boolean?,
    NoCollapse: boolean?,
    NoScrollBar: boolean?,
    NoSelectEffect: boolean?,
    NoFocusOnAppearing: boolean?,
    NoDefaultTitleBarButtons: boolean?,
    NoWindowRegistor: boolean?,
    OpenOnDoubleClick: boolean?,

    SetTheme: (Window, ThemeName: string) -> Window,
    SetTitle: (Window, Title: string) -> Window,
    UpdateConfig: (Window, Config: table) -> Window,
    SetCollapsed: (
        Window,
        Collapsed: boolean,
        NoAnimation: boolean?
    ) -> Window,
    SetCollapsible: (Window, Collapsible: boolean) -> Window,
    SetFocused: (Window, Focused: boolean) -> Window,
    Center: (Window) -> Window,
    SetVisible: (Window, Visible: boolean) -> Window,
    TagElements: (
        Window,
        Objects: {[GuiObject]: string}
    ) -> nil,
    Close: (Window) -> nil,
}
```

## Example

```lua
local TabsWindow = ReGui:TabsWindow({
    Title = "Hello world!",
    Size = UDim2.fromOffset(300, 200)
})
```

Create a tab:

```lua
local Tab = TabsWindow:CreateTab({
    Name = "Tab"
})

Tab:Label({
    Text = "Hello world!"
})
```

`TabsWindow` returns:

```text
TabSelector & Window
```

because the metatables are merged.

## Theme

| Tag                             | Affects                         |
| ------------------------------- | ------------------------------- |
| `WindowBg`                      | Background color                |
| `WindowBgTransparency`          | Background transparency         |
| `TitleBarBgCollapsed`           | Collapsed titlebar background   |
| `TitleBarTransparencyCollapsed` | Collapsed titlebar transparency |
| `TitleBarBgActive`              | Active titlebar background      |
| `TitleBarTransparencyActive`    | Active titlebar transparency    |
| `TitleBarBg`                    | Inactive titlebar background    |
| `TitleBarTransparency`          | Inactive titlebar transparency  |
| `Border`                        | Border color                    |
| `BorderTransparency`            | Inactive border transparency    |
| `BorderTransparencyActive`      | Active border transparency      |
| `ResizeGrab`                    | Resize grab color               |

---

# PopupModal

Creates a popup modal and returns a Canvas.

```lua
type PopupModal = {
    NoResize: boolean?,
    NoAnimation: boolean?,
    NoClose: boolean?,
    NoCollapse: boolean?,
    Theme: string,
    Parent: GuiObject?
}
```

## Example

```lua
local ModalWindow = Window:PopupModal({
    Title = "Delete?"
})

ModalWindow:Label({
    Text = "All those beautiful files will be deleted.\nThis operation cannot be undone!",
    TextWrapped = true
})

ModalWindow:Separator()

ModalWindow:Checkbox({
    Value = false,
    Label = "Don't ask me next time"
})

local Row = ModalWindow:Row({
    Expanded = true
})

Row:Button({
    Text = "Okay",

    Callback = function()
        ModalWindow:ClosePopup()
    end,
})

Row:Button({
    Text = "Cancel",

    Callback = function()
        ModalWindow:ClosePopup()
    end,
})
```

## Properties

| Property      | Description              |
| ------------- | ------------------------ |
| `NoResize`    | Prevents resizing        |
| `NoAnimation` | Disables modal animation |
| `NoClose`     | Prevents closing         |
| `NoCollapse`  | Prevents collapsing      |
| `Theme`       | Modal theme              |
| `Parent`      | Parent GUI object        |

## Theme

| Tag                             | Affects                         |
| ------------------------------- | ------------------------------- |
| `ModalWindowDimBg`              | Background of the modal dim     |
| `WindowBg`                      | Modal background color          |
| `WindowBgTransparency`          | Modal background transparency   |
| `TitleBarBgCollapsed`           | Collapsed titlebar background   |
| `TitleBarTransparencyCollapsed` | Collapsed titlebar transparency |
| `TitleBarBgActive`              | Active titlebar background      |
| `TitleBarTransparencyActive`    | Active titlebar transparency    |
| `TitleBarBg`                    | Inactive titlebar background    |
| `TitleBarTransparency`          | Inactive titlebar transparency  |
| `Border`                        | Border color                    |
| `BorderTransparency`            | Inactive border transparency    |
| `BorderTransparencyActive`      | Active border transparency      |
| `ResizeGrab`                    | Resize grab color               |

---

# Canvas Functions

Canvas is the base container into which ReGui elements can be inserted.

`Window`, `Row`, `CollapsingHeader`, `TreeNode`, `Region`, `List`, `Indent`, `Bullet`, and other elements can return Canvas objects.

## `:ClearChildElements()`

Destroys all child elements.

```lua
Canvas:ClearChildElements()
```

## `:GetChildElements()`

```lua
Canvas:GetChildElements(): table
```

Returns an array of elements in the Canvas.

## `:GetObject()`

```lua
Canvas:GetObject(): Instance
```

Returns the real Roblox object.

## `:TagElements()`

```lua
Canvas:TagElements(Objects: ObjectTable)
```

Works the same as `Window:TagElements`.

## `:SetElementFocused()`

```lua
Canvas:SetElementFocused(
    Object: GuiObject,
    Data
)
```

Disables interaction with other elements while the specified object is focused.

## `:Remove()`

```lua
Canvas:Remove()
```

Destroys the Canvas and all child elements.

---

# Configuration

ReGui does not provide a built-in filesystem interface. Your script must provide its own filesystem handler.

## `ReGui:DumpIni()`

```lua
ReGui:DumpIni(JsonEncode: boolean?): (table|string)
```

Returns ReGui Ini settings as either a table or JSON string.

## `ReGui:LoadIni()`

```lua
ReGui:LoadIni(
    NewSettings: (table|string),
    JsonEncoded: boolean?
)
```

Loads Ini settings into ReGui elements.

## `ReGui:AddIniFlag()`

```lua
ReGui:AddIniFlag(
    Flag: string,
    Element
)
```

Manually declares an element for an `IniFlag`.

## `ReGui:LoadIniIntoElement()`

```lua
ReGui:LoadIniIntoElement(
    Element,
    Values: table
)
```

Loads values from a value table into an element.

---

# Elements

## Label

```lua
type Label = {
    Text: string?,
    Bold: boolean?,
    Italic: boolean?,
    Font: string?
}
```

```lua
Canvas:Label({
    Text = "Hello world!"
})
```

### Theme

| Tag        | Affects        |
| ---------- | -------------- |
| `Text`     | Text color     |
| `TextFont` | Text fontface  |
| `TextSize` | Text font size |

---

## Error

```lua
type Error = {
    Text: string?
}
```

```lua
Canvas:Error({
    Text = "Hello world!"
})
```

---

## Button

```lua
type Button = {
    Text: string?,
    Callback: ((...any) -> unknown)?
}
```

```lua
Canvas:Button({
    Text = "Print",

    Callback = function(self)
        print("Hello world!")
    end
})
```

### Theme

| Tag         | Affects          |
| ----------- | ---------------- |
| `ButtonsBg` | Background color |
| `Text`      | Text color       |
| `TextFont`  | Text fontface    |
| `TextSize`  | Text font size   |

---

## SmallButton

```lua
type SmallButton = {
    Text: string?,
    Callback: ((...any) -> unknown)?
}
```

```lua
Canvas:SmallButton({
    Text = "Print",

    Callback = function(self)
        print("Hello world!")
    end
})
```

### Theme

Uses:

* `ButtonsBg`
* `Text`
* `TextFont`
* `TextSize`

---

## RadioButton

```lua
type RadioButton = {
    Icon: string?,
    IconRotation: number?,
    Callback: ((...any) -> unknown)?,
}
```

```lua
Canvas:RadioButton({
    Icon = 18754976792,

    Callback = function(self)
        print("Hello world!")
    end
})
```

---

## Image

```lua
type Image = {
    Image: (string|number),
    Callback: ((...any) -> unknown)
}
```

```lua
Canvas:Image({
    Image = 5205790785
})
```

> The provided type declares `Callback` as required, while the example does not provide one.

---

## VideoPlayer

```lua
type VideoPlayer = {
    Video: (string|number),
    Looped: boolean?,
    Play: (self) -> nil
} & VideoPlayer
```

```lua
local Video = Canvas:VideoPlayer({
    Video = 5608327482,
    Looped = true,
    Size = UDim2.fromOffset(200, 300)
})

Video:Play()
```

---

## Checkbox

```lua
type Checkbox = {
    Label: string?,
    Value: boolean,
    NoAnimation: boolean?,
    TickedImageSize: UDim2,
    UntickedImageSize: UDim2,
    Callback: ((...any) -> unknown)?,

    SetValue: (self: Checkbox, Value: boolean, NoAnimation: boolean) -> ...any,
    Toggle: (self: Checkbox) -> ...any
}
```

```lua
Canvas:Checkbox({
    Value = true,
    Label = "Check box",

    Callback = function(self, Value)
        print("Ticked", Value)
    end
})
```

### Methods

```lua
Checkbox:SetValue(true)
Checkbox:Toggle()
```

### Theme

| Tag         | Affects                              |
| ----------- | ------------------------------------ |
| `FrameBg`   | Background color                     |
| `CheckMark` | Checkmark background and image color |

---

## Radiobox

```lua
type Radiobox = {
    Label: string?,
    Value: boolean,
    NoAnimation: boolean?,
    TickedImageSize: UDim2,
    UntickedImageSize: UDim2,
    Callback: ((...any) -> unknown)?,

    SetValue: (self: Checkbox, Value: boolean, NoAnimation: boolean) -> ...any,
    Toggle: (self: Checkbox) -> ...any
}
```

```lua
Canvas:Radiobox({
    Value = true,
    Label = "Check box",

    Callback = function(self, Value)
        print("Ticked", Value)
    end
})
```

### Theme

| Tag         | Affects                              |
| ----------- | ------------------------------------ |
| `FrameBg`   | Background color                     |
| `CheckMark` | Checkmark background and image color |

---

## Viewport

```lua
type Viewport = {
    Model: Instance,
    WorldModel: WorldModel?,
    Viewport: ViewportFrame?,
    Camera: Camera?,
    Clone: boolean?,

    SetCamera: (self: Viewport, Camera: Camera) -> Viewport,
    SetModel: (self: Viewport, Model: Model, PivotTo: CFrame?) -> Model
}
```

```lua
local Viewport = Canvas:Viewport({
    Size = UDim2.new(1, 0, 0, 200),
    Clone = true,
    Model = workspace.Rig
})
```

### Methods

```lua
Viewport:SetCamera(Camera)
Viewport:SetModel(Model, PivotTo?)
```

---

## Console

```lua
type Console = {
    Enabled: boolean?,
    ReadOnly: boolean?,
    Value: string?,
    RichText: boolean?,
    TextWrapped: boolean?,
    LineNumbers: boolean?,
    AutoScroll: boolean,
    LinesFormat: string,
    MaxLines: number,

    UpdateLineNumbers: (Console) -> Console,
    UpdateScroll: (Console) -> Console,
    SetValue: (Console, Value: string) -> Console,
    GetValue: (Console) -> string,
    Clear: (Console) -> Console,
    AppendText: (Console, ...string) -> Console,
    CheckLineCount: (Console) -> Console
}
```

```lua
Canvas:Console({
    LineNumbers = true
})
```

### Theme

| Tag                  | Affects                   |
| -------------------- | ------------------------- |
| `ConsoleLineNumbers` | Line number color         |
| `TextFont`           | Line number and text font |
| `TextSize`           | Font size                 |

---

## Region

```lua
type Region = {
    Scroll: boolean?
}
```

```lua
local Region = Canvas:Region()

Region:Label({
    Text = "Hello world!"
})
```

---

## List

```lua
type List = {
    Padding: number?
}
```

```lua
local List = Canvas:List()

List:Label({
    Text = "Hello world!"
})
```

---

## CollapsingHeader

```lua
type CollapsingHeader = {
    Title: string,
    CollapseIcon: string?,
    Icon: string?,
    NoAnimation: boolean?,
    Collapsed: boolean?,
    Offset: number?,
    NoArrow: boolean?,
    OpenOnDoubleClick: boolean?,
    OpenOnArrow: boolean?,
    Activated: (CollapsingHeader) -> nil,

    Remove: (CollapsingHeader) -> nil,
    SetArrowVisible: (CollapsingHeader, Visible: boolean) -> nil,
    SetTitle: (CollapsingHeader, Title: string) -> nil,
    SetIcon: (CollapsingHeader, Icon: string) -> nil,
    SetVisible: (CollapsingHeader, Visible: boolean) -> nil,
    SetCollapsed: (CollapsingHeader, Open: boolean) -> CollapsingHeader
}
```

```lua
local Header = Canvas:CollapsingHeader({
    Title = "Settings"
})

Header:Label({
    Text = "Hello world!"
})
```

### Theme

| Tag                    | Affects          |
| ---------------------- | ---------------- |
| `TextFont`             | Text font        |
| `TextSize`             | Text size        |
| `CollapsingHeaderText` | Text color       |
| `CollapsingHeaderBg`   | Background color |

---

## TreeNode

```lua
type TreeNode = {
    Title: string,
    CollapseIcon: string?,
    Icon: string?,
    NoAnimation: boolean?,
    Collapsed: boolean?,
    Offset: number?,
    NoArrow: boolean?,
    OpenOnDoubleClick: boolean?,
    OpenOnArrow: boolean?,
    Activated: (TreeNode) -> nil,

    Remove: (TreeNode) -> nil,
    SetArrowVisible: (TreeNode, Visible: boolean) -> nil,
    SetTitle: (TreeNode, Title: string) -> nil,
    SetIcon: (TreeNode, Icon: string) -> nil,
    SetVisible: (TreeNode, Visible: boolean) -> nil,
    SetCollapsed: (TreeNode, Open: boolean) -> TreeNode
}
```

```lua
local TreeNode = Canvas:TreeNode({
    Title = "Player Settings"
})

TreeNode:Label({
    Text = "Hello world!"
})
```

### Theme

Uses:

* `TextFont`
* `TextSize`
* `CollapsingHeaderText`
* `CollapsingHeaderBg`

---

## Separator

```lua
type Separator = {
    Text: string?
}
```

```lua
Canvas:Separator({
    Text = "Separator"
})

Canvas:Separator()
```

### Theme

| Tag                     | Affects                 |
| ----------------------- | ----------------------- |
| `Separator`             | Background color        |
| `SeparatorTransparency` | Background transparency |

---

## Indent

```lua
type Indent = {
    Offset: number?
}
```

```lua
local Indent = Canvas:Indent({
    Offset = 30
})

Indent:Label({
    Text = "This is indented by 30 pixels"
})
```

---

## BulletText

```lua
type BulletText = {
    Padding: number,
    Icon: (string|number)?,
    Rows: {
        [number]: string?,
    }
}
```

```lua
Canvas:BulletText({
    Rows = {
        "This is point 1",
        "This is point 2"
    }
})
```

---

## Bullet

```lua
type Bullet = {
    Padding: number?
}
```

```lua
local Bullet = Canvas:Bullet()

Bullet:Label({
    Text = "Hello world!"
})
```

---

## Row

```lua
type Row = {
    Spacing: number?,
    Expand: (Row) -> Row
}
```

```lua
local Row = Canvas:Row()

Row:Label({
    Text = "Hello world!"
})
```

### Method

```lua
Row:Expand()
```

Expands the row according to ReGui's row layout behavior.

---

# Table

Creates a table layout containing rows and columns.

```lua
type Table = {
    Align: string?,
    Border: boolean?,
    RowBackground: boolean?,
    RowBgTransparency: number?,

    Row: (Table) -> {
        Column: (Row) -> Elements
    },

    ClearRows: (Table) -> unknown,
}
```

### Example

```lua
local Table = Canvas:Table()

local Row = Table:Row()

local Column1 = Row:Column()

Column1:Label({
    Text = "Column 1!"
})

local Column2 = Row:Column()

Column2:Label({
    Text = "Column 2!"
})
```

### Methods

```lua
local Row = Table:Row()

local Column = Row:Column()

Table:ClearRows()
```

### Properties

| Property            | Description                 |
| ------------------- | --------------------------- |
| `Align`             | Table alignment             |
| `Border`            | Enables table borders       |
| `RowBackground`     | Enables row backgrounds     |
| `RowBgTransparency` | Row background transparency |

---

# TabSelector

Creates a tabbed interface.

## Tab

```lua
type Tab = {
    Name: string,
    Focused: boolean?,
    AutoSize: string?,
    TabButton: boolean?,
    Closeable: boolean?,
    OnClosure: (Tab) -> nil,
    Icon: (string|number)?
}
```

## TabSelector

```lua
type TabSelector = {
    NoTabsBar: boolean?,
    NoAnimation: boolean?,
    AutoSelectNewTabs: boolean?,
    OnActiveTabChange: ((Tab: Tab, Previous: Tab) -> nil)?,

    CreateTab: (TabsBox, Tab) -> Elements,
    RemoveTab: (TabsBox, Target: (table|string)) -> nil,
    SetActiveTab: (TabsBox, Target: (table|string)) -> nil,
}
```

### Example

```lua
local TabSelector = Canvas:TabSelector()

local Names = {
    "Avocado",
    "Broccoli",
    "Cucumber"
}

for _, Name in Names do
    local Tab = TabSelector:CreateTab({
        Name = Name
    })

    Tab:Label({
        Text = `This is the {Name} tab!`
    })
end
```

### Methods

```lua
local Tab = TabSelector:CreateTab({
    Name = "Settings"
})

TabSelector:SetActiveTab("Settings")

TabSelector:RemoveTab("Settings")
```

### Theme

| Tag                     | Affects               |
| ----------------------- | --------------------- |
| `TabsBarBg`             | Tabs bar background   |
| `TabsBarBgTransparency` | Tabs bar transparency |
| `Text`                  | Text color            |
| `TextFont`              | Text font             |
| `TextSize`              | Text size             |
| `TabPagePadding`        | Page padding          |
| `TabBgActive`           | Active tab background |
| `TabTextActive`         | Active tab text color |

---

# Slider Elements

## SliderInt

```lua
type SliderInt = {
    Value: number?,
    Format: string?,
    Label: string?,
    Minimum: number?,
    Maximum: number?,
    Disabled: boolean?,
    NoGrab: boolean?,
    NoClick: boolean?,
    NoAnimation: boolean?,
    Callback: (number) -> any?,
    ReadOnly: boolean?,

    SetDisabled: (SliderInt, Disabled: boolean) -> Slider,
    SetValue: (Slider, Value: number, IsSlider: boolean?) -> Slider?
}
```

```lua
Canvas:SliderInt({
    Label = "Slider",
    Value = 5,
    Minimum = 1,
    Maximum = 32,
})
```

### Theme

* `FrameBg`
* `FrameBgTransparency`
* `Text`
* `TextFont`
* `TextSize`

---

## SliderFloat

```lua
type SliderFloat = {
    Value: number?,
    Format: string?,
    Label: string?,
    Minimum: number?,
    Maximum: number?
} & SliderIntFlags
```

```lua
Canvas:SliderFloat({
    Label = "Slider Float",
    Minimum = 0.0,
    Maximum = 1.0,
    Value = 0.5,
    Format = "Ratio = %.3f"
})
```

---

## SliderEnum

```lua
type SliderEnum = {
    Items: {
        [number]: any
    },
    Label: string,
    Value: number,
    Callback: (SliderEnum, Value: number?) -> nil
} & SliderIntFlags
```

```lua
Canvas:SliderEnum({
    Items = {
        "Fire",
        "Earth",
        "Air",
        "Water"
    },

    Value = 2,
    Label = "Item"
})
```

`Value` represents the selected item index.

---

## SliderColor3

```lua
type SliderColor3 = {
    Value: Color3?,
    Format: string?,
    Label: string?,
    Minimum: Color3?,
    Maximum: Color3?,

    SetValue: (InputColor3, Value: Color3) -> DragColor3,
} & SliderIntFlags
```

```lua
Canvas:SliderColor3({
    Value = Color3.fromRGB(255, 255, 255),
    Label = "Color slider!"
})
```

---

## SliderCFrame

```lua
type SliderCFrame = {
    Value: CFrame?,
    Format: string?,
    Label: string?,
    Minimum: CFrame?,
    Maximum: CFrame?,

    SetValue: (SliderCFrame, Value: CFrame) -> DragColor3,
} & SliderIntFlags
```

```lua
Canvas:SliderCFrame({
    Value = CFrame.new(1, 1, 1),
    Label = "CFrame slider!"
})
```

---

## SliderProgress

```lua
type SliderProgress = {
    Value: number?,
    Format: string?,
    Label: string?,
    Minimum: number,
    Maximum: number
} & SliderIntFlags
```

```lua
Canvas:SliderProgress({
    Label = "Progress Slider",
    Value = 8,
    Minimum = 1,
    Maximum = 32,
})
```

---

# Drag Elements

## DragInt

```lua
type DragInt = {
    Format: string?,
    Label: string?,
    Callback: (DragInt, number) -> any,
    Minimum: number?,
    Maximum: number?,
    Value: number?,
    ReadOnly: boolean?,

    SetValue: (DragIntFlags, number) -> DragIntFlags,
}
```

```lua
Canvas:DragInt({
    Maximum = 100,
    Minimum = 0,
    Label = "Drag Int 0..100"
})
```

---

## DragFloat

```lua
type DragFloat = {
    Format: string?,
    Label: string?,
    Minimum: number?,
    Maximum: number?,
    Value: number?,
    Callback: (DragFloat, number) -> nil,

    SetValue: (DragFloat, number) -> DragFloat,
} & DragInt
```

```lua
Canvas:DragFloat({
    Maximum = 1,
    Minimum = 0,
    Value = 0.5
})
```

---

## DragColor3

```lua
type DragColor3 = {
    Label: string?,
    Value: Color3?,
    Minimum: Color3?,
    Minimum: Color3?,
    Callback: (DragColor3, Value: Color3) -> nil,

    SetValue: (DragColor3, Value: Color3) -> DragColor3,
} & DragInt
```

```lua
Canvas:DragColor3({
    Value = Color3.fromRGB(255, 255, 255),
    Label = "Color 1"
})
```

> The supplied type definition contains `Minimum` twice.

---

## DragCFrame

```lua
type DragCFrame = {
    Label: string?,
    Value: CFrame?,
    Minimum: CFrame?,
    Minimum: CFrame?,
    Callback: (DragCFrame, Value: CFrame) -> nil,

    SetValue: (DragCFrame, Value: CFrame) -> InputColor3,
} & DragInt
```

```lua
Canvas:DragCFrame({
    Value = CFrame.new(1, 1, 1),
    Label = "Color 1"
})
```

> The supplied definition contains `Minimum` twice and declares `SetValue` as returning `InputColor3`.

---

# Input Elements

## InputText

```lua
type InputText = {
    Value: string,
    Placeholder: string?,
    MultiLine: boolean?,
    Label: string?,
    Disabled: boolean?,

    Callback: ((string, ...any) -> unknown)?,
    Clear: (InputText) -> InputText,
    SetValue: (InputText, Value: string) -> InputText,
    SetDisabled: (InputText, Disabled: boolean) -> InputText,
}
```

```lua
Canvas:InputText({
    Label = "Input text",
    Value = "Hello world!"
})
```

### Theme

* `FrameBg`
* `FrameBgTransparency`
* `Text`
* `TextFont`
* `TextSize`

---

## InputTextMultiline

```lua
type InputTextMultiline = {
    Value: string,
    Placeholder: string?,
    Disabled: boolean?,

    Callback: ((string, ...any) -> unknown)?,
    Clear: (InputText) -> InputText,
    SetValue: (InputText, Value: string) -> InputText,
    SetDisabled: (InputText, Disabled: boolean) -> InputText,
}
```

```lua
Canvas:InputTextMultiline({
    Value = "Hello world!"
})
```

### Theme

* `FrameBg`
* `FrameBgTransparency`
* `Text`
* `TextFont`
* `TextSize`

---

## InputInt

```lua
type InputInt = {
    Value: number,
    Maximum: number?,
    Minimum: number?,
    Placeholder: string?,
    MultiLine: boolean?,
    Increment: number?,
    Label: string?,
    Callback: ((string, ...any) -> unknown)?,

    SetValue: (InputInt, Value: number, NoTextUpdate: boolean?) -> InputInt,
    Decrease: (InputInt) -> nil,
    Increase: (InputInt) -> nil,
}
```

```lua
Canvas:InputInt({
    Label = "InputInt (w/ limit)",
    Value = 5,
    Maximum = 10,
    Minimum = 1
})
```

### Methods

```lua
InputInt:SetValue(8)
InputInt:Decrease()
InputInt:Increase()
```

---

## InputColor3

```lua
type InputColor3 = {
    Label: string?,
    Value: Color3?,
    Minimum: Color3?,
    Minimum: Color3?,
    Callback: (InputColor3, Value: Color3) -> any,

    SetValue: (InputColor3, Value: Color3) -> InputColor3,
}
```

```lua
Canvas:InputColor3({
    Value = Color3.fromRGB(255, 255, 255),
    Label = "Color 1"
})
```

> The supplied definition contains `Minimum` twice.

---

## InputCFrame

```lua
type InputCFrame = {
    Label: string?,
    Value: CFrame?,
    Minimum: CFrame?,
    Maximum: CFrame?,
    Callback: (InputCFrame, Value: CFrame) -> any,

    SetValue: (
        InputCFrame,
        Value: CFrame
    ) -> InputCFrame
}
```

```lua
Canvas:InputCFrame({
    Value = CFrame.new(1, 1, 1),
    Minimum = CFrame.new(0, 0, 0),
    Maximum = CFrame.new(200, 100, 50),
    --Callback = print
})
```

---

# ProgressBar

```lua
type ProgressBar = {
    Value: number?,
    Format: string?,
    Label: string?,
    NoAnimation: boolean?,

    SetPercentage: (
        Slider,
        Value: number,
        IsSlider: boolean?
    ) -> Slider?
}
```

```lua
Canvas:ProgressBar({
    Label = "Progress Slider",
    Value = 50
})
```

### Method

```lua
ProgressBar:SetPercentage(75)
```

---

# Combo

Creates a selection/dropdown control.

```lua
type Combo = {
    Label: string?,
    Placeholder: string?,
    Callback: ((Combo, Value: any) -> any)?,
    Items: {[number?]: any}?,
    GetItems: (() -> table)?
}
```

## Array

```lua
Canvas:Combo({
    Label = "Combo",
    Selected = "AAAA",

    Items = {
        "AAAA",
        "BBBB",
        "CCCC"
    }
})
```

## Dictionary

```lua
Canvas:Combo({
    Label = "Combo",
    Selected = "Apple",

    Items = {
        Apple = "AAA",
        Banana = "BBB",
        Orange = "CCC",
    },
})
```

## Function

```lua
Canvas:Combo({
    Label = "Combo",
    Selected = "aaa",

    GetItems = function()
        return {
            "aaa",
            "bbb",
            "ccc",
        }
    end,
})
```

### Theme

| Tag                   | Affects                 |
| --------------------- | ----------------------- |
| `FrameBg`             | Background color        |
| `FrameBgTransparency` | Background transparency |
| `Text`                | Text color              |
| `TextFont`            | Text font               |
| `TextSize`            | Text font size          |
| `ButtonsBg`           | Arrow button background |

---

# Keybind

```lua
type KeyId = (
    Enum.UserInputType |
    Enum.KeyCode
)
```

```lua
export type Keybind = {
    Value: Enum.KeyCode?,
    DeleteKey: Enum.KeyCode?,
    Enabled: boolean?,
    IgnoreGameProcessed: boolean?,

    Callback: ((KeyId) -> any)?,
    OnKeybindSet: ((KeyId) -> any)?,
    OnBlacklistedKeybindSet: ((KeyId) -> any)?,

    KeyBlacklist: {
        [number]: KeyId
    },

    SetValue: ((Keybind, New: Enum.KeyCode) -> any)?,
    WaitForNewKey: ((Keybind) -> any)?
}
```

### Example

```lua
Canvas:Keybind({
    Label = "Toggle checkbox",
    Value = Enum.KeyCode.Q,

    OnKeybindSet = function(self, KeyId)
        warn("[OnKeybindSet] .Value ->", KeyId)
    end,

    Callback = function(self, KeyId)
        print(KeyId)
        TestCheckbox:Toggle()
    end,
})
```

### Theme

| Tag                   | Affects                 |
| --------------------- | ----------------------- |
| `FrameBg`             | Background color        |
| `FrameBgTransparency` | Background transparency |
| `Text`                | Text color              |
| `TextFont`            | Text font               |
| `TextSize`            | Text font size          |

---

# PlotHistogram

Creates a graph from numeric points.

```lua
type Points = {
    [number]: number
}
```

```lua
type PlotHistogram = {
    Label: string?,
    Points: Points,
    Minimum: number?,
    Maximum: number?,

    GetBaseValues: (PlotHistogram) -> (number, number),
    UpdateGraph: (PlotHistogram) -> PlotHistogram,
    PlotGraph: (
        PlotHistogram,
        Points: Points
    ) -> PlotHistogram,

    Plot: (
        PlotHistogram,
        Value: number
    ) -> {
        SetValue: (Plot, Value: number) -> nil,
        GetPointIndex: (Plot) -> number,
        Remove: (Plot, Value: number) -> nil,
    },
}
```

### Example

```lua
Canvas:PlotHistogram({
    Points = {
        0.6,
        0.1,
        1.0,
        0.5,
        0.92,
        0.1,
        0.2
    }
})
```

### With Limits

```lua
Canvas:PlotHistogram({
    Minimum = 0,
    Maximum = 1,

    Points = {
        0.6,
        0.1,
        1.0,
        0.5,
        0.92,
        0.1,
        0.2
    }
})
```

### Methods

```lua
Histogram:GetBaseValues()

Histogram:UpdateGraph()

Histogram:PlotGraph({
    0.2,
    0.4,
    0.8,
    1.0
})

local Plot = Histogram:Plot(0.75)

Plot:SetValue(0.9)
Plot:GetPointIndex()
Plot:Remove(0.9)
```

---

# Code Editor

The Code Editor can be imported through the IDE module.

```lua
local IDEModule = require(...IDEModule)
```

## Type

```lua
type CodeEditor = {
    Editable: boolean?,
    FontSize: number?,
    FontFace: FontFace?,

    ApplyTheme: (self) -> nil,
    GetVersion: () -> string,
    ClearText: (self) -> nil,
    SetText: (self, Text: string) -> nil,
    GetText: (self) -> string,
    SetEditing: (self, Editing: boolean) -> nil,
    AppendText: (self, Text: string) -> nil,
    ResetSelection: (self, NoRefresh: boolean?) -> nil,
    GetSelectionText: (self) -> string,

    Gui: Frame,
    Editing: boolean
}
```

## Creating a Code Editor

```lua
local EditorTab = TabSelector:CreateTab({
    Name = "Editor"
})

local CodeEditor = IDEModule.CodeFrame.new({
    Editable = false,
    FontSize = 13,
    Colors = SyntaxColors,
    FontFace = TextFont
})
```

Apply ReGui flags:

```lua
ReGui:ApplyFlags({
    Object = CodeEditor.Gui,
    WindowClass = Window,

    Class = {
        Fill = true,
        Active = true,
        Parent = EditorTab:GetObject(),
        BackgroundTransparency = 1,
    }
})
```

## Methods

```lua
CodeEditor:ApplyTheme()

CodeEditor:GetVersion()

CodeEditor:ClearText()

CodeEditor:SetText("print('Hello world!')")

CodeEditor:GetText()

CodeEditor:SetEditing(true)

CodeEditor:AppendText("\nprint('Another line')")

CodeEditor:ResetSelection()

CodeEditor:GetSelectionText()
```

### Properties

| Property  | Type      | Description                        |
| --------- | --------- | ---------------------------------- |
| `Gui`     | `Frame`   | The editor GUI object              |
| `Editing` | `boolean` | Whether the editor is being edited |

---

# API Notes

Some supplied API definitions contain apparent inconsistencies, such as:

* `InputColor3` declaring `Minimum` twice.
* `DragColor3` declaring `Minimum` twice.
* `DragCFrame` declaring `Minimum` twice.
* Some methods use another element's type as their self type.
* `SliderColor3` and `SliderCFrame` contain return types that reference other element types.
* `Image` declares `Callback` as required while its example does not provide one.
* `InputTextMultiline` uses `InputText` in some method return types.
* `PopupModal` uses `ClosePopup()` in its example even though it is not included in the supplied type definition.

These definitions are preserved as provided rather than silently changing the documented API.
