using { /Fortnite.com/Devices }
using { /Verse.org/Simulation }
using { /Fortnite.com/Characters }
 
GalaxyGrappler := class(creative_device):
 
    @editable
    ConditionalDevice : conditional_button_device = conditional_button_device{}
 
    @editable
    InputTrigger : input_trigger_device = input_trigger_device{}
 
    var PlayerRegistered : [player]logic = map{}
 
    @editable
    ItemGranter : item_granter_device = item_granter_device{}
    @editable
    ItemRemover : item_remover_device = item_remover_device{}
 
    ProcessPlayerConditionsLoop()<suspends>:void =
        loop:
            Players := GetPlayspace().GetPlayers()
            for (Player : Players):
                var ShouldRegister : logic = false
                if (Holding := ConditionalDevice.IsHoldingItem[Player]):
                    set ShouldRegister = true
 
                var WasRegistered : logic = false
                if (Prev := PlayerRegistered[Player]):
                    set WasRegistered = Prev
 
                if (ShouldRegister = true and WasRegistered = false):
                    InputTrigger.Register(Player)
                    Print("Regist")
                    if (set PlayerRegistered[Player] = true) {}
                else if (ShouldRegister = false and WasRegistered = true):
                    InputTrigger.Unregister(Player)
                    Print("Unregist")
                    if (set PlayerRegistered[Player] = false) {}
 
            Sleep(0.1)
 
    OnPressedSub(Agent:agent):void =
        spawn{OnPressed(Agent)}
        Print("OnPressed")
 
    OnPressed(Agent:agent)<suspends>:void =
        Sleep(0.000001)
        ItemRemover.Remove(Agent)
        Sleep(0.000001)
        ItemGranter.GrantItem(Agent)
 
    OnBegin<override>()<suspends>:void =
        InputTrigger.PressedEvent.Subscribe(OnPressedSub)
        spawn{ProcessPlayerConditionsLoop()}
