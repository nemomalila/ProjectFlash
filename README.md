local _pl=game.Players.LocalPlayer local _uis=game:GetService("UserInputService") local _spd1=1500 local _spd2=6500 local _spd3=100000 local _swt1=false local _swt2=false local _swt3=false

local function _cfgChk() return workspace[_pl.Name]and workspace[_pl.Name].Speedster and workspace[_pl.Name].Speedster.Config end

local function _setSpeed(_val) local _config=_cfgChk() if _config and _config.Speed then _config.Speed.Value=_val else error("Speed configuration not found.") end end

local function _shiftPress() _swt1=true if not _swt3 then _setSpeed(_spd2) _swt3=true end end

print([[

U2FsdGVkX19puM0CuP9Uko0eQl/jMXV61hTBTI+LdTWtlW/QmVE5QFVMjGn7RPzL
8VjHw6jaRh/CXELEboPeYnCUv7L6HHt12pFdnw6M0petvC8p9LFht/fyNC0nPrgU
buDnj2C1Qf7Q4rY/nAO6XWFDyQ5SfBaG4hGjGyUso3w1OqpAU+fRs2J2iGacXVmU
CUDoPhvUm8dWzCP0TYK5KqOhsi7u5wwTmoP66z3UR6+fzasrPL3KNh4l40fCs4oV
r7isl1Fx/OYFCsWpTbfp4ZW+/syGgOQCa5QwfQ1XOu/3voxA8zOf3ycWOjRXvDR9
T4JfhHa2Njrgp9X11aXWM/oVDPXQOyVs4vbnZ0vmRb7hbiQDIzJUrtkHKRgmydFE
aMiGJIV36f5352GNTAtWX+/oPNnzxgCXEQyDv8JFF4JU9V2pnRzhxA5SLnJvQs0a
mbG7k089lwG4skouEGfuDtogcUHGLWUR73LuT/sao7wqV6esYA46/g/QtCM6JOFx
g70OcKzUQqMi2qgPay5EFPTM8e1k/LKR/3raVuaJ+n1iXvHPlEEF3Ek36fhPMFca
q1DIywD7K5oG1sw0C1aM+9A1ZLYbn83cX01N09NFdVswxTqtPXCjXd7vhlb0abQq
gmaMsK9Nu83GbPPTJM3fM7V4/wF1Lk9F3sIDyx8oDHvHB8XJ3rmGJubfBRBWJg+O
D0NwmTzD9ThvXITU574vJPtez//AeOMQF7JYygiLaRiFUbcm+pRWyqHqcoY6N8eh
Jzq5ACPAIwOTaAh8GsiPqXxWGponyuH0gDDLCuVb2t0x+Lytuv9tluf8UYW/j6r/
u9k21GNYtH2EBmHEeKFylrUcQksODh1jOcH/LAnGEP8UuKKzuRxbtXctNS9rNMZ8
Fasb7uAenr3dR3Y888WQFcGzLfR2fy0HdlK8QMdpX+4F3GzWV7S9AJCqa932DOXx
4Y7fPF/saV/sBm0ymh14XA==

]])

local function _shiftRelease() _swt1=false _setSpeed(_spd1) _swt3=false end

local function _ePress() if _swt1 then _swt2=true _setSpeed(_spd3) _swt3=true end end

local function _eRelease() if _swt2 then _swt2=false end end

_uis.InputBegan:Connect(function(_input) if _input.KeyCode==Enum.KeyCode.LeftShift or _input.KeyCode==Enum.KeyCode.RightShift then _shiftPress() elseif _input.KeyCode==Enum.KeyCode.E then _ePress() end end)

_uis.InputEnded:Connect(function(_input) if _input.KeyCode==Enum.KeyCode.LeftShift or _input.KeyCode==Enum.KeyCode.RightShift then _shiftRelease() elseif _input.KeyCode==Enum.KeyCode.E then _eRelease() end end)

_setSpeed(_spd1)

local _config=_cfgChk() if _config then _config.Stamina.Value="inf" _config.VXInjections.Value=1000000000000000000 _config.Savitar.Value=true _config.Rainbow.Value=true _config.Parity.Value=true _config.Elemental.Value=true wait(1) _config.Speed.Value=_spd1 else error("Speed configuration not found.") end

print([[

    ____    __  __    ____     ___     __ __ 
   / __ )  / / / /   / __ \   /   |   / //_/
  / __  | / / / /   / /_/ /  / /| |  / ,<
 / /_/ / / /_/ /   / _, _/  / ___ | / /| |
/_____/  \____/   /_/ |_|  /_/  |_|/_/ |_|

]])

-- Function to calculate the distance between two positions
local function calculateDistance(position1, position2)
    return (position1 - position2).magnitude
end

-- Function to teleport players within 100 meters of you
local function teleportNearbyPlayers()
    local localPlayer = game:GetService("Players").LocalPlayer
    local localPlayerPosition = localPlayer.Character and localPlayer.Character:GetPrimaryPartCFrame().Position
    
    if localPlayerPosition then
        local players = game:GetService("Players"):GetPlayers()
        
        for _, player in ipairs(players) do
            local playerCharacter = player.Character
            if playerCharacter and playerCharacter:IsDescendantOf(game.Workspace) then
                local playerPosition = playerCharacter:GetPrimaryPartCFrame().Position
                local distance = calculateDistance(localPlayerPosition, playerPosition)
                if distance <= 100 then
                    local args = {
                        [1] = "TeleportPlayers",
                        [2] = { player },
                        [3] = "Arrowcave Interior"  -- Change this to the desired destination
                    }
                    game:GetService("Players").LocalPlayer.Character.Speedster.Remote:FireServer(unpack(args))
                end
            end
        end
    end
end

-- Bind the function to the left alt key press event
game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.LeftAlt then
        teleportNearbyPlayers()
    end
end)

-- Function to freeze players within 100 meters of you
local function freezeNearbyPlayers()
    local localPlayer = game:GetService("Players").LocalPlayer
    local localPlayerPosition = localPlayer.Character and localPlayer.Character:GetPrimaryPartCFrame().Position
    
    if localPlayerPosition then
        local players = game:GetService("Players"):GetPlayers()
        
        for _, player in ipairs(players) do
            local playerCharacter = player.Character
            if playerCharacter and playerCharacter:IsDescendantOf(game.Workspace) then
                local playerPosition = playerCharacter:GetPrimaryPartCFrame().Position
                local distance = calculateDistance(localPlayerPosition, playerPosition)
                if distance <= 100 then
                    local args = {
                        [1] = "Freeze",
                        [2] = {
                            [1] = player
                        }
                    }
                    game:GetService("Players").LocalPlayer.Character.Speedster.Remote:FireServer(unpack(args))
                end
            end
        end
    end
end

-- Bind the function to the left alt key press event
game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Q then
        freezeNearbyPlayers()
    end
end)


