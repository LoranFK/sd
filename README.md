local ref = gui.Reference("Misc", "General", "Extra")
local autoteleport = gui.Checkbox(ref, "misc.autoteleport", "Auto Teleport", true)
autoteleport:SetDescription("No pasar")

local function CreateMove( cmd )
if not autoteleport:GetValue() then return false end
local pLocal = entities:GetLocalPlayer()


if pLocal:IsAlive() and pLocal:GetPropBool("m_jockeyVictim") and pLocal:GetPropEntity("m_jockeyVictim"):GetAbsOrigin(1.0) then -----------AutoJockeyTeleport

  cmd.forwardmove = 949.2457e3123
  

  
end

if pLocal:IsAlive() and pLocal:GetPropBool("m_carryVictim") and pLocal:GetPropEntity("m_carryVictim"):GetAbsOrigin(1.0) then
 -----------AutoChargerTeleport
 
  cmd.viewangles = EulerAngles(cmd.viewangles.pitch, cmd.viewangles.yaw + 1, 1e+37)


end


end

callbacks.Register("CreateMove", CreateMove)

  
local group = gui.Reference('Misc', 'General', "Extra")
local checkBox = gui.Checkbox(group, "lua_teleport_enable", "Enable", 1)
local teleportKey = gui.Keybox(group, 'lua_teleport_key', 'Teleport Key', 49)


local function isButtonDown(key)
    return key > 0 and input.IsButtonDown(key);
end

local function teleport (cmd)
 ------------Teleport(Jock & Char)
    if (checkBox:GetValue() and isButtonDown(teleportKey:GetValue()))  then
        cmd.forwardmove = 949.2457e3123 
      
        cmd.viewangles = EulerAngles(cmd.viewangles.pitch, cmd.viewangles.yaw + 1, 1e+37)
       end             
end

callbacks.Register('CreateMove' , teleport)

callbacks.Register("CreateMove", function(cmd)
local pLocal = entities:GetLocalPlayer()

if pLocal:IsAlive() and pLocal:GetPropBool("m_jockeyVictim") and pLocal:GetPropEntity("m_jockeyVictim"):GetAbsOrigin(1.0) then

 gui.SetValue("misc.bypassclient", false)---------Ignore Jockey(Client-side)
 
end

if pLocal:IsAlive() and pLocal:GetPropBool("m_jockeyAttacker") and pLocal:GetPropEntity("m_jockeyAttacker"):GetAbsOrigin(1.0) then -------AntiJockeyTeleport

        cmd.tick_count = 0x7F7FFFFF

end

if airstuck_key == 0 then return end
if not input.IsButtonDown(5) then return end --------Invisible Jockey

        cmd.forwardmove = 1e+37;

end)

local switch  = globals.FrameCount() ------Automatic Triggering(Bypass client-side

local function Switch()
   if globals.FrameCount() - switch > 625 then
       gui.SetValue("misc.bypassclient", 1)
       switch = globals.FrameCount()
   end
end

callbacks.Register("Draw", Switch) 
