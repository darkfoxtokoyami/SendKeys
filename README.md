# SendKeys
Send Keys in C# using user32.dll's SendInput method

## Purpose:

Useful for closing in-game windows using the Escape key. Has most US Keyboard keys mapped, using Hardware Keycodes (enum provided).

## Usage in Melon Loader:

Because Unity needs a few milliseconds of a key being pressed in order to detect it, you need to add a delay after the KeyDown event.  If you do *"System.Threading.Thread.Sleep(150);"* then it will pause the entire game, and it won't detect the KeyDown event.  So you need to start a separate routine with a MelonCoroutine. Then, you send the KeyDown; wait for a few milliseconds (e.g. 150ms); and then send a KeyUp event.

### Create a function like this:

    private static IEnumerator PressEsc()
	{
	  SendKeys.SendKeys.Send_Key((short)SendKeys.Keys.Esc, true);   // Send KeyDown (Escape Key)
	  yield return new WaitForSeconds(0.15f);                       // Wait for 150 milliseconds
	  SendKeys.SendKeys.Send_Key((short)SendKeys.Keys.Esc, false);  // Send KeyUp   (Escape Key) 
	}
    
### In whatever function you want to send a KeyPress from, start a Melon Co-Routine when you want to send the KeyPress event:

    MelonCoroutines.Start(PressEsc());

## To use in VRChat:
* Place the file in the "..."Steam\steamapps\common\VRChat" main directory. 
* Add a reference to it in your C# Class Library project
* Access its functionality within the SendKeys namespace
