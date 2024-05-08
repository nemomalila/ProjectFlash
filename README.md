local _pl=game.Players.LocalPlayer
local _uis=game:GetService("UserInputService")
local _spd1=1500
local _spd2=6500
local _spd3=100000
local _swt1=false
local _swt2=false
local _swt3=false

local function _cfgChk()
    return workspace[_pl.Name]and workspace[_pl.Name].Speedster and workspace[_pl.Name].Speedster.Config
end

local function _setSpeed(_val)
    local _config=_cfgChk()
    if _config and _config.Speed then
        _config.Speed.Value=_val
    else
        error("Speed configuration not found.")
    end
end

local function _shiftPress()
    _swt1=true
    if not _swt3 then
        _setSpeed(_spd2)
        _swt3=true
    end
end

local function _shiftRelease()
    _swt1=false
    _setSpeed(_spd1)
    _swt3=false
end

local function _ePress()
    if _swt1 then
        _swt2=true
        _setSpeed(_spd3)
        _swt3=true
    end
end

local function _eRelease()
    if _swt2 then
        _swt2=false
    end
end

_uis.InputBegan:Connect(function(_input)
    if _input.KeyCode==Enum.KeyCode.LeftShift or _input.KeyCode==Enum.KeyCode.RightShift then
        _shiftPress()
    elseif _input.KeyCode==Enum.KeyCode.E then
        _ePress()
    end
end)

_uis.InputEnded:Connect(function(_input)
    if _input.KeyCode==Enum.KeyCode.LeftShift or _input.KeyCode==Enum.KeyCode.RightShift then
        _shiftRelease()
    elseif _input.KeyCode==Enum.KeyCode.E then
        _eRelease()
    end
end)

_setSpeed(_spd1)

local _config=_cfgChk()
if _config then
    _config.Stamina.Value="inf"
    _config.VXInjections.Value=1000000000000000000
    _config.Savitar.Value=true
    _config.Rainbow.Value=true
    _config.Parity.Value=true
    _config.Elemental.Value=true
    wait(1)
    _config.Speed.Value=_spd1
else
    error("Speed configuration not found.")
end

print([[
    
    ____    __  __    ____     ___     __ __
   / __ )  / / / /   / __ \   /   |   / //_/
  / __  | / / / /   / /_/ /  / /| |  /  <
 / /_/ / / /_/ /   / _, _/  / ___ | / /| |
/_____/  \____/   /_/ |_|  /_/  |_|/_/ |_|

]])
